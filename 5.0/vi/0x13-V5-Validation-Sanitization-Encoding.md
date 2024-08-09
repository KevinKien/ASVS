# V5 Validation, Sanitization and Encoding

## Control Objective

Điểm yếu bảo mật ứng dụng web phổ biến nhất là sử dụng nội dung không đáng tin cậy trong ngữ cảnh không an toàn mà không có bất kỳ mã hóa đầu ra, tham số hóa truy vấn hoặc cơ chế bảo vệ xử lý đầu ra nào khác. Điểm yếu này dẫn đến hầu hết các lỗ hổng nghiêm trọng trong các ứng dụng web, chẳng hạn như Kịch bản trên nhiều trang web (XSS), SQL injection, OS command injection, template injection, log injection, LDAP injection, v.v.

Đảm bảo rằng một ứng dụng đã được xác minh đáp ứng các yêu cầu cấp cao sau:

* Kiến trúc xác thực đầu vào và mã hóa đầu ra có một quy trình đã được thống nhất để ngăn chặn các cuộc tấn công tiêm.
* Dữ liệu đầu vào được nhập mạnh, xác thực, kiểm tra phạm vi hoặc độ dài, hoặc tệ nhất là được làm sạch hoặc lọc.
* Dữ liệu đầu ra được mã hóa hoặc thoát theo ngữ cảnh của dữ liệu càng gần trình thông dịch càng tốt.

Với kiến trúc ứng dụng web hiện đại, mã hóa đầu ra quan trọng hơn bao giờ hết. Thật khó để cung cấp xác thực đầu vào mạnh mẽ trong một số tình huống nhất định, vì vậy việc sử dụng API an toàn hơn như truy vấn tham số hóa, khung mẫu tự động thoát hoặc mã hóa đầu ra được lựa chọn cẩn thận là rất quan trọng đối với bảo mật của ứng dụng.

## V5.1 Input Validation

Đầu vào có thể đến từ nhiều nguồn khác nhau bao gồm các trường biểu mẫu HTML, yêu cầu REST, tham số URL, tiêu đề HTTP, cookie, tệp trên đĩa, cơ sở dữ liệu, API bên ngoài, v.v.

Các biện pháp kiểm soát xác thực đầu vào được triển khai đúng cách, sử dụng danh sách cho phép tích cực và kiểu dữ liệu mạnh mẽ, cung cấp một biện pháp thực thi quan trọng các biện pháp kiểm soát logic nghiệp vụ xung quanh loại dữ liệu mà ứng dụng dự kiến sẽ nhận được. Tuy nhiên, ngoại trừ những trường hợp cụ thể, nó thường không nhằm mục đích ngăn chặn các cuộc tấn công cụ thể.

Xác thực đầu vào vẫn cung cấp vệ sinh bảo mật có giá trị và nên được áp dụng cho tất cả các đầu vào nếu có thể. Tuy nhiên, vì xác thực đầu vào không phải là một chiến lược bảo mật hoàn chỉnh, người ta cũng nên sử dụng hộp cát, vệ sinh, mã hóa và tham số hóa bất cứ khi nào đầu vào được sử dụng trong ngữ cảnh có khả năng nguy hiểm.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.1.1** | [MODIFIED] Xác minh rằng ứng dụng có biện pháp bảo vệ chống lại các cuộc tấn công ô nhiễm tham số HTTP, đặc biệt nếu khung ứng dụng không phân biệt nguồn gốc của các tham số yêu cầu (chuỗi truy vấn, tham số nội dung, cookie hoặc tiêu đề). | ✓ | ✓ | ✓ | 235 |
| **5.1.2** | Xác minh rằng các khung bảo vệ chống lại các cuộc tấn công gán tham số hàng loạt hoặc ứng dụng có các biện pháp đối phó để bảo vệ chống lại việc gán tham số không an toàn, chẳng hạn như đánh dấu các trường là riêng tư hoặc tương tự. | ✓ | ✓ | ✓ | 915 |
| **5.1.3** | [MODIFIED] Xác minh rằng tất cả đầu vào đều được xác thực bằng xác thực dương, sử dụng danh sách các giá trị hoặc mẫu được cho phép. | ✓ | ✓ | ✓ | 20 |
| **5.1.4** | [GRAMMAR] Xác minh rằng dữ liệu có cấu trúc được nhập mạnh và được xác thực dựa trên lược đồ đã xác định bao gồm các ký tự, độ dài và mẫu được phép (ví dụ: số thẻ tín dụng, địa chỉ email, số điện thoại hoặc xác thực rằng hai trường liên quan là hợp lý, chẳng hạn như kiểm tra xem vùng ngoại ô và mã zip có khớp không). | ✓ | ✓ | ✓ | 20 |
| **5.1.5** | [MODIFIED, SPLIT TO 50.7.1] Xác minh rằng ứng dụng sẽ chỉ tự động chuyển hướng người dùng đến một URL khác trực tiếp từ URL ứng dụng nơi đích xuất hiện trong danh sách cho phép. | ✓ | ✓ | ✓ | 601 |
| **5.1.6** | [ADDED] Xác minh rằng đầu vào không đáng tin cậy được xác thực về độ dài trước khi được đưa vào cookie (bao gồm cả một phần của JWT) và tổng độ dài tên và giá trị của cookie không quá 4096 byte. | | ✓ | ✓ | |

