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

Các công cụ tự động và quét trực tuyến không thể hoàn thành hơn một nửa của ASVS mà không có sự trợ giúp của con người. Nếu việc tự động hoàn chỉnh cho mỗi phiên bản được yêu cầu, thì một sự kết hợp của các kiểm thử đơn vị và kiểm thử tích hợp tùy chỉnh, cùng với các quét trực tuyến khởi động bởi build, được sử dụng. Kiểm tra lỗ hổng trong logic và kiểm tra kiểm soát truy cập chỉ có thể được thực hiện thông qua sự hỗ trợ của con người. Chúng nên được chuyển đổi thành các kiểm thử đơn vị và tích hợp.
