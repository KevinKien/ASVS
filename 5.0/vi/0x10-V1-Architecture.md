# V1 Architecture, Design and Threat Modeling

## Control Objective

Kiến trúc bảo mật gần như đã trở thành một nghệ thuật bị lãng quên trong nhiều tổ chức. Thời đại của kiến trúc sư doanh nghiệp đã qua trong kỷ nguyên DevSecOps. Lĩnh vực bảo mật ứng dụng phải bắt kịp và áp dụng các nguyên tắc bảo mật linh hoạt đồng thời giới thiệu lại các nguyên tắc kiến trúc bảo mật hàng đầu cho các chuyên gia phần mềm. Kiến trúc không phải là một triển khai, mà là một cách suy nghĩ về một vấn đề có khả năng có nhiều câu trả lời khác nhau và không có một câu trả lời "chính xác" duy nhất nào. Thông thường, bảo mật bị coi là không linh hoạt và yêu cầu các nhà phát triển sửa mã theo một cách cụ thể, trong khi các nhà phát triển có thể biết một cách tốt hơn nhiều để giải quyết vấn đề. Không có giải pháp đơn lẻ, đơn giản nào cho kiến trúc và giả vờ ngược lại là một sự bất lợi cho lĩnh vực kỹ thuật phần mềm.

Một triển khai cụ thể của một ứng dụng web có khả năng sẽ được sửa đổi liên tục trong suốt vòng đời của nó, nhưng kiến trúc tổng thể có thể sẽ hiếm khi thay đổi mà chỉ phát triển chậm. Kiến trúc bảo mật cũng giống như vậy - chúng ta cần xác thực ngày hôm nay, chúng ta sẽ cần xác thực vào ngày mai và chúng ta sẽ cần nó trong năm năm tới. Nếu chúng ta đưa ra quyết định đúng đắn ngay hôm nay, chúng ta có thể tiết kiệm rất nhiều công sức, thời gian và tiền bạc nếu chúng ta chọn và sử dụng lại các giải pháp tuân thủ kiến trúc. Ví dụ, một thập kỷ trước, xác thực đa yếu tố hiếm khi được triển khai.

Nếu các nhà phát triển đã đầu tư vào một mô hình nhà cung cấp danh tính an toàn duy nhất, chẳng hạn như danh tính liên kết SAML, thì nhà cung cấp danh tính có thể được cập nhật để kết hợp các yêu cầu mới như tuân thủ NIST SP 800-63, đồng thời không thay đổi giao diện của ứng dụng ban đầu. Nếu nhiều ứng dụng chia sẻ cùng một kiến trúc bảo mật và do đó cùng một thành phần đó, thì tất cả chúng đều được hưởng lợi từ bản nâng cấp này cùng một lúc. Tuy nhiên, SAML có thể không phải lúc nào cũng là giải pháp xác thực phù hợp nhất - có thể cần phải hoán đổi nó cho các giải pháp khác khi các yêu cầu thay đổi. Những thay đổi như thế này hoặc là phức tạp, tốn kém đến mức cần phải viết lại hoàn toàn hoặc hoàn toàn không thể thực hiện được nếu không có kiến trúc bảo mật.

Trong chương này, ASVS bao gồm các khía cạnh chính của bất kỳ kiến trúc bảo mật hợp lý nào: tính khả dụng, tính bảo mật, tính toàn vẹn xử lý, tính không thể chối cãi và quyền riêng tư. Mỗi nguyên tắc bảo mật này phải được tích hợp và là bản chất của tất cả các ứng dụng. Điều quan trọng là phải "dịch chuyển sang trái", bắt đầu bằng việc cho phép nhà phát triển có danh sách kiểm tra mã hóa an toàn, cố vấn và đào tạo, mã hóa và kiểm thử, xây dựng, triển khai, cấu hình và vận hành, và kết thúc bằng kiểm tra độc lập tiếp theo để đảm bảo rằng tất cả các biện pháp kiểm soát bảo mật đều có mặt và hoạt động. Bước cuối cùng từng là tất cả những gì chúng tôi đã làm với tư cách là một ngành, nhưng điều đó không còn đủ khi các nhà phát triển đưa mã vào sản xuất hàng chục hoặc hàng trăm lần một ngày. Các chuyên gia bảo mật ứng dụng phải theo kịp các kỹ thuật nhanh nhẹn, có nghĩa là áp dụng các công cụ dành cho nhà phát triển, học cách viết mã và làm việc với các nhà phát triển thay vì chỉ trích dự án vài tháng sau khi mọi người khác đã chuyển sang.