## V5.2 Sanitization and Sandboxing

Xác thực đầu vào là một chủ đề phức tạp.

Đôi khi xác thực đầu vào sẽ không hữu ích cho bảo mật, những lúc khác nó sẽ giúp ích ở mức độ vừa phải, trong khi những lúc khác nó sẽ là cơ bản cho việc bảo vệ bảo mật. Nó phụ thuộc vào loại dữ liệu và việc sử dụng dữ liệu đó để xác định mức độ hiệu quả của xác thực đầu vào.

Ví dụ:

* Sanitization: Khi người dùng đang tạo HTML, biện pháp bảo vệ tiêu chuẩn là tiêu chuẩn hóa HTML để loại bỏ Thực hiện vệ sinh JSON trước khi sử dụng trình phân tích cú pháp JSON và tất nhiên là vệ sinh HTML để bảo vệ XSS
* Escaping: Được thực hiện trong UI khi bạn muốn giữ nguyên nội dung hiển thị như người dùng đã nhập, cũng để bảo vệ một số lần tiêm như bảo vệ LDAP injection
* Parameterization: Đối với SQL Injection
* Sandboxing: Khi bạn không Sanitization HTML vì lý do nào đó và cần đổ nội dung có khả năng hoạt động trên trang web của mình, thì việc sử dụng hộp cát iframe là rất quan trọng. CSP cũng có một số khả năng hộp cát.
* URL trong giao diện người dùng web nên chặn JavaScript và URL dữ liệu để bảo vệ chống lại các cuộc tấn công XSS. Tuy nhiên, điều quan trọng cần lưu ý là thông thường, ngay cả dữ liệu hợp lệ vẫn có thể gây ra mối đe dọa.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.2.1** | [MODIFIED] Xác minh rằng tất cả đầu vào HTML không đáng tin cậy từ các trình soạn thảo WYSIWYG hoặc tương tự đều được vệ sinh đúng cách bằng thư viện vệ sinh HTML nổi tiếng và an toàn hoặc tính năng khung. | ✓ | ✓ | ✓ | 116 |
| **5.2.2** | Xác minh rằng dữ liệu không có cấu trúc được vệ sinh để thực thi các biện pháp an toàn như ký tự và độ dài được phép. | ✓ | ✓ | ✓ | 138 |
| **5.2.3** | Xác minh rằng ứng dụng vệ sinh đầu vào của người dùng trước khi chuyển đến hệ thống thư để bảo vệ chống lại các cuộc tấn công tiêm SMTP hoặc IMAP. | ✓ | ✓ | ✓ | 147 |
| **5.2.4** | Xác minh rằng ứng dụng tránh sử dụng eval () hoặc các tính năng thực thi mã động khác. Trong trường hợp không có giải pháp thay thế, bất kỳ đầu vào của người dùng nào được bao gồm phải được vệ sinh hoặc đưa vào hộp cát trước khi được thực thi. | ✓ | ✓ | ✓ | 95 |
| **5.2.5** | [MODIFIED] Xác minh rằng ứng dụng bảo vệ chống lại các cuộc tấn công tiêm mẫu bằng cách không cho phép xây dựng mẫu dựa trên đầu vào không đáng tin cậy. Trong trường hợp không có giải pháp thay thế, bất kỳ đầu vào không đáng tin cậy nào được bao gồm động trong quá trình tạo mẫu phải được vệ sinh hoặc xác thực nghiêm ngặt. | ✓ | ✓ | ✓ | 94 |
| **5.2.6** | Xác minh rằng ứng dụng bảo vệ chống lại các cuộc tấn công SSRF, bằng cách xác thực hoặc vệ sinh dữ liệu không đáng tin cậy hoặc siêu dữ liệu tệp HTTP, chẳng hạn như tên tệp và trường nhập URL, đồng thời sử dụng danh sách cho phép các giao thức, miền, đường dẫn và cổng. | ✓ | ✓ | ✓ | 918 |
| **5.2.7** | Xác minh rằng ứng dụng vệ sinh, vô hiệu hóa hoặc đưa vào hộp cát nội dung có thể viết kịch bản Đồ họa Vector có thể mở rộng (SVG) do người dùng cung cấp, đặc biệt là khi chúng liên quan đến XSS do tập lệnh nội tuyến và đối tượng nước ngoài gây ra. | ✓ | ✓ | ✓ | 159 |
| **5.2.8** | Xác minh rằng ứng dụng vệ sinh, vô hiệu hóa hoặc đưa vào hộp cát nội dung ngôn ngữ mẫu có thể viết kịch bản hoặc biểu thức do người dùng cung cấp, chẳng hạn như Markdown, CSS hoặc biểu định kiểu XSL, BBCode hoặc tương tự. | ✓ | ✓ | ✓ | 94 |
| **5.2.9** | [ADDED] Xác minh rằng ứng dụng sử dụng dấu gạch chéo để thoát chính xác các ký tự đặc biệt đang được sử dụng trong biểu thức chính quy để đảm bảo chúng không bị hiểu sai thành ký tự điều khiển. | ✓ | ✓ | ✓ | 624 |
| **5.2.10** | [ADDED] Xác minh rằng các biểu thức chính quy không có các phần tử gây ra sự quay lui theo cấp số nhân và đảm bảo đầu vào không đáng tin cậy được vệ sinh để giảm thiểu các cuộc tấn công ReDoS hoặc Runaway Regex. | ✓ | ✓ | ✓ | 1333 |
| **5.2.11** | [ADDED] Xác minh rằng ứng dụng vệ sinh đầu vào không đáng tin cậy một cách thích hợp trước khi sử dụng trong các truy vấn Giao diện Đặt tên và Thư mục Java (JNDI) và JNDI được định cấu hình càng an toàn càng tốt để ngăn chặn các cuộc tấn công tiêm JNDI. | ✓ | ✓ | ✓ | 917 |
| **5.2.12** | [ADDED] Xác minh rằng ứng dụng vệ sinh nội dung trước khi gửi đến memcache để ngăn chặn các cuộc tấn công tiêm. | | ✓ | ✓ | |
| **5.2.13** | [MODIFIED, MOVED FROM 5.4.2] Xác minh rằng các chuỗi định dạng có thể phân giải theo cách không mong muốn hoặc độc hại khi được sử dụng sẽ được vệ sinh trước khi xử lý. | | ✓ | ✓ | 134 |

