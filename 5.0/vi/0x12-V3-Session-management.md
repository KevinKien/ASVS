# V3 Session Management

## Control Objective

Một trong những thành phần cốt lõi của bất kỳ ứng dụng dựa trên web hoặc API có trạng thái là cơ chế mà nó kiểm soát và duy trì trạng thái cho người dùng hoặc thiết bị tương tác với nó. Quản lý phiên thay đổi một giao thức không trạng thái thành có trạng thái, điều này rất quan trọng để phân biệt các người dùng hoặc thiết bị khác nhau.

Đảm bảo rằng một ứng dụng đã được xác minh đáp ứng các yêu cầu quản lý phiên cấp cao sau:

* Phiên là duy nhất cho mỗi cá nhân và không thể đoán hoặc chia sẻ.
* Phiên bị vô hiệu hóa khi không còn cần thiết và hết thời gian chờ trong thời gian không hoạt động.

Như đã lưu ý trước đó, các yêu cầu này đã được điều chỉnh để trở thành một tập hợp con tuân thủ các điều khiển NIST SP 800-63B đã chọn, tập trung vào các mối đe dọa phổ biến và các điểm yếu xác thực thường bị khai thác. Các yêu cầu xác minh trước đó đã bị loại bỏ, không sử dụng nữa hoặc trong hầu hết các trường hợp được điều chỉnh để phù hợp chặt chẽ với mục đích của các yêu cầu bắt buộc [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html).

## V3.1 Fundamental Session Management Security

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.1.1** | [DELETED, MERGED TO 8.3.1] | | | | | |
| **3.1.2** | [ADDED] Xác minh rằng ứng dụng thực hiện tất cả xác minh mã thông báo phiên bằng dịch vụ phụ trợ đáng tin cậy. | ✓ | ✓ | ✓ | 603 | |
| **3.1.3** | [MODIFIED, MOVED FROM 3.5.2, LEVEL L2 > L1] Xác minh rằng ứng dụng sử dụng mã thông báo được ký bằng mật mã hoặc mã thông báo không rõ ràng để quản lý phiên. Nên tránh các bí mật và khóa API tĩnh. | ✓ | ✓ | ✓ | 798 | 7.1 |

## V3.2 Session Binding

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.2.1** | [MODIFIED] Xác minh ứng dụng tạo mã thông báo phiên mới khi xác thực người dùng, bao gồm cả xác thực lại và chấm dứt mã thông báo phiên hiện tại. | ✓ | ✓ | ✓ | 384 | 7.1 |
| **3.2.2** | [MODIFIED] Xác minh rằng các mã thông báo phiên không rõ ràng có ít nhất 128 bit entropy. | ✓ | ✓ | ✓ | 331 | 7.1 |
| **3.2.3** | [DELETED, MERGED TO 8.2.2] | | | | | |
| **3.2.4** | [MODIFIED] Xác minh rằng các mã thông báo phiên không rõ ràng được tạo bằng hàm ngẫu nhiên an toàn. | | ✓ | ✓ | 330 | 7.1 |
| **3.2.5** | [ADDED] Xác minh rằng việc tạo phiên cho ứng dụng yêu cầu sự đồng ý của người dùng và ứng dụng được bảo vệ chống lại kiểu tấn công CSRF, trong đó phiên ứng dụng mới cho người dùng được tạo thông qua SSO mà không có tương tác của người dùng. | | ✓ | ✓ | | |

TLS hoặc một kênh vận chuyển an toàn khác là bắt buộc để quản lý phiên. Điều này được đề cập trong chương Bảo mật Truyền thông.

## V3.3 Session Timeout

Thời gian chờ phiên đã được điều chỉnh phù hợp với NIST SP 800-63, cho phép thời gian chờ phiên dài hơn nhiều so với thời gian chờ theo truyền thống được phép bởi các tiêu chuẩn bảo mật. Các tổ chức nên xem lại bảng dưới đây. Nếu muốn có thời gian chờ lâu hơn dựa trên hồ sơ rủi ro của ứng dụng, thì giá trị NIST sẽ đóng vai trò là giới hạn tối đa cho thời gian chờ không hoạt động của phiên.