## V1.1 Secure Software Development Lifecycle

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.1.1** | [DELETED, NOT IN SCOPE] | | | | |
| **1.1.2** | [DELETED, NOT IN SCOPE] | | | | |
| **1.1.3** | [DELETED, NOT IN SCOPE] | | | | |
| **1.1.4** | Xác minh tài liệu và biện minh cho tất cả các ranh giới tin cậy, các thành phần và các luồng dữ liệu quan trọng của ứng dụng. | | ✓ | ✓ | 1059 |
| **1.1.5** | Xác minh định nghĩa và phân tích bảo mật kiến trúc cấp cao của ứng dụng và tất cả các dịch vụ từ xa được kết nối. | | ✓ | ✓ | 1059 |
| **1.1.6** | Xác minh việc triển khai các biện pháp kiểm soát bảo mật tập trung, đơn giản (tiết kiệm thiết kế), đã được kiểm tra, an toàn và có thể tái sử dụng để tránh các biện pháp kiểm soát trùng lặp, thiếu sót, không hiệu quả hoặc không an toàn. | | ✓ | ✓ | 637 |
| **1.1.7** | [DELETED, NOT IN SCOPE] | | | | |

## V1.2 Authentication Architecture

Khi thiết kế hệ thống xác thực, sức mạnh của xác thực đa yếu tố hỗ trợ phần cứng trở nên không còn liên quan nếu kẻ tấn công có thể dễ dàng đặt lại tài khoản bằng cách gọi đến tổng đài và trả lời các câu hỏi thường gặp. Để đảm bảo xác minh danh tính an toàn, tất cả các đường dẫn xác thực phải có độ mạnh tương đương.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.2.1** | [MOVED TO 1.14.7] | | | | |
| **1.2.2** | [MODIFIED] Xác minh rằng các liên lạc giữa các thành phần ứng dụng phụ trợ (back-end), bao gồm các API, phần mềm trung gian và lớp dữ liệu, được xác thực và sử dụng các tài khoản người dùng riêng lẻ. | | ✓ | ✓ | 306 |
| **1.2.3** | [MODIFIED] Xác minh rằng ứng dụng sử dụng một cơ chế xác thực người dùng duy nhất đã được kiểm tra, được biết là an toàn, có thể được mở rộng để bao gồm xác thực mạnh và có đủ khả năng ghi nhật ký và giám sát để phát hiện lạm dụng hoặc vi phạm tài khoản. | | ✓ | ✓ | 306 |
| **1.2.4** | [MODIFIED, SPLIT TO 2.2.11] Xác minh rằng, nếu ứng dụng bao gồm nhiều đường dẫn xác thực, tất cả những đường dẫn này đều được ghi lại cùng với các biện pháp kiểm soát bảo mật và độ mạnh xác thực cần được thực thi nhất quán trên tất cả chúng. | | ✓ | ✓ | 306 |
| **1.2.5** | [ADDED] Xác minh rằng một danh sách các từ ngữ cụ thể theo ngữ cảnh được ghi lại để ngăn chặn việc sử dụng chúng trong mật khẩu. | | ✓ | ✓ | 521 |

## V1.3 Session Management Architecture

Đây là phần dành cho các yêu cầu kiến trúc trong tương lai.