## V5.3 Output Encoding and Injection Prevention

Mã hóa đầu ra gần hoặc liền kề với trình thông dịch đang sử dụng là rất quan trọng đối với bảo mật của bất kỳ ứng dụng nào. Thông thường, mã hóa đầu ra không được duy trì mà được sử dụng để hiển thị đầu ra một cách an toàn trong ngữ cảnh thích hợp để sử dụng ngay lập tức. Không mã hóa đầu ra sẽ dẫn đến một ứng dụng không an toàn, có thể bị tiêm và không an toàn.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.3.1** | [MODIFIED] Xác minh rằng mã hóa đầu ra cho phản hồi HTTP/tài liệu HTML/tài liệu XML có liên quan đến ngữ cảnh bắt buộc, chẳng hạn như mã hóa các ký tự có liên quan cho các phần tử HTML, thuộc tính HTML, nhận xét HTML, JavaScript, CSS hoặc tiêu đề HTTP, để tránh thay đổi cấu trúc tin nhắn hoặc tài liệu. | ✓ | ✓ | ✓ | 116 |
| **5.3.2** | [DELETED, DUPLICATE OF 14.4.1] | | | | |
| **5.3.3** | Xác minh rằng việc thoát đầu ra theo ngữ cảnh, tốt nhất là tự động - hoặc tệ nhất là thủ công - bảo vệ chống lại XSS phản xạ, XSS lưu trữ và XSS dựa trên DOM. | ✓ | ✓ | ✓ | 79 |
| **5.3.4** | [MODIFIED] Xác minh rằng việc lựa chọn dữ liệu hoặc truy vấn cơ sở dữ liệu (ví dụ: SQL, HQL, NoSQL, Cypher) sử dụng các truy vấn tham số hóa, ORM, khung thực thể hoặc được bảo vệ khỏi SQL Injection và các cuộc tấn công tiêm cơ sở dữ liệu khác. Điều này cũng nên được xem xét khi viết các thủ tục được lưu trữ. | ✓ | ✓ | ✓ | 89 |
| **5.3.5** | [DELETED, DUPLICATE OF 5.3.4] | | | | |
| **5.3.6** | [MODIFIED] Xác minh rằng ứng dụng bảo vệ chống lại các cuộc tấn công tiêm JSON. | ✓ | ✓ | ✓ | 75 |
| **5.3.7** | Xác minh rằng ứng dụng bảo vệ chống lại các lỗ hổng tiêm LDAP hoặc các biện pháp kiểm soát bảo mật cụ thể để ngăn chặn tiêm LDAP đã được triển khai. | ✓ | ✓ | ✓ | 90 |
| **5.3.8** | Xác minh rằng ứng dụng bảo vệ chống lại tiêm lệnh OS và các lệnh gọi hệ điều hành sử dụng các truy vấn OS tham số hóa hoặc sử dụng mã hóa đầu ra dòng lệnh theo ngữ cảnh. | ✓ | ✓ | ✓ | 78 |
| **5.3.9** | [DELETED, DUPLICATE OF 12.3.2, 12.3.3] | | | | |
| **5.3.10** | Xác minh rằng ứng dụng bảo vệ chống lại các cuộc tấn công tiêm XPath hoặc tiêm XML. | ✓ | ✓ | ✓ | 643 |
| **5.3.11** | [ADDED] Xác minh rằng ứng dụng được bảo vệ chống lại CSV và Tiêm Công thức. Ứng dụng nên tuân theo các quy tắc thoát được xác định trong RFC4180 2.6 và 2.7 khi xuất tệp CSV. Ứng dụng nên thoát các ký tự đặc biệt bao gồm '=', '+', '-', '@' '\t' (tab) và '\00' (ký tự null) bằng cách sử dụng dấu nháy đơn, nếu chúng là ký tự đầu tiên trong một trường, khi xuất tệp CSV và các định dạng bảng tính khác như xls, xlsx, odf. | ✓ | ✓ | ✓ | 1236 |
| **5.3.12** | [ADDED] Xác minh rằng các bộ xử lý LaTeX được định cấu hình an toàn (chẳng hạn như không sử dụng cờ "--shell-escape") và danh sách cho phép lệnh được sử dụng để ngăn chặn các cuộc tấn công tiêm LaTeX. | | ✓ | ✓ | |
| **5.3.13** | [ADDED, SPLIT FROM 5.3.1] Xác minh rằng khi xây dựng URL động, dữ liệu không đáng tin cậy được mã hóa theo ngữ cảnh của nó (ví dụ: mã hóa URL hoặc mã hóa base64url cho các tham số truy vấn hoặc đường dẫn). Đảm bảo rằng chỉ các giao thức URL an toàn mới được phép (ví dụ: không cho phép javascript: hoặc data:). | ✓ | ✓ | ✓ | 116 |
| **5.3.14** | [ADDED] Xác minh rằng mã hóa đầu ra có liên quan đến trình thông dịch và ngữ cảnh bắt buộc trong bất kỳ ngữ cảnh nào mà trình thông dịch có khả năng nguy hiểm, không được đề cập ở trên, đang được sử dụng. | | ✓ | ✓ | |

