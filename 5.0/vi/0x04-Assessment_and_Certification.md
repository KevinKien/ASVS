# Assessment and Certification

## OWASP's Stance on ASVS Certifications and Trust Marks

OWASP, với tư cách là một tổ chức phi lợi nhuận trung lập với nhà cung cấp, hiện không chứng nhận bất kỳ nhà cung cấp, người xác minh hoặc phần mềm nào.

Tất cả các xác nhận đảm bảo, nhãn hiệu tin cậy hoặc chứng nhận đó không được OWASP chính thức kiểm tra, đăng ký hoặc chứng nhận, vì vậy một tổ chức dựa vào quan điểm đó cần phải thận trọng về niềm tin đặt vào bất kỳ bên thứ ba hoặc nhãn hiệu tin cậy nào tuyên bố chứng nhận ASVS.

Điều này không nên cản trở các tổ chức cung cấp các dịch vụ đảm bảo như vậy, miễn là họ không tuyên bố chứng nhận OWASP chính thức.

## Guidance for Certifying Organizations

Tiêu chuẩn Xác minh Bảo mật Ứng dụng có thể được sử dụng như một xác minh mở đối với ứng dụng, bao gồm quyền truy cập mở và không hạn chế vào các tài nguyên chính như kiến trúc sư và nhà phát triển, tài liệu dự án, mã nguồn, quyền truy cập đã xác thực vào các hệ thống thử nghiệm (bao gồm quyền truy cập vào một hoặc nhiều tài khoản trong mỗi vai trò), đặc biệt là đối với xác minh L2 và L3.

Trong lịch sử, kiểm tra thâm nhập và đánh giá mã an toàn đã bao gồm các vấn đề “ngoại lệ” - nghĩa là chỉ các bài kiểm tra không thành công mới xuất hiện trong báo cáo cuối cùng. Một tổ chức chứng nhận phải bao gồm trong bất kỳ báo cáo nào phạm vi xác minh (đặc biệt nếu một thành phần chính nằm ngoài phạm vi, chẳng hạn như xác thực SSO), tóm tắt các phát hiện xác minh, bao gồm các bài kiểm tra đã qua và không thành công, với các chỉ dẫn rõ ràng về cách giải quyết các bài kiểm tra không thành công.

Một số yêu cầu xác minh có thể không áp dụng cho ứng dụng cụ thể đang được kiểm tra. Ví dụ: nếu bạn cung cấp API lớp dịch vụ không trạng thái mà không có triển khai máy khách cho khách hàng của mình, thì nhiều yêu cầu trong V3 Quản lý Phiên không áp dụng trực tiếp. Trong những trường hợp như vậy, một tổ chức chứng nhận vẫn có thể yêu cầu tuân thủ ASVS đầy đủ, nhưng phải chỉ rõ trong bất kỳ báo cáo nào lý do không áp dụng đối với các yêu cầu xác minh bị loại trừ đó.

Lưu giữ các giấy tờ làm việc chi tiết, ảnh chụp màn hình hoặc phim, tập lệnh để khai thác sự cố một cách đáng tin cậy và lặp đi lặp lại, và hồ sơ điện tử về thử nghiệm, chẳng hạn như nhật ký proxy chặn và các ghi chú liên quan như danh sách dọn dẹp, được coi là tiêu chuẩn thực hành công nghiệp và có thể thực sự hữu ích như bằng chứng về những phát hiện cho các nhà phát triển nghi ngờ nhất. Không đủ để chỉ cần chạy một công cụ và báo cáo về các lỗi; điều này (hoàn toàn) không cung cấp đủ bằng chứng cho thấy tất cả các vấn đề ở cấp độ chứng nhận đã được kiểm tra và kiểm tra kỹ lưỡng. Trong trường hợp có tranh chấp, cần có đủ bằng chứng đảm bảo để chứng minh từng yêu cầu đã được xác minh thực sự đã được kiểm tra.

### Testing Method

Các tổ chức chứng nhận có thể tự do lựa chọn (các) phương pháp kiểm tra phù hợp, nhưng nên chỉ ra chúng trong báo cáo.

Tùy thuộc vào ứng dụng đang được kiểm tra và yêu cầu xác minh, các phương pháp kiểm tra khác nhau có thể được sử dụng để đạt được sự tin cậy tương tự về kết quả. Ví dụ: xác thực hiệu quả của cơ chế xác minh đầu vào của ứng dụng có thể được đánh giá thông qua kiểm tra thâm nhập thủ công hoặc bằng cách tiến hành phân tích mã nguồn.

#### The Role of Automated Security Testing Tools 

Việc sử dụng các công cụ kiểm tra thâm nhập tự động được khuyến khích để cung cấp phạm vi phủ sóng càng nhiều càng tốt.

Không thể hoàn thành đầy đủ xác minh ASVS chỉ bằng các công cụ kiểm tra thâm nhập tự động. Trong khi phần lớn các yêu cầu trong L1 có thể được thực hiện bằng cách sử dụng các bài kiểm tra tự động, thì phần lớn các yêu cầu không phù hợp với kiểm tra thâm nhập tự động.

Xin lưu ý rằng ranh giới giữa kiểm tra tự động và thủ công đã bị xóa nhòa khi ngành công nghiệp bảo mật ứng dụng trưởng thành. Các công cụ tự động thường được các chuyên gia điều chỉnh thủ công và những người kiểm tra thủ công thường tận dụng nhiều công cụ tự động khác nhau.

#### The Role of Penetration Testing

Trong phiên bản 4.0, chúng tôi quyết định làm cho L1 có thể kiểm tra thâm nhập hoàn toàn mà không cần truy cập vào mã nguồn, tài liệu hoặc nhà phát triển. Hai mục ghi nhật ký, bắt buộc phải tuân thủ OWASP Top 10 2017 A10, sẽ yêu cầu phỏng vấn, ảnh chụp màn hình hoặc thu thập bằng chứng khác, giống như trong OWASP Top 10 2017. Tuy nhiên, kiểm tra mà không có quyền truy cập vào thông tin cần thiết không phải là một phương pháp xác minh bảo mật lý tưởng, vì nó bỏ lỡ khả năng xem xét mã nguồn, xác định các mối đe dọa và các biện pháp kiểm soát còn thiếu, đồng thời thực hiện kiểm tra kỹ lưỡng hơn trong khung thời gian ngắn hơn.

Nếu có thể, cần có quyền truy cập vào nhà phát triển, tài liệu, mã và quyền truy cập vào ứng dụng thử nghiệm với dữ liệu không phải sản xuất khi thực hiện Đánh giá L2 hoặc L3. Kiểm tra thâm nhập được thực hiện ở các cấp độ này yêu cầu mức độ truy cập này, mà chúng tôi gọi là "đánh giá kết hợp" hoặc "kiểm tra thâm nhập kết hợp".
