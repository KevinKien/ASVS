# Sử dụng ASVS

ASVS có hai mục tiêu chính:

* để giúp các tổ chức phát triển và duy trì các ứng dụng an toàn.
* để cho phép nhà cung cấp dịch vụ bảo mật, nhà cung cấp công cụ bảo mật và khách hàng đồng bộ hóa yêu cầu và các sản phẩm của họ.

## Application Security Verification Levels

Application Security Verification Standard định nghĩa ba cấp độ xác minh bảo mật, với mỗi cấp độ sẽ tăng dần về độ sâu.

* Cấp độ ASVS Level 1 là dành cho mức độ xác thực an ninh thấp và hoàn toàn có thể kiểm tra thâm nhập
* Cấp độ ASVS Level 2 là dành cho các ứng dụng chứa dữ liệu nhạy cảm, yêu cầu bảo vệ và là cấp độ được khuyến nghị cho hầu hết các ứng dụng.
* Cấp độ ASVS Level 3 là dành cho các ứng dụng quan trọng nhất - các ứng dụng thực hiện giao dịch có giá trị cao, chứa dữ liệu y tế nhạy cảm hoặc bất kỳ ứng dụng nào yêu cầu mức độ tin cậy cao nhất.

Mỗi cấp độ của ASVS chứa một danh sách yêu cầu bảo mật. Mỗi yêu cầu này cũng có thể được ánh xạ đến các tính năng và khả năng cụ thể liên quan đến bảo mật mà các nhà phát triển phần mềm phải tích hợp vào.