Lưu ý: Sử dụng các truy vấn tham số hóa hoặc thoát SQL không phải lúc nào cũng đủ; tên bảng và cột, ORDER BY, v.v., không thể thoát được. Việc đưa dữ liệu do người dùng cung cấp đã thoát vào các trường này dẫn đến truy vấn không thành công hoặc SQL injection.

Lưu ý: Định dạng SVG cho phép rõ ràng tập lệnh ECMA trong hầu hết mọi ngữ cảnh, vì vậy có thể không thể chặn hoàn toàn tất cả các vectơ XSS SVG. Nếu yêu cầu tải lên SVG, chúng tôi đặc biệt khuyên bạn nên phân phát các tệp đã tải lên này dưới dạng text/plain hoặc sử dụng một miền nội dung do người dùng cung cấp riêng biệt để ngăn XSS thành công chiếm quyền điều khiển ứng dụng.

## V5.4 Memory, String, and Unmanaged Code

Các yêu cầu sau đây sẽ chỉ áp dụng khi ứng dụng sử dụng ngôn ngữ hệ thống hoặc mã không được quản lý.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.4.1** | Xác minh rằng ứng dụng sử dụng chuỗi an toàn bộ nhớ, sao chép bộ nhớ an toàn hơn và số học con trỏ để phát hiện hoặc ngăn chặn tràn ngăn xếp, bộ đệm hoặc heap. | | ✓ | ✓ | 120 |
| **5.4.2** | [DELETED, MOVED TO 5.2.13] | | | | |
| **5.4.3** | Xác minh rằng các kỹ thuật dấu hiệu, phạm vi và xác thực đầu vào được sử dụng để ngăn chặn tràn số nguyên. | | ✓ | ✓ | 190 |

