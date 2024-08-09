# Sử dụng ASVS

Như đã lưu ý trong phần mở đầu, ASVS là một tiêu chuẩn xác định các yêu cầu bảo mật chức năng và phi chức năng cần xem xét cho các ứng dụng web và dịch vụ web hiện đại.

Do đó, nó tập trung vào nội dung của ứng dụng chứ không phải quy trình an toàn để phát triển ứng dụng. Các quy trình Phát triển An toàn được đề cập tốt hơn trong dự án [OWASP SAMM](https://owaspsamm.org/) và không phải là phạm vi chính của ASVS.

Trong bối cảnh các yêu cầu an toàn, ASVS sẽ hữu ích cho bất kỳ ai đang cố gắng:

- Phát triển và duy trì các ứng dụng an toàn.
- Đánh giá tính bảo mật của các ứng dụng.

Chương này sẽ đề cập đến một số khía cạnh chính của việc sử dụng ASVS bao gồm sử dụng các cấp độ để áp dụng cách tiếp cận dựa trên rủi ro và các trường hợp sử dụng khác nhau cho tiêu chuẩn.

## Application Security Verification Levels

The Application Security Verification Standard xác định ba cấp độ xác minh bảo mật, với mỗi cấp độ tăng dần về độ sâu.

* ASVS Level 1 dành cho mức độ đảm bảo thấp và hoàn toàn có thể xác minh được thông qua kiểm tra thâm nhập.
* ASVS Level 2 dành cho các ứng dụng chứa dữ liệu nhạy cảm, cần được bảo vệ và là mức khuyến nghị cho hầu hết các ứng dụng.
* ASVS Level 3 dành cho các ứng dụng quan trọng nhất, chẳng hạn như các ứng dụng xử lý giao dịch có giá trị cao, chứa dữ liệu y tế nhạy cảm hoặc bất kỳ ứng dụng nào yêu cầu mức độ tin cậy cao nhất.

Mỗi cấp độ ASVS chứa một danh sách các yêu cầu bảo mật. Mỗi yêu cầu này cũng có thể được ánh xạ tới các tính năng và khả năng bảo mật cụ thể mà các nhà phát triển phải tích hợp vào phần mềm.

Level 1 là cấp duy nhất có thể kiểm tra thâm nhập hoàn toàn bằng con người. Tất cả các cấp khác yêu cầu quyền truy cập vào tài liệu, mã nguồn, cấu hình và những người tham gia vào quá trình phát triển. Tuy nhiên, ngay cả khi L1 cho phép kiểm tra "hộp đen" (không có tài liệu và không có nguồn) xảy ra, nó không phải là một hoạt động đảm bảo hiệu quả và nên được khuyến khích không nên sử dụng. Kẻ tấn công độc hại có rất nhiều thời gian, hầu hết các bài kiểm tra thâm nhập đều kết thúc trong vòng vài tuần. Người bảo vệ cần kết hợp các biện pháp kiểm soát bảo mật, bảo vệ, tìm và giải quyết tất cả các điểm yếu, đồng thời phát hiện và ứng phó với các tác nhân độc hại trong một khoảng thời gian hợp lý. Các tác nhân độc hại về cơ bản có thời gian vô hạn và chỉ cần một lỗ hổng duy nhất, một điểm yếu duy nhất hoặc thiếu phát hiện để thành công. Kiểm tra hộp đen, thường được thực hiện vào cuối quá trình phát triển, một cách nhanh chóng hoặc hoàn toàn không thực hiện, hoàn toàn không thể đối phó với sự bất đối xứng đó.

Trong hơn 30 năm qua, kiểm tra hộp đen đã nhiều lần chứng minh là bỏ sót các vấn đề bảo mật quan trọng dẫn trực tiếp đến các vi phạm ngày càng lớn. Chúng tôi khuyến khích mạnh mẽ việc sử dụng nhiều biện pháp đảm bảo và xác minh bảo mật, bao gồm thay thế các bài kiểm tra thâm nhập bằng các bài kiểm tra thâm nhập do mã nguồn dẫn dắt (lai) ở Level 1, với quyền truy cập đầy đủ vào các nhà phát triển và tài liệu trong suốt quá trình phát triển. Các cơ quan quản lý tài chính không chấp nhận kiểm toán tài chính bên ngoài mà không có quyền truy cập vào sổ sách, giao dịch mẫu hoặc những người thực hiện kiểm soát. Ngành công nghiệp và chính phủ phải yêu cầu tiêu chuẩn minh bạch tương tự trong lĩnh vực kỹ thuật phần mềm.

Chúng tôi khuyến khích mạnh mẽ việc sử dụng các công cụ bảo mật trong chính quá trình phát triển. Các công cụ DAST và SAST, khi được triển khai liên tục trong quy trình xây dựng, có thể xác định và giải quyết hiệu quả các vấn đề bảo mật đơn giản không bao giờ nên tồn tại.

Các công cụ tự động và quét trực tuyến không thể hoàn thành hơn một nửa ASVS mà không có sự trợ giúp của con người. Nếu cần tự động hóa kiểm tra toàn diện cho mỗi bản dựng, thì sẽ sử dụng kết hợp các bài kiểm tra đơn vị và tích hợp tùy chỉnh, cùng với các bản quét trực tuyến được khởi tạo khi xây dựng. Lỗi logic nghiệp vụ và kiểm tra kiểm soát truy cập chỉ có thể thực hiện được bằng sự trợ giúp của con người. Những điều này nên được chuyển thành các bài kiểm tra đơn vị và tích hợp.

## Cách sử dụng tiêu chuẩn này

Một trong những cách tốt nhất để sử dụng Tiêu chuẩn Xác minh Bảo mật Ứng dụng là sử dụng nó làm bản thiết kế để tạo Danh sách Kiểm tra Mã hóa An toàn dành riêng cho ứng dụng, nền tảng hoặc tổ chức của bạn. Điều chỉnh ASVS cho các trường hợp sử dụng của bạn sẽ làm tăng sự tập trung vào các yêu cầu bảo mật quan trọng nhất đối với dự án và môi trường của bạn.

### Level 1 - First steps, automated, or whole of portfolio view

Một ứng dụng đạt ASVS Level 1 nếu nó bảo vệ đầy đủ chống lại các lỗ hổng bảo mật ứng dụng dễ phát hiện và được bao gồm trong OWASP Top 10 và các danh sách kiểm tra tương tự khác.

Level 1 là mức tối thiểu mà tất cả các ứng dụng nên phấn đấu. Nó cũng hữu ích như một bước đầu tiên trong nỗ lực nhiều giai đoạn hoặc khi các ứng dụng không lưu trữ hoặc xử lý dữ liệu nhạy cảm và do đó không cần các biện pháp kiểm soát nghiêm ngặt hơn của Cấp 2 hoặc 3. Các biện pháp kiểm soát Cấp 1 có thể được kiểm tra tự động bằng công cụ hoặc đơn giản là thủ công mà không cần truy cập vào mã nguồn. Chúng tôi coi Cấp 1 là mức tối thiểu cần thiết cho tất cả các ứng dụng.

Các mối đe dọa đối với ứng dụng rất có thể sẽ đến từ những kẻ tấn công đang sử dụng các kỹ thuật đơn giản và ít tốn công sức để xác định các lỗ hổng dễ tìm và dễ khai thác. Điều này trái ngược với một kẻ tấn công kiên quyết, người sẽ dành năng lượng tập trung để nhắm mục tiêu cụ thể vào ứng dụng. Nếu ứng dụng của bạn xử lý dữ liệu có giá trị cao, bạn hiếm khi muốn dừng lại ở đánh giá Cấp 1.

### Level 2 - Most applications

Một ứng dụng đạt ASVS Level 2 (hoặc Tiêu chuẩn) nếu nó bảo vệ đầy đủ chống lại hầu hết các rủi ro liên quan đến phần mềm ngày nay.

Cấp 2 đảm bảo rằng các biện pháp kiểm soát bảo mật được áp dụng, hiệu quả và được sử dụng trong ứng dụng. Level 2 thường thích hợp cho các ứng dụng xử lý các giao dịch kinh doanh quan trọng giữa các doanh nghiệp, bao gồm cả các ứng dụng xử lý thông tin chăm sóc sức khỏe, triển khai các chức năng quan trọng hoặc nhạy cảm đối với doanh nghiệp hoặc xử lý các tài sản nhạy cảm khác, hoặc các ngành mà tính toàn vẹn là một khía cạnh quan trọng để bảo vệ hoạt động kinh doanh của họ, chẳng hạn như ngành công nghiệp trò chơi để ngăn chặn những kẻ gian lận và hack trò chơi.

Các mối đe dọa đối với các ứng dụng Level 2 thường là những kẻ tấn công có kỹ năng và động lực, tập trung vào các mục tiêu cụ thể bằng cách sử dụng các công cụ và kỹ thuật được thực hành nhiều và hiệu quả trong việc phát hiện và khai thác các điểm yếu trong ứng dụng.

### Level 3 - High value, high assurance, or high safety

ASVS Level 3 là cấp độ xác minh cao nhất trong ASVS. Cấp độ này thường dành riêng cho các ứng dụng yêu cầu mức độ xác minh bảo mật đáng kể, chẳng hạn như các ứng dụng có thể được tìm thấy trong các lĩnh vực quân sự, y tế và an toàn, cơ sở hạ tầng quan trọng, v.v.

Các tổ chức có thể yêu cầu ASVS Level 3 đối với các ứng dụng thực hiện các chức năng quan trọng, trong đó lỗi có thể ảnh hưởng đáng kể đến hoạt động của tổ chức và thậm chí cả khả năng tồn tại của tổ chức. Ví dụ hướng dẫn về việc áp dụng ASVS Level 3 được cung cấp bên dưới. Một ứng dụng đạt ASVS Cấp 3 (hoặc Nâng cao) nếu nó bảo vệ đầy đủ chống lại các lỗ hổng bảo mật ứng dụng nâng cao và cũng thể hiện các nguyên tắc thiết kế bảo mật tốt.

Một ứng dụng ở mức ASVS Level 3 yêu cầu phân tích chuyên sâu hơn về kiến trúc, mã hóa và kiểm thử so với tất cả các cấp khác. Một ứng dụng an toàn được mô-đun hóa một cách có ý nghĩa (để tạo điều kiện cho khả năng phục hồi, khả năng mở rộng và trên hết là các lớp bảo mật), và mỗi mô-đun (được phân tách bằng kết nối mạng và/hoặc phiên bản vật lý) đảm nhận trách nhiệm bảo mật của riêng nó (phòng thủ theo chiều sâu), cần được ghi lại đúng cách. Các trách nhiệm bao gồm các biện pháp kiểm soát để đảm bảo tính bảo mật (ví dụ: mã hóa), tính toàn vẹn (ví dụ: giao dịch, xác thực đầu vào), tính khả dụng (ví dụ: xử lý tải một cách uyển chuyển), xác thực (bao gồm cả giữa các hệ thống), ủy quyền và kiểm toán (ghi nhật ký).

## Cách Tham Chiếu các Yêu cầu ASVS

Mỗi yêu cầu có một định danh theo định dạng `<chapter>.<section>.<requirement>` trong đó mỗi phần tử là một số, ví dụ: 1.11.3.

* Giá trị `<chapter>` tương ứng với chương mà yêu cầu đến từ đó, ví dụ: tất cả các yêu cầu `1.#.#` đều đến từ chương `Kiến trúc`.
* Giá trị `<section>` tương ứng với phần trong chương đó, nơi yêu cầu xuất hiện, ví dụ: tất cả các yêu cầu `1.11.#` đều nằm trong phần `Yêu cầu Kiến trúc Logic Nghiệp vụ` của chương `Kiến trúc`.
* Giá trị `<requirement>` xác định yêu cầu cụ thể trong chương và phần, ví dụ: `1.11.3` mà theo phiên bản `4.0.2` của tiêu chuẩn này là:

> Xác minh rằng tất cả các luồng logic nghiệp vụ có giá trị cao, bao gồm xác thực, quản lý phiên và kiểm soát truy cập đều an toàn luồng và chống lại các điều kiện race time-of-check và time-of-use.

Vì các định danh có thể thay đổi giữa các phiên bản của tiêu chuẩn, nên các tài liệu, báo cáo hoặc công cụ khác nên sử dụng định dạng sau: `v<version>-<chapter>.<section>.<requirement>` trong đó: 'version' là thẻ phiên bản ASVS. Ví dụ: `v4.0.2-1.11.3` sẽ được hiểu là yêu cầu thứ 3 trong phần 'Yêu cầu Kiến trúc Logic Nghiệp vụ' của chương 'Kiến trúc' từ phiên bản 4.0.2. (Điều này có thể được tóm tắt là v<phiên bản>-<định danh_yêu cầu>.)

Lưu ý: Chữ `v` đứng trước số phiên bản trong định dạng phải luôn luôn là chữ thường.

Nếu các định danh được sử dụng mà không bao gồm phần tử `v<version>` thì chúng nên được giả định là đề cập đến nội dung Tiêu chuẩn Xác minh Bảo mật Ứng dụng mới nhất. Khi tiêu chuẩn phát triển và thay đổi, điều này sẽ trở nên có vấn đề, đó là lý do tại sao người viết hoặc nhà phát triển nên bao gồm phần tử phiên bản.

Danh sách yêu cầu ASVS được cung cấp ở định dạng CSV, JSON và các định dạng khác có thể hữu ích cho mục đích tham khảo hoặc sử dụng theo chương trình.

## Tạo nhánh ASVS

Nhiều tổ chức có thể hưởng lợi từ việc áp dụng ASVS, bằng cách chọn một trong ba cấp độ hoặc bằng cách tạo nhánh ASVS và thay đổi những gì được yêu cầu cho từng mức độ rủi ro ứng dụng theo cách cụ thể cho từng lĩnh vực. Chúng tôi khuyến khích loại tạo nhánh này miễn là khả năng truy xuất nguồn gốc được duy trì để nếu một ứng dụng đã vượt qua yêu cầu 4.1.1, điều này có nghĩa tương tự đối với các bản sao của tiêu chuẩn khi nó phát triển.

Lý tưởng nhất là mọi tổ chức nên có ASVS được tạo nhánh riêng và chọn các yêu cầu phù hợp. Vì vậy, nếu tổ chức không sử dụng GraphQL, Websockets hoặc dịch vụ web SOAP trên các ứng dụng của họ, họ nên bỏ các phần đó khỏi ASVS đã tạo nhánh của họ. Quá trình tạo nhánh phải bắt đầu bằng cách xem xét các yêu cầu ASVS cấp 1 làm cơ sở cho tổ chức và sau đó dần dần chuyển sang ASVS cấp 2 hoặc 3 dựa trên mức độ rủi ro của ứng dụng.

## Công dụng của ASVS

ASVS có thể được sử dụng để đánh giá tính bảo mật của một ứng dụng và điều này được khám phá sâu hơn trong chương tiếp theo. Tuy nhiên, chúng tôi đã xác định một số công dụng tiềm năng khác cho ASVS (hoặc một phiên bản đã tạo nhánh).

### As Detailed Security Architecture Guidance

Một trong những ứng dụng phổ biến hơn của Tiêu chuẩn Xác minh Bảo mật Ứng dụng là một tài nguyên cho các kiến trúc sư bảo mật. Kiến trúc Bảo mật Kinh doanh Ứng dụng Sherwood (SABSA) còn thiếu rất nhiều thông tin cần thiết để hoàn thành đánh giá kiến trúc bảo mật ứng dụng kỹ lưỡng. ASVS có thể được sử dụng để lấp đầy những khoảng trống đó bằng cách cho phép các kiến trúc sư bảo mật chọn các biện pháp kiểm soát tốt hơn cho các vấn đề phổ biến, chẳng hạn như các mẫu bảo vệ dữ liệu và chiến lược xác thực đầu vào.

### As a Specialized Secure Coding Checklist

ASVS có thể được sử dụng như một danh sách kiểm tra mã hóa an toàn để phát triển ứng dụng an toàn, giúp các nhà phát triển đảm bảo rằng họ luôn ghi nhớ bảo mật khi xây dựng phần mềm. Danh sách kiểm tra mã hóa an toàn nên được thống nhất, rõ ràng và áp dụng cho tất cả các nhóm phát triển. Lý tưởng nhất là nó nên được chuẩn bị dựa trên hướng dẫn từ các kỹ sư bảo mật hoặc kiến trúc sư bảo mật.

### As a Guide for Automated Unit and Integration Tests

ASVS được thiết kế để có khả năng kiểm thử cao, ngoại trừ các yêu cầu về kiến trúc và mã độc hại. Bằng cách xây dựng các bài kiểm thử đơn vị và tích hợp kiểm tra các trường hợp fuzz và lạm dụng cụ thể và có liên quan, ứng dụng gần như có thể tự xác minh với mỗi lần xây dựng. Ví dụ: các bài kiểm thử bổ sung có thể được tạo cho bộ kiểm thử cho bộ điều khiển đăng nhập, kiểm tra tham số tên người dùng cho các tên người dùng mặc định phổ biến, liệt kê tài khoản, tấn công brute force, LDAP và SQL injection, và XSS. Tương tự, một bài kiểm thử trên tham số mật khẩu nên bao gồm các mật khẩu phổ biến, độ dài mật khẩu, tiêm null byte, xóa tham số, XSS, v.v.

### For Secure Development Training

ASVS cũng có thể được sử dụng để xác định các đặc điểm của phần mềm an toàn. Nhiều khóa học "mã hóa an toàn" chỉ đơn giản là các khóa học hack đạo đức với một chút mẹo mã hóa. Điều này có thể không nhất thiết giúp các nhà phát triển viết mã an toàn hơn. Thay vào đó, các khóa học phát triển an toàn có thể sử dụng ASVS với trọng tâm mạnh mẽ vào các biện pháp kiểm soát chủ động được tìm thấy trong ASVS, thay vì 10 điều tiêu cực hàng đầu không nên làm.

### As a Driver for Agile Application Security

ASVS có thể được sử dụng trong quy trình phát triển nhanh nhẹn như một khuôn khổ để xác định các nhiệm vụ cụ thể cần được nhóm thực hiện để có một sản phẩm an toàn. Một cách tiếp cận có thể là: Bắt đầu với Cấp 1, xác minh ứng dụng hoặc hệ thống cụ thể theo các yêu cầu ASVS cho cấp độ được chỉ định, tìm các biện pháp kiểm soát còn thiếu và đưa ra các phiếu/nhiệm vụ cụ thể trong backlog. Điều này giúp ưu tiên các nhiệm vụ cụ thể (hoặc grooming) và làm cho bảo mật hiển thị trong quy trình nhanh nhẹn. Cách tiếp cận này cũng có thể được sử dụng để ưu tiên các nhiệm vụ kiểm toán và đánh giá trong tổ chức. Một yêu cầu ASVS cụ thể có thể thúc đẩy việc đánh giá, cấu trúc lại hoặc kiểm toán cho một thành viên nhóm cụ thể và hiển thị dưới dạng 'nợ' trong backlog cuối cùng phải được giải quyết.

### As a Framework for Guiding the Procurement of Secure Software

ASVS là một khuôn khổ tuyệt vời để hỗ trợ mua sắm phần mềm an toàn hoặc mua sắm các dịch vụ phát triển tùy chỉnh. Người mua có thể chỉ cần đặt ra yêu cầu rằng phần mềm họ muốn mua phải được phát triển ở ASVS cấp X và yêu cầu người bán chứng minh rằng phần mềm đáp ứng ASVS cấp X. Điều này hoạt động tốt khi kết hợp với Phụ lục Hợp đồng Phần mềm An toàn OWASP.

## Áp dụng ASVS trong Thực tế

Các mối đe dọa khác nhau có động cơ khác nhau. Một số ngành có thông tin và tài sản công nghệ độc đáo và các yêu cầu tuân thủ quy định cụ thể theo từng lĩnh vực.

Các tổ chức được khuyến khích mạnh mẽ xem xét kỹ lưỡng các đặc điểm rủi ro duy nhất của họ dựa trên bản chất hoạt động kinh doanh của họ và dựa trên rủi ro và yêu cầu kinh doanh đó để xác định cấp độ ASVS phù hợp.

Chúng tôi đã nhận được phản hồi từ nhiều thành viên khác nhau trong cộng đồng về cách họ triển khai tiêu chuẩn trong thực tế:

### Personal Case Studies

#### Matthew Hackling

* Định hướng phạm vi và các trường hợp kiểm thử thâm nhập
* Định hướng các yêu cầu bảo mật cho việc hỗ trợ thiết kế
* Xây dựng một khuôn khổ quy chuẩn tổ chức ISO27034 hay còn gọi là thư viện yêu cầu.

#### Dominique Righetto

* Được sử dụng để đánh giá mã và như một danh sách kiểm tra khi thực hiện đánh giá lỗ hổng ứng dụng web.

#### Giovanni Cruz

* Trong chuyến OWASP Latam Tour Bogotá 2019 gần đây nhất, một khóa đào tạo đã được chuẩn bị hoàn toàn dựa trên ASVS. Tất cả nội dung đã được tạo ra với một nền tảng dễ bị tấn công để đào tạo nhằm hỗ trợ các nhà phát triển. Nó đã nhận được phản hồi tuyệt vời vì họ đã chỉ cho họ cách sử dụng nó và mức độ bảo mật mà họ có thể muốn đạt được dựa trên một số tiêu chuẩn.

#### Sebastien Gioria

* Đối với một số khách hàng, sử dụng nó làm cơ sở cho các yêu cầu bắt buộc để thực hiện thiết kế và mã hóa an toàn.

#### Riotaro Okada

* Trong những năm gần đây, quan sát thấy một số ngân hàng ở Nhật Bản đã đưa ASVS vào RFP của họ đối với các dịch vụ kiểm tra bảo mật, như một yêu cầu bắt buộc của họ. Họ muốn các đề xuất mà các nhà cung cấp bảo mật sẽ phù hợp với các cấp độ ASVS thích hợp.
* Một nhà cung cấp phần mềm địa phương ở Nhật Bản bán các gói liên quan đến SFA đã nhận được tiêu chí của khách hàng để kiểm tra xem sản phẩm của họ có phù hợp với ASVS hay không và sản phẩm phù hợp với cấp độ nào. (Đó là một khởi đầu tốt để nhà cung cấp giới thiệu phát triển và xác minh an toàn vào nhóm của họ)

#### John Patrick Lita

* Sử dụng điều này và tích hợp điều này trong hoạt động CI/CD của họ

### Use within other projects and tools

* OWASP Defectdojo có hỗ trợ ASVS tích hợp sẵn https://www.defectdojo.org/
* Một vài tuần sau khi ASVS 4 phát hành, RIPS đã thêm hỗ trợ cho nó: https://blog.ripstech.com/2019/rips-3.1-adds-teamcity-ldap-jsp-support/