## V1.4 Access Control Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.4.1** | [DELETED, DUPLICATE OF 4.1.1] | | | | |
| **1.4.2** | [DELETED] | | | | |
| **1.4.3** | [DELETED, DUPLICATE OF 4.1.3] | | | | |
| **1.4.4** | Xác minh ứng dụng sử dụng một cơ chế kiểm soát truy cập duy nhất và đã được kiểm chứng kỹ lưỡng để truy cập dữ liệu và tài nguyên được bảo vệ. Tất cả các yêu cầu phải thông qua cơ chế duy nhất này để tránh sao chép và dán hoặc các đường dẫn thay thế không an toàn. | | ✓ | ✓ | 284 |
| **1.4.5** | [GRAMMAR] Xác minh rằng kiểm soát truy cập dựa trên thuộc tính hoặc tính năng được sử dụng, theo đó mã kiểm tra ủy quyền của người dùng đối với một tính năng hoặc mục dữ liệu thay vì chỉ kiểm tra vai trò của họ. Quyền vẫn nên được phân bổ bằng cách sử dụng vai trò. | | ✓ | ✓ | 275 |
| **1.4.6** | [ADDED] Xác minh rằng các giao tiếp giữa các thành phần ứng dụng phụ trợ, bao gồm API, phần mềm trung gian và các lớp dữ liệu, được thực hiện với các đặc quyền cần thiết tối thiểu. | | ✓ | ✓ | 272 |

## V1.5 Input and Output Architecture

Trong phiên bản 4.0, chúng ta đã không còn sử dụng thuật ngữ "phía máy chủ" như một thuật ngữ ranh giới tin cậy được tải. Ranh giới tin cậy vẫn còn là một vấn đề - việc đưa ra quyết định trên các trình duyệt hoặc thiết bị khách không đáng tin cậy có thể bị bỏ qua. Tuy nhiên, trong các triển khai kiến trúc chủ đạo hiện nay, điểm thực thi tin cậy đã thay đổi đáng kể. Do đó, khi thuật ngữ "lớp dịch vụ đáng tin cậy" được sử dụng trong ASVS, chúng ta muốn nói đến bất kỳ điểm thực thi tin cậy nào, bất kể vị trí, chẳng hạn như microservice, API không máy chủ, phía máy chủ, API đáng tin cậy trên thiết bị khách có khởi động an toàn, API đối tác hoặc bên ngoài, v.v.

Thuật ngữ "máy khách không đáng tin cậy" ở đây đề cập đến các công nghệ phía máy khách hiển thị lớp trình bày, thường được gọi là công nghệ 'front-end'. Thuật ngữ 'serialization' (chuỗi hóa) trong ngữ cảnh này không chỉ đề cập đến việc truyền dữ liệu qua mạng, chẳng hạn như một mảng các giá trị hoặc xử lý cấu trúc JSON mà còn đề cập đến việc xử lý các đối tượng phức tạp có thể chứa logic.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.5.1** | [MODIFIED, LEVEL L2 > L1] Xác minh rằng các yêu cầu đầu vào và đầu ra xác định rõ ràng cách xử lý và xử lý dữ liệu dựa trên loại và nội dung. | ✓ | ✓ | ✓ | 20 |
| **1.5.2** | [DELETED, MERGED TO 5.5.3] | | | | |
| **1.5.3** | [MOVED TO 5.6.2] | | | | |
| **1.5.4** | [MOVED TO 5.6.3] | | | | |

## V1.6 Cryptographic Architecture

Các ứng dụng cần được thiết kế với kiến trúc mật mã mạnh để bảo vệ tài sản dữ liệu theo phân loại của chúng. Mã hóa mọi thứ là lãng phí, không mã hóa bất cứ thứ gì là bất cẩn về mặt pháp lý. Cần phải có sự cân bằng, thường là trong quá trình thiết kế kiến trúc hoặc thiết kế cấp cao, thiết kế nước rút hoặc tăng đột biến kiến trúc. Thiết kế mật mã khi bạn đi hoặc trang bị thêm nó chắc chắn sẽ tốn nhiều chi phí hơn để triển khai an toàn so với việc xây dựng nó ngay từ đầu.