L1 trong ngữ cảnh này là IAL1/AAL1, L2 là IAL2/AAL3, L3 là IAL3/AAL3. Đối với cả IAL2/AAL2 và IAL3/AAL3, thời gian chờ không hoạt động càng ngắn thì giới hạn thời gian không hoạt động để bị đăng xuất hoặc xác thực lại để tiếp tục phiên càng thấp.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.3.1** | [MOVED TO 3.8.1] | | | | | |
| **3.3.2** | [MODIFIED, SPLIT TO 3.3.5] Xác minh rằng có thời gian tồn tại phiên tối đa tuyệt đối sao cho yêu cầu xác thực lại ít nhất 30 ngày một lần đối với ứng dụng L1 hoặc 12 giờ một lần đối với ứng dụng L2 và L3. | ✓ | ✓ | ✓ | 613 | 7.2 |
| **3.3.3** | [MOVED TO 3.8.2] | | | | | |
| **3.3.4** | [MOVED TO 3.8.3] | | | | | |
| **3.3.5** | [ADDED, SPLIT FROM 3.3.2] Xác minh rằng yêu cầu xác thực lại sau 30 phút không hoạt động đối với ứng dụng L2 hoặc sau 15 phút không hoạt động đối với ứng dụng L3. | | ✓ | ✓ | 613 | 7.2 |

## V3.4 Cookie-based Session Management

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.4.1** | Xác minh rằng các mã thông báo phiên dựa trên cookie có thuộc tính 'Secure'. | ✓ | ✓ | ✓ | 614 | 7.1.1 |
| **3.4.2** | [MODIFIED] Xác minh rằng các mã thông báo phiên dựa trên cookie không thể đọc được bằng các tập lệnh phía máy khách. Cookie mã thông báo phiên phải có thuộc tính 'HttpOnly' được đặt và giá trị mã thông báo phiên chỉ nên được chuyển đến máy khách thông qua tiêu đề Set-Cookie. | ✓ | ✓ | ✓ | 1004 | 7.1.1 |
| **3.4.3** | Xác minh rằng các mã thông báo phiên dựa trên cookie sử dụng thuộc tính 'SameSite' để hạn chế sự tiếp xúc với các cuộc tấn công giả mạo yêu cầu trên nhiều trang web. | ✓ | ✓ | ✓ | 1275 | 7.1.1 |
| **3.4.4** | Xác minh rằng các mã thông báo phiên dựa trên cookie sử dụng tiền tố "__Host-" để cookie chỉ được gửi đến máy chủ ban đầu đặt cookie. | ✓ | ✓ | ✓ | 16 | 7.1.1 |
| **3.4.5** | [DELETED, DEPRECATED BY 50.1.1] | | | | | |

## V3.5 Token-based Session Management

Quản lý phiên dựa trên mã thông báo bao gồm JWT, OAuth, SAML và khóa API. Trong số này, khóa API được biết là yếu và không nên được sử dụng trong mã mới. JWT và mã thông báo SAML là các ví dụ về mã thông báo phiên không trạng thái. Tất cả các kiểm tra được ghi chú bên dưới phải được thực thi bởi một dịch vụ phụ trợ đáng tin cậy như đã lưu ý ở trên.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.5.1** | [GRAMMAR] Xác minh rằng ứng dụng cho phép người dùng thu hồi mã thông báo OAuth tạo mối quan hệ tin cậy với các ứng dụng được liên kết. | | ✓ | ✓ | 290 | 7.1.2 |
| **3.5.2** | [MOVED TO 3.1.3] | | | | | |
| **3.5.3** | [MODIFIED, LEVEL L2 > L1] Xác minh rằng các mã thông báo phiên không trạng thái sử dụng chữ ký số để bảo vệ chống lại giả mạo và điều này được kiểm tra trước khi xử lý thêm. | ✓ | ✓ | ✓ | 345 | |
| **3.5.4** | [ADDED] Xác minh rằng các mã thông báo không trạng thái được kiểm tra hết hạn trước khi xử lý thêm. | ✓ | ✓ | ✓ | 613 | |
| **3.5.5** | [ADDED] Xác minh rằng chỉ các thuật toán ký được cho phép mới được phép đối với mã thông báo không trạng thái. | ✓ | ✓ | ✓ | 757 | |
| **3.5.6** | [ADDED] Xác minh rằng các thuộc tính nhạy cảm với bảo mật khác của mã thông báo không trạng thái đang được xác minh. Ví dụ: trong JWT, điều này có thể bao gồm nhà phát hành, chủ đề và đối tượng. | ✓ | ✓ | ✓ | 287 | |
| **3.5.7** | [ADDED] Xác minh rằng tất cả các mã thông báo không trạng thái đang hoạt động, đang được dựa vào để đưa ra quyết định kiểm soát truy cập, đều bị thu hồi khi quản trị viên thay đổi quyền hoặc vai trò của người dùng. | ✓ | ✓ | ✓ | 613 | |