## V5.5 Deserialization Prevention

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.5.1** | [DELETED, INCORRECT] | | | | |
| **5.5.2** | Xác minh rằng ứng dụng hạn chế chính xác các trình phân tích cú pháp XML chỉ sử dụng cấu hình hạn chế nhất có thể và để đảm bảo rằng các tính năng không an toàn như phân giải các thực thể bên ngoài bị vô hiệu hóa để ngăn chặn các cuộc tấn công Thực thể Bên ngoài XML (XXE). | ✓ | ✓ | ✓ | 611 |
| **5.5.3** | [MODIFIED, MERGED FROM 1.5.2] Xác minh rằng nếu giải tuần tự hóa được sử dụng khi giao tiếp với các máy khách không đáng tin cậy, thì đầu vào được xử lý an toàn. Ví dụ: bằng cách chỉ cho phép danh sách cho phép các loại đối tượng hoặc không cho phép máy khách xác định loại đối tượng để giải tuần tự hóa, để ngăn chặn các cuộc tấn công giải tuần tự hóa. | ✓ | ✓ | ✓ | 502 |
| **5.5.4** | [DELETED, DUPLICATE OF 5.2.4] | | | | |
| **5.5.5** | [MODIFIED, MOVED FROM 13.1.1, LEVEL L1 > L2] Xác minh rằng các trình phân tích cú pháp khác nhau được sử dụng trong ứng dụng cho cùng một kiểu dữ liệu (ví dụ: trình phân tích cú pháp JSON, trình phân tích cú pháp XML, trình phân tích cú pháp URL), thực hiện phân tích cú pháp một cách nhất quán và sử dụng cùng một cơ chế mã hóa ký tự để tránh các sự cố như lỗ hổng Khả năng tương tác JSON hoặc hành vi phân tích cú pháp URI hoặc tệp khác nhau bị khai thác trong các cuộc tấn công Bao gồm Tệp Từ xa (RFI) hoặc Giả mạo Yêu cầu Phía Máy chủ (SSRF). | | ✓ | ✓ | 436 |

## V5.6 Validation and Sanitization Architecture