Các yêu cầu kiến trúc vốn có trong toàn bộ cơ sở mã và do đó khó kiểm tra đơn vị hoặc tích hợp. Các yêu cầu kiến trúc cần được xem xét trong các tiêu chuẩn mã hóa, trong suốt giai đoạn mã hóa và nên được xem xét trong kiến trúc bảo mật, đánh giá ngang hàng hoặc mã hoặc hồi cứu.

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.6.1** | Xác minh rằng có một chính sách rõ ràng để quản lý các khóa mật mã và vòng đời của khóa mật mã tuân theo một tiêu chuẩn quản lý khóa như NIST SP 800-57. | | ✓ | ✓ | 320 |
| **1.6.2** | Xác minh rằng người dùng các dịch vụ mật mã bảo vệ dữ liệu khóa và các bí mật khác bằng cách sử dụng hầm khóa hoặc các giải pháp thay thế dựa trên API. | | ✓ | ✓ | 320 |
| **1.6.3** | Xác minh rằng tất cả các khóa và mật khẩu đều có thể thay thế và là một phần của quy trình được xác định rõ để mã hóa lại dữ liệu nhạy cảm | | ✓ | ✓ | 320 |
| **1.6.4** | [GRAMMAR] Xác minh rằng kiến trúc coi các bí mật phía máy khách (như khóa đối xứng, mật khẩu hoặc mã thông báo API) là không an toàn và không bao giờ sử dụng chúng để bảo vệ hoặc truy cập dữ liệu nhạy cảm. | | ✓ | ✓ | 320 |

## V1.7 Errors, Logging and Auditing Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.7.1** | [MOVED TO 7.1.7] | | | | |
| **1.7.2** | [MOVED TO 7.3.5] | | | | |
| **1.7.3** | [ADDED] Xác minh rằng có một bản kiểm kê ghi lại việc ghi nhật ký được thực hiện ở mỗi lớp của ngăn xếp công nghệ của ứng dụng, những sự kiện nào đang được ghi nhật ký, định dạng nhật ký, nơi lưu trữ nhật ký đó, cách sử dụng nó, cách kiểm soát quyền truy cập vào nó và nhật ký được lưu giữ trong bao lâu. | | ✓ | ✓ | 778 |

## V1.8 Data Protection and Privacy Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.8.1** | [MODIFIED, MERGED FROM 8.3.4, LEVEL L2 > L1] Xác minh rằng tất cả dữ liệu nhạy cảm được tạo và xử lý bởi ứng dụng đã được xác định và phân loại thành các cấp độ bảo vệ và đảm bảo rằng có một chính sách về cách xử lý dữ liệu nhạy cảm. | ✓ | ✓ | ✓ | 213 |
| **1.8.2** | [MODIFIED] Xác minh rằng tất cả các cấp độ bảo vệ đều có một tập hợp các yêu cầu bảo vệ liên quan và chúng được áp dụng trong kiến trúc. Điều này nên bao gồm (nhưng không giới hạn) các yêu cầu liên quan đến mã hóa, xác minh tính toàn vẹn, lưu giữ, quyền riêng tư và các công nghệ nâng cao quyền riêng tư sẽ được sử dụng và các yêu cầu bảo mật khác. | | ✓ | ✓ | |

## V1.9 Communications Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.9.1** | [DELETED, DUPLICATE OF 9.1.1, 9.2.2, 9.3.1] | | | | |
| **1.9.2** | [DELETED, DUPLICATE OF 9.2.3, 9.3.2] | | | | |

## V1.10 Malicious Software Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.10.1** | [DELETED, NOT IN SCOPE] | | | | |

