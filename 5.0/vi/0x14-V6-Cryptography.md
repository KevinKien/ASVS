# V6 Stored Cryptography

## Control Objective

Đảm bảo rằng một ứng dụng đã xác minh đáp ứng các yêu cầu cấp cao sau:

* Tất cả các mô-đun mã hóa thất bại một cách an toàn và các lỗi được xử lý chính xác.
* Một trình tạo số ngẫu nhiên phù hợp được sử dụng.
* Quyền truy cập vào các khóa được quản lý an toàn.

## V6.1 Data Classification

Tài sản quan trọng nhất là dữ liệu được xử lý, lưu trữ hoặc truyền bởi một ứng dụng. Luôn thực hiện đánh giá tác động quyền riêng tư để phân loại chính xác nhu cầu bảo vệ dữ liệu của bất kỳ dữ liệu được lưu trữ nào.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **6.1.1** | Xác minh rằng dữ liệu riêng tư được quản lý được lưu trữ dưới dạng được mã hóa khi không sử dụng, chẳng hạn như Thông tin nhận dạng Cá nhân (PII), thông tin cá nhân nhạy cảm hoặc dữ liệu được đánh giá có khả năng tuân theo GDPR của EU. | | ✓ | ✓ | 311 |
| **6.1.2** | Xác minh rằng dữ liệu y tế được quản lý được lưu trữ dưới dạng được mã hóa khi không sử dụng, chẳng hạn như hồ sơ y tế, chi tiết thiết bị y tế hoặc hồ sơ nghiên cứu đã được hủy ẩn danh. | | ✓ | ✓ | 311 |
| **6.1.3** | Xác minh rằng dữ liệu tài chính được quản lý được lưu trữ dưới dạng được mã hóa khi không sử dụng, chẳng hạn như tài khoản tài chính, mặc định hoặc lịch sử tín dụng, hồ sơ thuế, lịch sử thanh toán, người thụ hưởng hoặc hồ sơ thị trường hoặc nghiên cứu đã được hủy ẩn danh. | | ✓ | ✓ | 311 |

## V6.2 Algorithms

Những tiến bộ gần đây trong lĩnh vực mật mã có nghĩa là các thuật toán và độ dài khóa trước đây an toàn không còn an toàn hoặc đủ để bảo vệ dữ liệu. Do đó, cần có khả năng thay đổi thuật toán.