![ASVS Levels](https://raw.githubusercontent.com/OWASP/ASVS/master/4.0/images/asvs_40_levels.png "ASVS Levels")

Hình 1 - OWASP Application Security Verification Standard 4.0 Levels

Level 1 là cấp độ duy nhất mà có thể hoàn toàn kiểm thử xâm nhập bằng con người. Các cấp độ khác đòi hỏi truy cập tài liệu, mã nguồn, cấu hình và những người tham gia vào quá trình phát triển. Tuy nhiên, ngay cả khi L1 cho phép kiểm thử "hộp đen" (không có tài liệu và mã nguồn), thì đó không phải là một hoạt động đảm bảo hiệu quả và khuyến khích không nên thực hiện. Kẻ tấn công có rất nhiều thời gian, hầu hết các cuộc kiểm thử xâm nhập chỉ diễn ra trong vài tuần. Người phòng thủ cần xây dựng các kiểm soát bảo mật, bảo vệ, tìm và khắc phục tất cả các điểm yếu, phát hiện trong một thời gian hợp lý. Kẻ tấn công có thời gian không giới hạn và chỉ cần một lỗ hổng, một điểm yếu để thành công. Kiểm thử hộp đen, thường được thực hiện ở giai đoạn cuối của quá trình phát triển, thực hiện một cách nhanh chóng hoặc hoàn toàn không, hoàn toàn không thể đối phó với sự bất đối xứng đó.

Trong hơn 30 năm qua, kiểm thử hộp đen đã được chứng minh lần lượt bỏ qua các vấn đề bảo mật quan trọng dẫn đến các cuộc tấn công ngày càng lớn hơn. Chúng tôi mạnh dạn khuyến khích việc sử dụng một loạt các phương pháp đảm bảo và xác thực an ninh, bao gồm thay thế kiểm thử xâm nhập bằng kiểm thử xâm nhập dựa trên mã nguồn (hybrid) ở cấp độ 1, với đầy đủ quyền truy cập vào các tài liệu phát triển và nhà phát triển trong suốt quá trình phát triển. Các cơ quan quản lý tài chính không dung thứ cho các cuộc kiểm toán tài chính bên ngoài mà không có quyền truy cập vào sổ sách, giao dịch mẫu hoặc những người thực hiện kiểm soát. Ngành công nghiệp và các chính phủ phải yêu cầu cùng một tiêu chuẩn minh bạch trong lĩnh vực công nghệ phần mềm.

Chúng tôi rất khuyến khích việc sử dụng các công cụ bảo mật trong quá trình phát triển phần mềm. Các công cụ DAST và SAST có thể được sử dụng liên tục bởi pipeline để tìm kiếm các lỗ hổng không bao giờ xuất hiện.

Các công cụ tự động và quét trực tuyến không thể hoàn thành hơn một nửa của ASVS mà không có sự trợ giúp của con người. Nếu yêu cầu tự động hóa thử nghiệm toàn diện cho từng bản build, thì sẽ sử dụng kết hợp các thử nghiệm unit và integration tests, cùng với quá trình quét trực tuyến bắt đầu xây dựng. Lỗi logic nghiệp vụ và kiểm tra kiểm soát truy cập chỉ có thể thực hiện được khi có sự trợ giúp của con người. Chúng nên được biến thành các unit và integration tests.

## Cách sử dụng tiêu chuẩn

Một trong những cách tốt nhất để sử dụng Application Security Verification Standard là sử dụng nó làm bản thiết kế để tạo một Secure Coding Checklist dành riêng cho ứng dụng, nền tảng hoặc tổ chức của bạn. Điều chỉnh ASVS cho phù hợp với các trường hợp sử dụng của bạn sẽ tăng cường tập trung vào các yêu cầu bảo mật quan trọng nhất đối với các dự án và môi trường của bạn.

### Level 1 - First steps, automated, or whole of portfolio view

Một ứng dụng đạt được ASVS Level 1 nếu ứng dụng đó bảo vệ đầy đủ trước các lỗ hổng bảo mật ứng dụng dễ phát hiện và được đưa vào Top 10 của OWASP cũng như các danh sách kiểm tra tương tự khác.

Level 1 là mức tối thiểu mà tất cả các ứng dụng nên cố gắng đạt được. Nó cũng hữu ích như là bước đầu tiên trong nỗ lực nhiều giai đoạn hoặc khi các ứng dụng không lưu trữ hoặc xử lý dữ liệu nhạy cảm và do đó không cần các biện pháp kiểm soát chặt chẽ hơn ở Level 2 hoặc 3. Kiểm soát level 1 có thể được kiểm tra tự động bằng công cụ hoặc chỉ đơn giản là thủ công mà không cần truy cập vào mã nguồn. Chúng tôi coi Level 1 là yêu cầu tối thiểu đối với tất cả các ứng dụng.

Các mối đe dọa đối với ứng dụng rất có thể là từ những kẻ tấn công đang sử dụng các kỹ thuật đơn giản và tốn ít công sức để xác định các lỗ hổng dễ tìm và dễ khai thác. Điều này trái ngược với kẻ tấn công kiên quyết sẽ tập trung để nhắm vào mục tiêu cụ thể. Nếu dữ liệu do ứng dụng của bạn xử lý có giá trị cao, bạn sẽ hiếm khi muốn dừng lại ở đánh giá Level 1.

### Level 2 - Most applications

Một ứng dụng đạt được ASVS Level 2 (hoặc Tiêu chuẩn) nếu nó bảo vệ đầy đủ trước hầu hết các rủi ro liên quan đến phần mềm hiện nay.

Level 2 đảm bảo rằng các biện pháp kiểm soát bảo mật được áp dụng, hiệu quả và được sử dụng trong ứng dụng. Level 2 thường thích hợp cho các ứng dụng xử lý các giao dịch quan trọng giữa doanh nghiệp với doanh nghiệp, bao gồm các giao dịch xử lý thông tin chăm sóc sức khỏe, triển khai các chức năng quan trọng hoặc nhạy cảm trong kinh doanh hoặc xử lý các tài sản nhạy cảm khác hoặc các ngành mà tính toàn vẹn là khía cạnh quan trọng để bảo vệ doanh nghiệp của họ, chẳng hạn như ngành công nghiệp trò chơi để ngăn chặn những kẻ gian lận và hack trò chơi.

Các mối đe dọa đối với các ứng dụng Level 2 thường sẽ là những kẻ tấn công có kỹ năng và động cơ tập trung vào các mục tiêu cụ thể bằng cách sử dụng các công cụ và kỹ thuật cao và hiệu quả trong việc phát hiện và khai thác các điểm yếu trong ứng dụng.

### Level 3 - High value, high assurance, or high safety

ASVS Level 3 là cấp xác minh cao nhất trong ASVS. Cấp độ này thường được dành riêng cho các ứng dụng yêu cầu mức độ xác minh bảo mật quan trọng, chẳng hạn như những ứng dụng có thể được tìm thấy trong các lĩnh vực quân sự, sức khỏe và an toàn, cơ sở hạ tầng quan trọng, v.v.

Các tổ chức có thể yêu cầu ASVS Level 3 cho các ứng dụng thực hiện các chức năng quan trọng, trong đó lỗi có thể ảnh hưởng đáng kể đến hoạt động của tổ chức và thậm chí là khả năng tồn tại của nó. Hướng dẫn ví dụ về việc áp dụng ASVS Level 3 được cung cấp bên dưới. Một ứng dụng đạt được ASVS Level 3 (hoặc Nâng cao) nếu nó bảo vệ đầy đủ trước các lỗ hổng bảo mật ứng dụng nâng cao và cũng thể hiện các nguyên tắc thiết kế bảo mật tốt.

Một ứng dụng ở ASVS Level 3 yêu cầu phân tích sâu hơn về kiến trúc, viết mã và thử nghiệm hơn tất cả các cấp độ khác. Một ứng dụng bảo mật được mô-đun hóa theo cách có ý nghĩa (để tạo điều kiện thuận lợi cho khả năng phục hồi, khả năng mở rộng và hơn hết là các lớp bảo mật) và mỗi mô-đun (được phân tách bằng kết nối mạng và/hoặc phiên bản vật lý) đảm nhận các trách nhiệm bảo mật của chính nó (Phòng ngự chiều sau), cần phải được ghi lại đúng cách. Các trách nhiệm bao gồm các biện pháp kiểm soát để đảm bảo tính bảo mật (ví dụ: mã hóa), tính toàn vẹn (ví dụ: giao dịch, xác thực đầu vào), tính khả dụng (ví dụ: xử lý tải một cách linh hoạt), xác thực (bao gồm giữa các hệ thống), ủy quyền và kiểm tra (ghi nhật ký).

## Ứng Dụng ASVS Trong Thực Tế

Các mối đe dọa khác nhau có những động lực khác nhau. Một số ngành có tài sản công nghệ và thông tin duy nhất và các yêu cầu tuân thủ quy định cụ thể theo từng domain.

Các tổ chức được khuyến khích xem xét kỹ lưỡng các đặc điểm rủi ro duy nhất của họ dựa trên bản chất hoạt động kinh doanh của họ và dựa trên rủi ro đó cũng như các yêu cầu kinh doanh để xác định mức ASVS phù hợp.

## Cách tham khảo các yêu cầu ASVS