## V1.11 Business Logic Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.11.1** | Xác minh định nghĩa và tài liệu của tất cả các thành phần ứng dụng về các chức năng kinh doanh hoặc bảo mật mà chúng cung cấp. | | ✓ | ✓ | 1059 |
| **1.11.2** | [MODIFIED] Xác minh rằng tất cả các luồng ứng dụng bao gồm xác thực, quản lý phiên và kiểm soát truy cập, duy trì trạng thái ứng dụng và người dùng nhất quán để ngăn chặn các điều kiện race và lỗ hổng logic nghiệp vụ. | | ✓ | ✓ | 362 |
| **1.11.3** | Xác minh rằng tất cả các luồng logic nghiệp vụ có giá trị cao, bao gồm xác thực, quản lý phiên và kiểm soát truy cập đều an toàn luồng và chống lại các điều kiện race time-of-check và time-of-use. | | | ✓ | 367 |
| **1.11.4** | [ADDED] Xác minh rằng các kỳ vọng về giới hạn và xác thực logic nghiệp vụ được ghi lại rõ ràng bao gồm cả trên mỗi người dùng và cả trên toàn cầu trong ứng dụng. | | ✓ | ✓ | |

## V1.12 Secure File Upload Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.12.1** | [DELETED, DUPLICATE OF 12.4.1] | | | | |
| **1.12.2** | [MOVED TO 50.5.2] | | | | |

## V1.13 API Architecture

This is a placeholder for future architectural requirements.

## V1.14 Configuration Architecture

| # | Description | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **1.14.1** | [MODIFIED] Xác minh sự phân tách các thành phần phụ trợ (back-end) có mức độ tin cậy khác nhau thông qua các biện pháp kiểm soát bảo mật được xác định rõ, quy tắc tường lửa, cổng API, proxy ngược, nhóm bảo mật dựa trên đám mây hoặc các cơ chế tương tự. | | ✓ | ✓ | 923 |
| **1.14.2** | [DELETED, NOT IN SCOPE] | | | | |
| **1.14.3** | [DELETED, DUPLICATE OF 14.2.1] | | | | |
| **1.14.4** | [DELETED, NOT IN SCOPE] | | | | |
| **1.14.5** | [MODIFIED] Xác minh rằng việc triển khai ứng dụng cách ly hoặc cô lập đầy đủ ở cấp độ mạng để trì hoãn và ngăn chặn kẻ tấn công tấn công các ứng dụng khác, đặc biệt là khi chúng đang thực hiện các hành động nhạy cảm hoặc nguy hiểm như deserialization. | | ✓ | ✓ | 265 |
| **1.14.6** | [MOVED TO 50.7.2] | | | | |
| **1.14.7** | [MODIFIED, MOVED FROM 1.2.1] Xác minh việc sử dụng các tài khoản hệ điều hành đặc quyền thấp duy nhất hoặc đặc biệt cho tất cả các thành phần, dịch vụ và máy chủ ứng dụng phụ trợ. | | ✓ | ✓ | 250 |
| **1.14.8** | [ADDED] Xác minh rằng ứng dụng có thể phân biệt và sử dụng địa chỉ IP thực của người dùng để cung cấp cho các chức năng nhạy cảm, bao gồm giới hạn tốc độ và ghi nhật ký. | | ✓ | ✓ | 348 |

## References

For more information, see also:

* [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html)
* [OWASP Attack Surface Analysis Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Attack_Surface_Analysis_Cheat_Sheet.html)
* [OWASP Threat modeling](https://owasp.org/www-community/Application_Threat_Modeling)
* [OWASP Software Assurance Maturity Model Project](https://owasp.org/www-project-samm/)
* [Microsoft SDL](https://www.microsoft.com/en-us/securityengineering/sdl/)
* [NIST SP 800-57](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final)
* [More information on security.txt including a link to the RFC](https://securitytxt.org/)