Mặc dù phần này không dễ dàng kiểm tra thâm nhập, nhưng các nhà phát triển nên coi toàn bộ phần này là bắt buộc mặc dù L1 bị thiếu trong hầu hết các mục.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **6.2.1** | Xác minh rằng tất cả các mô-đun mật mã đều thất bại một cách an toàn và các lỗi được xử lý theo cách không cho phép các cuộc tấn công Padding Oracle. | ✓ | ✓ | ✓ | 310 |
| **6.2.2** | Xác minh rằng các thuật toán, chế độ và thư viện mật mã đã được chứng minh trong ngành hoặc được chính phủ phê duyệt được sử dụng, thay vì mật mã được mã hóa tùy chỉnh. | | ✓ | ✓ | 327 |
| **6.2.3** | [DELETED, DUPLICATE OF 6.2.5] | | | | |
| **6.2.4** | Xác minh rằng số ngẫu nhiên, thuật toán mã hóa hoặc băm, độ dài khóa, vòng, mã hóa hoặc chế độ có thể được cấu hình lại, nâng cấp hoặc hoán đổi bất cứ lúc nào, để bảo vệ chống lại các lỗ hổng mật mã. | | ✓ | ✓ | 326 |
| **6.2.5** | [MODIFIED] Xác minh rằng các chế độ khối không an toàn đã biết (tức là ECB, v.v.), chế độ đệm (tức là PKCS#1 v1.5, v.v.), mã hóa với kích thước khối nhỏ (tức là Triple-DES, Blowfish, v.v.) và các thuật toán băm yếu (tức là MD5, SHA1, v.v.) không được sử dụng. | | ✓ | ✓ | 326 |
| **6.2.6** | [MODIFIED, LEVEL L2 > L3] Xác minh rằng nonce, vectơ khởi tạo và các số sử dụng một lần khác không được sử dụng cho nhiều hơn một cặp khóa mã hóa/phần tử dữ liệu. Phương pháp tạo phải phù hợp với thuật toán đang được sử dụng. | | | ✓ | 326 |
| **6.2.7** | Xác minh rằng dữ liệu được mã hóa được xác thực thông qua chữ ký, chế độ mã hóa đã xác thực hoặc HMAC để đảm bảo rằng văn bản mã hóa không bị thay đổi bởi một bên trái phép. | | | ✓ | 326 |
| **6.2.8** | Xác minh rằng tất cả các hoạt động mật mã đều có thời gian không đổi, không có hoạt động 'đoản mạch' trong các phép so sánh, tính toán hoặc trả về, để tránh rò rỉ thông tin. | | | ✓ | 385 |

## V6.3 Random Values

Trình tạo Số giả ngẫu nhiên Bảo mật Mật mã (CSPRNG) cực kỳ khó để thực hiện đúng. Nói chung, các nguồn entropy tốt trong một hệ thống sẽ nhanh chóng cạn kiệt nếu bị lạm dụng quá mức, nhưng các nguồn có độ ngẫu nhiên thấp hơn có thể dẫn đến các khóa và bí mật có thể đoán trước được.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **6.3.1** | [MODIFIED] Xác minh rằng tất cả các số ngẫu nhiên, tên tệp ngẫu nhiên và chuỗi ngẫu nhiên được tạo bằng trình tạo số giả ngẫu nhiên an toàn về mặt mật mã (CSPRNG) khi các giá trị ngẫu nhiên này nhằm mục đích không để kẻ tấn công đoán được. | | ✓ | ✓ | 338 |
| **6.3.2** | [MODIFIED] Xác minh rằng GUID được tạo bằng cách triển khai thuật toán GUID v4 sử dụng trình tạo số giả ngẫu nhiên an toàn về mặt mật mã (CSPRNG). GUID được tạo bằng các phiên bản thuật toán khác hoặc sử dụng trình tạo số giả ngẫu nhiên không đủ an toàn có thể đoán trước được. | | ✓ | ✓ | 338 |
| **6.3.3** | Xác minh rằng các số ngẫu nhiên được tạo với entropy thích hợp ngay cả khi ứng dụng đang chịu tải nặng hoặc ứng dụng giảm cấp độ một cách duyên dáng trong những trường hợp như vậy. | | | ✓ | 338 |

## V6.4 Secret Management

Mặc dù phần này không dễ dàng kiểm tra thâm nhập, nhưng các nhà phát triển nên coi toàn bộ phần này là bắt buộc mặc dù L1 bị thiếu trong hầu hết các mục.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **6.4.1** | [MODIFIED] Xác minh rằng giải pháp quản lý bí mật như hầm khóa được sử dụng để tạo, lưu trữ, kiểm soát truy cập và hủy các bí mật phụ trợ một cách an toàn như thông tin đăng nhập tài khoản dịch vụ hoặc ứng dụng bên thứ 3. | | ✓ | ✓ | 798 |
| **6.4.2** | [MODIFIED] Xác minh rằng dữ liệu khóa không được hiển thị cho ứng dụng (cả mặt trước và mặt sau) mà thay vào đó sử dụng mô-đun bảo mật biệt lập như hầm để thực hiện các hoạt động mật mã. | | ✓ | ✓ | 320 |

## References

For more information, see also:

* [OWASP Testing Guide 4.0: Testing for Weak Cryptography](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/README.html)
* [OWASP Cheat Sheet: Cryptographic Storage](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html)
* [FIPS 140-3](https://csrc.nist.gov/pubs/fips/140-3/final)