## V3.6 Federated Re-authentication

Phần này liên quan đến những người viết mã Bên dựa vào (RP) hoặc mã Nhà cung cấp Dịch vụ Thông tin Đăng nhập (CSP). Nếu dựa vào mã triển khai các tính năng này, hãy đảm bảo rằng các vấn đề này được xử lý chính xác.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.6.1** | Xác minh rằng các Bên dựa vào (RP) chỉ định thời gian xác thực tối đa cho các Nhà cung cấp Dịch vụ Thông tin Đăng nhập (CSP) và CSP xác thực lại người dùng nếu họ không sử dụng phiên trong khoảng thời gian đó. | | | ✓ | 613 | 7.2.1 |
| **3.6.2** | Xác minh rằng các Nhà cung cấp Dịch vụ Thông tin Đăng nhập (CSP) thông báo cho các Bên dựa vào (RP) về sự kiện xác thực cuối cùng, để cho phép RP xác định xem họ có cần xác thực lại người dùng hay không. | | | ✓ | 613 | 7.2.1 |

## V3.7 Defenses Against Session Management Exploits

Có một số ít các cuộc tấn công quản lý phiên, một số liên quan đến trải nghiệm người dùng (UX) của các phiên. Trước đây, dựa trên các yêu cầu của ISO 27002, ASVS đã yêu cầu chặn nhiều phiên đồng thời. Việc chặn các phiên đồng thời không còn phù hợp nữa, không chỉ vì người dùng hiện đại có nhiều thiết bị hoặc ứng dụng là API không có phiên trình duyệt, mà trong hầu hết các triển khai này, trình xác thực cuối cùng sẽ thắng, thường là kẻ tấn công. Phần này cung cấp hướng dẫn hàng đầu về việc ngăn chặn, trì hoãn và phát hiện các cuộc tấn công quản lý phiên bằng cách sử dụng mã.

### Description of the half-open Attack

Đầu năm 2018, một số tổ chức tài chính đã bị xâm nhập bằng cách sử dụng thứ mà những kẻ tấn công gọi là "cuộc tấn công nửa mở". Thuật ngữ này đã bị mắc kẹt trong ngành. Những kẻ tấn công đã tấn công nhiều tổ chức với các cơ sở mã độc quyền khác nhau, và thực sự có vẻ như các cơ sở mã khác nhau trong cùng một tổ chức. Cuộc tấn công nửa mở khai thác lỗ hổng mẫu thiết kế thường có trong nhiều hệ thống xác thực, quản lý phiên và kiểm soát truy cập.

