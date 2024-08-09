# V4 Access Control

## Control Objective

Ủy quyền là khái niệm cho phép truy cập vào tài nguyên chỉ dành cho những người được phép sử dụng chúng. Đảm bảo rằng một ứng dụng đã được xác minh đáp ứng các yêu cầu cấp cao sau:

* Những người truy cập tài nguyên có thông tin đăng nhập hợp lệ để làm như vậy.
* Người dùng được liên kết với một tập hợp các quyền được xác định rõ.
* Siêu dữ liệu chính sách kiểm soát truy cập được bảo vệ khỏi phát lại hoặc giả mạo.

Các thiếu sót về kiểm soát truy cập không có khả năng được phát hiện bằng các công cụ kiểm tra tự động chung. Việc xác minh các yêu cầu trong phần này sẽ yêu cầu kiểm tra thủ công hoặc hỗ trợ thủ công hoặc một loạt các bài kiểm tra kiểm soát truy cập đầu cuối tự động mạnh mẽ để xác nhận hiệu quả của các biện pháp kiểm soát truy cập trong các tình huống khác nhau. Việc tích hợp các bài kiểm tra này vào quy trình tích hợp liên tục/triển khai liên tục (CI/CD) sẽ giúp dễ dàng xác thực các yêu cầu này một cách liên tục.

## V4.1 General Access Control Design

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **4.1.1** | [MODIFIED] Xác minh rằng ứng dụng thực thi các quy tắc kiểm soát truy cập tại một lớp dịch vụ đáng tin cậy và không dựa vào các biện pháp kiểm soát mà người dùng không đáng tin cậy có thể thao tác như JavaScript phía máy khách. | ✓ | ✓ | ✓ | 602 |
| **4.1.2** | [MODIFIED] Xác minh rằng có các biện pháp kiểm soát cụ thể để ngăn người dùng cuối thực hiện các thay đổi đối với thông tin chính sách kiểm soát truy cập, chẳng hạn như vai trò người dùng, quyền và cấp độ truy cập tính năng, trừ khi họ được ủy quyền rõ ràng để làm như vậy. | ✓ | ✓ | ✓ | 639 |
| **4.1.3** | Xác minh rằng nguyên tắc đặc quyền tối thiểu tồn tại - người dùng chỉ có thể truy cập các chức năng, tệp dữ liệu, URL, bộ điều khiển, dịch vụ và các tài nguyên khác mà họ có ủy quyền cụ thể. Điều này ngụ ý bảo vệ chống lại giả mạo và nâng cao đặc quyền. | ✓ | ✓ | ✓ | 285 |
| **4.1.4** | [DELETED, DUPLICATE OF 4.1.3] | | | | |
| **4.1.5** | [GRAMMAR] Xác minh rằng các biện pháp kiểm soát truy cập không thành công một cách an toàn bằng cách từ chối truy cập, kể cả khi xảy ra ngoại lệ. | ✓ | ✓ | ✓ | 285 |

## V4.2 Operation Level Access Control

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **4.2.1** | Xác minh rằng dữ liệu và API nhạy cảm được bảo vệ chống lại các cuộc tấn công Tham chiếu Đối tượng Trực tiếp Không an toàn (IDOR) nhắm mục tiêu tạo, đọc, cập nhật và xóa bản ghi, chẳng hạn như tạo hoặc cập nhật bản ghi của người khác, xem bản ghi của mọi người hoặc xóa tất cả các bản ghi. | ✓ | ✓ | ✓ | 639 |
| **4.2.2** | [MOVED TO 50.3.1] | | | | |

## V4.3 Other Access Control Considerations

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **4.3.1** | [MODIFIED] Xác minh rằng các giao diện quản trị chỉ có thể được truy cập hợp lý từ các điểm cuối hoặc vị trí đáng tin cậy. Ví dụ: hạn chế truy cập vào máy chủ bastion hoặc máy chủ nhảy, máy trạm hoặc điểm cuối quản trị đáng tin cậy (ví dụ: xác thực thiết bị), mạng LAN quản trị, v.v. | ✓ | ✓ | ✓ | 419 |
| **4.3.2** | [SPLIT TO 14.3.4, 14.3.5] | | | | |
| **4.3.3** | [MODIFIED] Xác minh rằng, nếu ứng dụng cho phép thay đổi cấu hình có độ nhạy cao xung quanh mật khẩu hoặc tham số kết nối để tích hợp với cơ sở dữ liệu và hệ thống bên thứ ba, chúng được bảo vệ bởi các biện pháp kiểm soát bổ sung như xác thực lại hoặc phê duyệt nhiều người dùng. | | ✓ | ✓ | 732 |

## References

For more information, see also:

* [OWASP Testing Guide 4.0: Authorization](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/05-Authorization_Testing/README.html)
* [OWASP Cheat Sheet: Access Control](https://cheatsheetseries.owasp.org/cheatsheets/Access_Control_Cheat_Sheet.html)