Với các yêu cầu cụ thể về cú pháp, chúng tôi nói "hãy làm điều đúng đắn" và đây là những yêu cầu để nói "hãy làm điều đó theo đúng thứ tự" và "làm điều đó ở đúng nơi".

Ngoài ra, các yêu cầu nhằm đảm bảo rằng bất cứ khi nào dữ liệu được lưu trữ, nó sẽ được lưu trữ ở trạng thái ban đầu chứ không phải ở trạng thái được mã hóa (ví dụ: mã hóa HTML) để ngăn chặn các sự cố mã hóa kép.

<!--
The requirement belongs here if it is:

  * input validation, sanitization or encoding architecture
  * input validation, sanitization or encoding processing (order)

The requirement does not belong here, if it is:

  * syntax specific or clear input validation, sanitization or encoding requirement

reorg: move it to 1st chapter in the paragraph
-->

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **5.6.1** | [ADDED] Xác minh rằng đầu vào được giải mã hoặc không được thoát thành một dạng chuẩn chỉ một lần và điều này được thực hiện trước khi xử lý thêm đầu vào, ví dụ: nó không được thực hiện sau khi xác thực đầu vào hoặc vệ sinh. | ✓ | ✓ | ✓ | 174 |
| **5.6.2** | [MODIFIED, MOVED FROM 1.5.3, LEVEL L2 > L1] Xác minh rằng ứng dụng được thiết kế để thực thi xác thực đầu vào tại một lớp dịch vụ đáng tin cậy. Mặc dù xác thực phía máy khách cải thiện khả năng sử dụng, nhưng bảo mật không được dựa vào nó. | ✓ | ✓ | ✓ | 602 |
| **5.6.3** | [MODIFIED, MOVED FROM 1.5.4] Xác minh rằng ứng dụng thực hiện mã hóa đầu ra và thoát dưới dạng bước cuối cùng trước khi được trình thông dịch sử dụng theo ý định hoặc bởi chính trình thông dịch. | | ✓ | ✓ | 116 |

## References

For more information, see also:

* [OWASP Testing Guide 4.0: Input Validation Testing](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/07-Input_Validation_Testing/README.html)
* [OWASP Cheat Sheet: Input Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
* [OWASP Testing Guide 4.0: Testing for HTTP Parameter Pollution](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/07-Input_Validation_Testing/04-Testing_for_HTTP_Parameter_Pollution.html)
* [OWASP LDAP Injection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.html)
* [OWASP Testing Guide 4.0: Client-Side Testing](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/11-Client-side_Testing/README)
* [OWASP Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
* [OWASP DOM Based Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)
* [OWASP Java Encoding Project](https://owasp.org/owasp-java-encoder/)
* [OWASP Mass Assignment Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html)
* [DOMPurify - Client-side HTML Sanitization Library](https://github.com/cure53/DOMPurify)
* [XML External Entity (XXE) Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)

For more information on auto-escaping, please see:

* [Reducing XSS by way of Automatic Context-Aware Escaping in Template Systems](https://googleonlinesecurity.blogspot.com/2009/03/reducing-xss-by-way-of-automatic.html)
* [AngularJS Strict Contextual Escaping](https://docs.angularjs.org/api/ng/service/$sce)
* [AngularJS ngBind](https://docs.angularjs.org/api/ng/directive/ngBind)
* [Angular Sanitization](https://angular.io/guide/security#sanitization-and-security-contexts)
* [Angular Security](https://angular.io/guide/security)
* [ReactJS Escaping](https://reactjs.org/docs/introducing-jsx.html#jsx-prevents-injection-attacks)
* [Improperly Controlled Modification of Dynamically-Determined Object Attributes](https://cwe.mitre.org/data/definitions/915.html)

For more information on deserialization or parsing issues, please see:

* [OWASP Deserialization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html)
* [OWASP Deserialization of Untrusted Data Guide](https://owasp.org/www-community/vulnerabilities/Deserialization_of_untrusted_data)
* [An Exploration of JSON Interoperability Vulnerabilities](https://bishopfox.com/blog/json-interoperability-vulnerabilities)
* [Orange Tsai - A New Era of SSRF Exploiting URL Parser In Trending Programming Languages](https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf)