Kẻ tấn công bắt đầu một cuộc tấn công nửa mở bằng cách cố gắng khóa, đặt lại hoặc khôi phục thông tin đăng nhập. Một mẫu thiết kế quản lý phiên phổ biến sử dụng lại các đối tượng/mô hình phiên hồ sơ người dùng giữa mã chưa được xác thực, được xác thực một nửa (đặt lại mật khẩu, quên tên người dùng) và mã được xác thực đầy đủ. Mẫu thiết kế này tạo ra một đối tượng hoặc mã thông báo phiên hợp lệ có chứa hồ sơ của nạn nhân, bao gồm cả hàm băm mật khẩu và vai trò. Nếu kiểm tra kiểm soát truy cập trong bộ điều khiển hoặc bộ định tuyến không xác minh chính xác rằng người dùng đã đăng nhập đầy đủ, kẻ tấn công sẽ có thể hoạt động như người dùng. Các cuộc tấn công có thể bao gồm thay đổi mật khẩu của người dùng thành một giá trị đã biết, cập nhật địa chỉ email để thực hiện đặt lại mật khẩu hợp lệ, tắt xác thực đa yếu tố hoặc đăng ký thiết bị MFA mới, tiết lộ hoặc thay đổi khóa API, v.v.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.7.1** | [MODIFIED] Xác minh rằng ứng dụng yêu cầu xác thực lại hoặc xác minh phụ trước khi cho phép các giao dịch có độ nhạy cao, sửa đổi hồ sơ tài khoản hoặc cài đặt xác thực hoặc xuất một lượng lớn dữ liệu nhạy cảm. | ✓ | ✓ | ✓ | 306 | |

## V3.8 Session Termination

Việc chấm dứt phiên có thể được xử lý bởi chính ứng dụng hoặc bởi nhà cung cấp SSO nếu nhà cung cấp SSO đang xử lý việc quản lý phiên thay vì ứng dụng. Có thể cần phải quyết định xem nhà cung cấp SSO có nằm trong phạm vi hay không khi xem xét các yêu cầu trong phần này vì một số yêu cầu có thể được kiểm soát bởi nhà cung cấp.

Việc chấm dứt phiên sẽ dẫn đến yêu cầu xác thực lại và có hiệu lực trên toàn bộ ứng dụng, đăng nhập liên kết (nếu có) và bất kỳ bên dựa vào nào.

Đối với các cơ chế phiên có trạng thái, điều này sẽ chỉ yêu cầu vô hiệu hóa phiên ở phía phụ trợ. Nếu đang sử dụng cơ chế phiên không trạng thái với mã thông báo đã ký, sẽ cần một cách để thu hồi các mã thông báo này.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **3.8.1** | [MODIFIED, MOVED FROM 3.3.1] Xác minh rằng việc đăng xuất và hết hạn chấm dứt phiên của người dùng, do đó nút quay lại hoặc bên dựa vào hạ nguồn không thể tiếp tục phiên đã xác thực. | ✓ | ✓ | ✓ | 613 | 7.1 |
| **3.8.2** | [MODIFIED, LEVEL L2 > L1, MOVED FROM 3.3.3] Xác minh rằng ứng dụng cung cấp tùy chọn chấm dứt tất cả các phiên đang hoạt động khác sau khi thay đổi hoặc xóa thành công bất kỳ yếu tố xác thực nào (bao gồm cả thay đổi mật khẩu thông qua đặt lại hoặc khôi phục và nếu có, cập nhật cài đặt MFA). | ✓ | ✓ | ✓ | 613 | |
| **3.8.3** | [MODIFIED, MOVED FROM 3.3.4] Xác minh rằng người dùng có thể xem và (sau khi nhập lại thông tin đăng nhập) chấm dứt bất kỳ hoặc tất cả các phiên hiện đang hoạt động. | | ✓ | ✓ | 613 | 7.1 |
| **3.8.4** | [ADDED] Xác minh rằng tất cả các trang yêu cầu xác thực đều có quyền truy cập dễ dàng và hiển thị vào chức năng đăng xuất. | | ✓ | ✓ | | |
| **3.8.5** | [ADDED] Xác minh rằng ứng dụng chấm dứt tất cả các phiên đang hoạt động khi tài khoản người dùng bị vô hiệu hóa hoặc xóa (chẳng hạn như nhân viên rời khỏi công ty). | ✓ | ✓ | ✓ | 613 | |
| **3.8.6** | [ADDED] Xác minh rằng quản trị viên ứng dụng có thể chấm dứt các phiên đang hoạt động cho một người dùng cá nhân hoặc cho tất cả người dùng. | ✓ | ✓ | ✓ | 613 | 7.1 |

## References

For more information, see also:

* [OWASP Testing Guide 4.0: Session Management Testing](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/06-Session_Management_Testing/README.html)
* [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
* [Set-Cookie __Host- prefix details](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie#cookie_prefixes)
