# V2 Authentication

## Control Objective

Xác thực là quá trình thiết lập hoặc xác nhận tính xác thực của một cá nhân hoặc thiết bị. Nó liên quan đến việc xác minh các tuyên bố do một người đưa ra hoặc về một thiết bị, đảm bảo khả năng chống mạo danh và ngăn chặn việc khôi phục hoặc đánh cắp mật khẩu.

Khi ASVS được phát hành lần đầu, sự kết hợp giữa tên người dùng và mật khẩu là hình thức xác thực phổ biến nhất, ngoại trừ trong các hệ thống bảo mật cao. Xác thực Đa yếu tố (MFA) thường được chấp nhận trong giới bảo mật nhưng hiếm khi được yêu cầu ở những nơi khác. Khi số lượng vi phạm mật khẩu tăng lên, ý tưởng rằng tên người dùng bằng cách nào đó là bí mật và mật khẩu không được biết đến, khiến nhiều biện pháp kiểm soát bảo mật trở nên không thể thực hiện được. Ví dụ: NIST SP 800-63 coi tên người dùng và Xác thực Dựa trên Kiến thức (KBA) là thông tin công khai, email là [không được phép](https://pages.nist.gov/800-63-FAQ/#q-b11), SMS dưới dạng ["loại trình xác thực bị hạn chế"](https://pages.nist.gov/800-63-FAQ/#q-b01) và mật khẩu dưới dạng đã bị vi phạm trước đó. Thực tế này khiến các trình xác thực dựa trên kiến thức, khôi phục SMS và email, và các biện pháp kiểm soát liên quan đến mật khẩu như lịch sử, độ phức tạp và xoay vòng trở nên không hiệu quả. Các biện pháp kiểm soát này luôn luôn ít hữu ích, thường buộc người dùng phải đưa ra mật khẩu yếu sau mỗi vài tháng, nhưng với việc phát hành hơn 5 tỷ vi phạm tên người dùng và mật khẩu, đã đến lúc phải tiếp tục.

Trong tất cả các chương trong ASVS, các chương về xác thực và quản lý phiên đã thay đổi nhiều nhất. Việc áp dụng thực tiễn hàng đầu hiệu quả, dựa trên bằng chứng sẽ là một thách thức đối với nhiều người và điều đó hoàn toàn ổn. Chúng ta phải bắt đầu quá trình chuyển đổi sang tương lai không còn mật khẩu ngay bây giờ.

## NIST SP 800-63 - Modern, evidence-based authentication standard

[NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html) là một tiêu chuẩn hiện đại, dựa trên bằng chứng và đại diện cho lời khuyên tốt nhất hiện có, bất kể khả năng áp dụng. Tiêu chuẩn này hữu ích cho tất cả các tổ chức trên toàn thế giới nhưng đặc biệt phù hợp với các cơ quan Hoa Kỳ và những người giao dịch với các cơ quan Hoa Kỳ.

Thuật ngữ NIST SP 800-63 ban đầu có thể hơi khó hiểu, đặc biệt nếu bạn chỉ quen với xác thực bằng tên người dùng + mật khẩu. Những tiến bộ trong xác thực hiện đại là cần thiết, vì vậy chúng tôi phải giới thiệu thuật ngữ sẽ trở nên phổ biến trong tương lai, nhưng chúng tôi hiểu sự khó khăn trong việc hiểu cho đến khi ngành công nghiệp giải quyết các thuật ngữ mới này. Chúng tôi đã cung cấp một bảng chú giải thuật ngữ ở cuối chương này để hỗ trợ. Chúng tôi đã diễn đạt lại nhiều yêu cầu để đáp ứng ý định của yêu cầu, thay vì văn bản của yêu cầu. Ví dụ: ASVS sử dụng thuật ngữ "mật khẩu" trong khi NIST sử dụng "bí mật ghi nhớ" trong suốt tiêu chuẩn này.

Các chương V2 Xác thực và V3 Quản lý Phiên trong ASVS, và ở mức độ thấp hơn là chương V4 Kiểm soát Truy cập, đã được điều chỉnh để phù hợp như một tập hợp con tuân thủ của các biện pháp kiểm soát NIST SP 800-63B đã chọn. Sự điều chỉnh này tập trung vào các mối đe dọa phổ biến và các điểm yếu xác thực thường bị khai thác. Đối với các trường hợp cần tuân thủ NIST SP 800-63 đầy đủ, vui lòng tham khảo NIST SP 800-63.

### Selecting an appropriate NIST AAL Level

Tiêu chuẩn Xác minh Bảo mật Ứng dụng đã cố gắng ánh xạ các yêu cầu ASVS L1 với NIST AAL1, L2 với AAL2 và L3 với AAL3. Tuy nhiên, cách tiếp cận của ASVS Cấp 1 là các biện pháp kiểm soát "thiết yếu" có thể không nhất thiết phải là mức AAL chính xác để xác minh ứng dụng hoặc API. Ví dụ: nếu ứng dụng là ứng dụng Cấp 3 hoặc có yêu cầu quy định là AAL3, thì nên chọn Cấp 3 trong các chương V2 và V3 Quản lý Phiên. Việc lựa chọn Mức Xác nhận Xác thực (AAL) tuân thủ NIST nên được thực hiện theo hướng dẫn của NIST SP 800-63B như được nêu trong Chọn AAL trong [NIST SP 800-63B Section 6.2](https://pages.nist.gov/800-63-3/sp800-63-3.html#AAL_CYOA).

## V2.1 Password Security

Mật khẩu, được NIST SP 800-63 gọi là "Bí mật Ghi nhớ", bao gồm mật khẩu, mã PIN, mẫu mở khóa, chọn mèo con chính xác hoặc một yếu tố hình ảnh khác và cụm mật khẩu. Chúng thường được coi là "thứ bạn biết" và thường được sử dụng làm trình xác thực một yếu tố. Việc tiếp tục sử dụng xác thực một yếu tố có những thách thức đáng kể, bao gồm hàng tỷ tên người dùng và mật khẩu hợp lệ được tiết lộ trên Internet, mật khẩu mặc định hoặc yếu, bảng cầu vồng và từ điển có thứ tự của các mật khẩu phổ biến nhất.

Các ứng dụng nên khuyến khích mạnh mẽ người dùng đăng ký xác thực đa yếu tố và nên cho phép người dùng sử dụng lại mã thông báo mà họ đã sở hữu, chẳng hạn như mã thông báo FIDO hoặc U2F, hoặc liên kết đến nhà cung cấp dịch vụ thông tin đăng nhập cung cấp xác thực đa yếu tố.

Nhà cung cấp Dịch vụ Thông tin Đăng nhập (CSP) cung cấp danh tính liên kết cho người dùng. Người dùng thường sẽ có nhiều hơn một danh tính với nhiều CSP, chẳng hạn như danh tính doanh nghiệp sử dụng Azure AD, Okta, Ping Identity hoặc Google, hoặc danh tính người tiêu dùng sử dụng Facebook, Twitter, Google hoặc WeChat, chỉ để nêu tên một số lựa chọn thay thế phổ biến. Danh sách này không phải là sự chứng thực cho các công ty hoặc dịch vụ này, mà chỉ đơn giản là một sự khuyến khích cho các nhà phát triển xem xét thực tế rằng nhiều người dùng có nhiều danh tính đã được thiết lập. Các tổ chức nên xem xét tích hợp với danh tính người dùng hiện có, theo hồ sơ rủi ro về độ mạnh chứng minh danh tính của CSP. Ví dụ: không chắc một tổ chức chính phủ sẽ chấp nhận danh tính mạng xã hội làm thông tin đăng nhập cho các hệ thống nhạy cảm, vì rất dễ tạo danh tính giả hoặc vứt bỏ, trong khi một công ty trò chơi di động có thể cần tích hợp với các nền tảng mạng xã hội lớn để phát triển cơ sở người chơi tích cực của họ.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.1.1** | [MODIFIED] Xác minh rằng mật khẩu do người dùng đặt có độ dài ít nhất 8 ký tự. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.2** | [MODIFIED, SPLIT TO 2.4.6] Xác minh rằng mật khẩu có ít nhất 64 ký tự được phép. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.3** | [MODIFIED] Xác minh rằng ứng dụng xác minh mật khẩu của người dùng chính xác như nhận được từ người dùng, không có bất kỳ sửa đổi nào như cắt bớt hoặc chuyển đổi chữ hoa chữ thường. | ✓ | ✓ | ✓ | | 5.1.1.2 |
| **2.1.4** | Xác minh rằng bất kỳ ký tự Unicode có thể in nào, bao gồm cả các ký tự trung lập ngôn ngữ như dấu cách và Biểu tượng cảm xúc đều được phép trong mật khẩu. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.5** | Xác minh người dùng có thể thay đổi mật khẩu của họ. | ✓ | ✓ | ✓ | 620 | 5.1.1.2 |
| **2.1.6** | Xác minh rằng chức năng thay đổi mật khẩu yêu cầu mật khẩu hiện tại và mật khẩu mới của người dùng. | ✓ | ✓ | ✓ | 620 | 5.1.1.2 |
| **2.1.7** | [MODIFIED, SPLIT TO 2.1.14] Xác minh rằng mật khẩu được gửi trong quá trình đăng ký tài khoản hoặc thay đổi mật khẩu được kiểm tra dựa trên một tập hợp có sẵn, ít nhất là 3000 mật khẩu hàng đầu. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.8** | [DELETED, INSUFFICIENT IMPACT] | | | | | |
| **2.1.9** | Xác minh rằng không có quy tắc thành phần mật khẩu nào giới hạn loại ký tự được phép. Không nên có yêu cầu về chữ hoa, chữ thường, số hoặc ký tự đặc biệt. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.10** | [MODIFIED, SPLIT TO 2.1.13, LEVEL L1 > L2] Xác minh rằng ứng dụng không yêu cầu thay đổi định kỳ thông tin đăng nhập. | | ✓ | ✓ | | 5.1.1.2 |
| **2.1.11** | Xác minh rằng chức năng "dán", trình trợ giúp mật khẩu của trình duyệt và trình quản lý mật khẩu bên ngoài được phép. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.12** | [MODIFIED] Xác minh rằng các trường nhập mật khẩu sử dụng type=password để che dấu mục nhập. Các ứng dụng có thể cho phép người dùng tạm thời xem toàn bộ mật khẩu bị che hoặc ký tự cuối cùng đã nhập của mật khẩu. | ✓ | ✓ | ✓ | 549 | 5.1.1.2 |
| **2.1.13** | [ADDED, SPLIT FROM 2.1.10, LEVEL L1 > L2] Xác minh rằng ứng dụng không lưu giữ lịch sử mật khẩu. | | ✓ | ✓ | | 5.1.1.2 |
| **2.1.14** | [ADDED, SPLIT FROM 2.1.7, LEVEL L1 > L3] Xác minh rằng mật khẩu được gửi trong quá trình đăng ký tài khoản hoặc thay đổi mật khẩu được kiểm tra dựa trên một tập hợp mật khẩu đã bị rò rỉ. | | | ✓ | | 5.1.1.2 |
| **2.1.15** | [ADDED] Xác minh rằng danh sách các từ ngữ cụ thể theo ngữ cảnh đã được ghi lại được sử dụng để ngăn tạo mật khẩu dễ đoán. | | ✓ | ✓ | 521 | 5.1.1.2 |

Các nguồn mật khẩu thường được sử dụng cho yêu cầu 2.1.7 có thể bao gồm:

* <https://github.com/danielmiessler/SecLists/tree/master/Passwords>
* <https://www.ncsc.gov.uk/blog-post/passwords-passwords-everywhere>

## V2.2 General Authenticator Security

Tính linh hoạt của trình xác thực là điều cần thiết để ứng dụng có thể chống lại các thay đổi trong tương lai. Cải tiến các trình xác minh ứng dụng để cho phép các trình xác thực bổ sung theo sở thích của người dùng, cũng như loại bỏ các trình xác thực không dùng nữa hoặc không an toàn một cách có trật tự.

NIST coi SMS là ["loại trình xác thực bị hạn chế"](https://pages.nist.gov/800-63-FAQ/#q-b01), và chúng có khả năng sẽ bị xóa khỏi NIST SP 800-63 và do đó khỏi ASVS trong tương lai. Các ứng dụng nên lập kế hoạch lộ trình không yêu cầu sử dụng SMS.

Như đã lưu ý ở trên, NIST SP 800-63 coi email là [không thể chấp nhận](https://pages.nist.gov/800-63-FAQ/#q-b11) được làm trình xác thực.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.2.1** | [MODIFIED] Xác minh rằng các biện pháp kiểm soát chống tự động hóa có hiệu quả trong việc giảm thiểu việc kiểm tra thông tin đăng nhập bị xâm phạm, tấn công brute force và khóa tài khoản. Các biện pháp kiểm soát như vậy bao gồm chặn các mật khẩu bị xâm phạm phổ biến nhất, khóa mềm, giới hạn tốc độ, CAPTCHA, tăng dần độ trễ giữa các lần thử, hạn chế địa chỉ IP hoặc hạn chế dựa trên rủi ro như vị trí, lần đăng nhập đầu tiên trên thiết bị, các lần thử gần đây để mở khóa tài khoản hoặc tương tự. Hơn 5 lần thử xác thực không thành công mỗi giờ đối với một tài khoản nên kích hoạt một số loại phản ứng hoặc cảnh báo. | ✓ | ✓ | ✓ | 307 | 5.2.2 / 5.1.1.2 / 5.1.4.2 / 5.1.5.2 |
| **2.2.2** | [MODIFIED, SPLIT TO 2.2.12] Xác minh rằng các trình xác thực bị hạn chế (những trình sử dụng PSTN để gửi OTP qua điện thoại hoặc SMS) chỉ được cung cấp khi các phương pháp thay thế mạnh hơn cũng được cung cấp và khi dịch vụ cung cấp thông tin về rủi ro bảo mật của chúng cho người dùng. | ✓ | ✓ | ✓ | 304 | 5.2.10 |
| **2.2.3** | [MODIFIED, SPLIT TO 2.2.10] Xác minh rằng người dùng được thông báo sau khi cập nhật chi tiết xác thực, chẳng hạn như đặt lại thông tin đăng nhập hoặc sửa đổi tên người dùng hoặc địa chỉ email. | ✓ | ✓ | ✓ | 778 | 6.1.2 |
| **2.2.4** | [MODIFIED, SPLIT TO 2.2.9] Xác minh rằng trình xác thực dựa trên phần cứng và trình xác thực cung cấp khả năng chống mạo danh trình xác minh trước các cuộc tấn công lừa đảo (chẳng hạn như WebAuthn) được sử dụng. | | | ✓ | 308 | 4.3.1 |
| **2.2.5** | Xác minh rằng khi Nhà cung cấp Dịch vụ Thông tin Đăng nhập (CSP) và ứng dụng xác minh xác thực được tách biệt, TLS được xác thực lẫn nhau giữa hai điểm cuối. | | | ✓ | 319 | 5.2.6 |
| **2.2.6** | Xác minh khả năng chống phát lại thông qua việc sử dụng bắt buộc các thiết bị Mật khẩu Một lần (OTP), trình xác thực mật mã hoặc mã tra cứu. | | | ✓ | 308 | 5.2.8 |
| **2.2.7** | Xác minh ý định xác thực bằng cách yêu cầu nhập mã thông báo OTP hoặc hành động do người dùng khởi tạo như nhấn nút trên khóa phần cứng FIDO. | | | ✓ | 308 | 5.2.9 |
| **2.2.8** | [ADDED] Xác minh rằng không thể suy ra người dùng hợp lệ từ các thử thách xác thực không thành công, chẳng hạn như dựa trên thông báo lỗi, mã phản hồi HTTP hoặc thời gian phản hồi khác nhau. Chức năng đăng ký và quên mật khẩu cũng nên có sự bảo vệ này. | | | ✓ | | |
| **2.2.9** | [ADDED, SPLIT FROM 2.2.4] Xác minh rằng yêu cầu xác thực đa yếu tố, nghĩa là ứng dụng sử dụng trình xác thực đa yếu tố hoặc kết hợp các trình xác thực đơn yếu tố. | | ✓ | ✓ | 308 | 4.2.1 |
| **2.2.10** | [ADDED, SPLIT FROM 2.2.3] Xác minh rằng người dùng được thông báo về các nỗ lực xác thực đáng ngờ. Các nỗ lực xác thực đáng ngờ có thể bao gồm xác thực thành công hoặc không thành công từ một vị trí hoặc máy khách bất thường, xác thực thành công một phần chỉ với một trong nhiều yếu tố, xác thực thành công hoặc không thành công sau một thời gian dài không hoạt động hoặc xác thực thành công sau nhiều lần thử không thành công. | | ✓ | ✓ | 778 | |
| **2.2.11** | [ADDED, SPLIT FROM 1.2.4] Xác minh rằng, nếu ứng dụng bao gồm nhiều đường dẫn xác thực, không có đường dẫn nào không có tài liệu và các biện pháp kiểm soát bảo mật và độ mạnh xác thực được thực thi một cách nhất quán. | | ✓ | ✓ | 306 | |
| **2.2.12** | [ADDED, SPLIT FROM 2.2.2] Xác minh rằng email không được sử dụng làm cơ chế xác thực đơn lẻ hoặc đa yếu tố. | ✓ | ✓ | ✓ | 1390 | |

## V2.3 Authenticator Lifecycle

Trình xác thực là mật khẩu, mã thông báo mềm, mã thông báo phần cứng và thiết bị sinh trắc học. Vòng đời của trình xác thực rất quan trọng đối với bảo mật của ứng dụng - nếu bất kỳ ai cũng có thể tự đăng ký tài khoản mà không có bằng chứng về danh tính, thì có thể có rất ít sự tin tưởng vào xác nhận danh tính. Đối với các trang mạng xã hội như Reddit, điều đó hoàn toàn ổn. Đối với hệ thống ngân hàng, việc tập trung nhiều hơn vào việc đăng ký và cấp thông tin đăng nhập và thiết bị là rất quan trọng đối với bảo mật của ứng dụng.

Lưu ý: Mật khẩu không có thời hạn sử dụng tối đa hoặc phải tuân theo quy tắc xoay vòng mật khẩu. Mật khẩu nên được kiểm tra xem có bị xâm phạm hay không, không nên thay đổi thường xuyên.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.3.1** | [MODIFIED] Xác minh mật khẩu ban đầu hoặc mã kích hoạt do hệ thống tạo được tạo ngẫu nhiên an toàn, dài ít nhất 6 ký tự, có thể chứa chữ cái và số, hết hạn sau một thời gian ngắn và chỉ sử dụng một lần. Những bí mật ban đầu này không được phép trở thành mật khẩu dài hạn. | ✓ | ✓ | ✓ | 330 | 5.1.1.2 / A.3 |
| **2.3.2** | Xác minh rằng việc đăng ký và sử dụng các thiết bị xác thực do người dùng cung cấp được hỗ trợ, chẳng hạn như mã thông báo U2F hoặc FIDO. | | ✓ | ✓ | 308 | 6.1.3 |
| **2.3.3** | [MODIFIED] Xác minh rằng các lời nhắc tự động được định cấu hình và hành động để đảm bảo rằng hướng dẫn gia hạn cho các trình xác thực giới hạn thời gian được gửi với đủ thời gian để thực hiện trước khi trình xác thực cũ hết hạn. | | ✓ | ✓ | 287 | 6.1.4 |
| **2.3.4** | [ADDED] Quản trị viên hệ thống không được phép thay đổi hoặc chọn mật khẩu của bất kỳ người dùng nào, mà chỉ có thể khởi tạo quy trình đặt lại mật khẩu cho người dùng. | ✓ | ✓ | ✓ | 620 | |

## V2.4 Credential Storage

Kiến trúc sư và nhà phát triển nên tuân thủ phần này khi xây dựng hoặc cấu trúc lại mã.

Danh sách hiện tại các thuật toán băm mật khẩu được phê duyệt được trình bày chi tiết trong NIST SP 800-63B mục 5.1.1.2 và trong [OWASP Password Storage Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html#password-hashing-algorithms). Hãy chú ý cẩn thận đến hướng dẫn cấu hình để nhận biết bất kỳ thách thức hoặc giới hạn triển khai nào với mỗi thuật toán.

Đặc biệt, lưu ý rằng vì các thuật toán này cố ý tiêu tốn nhiều tài nguyên tính toán, nên đã có những trường hợp trong quá khứ khi cung cấp mật khẩu rất dài dẫn đến tình trạng từ chối dịch vụ. Do đó, điều rất quan trọng là phải bảo vệ chống lại điều này.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.4.1** | [MODIFIED, MERGED FROM 2.4.3, 2.4.4] Xác minh rằng mật khẩu người dùng được lưu trữ bằng thuật toán băm mật khẩu được phê duyệt, được cấu hình an toàn theo hướng dẫn hiện hành. | | ✓ | ✓ | 916 | 5.1.1.2 |
| **2.4.2** | [DELETED, INCORRECT] | | | | | |
| **2.4.3** | [DELETED, MERGED TO 2.4.1] | | | | | |
| **2.4.4** | [DELETED, MERGED TO 2.4.1] | | | | | |
| **2.4.5** | [DELETED, INCORRECT] | | | | | |
| **2.4.6** | [ADDED, SPLIT FROM 2.1.2] Xác minh rằng ứng dụng được bảo vệ chống lại tấn công từ chối dịch vụ do xử lý mật khẩu quá dài. | | ✓ | ✓ | | |

Trong trường hợp đề cập đến các tiêu chuẩn Hoa Kỳ, một tiêu chuẩn khu vực hoặc địa phương có thể được sử dụng thay thế hoặc bổ sung cho tiêu chuẩn Hoa Kỳ nếu cần.

## V2.5 Credential Recovery

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.5.1** | [DELETED, INCORRECT] | | | | | |
| **2.5.2** | Xác minh rằng gợi ý mật khẩu hoặc knowledge-based authentication (còn gọi là "câu hỏi bí mật") không có mặt. | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.3** | [DELETED, DUPLICATE OF 2.4.1] | | | | | |
| **2.5.4** | [MODIFIED] Xác minh rằng các tài khoản người dùng mặc định (ví dụ: "root", "admin" hoặc "sa") được loại bỏ hoặc bị vô hiệu hóa. | ✓ | ✓ | ✓ | 798 | |
| **2.5.5** | [DELETED, DUPLICATE OF 2.2.3] | | | | | |
| **2.5.6** | Xác minh rằng mật khẩu bị quên và các đường dẫn khôi phục khác sử dụng cơ chế khôi phục an toàn, chẳng hạn như OTP dựa trên thời gian (TOTP) hoặc mã thông báo mềm khác, thông báo đẩy trên thiết bị di động hoặc cơ chế khôi phục ngoại tuyến khác. | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.7** | [LEVEL L2 > L1] Xác minh rằng nếu OTP hoặc các yếu tố xác thực đa yếu tố bị mất, thì bằng chứng về chứng minh danh tính được thực hiện ở cùng cấp độ như trong quá trình đăng ký. | ✓ | ✓ | ✓ | 308 | 6.1.2.3 |

## V2.6 Lookup Secret Verifier

Bí mật tra cứu là danh sách các mã bí mật được tạo trước, tương tự như Số Ủy quyền Giao dịch (TAN), mã khôi phục mạng xã hội hoặc lưới chứa một tập hợp các giá trị ngẫu nhiên. Chúng được phân phối an toàn cho người dùng. Các mã tra cứu này chỉ sử dụng một lần. Sau khi tất cả được sử dụng, danh sách bí mật tra cứu sẽ bị loại bỏ. Loại trình xác thực này được coi là "thứ bạn có".

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.6.1** | Xác minh rằng bí mật tra cứu chỉ có thể được sử dụng một lần. | | ✓ | ✓ | 308 | 5.1.2.2 |
| **2.6.2** | [MODIFIED, SPLIT TO 2.6.4] Xác minh rằng các bí mật tra cứu được lưu trữ ở back-end với ít hơn 112 bit entropy (19 ký tự chữ và số ngẫu nhiên hoặc 34 chữ số ngẫu nhiên) được băm bằng thuật toán băm lưu trữ mật khẩu được phê duyệt kết hợp với muối ngẫu nhiên 32 bit. Một hàm băm tiêu chuẩn có thể được sử dụng nếu bí mật có 112 bit entropy trở lên. | | ✓ | ✓ | 330 | 5.1.2.2 |
| **2.6.3** | [MODIFIED] Xác minh rằng các bí mật tra cứu được tạo bằng Trình tạo Số giả ngẫu nhiên Bảo mật Mật mã (CSPRNG) để tránh các giá trị có thể dự đoán được. | | ✓ | ✓ | 310 | 5.1.2.2 |
| **2.6.4** | [ADDED, SPLIT FROM 2.6.2] Xác minh rằng các bí mật tra cứu có tối thiểu 20 bit entropy (thường là 4 ký tự chữ và số ngẫu nhiên hoặc 6 chữ số ngẫu nhiên là đủ). | | ✓ | ✓ | 330 | 5.1.2.1 |

## V2.7 Out-of-Band Verifier

Trước đây, một trình xác minh ngoài băng tần phổ biến sẽ là một email hoặc SMS có chứa liên kết đặt lại mật khẩu. Kẻ tấn công sử dụng cơ chế yếu này để đặt lại các tài khoản mà họ chưa kiểm soát, chẳng hạn như chiếm đoạt tài khoản email của một người và sử dụng lại bất kỳ liên kết đặt lại nào được phát hiện. Có những cách tốt hơn để xử lý xác minh ngoài băng tần.

Trình xác thực ngoài băng tần an toàn là thiết bị vật lý có thể giao tiếp với trình xác minh qua kênh phụ an toàn. Ví dụ bao gồm thông báo đẩy đến thiết bị di động. Loại trình xác thực này được coi là "thứ bạn có". Khi người dùng muốn xác thực, ứng dụng xác minh sẽ gửi tin nhắn đến trình xác thực ngoài băng tần thông qua kết nối trực tiếp hoặc gián tiếp với trình xác thực thông qua dịch vụ của bên thứ ba. Tin nhắn bao gồm mã xác thực, thường là một số có sáu chữ số ngẫu nhiên hoặc có hộp thoại phê duyệt theo phương thức. Ứng dụng xác minh chờ nhận mã xác thực thông qua kênh chính và so sánh hàm băm của giá trị nhận được với hàm băm của mã xác thực ban đầu. Nếu chúng khớp, trình xác minh ngoài băng tần có thể giả định rằng người dùng đã được xác thực.

ASVS giả định rằng chỉ một số ít nhà phát triển sẽ phát triển trình xác thực ngoài băng tần mới, chẳng hạn như thông báo đẩy, và do đó các biện pháp kiểm soát ASVS sau đây áp dụng cho trình xác minh, chẳng hạn như API xác thực, ứng dụng và triển khai đăng nhập một lần. Nếu phát triển trình xác thực ngoài băng tần mới, vui lòng tham khảo NIST SP 800-63B &sect; 5.1.3.1.

Không cho phép sử dụng trình xác thực ngoài băng tần không an toàn như e-mail và VOIP. Xác thực PSTN và SMS hiện đang bị NIST "hạn chế" và nên không được dùng nữa để thay thế bằng thông báo đẩy hoặc tương tự. Nếu bạn cần sử dụng xác thực ngoài băng tần qua điện thoại hoặc SMS, vui lòng xem NIST SP 800-63B &sect; 5.1.3.3.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.7.1** | [GRAMMAR] Xác minh rằng các trình xác thực ngoài băng tần văn bản rõ ràng (NIST "bị hạn chế"), chẳng hạn như SMS hoặc PSTN, không được cung cấp theo mặc định và các giải pháp thay thế mạnh hơn như thông báo đẩy được cung cấp trước. | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.2** | [MODIFIED] Xác minh rằng trình xác minh ngoài băng tần hết hạn các yêu cầu, mã hoặc mã thông báo xác thực ngoài băng tần trong vòng 10 phút. | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.3** | [GRAMMAR] Xác minh rằng các yêu cầu, mã hoặc mã thông báo xác thực của trình xác minh ngoài băng tần chỉ có thể sử dụng một lần và chỉ dành cho yêu cầu xác thực ban đầu. | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.4** | [GRAMMAR] Xác minh rằng trình xác thực và trình xác minh ngoài băng tần giao tiếp qua một kênh độc lập an toàn. | ✓ | ✓ | ✓ | 523 | 5.1.3.2 |
| **2.7.5** | [GRAMMAR] Xác minh rằng trình xác minh ngoài băng tần chỉ giữ lại phiên bản băm của mã xác thực. | | ✓ | ✓ | 256 | 5.1.3.2 |
| **2.7.6** | [MODIFIED] Xác minh rằng mã xác thực ban đầu được tạo bởi trình tạo số ngẫu nhiên an toàn, chứa ít nhất 20 bit entropy (thường là 4 ký tự chữ và số ngẫu nhiên hoặc 6 chữ số ngẫu nhiên là đủ). | | ✓ | ✓ | 310 | 5.1.3.2 |
| **2.7.7** | [ADDED] Xác minh rằng mã xác thực ban đầu được bảo vệ chống lại các cuộc tấn công brute force bằng cách sử dụng giới hạn tốc độ hoặc mã có ít nhất 64 bit entropy. | | ✓ | ✓ | 307 | 5.1.3.2 |

## V2.8 One-Time Verifier

Mật khẩu một lần đơn nhân tố (OTP) là mã thông báo vật lý hoặc mềm hiển thị một thử thách một lần giả ngẫu nhiên liên tục thay đổi. Các thiết bị này khiến lừa đảo (mạo danh) trở nên khó khăn nhưng không phải là không thể. Loại trình xác thực này được coi là "thứ bạn có". Mã thông báo đa yếu tố tương tự như OTP đơn nhân tố, nhưng yêu cầu mã PIN hợp lệ, mở khóa sinh trắc học, cắm USB hoặc ghép nối NFC hoặc một số giá trị bổ sung (chẳng hạn như máy tính ký giao dịch) để được nhập để tạo OTP cuối cùng.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.8.1** | Xác minh rằng OTP dựa trên thời gian có thời gian tồn tại xác định trước khi hết hạn. | ✓ | ✓ | ✓ | 613 | 5.1.4.2 / 5.1.5.2 |
| **2.8.2** | Xác minh rằng các khóa đối xứng được sử dụng để xác minh OTP đã gửi được bảo vệ cao, chẳng hạn như bằng cách sử dụng mô-đun bảo mật phần cứng hoặc bộ nhớ khóa dựa trên hệ điều hành an toàn. | | ✓ | ✓ | 320 | 5.1.4.2 / 5.1.5.2 |
| **2.8.3** | Xác minh rằng các thuật toán mật mã được phê duyệt được sử dụng để tạo, gieo hạt và xác minh OTP. | | ✓ | ✓ | 326 | 5.1.4.2 / 5.1.5.2 |
| **2.8.4** | Xác minh rằng OTP dựa trên thời gian chỉ có thể được sử dụng một lần trong thời gian hiệu lực. | | ✓ | ✓ | 287 | 5.1.4.2 / 5.1.5.2 |
| **2.8.5** | Xác minh rằng nếu mã thông báo OTP đa yếu tố dựa trên thời gian được sử dụng lại trong thời gian hiệu lực, nó sẽ được ghi lại và từ chối với các thông báo an toàn được gửi đến chủ sở hữu thiết bị. | | ✓ | ✓ | 287 | 5.1.5.2 |
| **2.8.6** | Xác minh rằng trình tạo OTP đơn nhân tố vật lý có thể bị thu hồi trong trường hợp bị đánh cắp hoặc mất mát khác. Đảm bảo rằng việc thu hồi có hiệu lực ngay lập tức trên các phiên đã đăng nhập, bất kể vị trí. | | ✓ | ✓ | 613 | 5.2.1 |
| **2.8.7** | [MODIFIED, LEVEL L2 > L3] Xác minh rằng các trình xác thực sinh trắc học chỉ được sử dụng làm yếu tố phụ cùng với một thứ bạn có hoặc một thứ bạn biết. | | | ✓ | 308 | 5.2.3 |
| **2.8.8** | [ADDED] Đảm bảo rằng việc tạo mã thông báo OTP đa yếu tố dựa trên thời gian dựa trên thời gian hệ thống của máy chủ chứ không phải máy của máy khách. | | | ✓ | 367 | 5.1.4.2 / 5.1.5.2 |

## V2.9 Cryptographic Verifier

Khóa bảo mật mật mã là thẻ thông minh hoặc khóa FIDO, trong đó người dùng phải cắm hoặc ghép nối thiết bị mật mã với máy tính để hoàn tất xác thực. Trình xác minh gửi một thử thách nonce đến các thiết bị hoặc phần mềm mật mã, và thiết bị hoặc phần mềm tính toán phản hồi dựa trên khóa mật mã được lưu trữ an toàn.

Các yêu cầu đối với thiết bị và phần mềm mật mã đơn nhân tố và thiết bị và phần mềm mật mã đa yếu tố là giống nhau, vì việc xác minh trình xác thực mật mã chứng minh quyền sở hữu của yếu tố xác thực.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.9.1** | Xác minh rằng các khóa mật mã được sử dụng trong quá trình xác minh được lưu trữ an toàn và được bảo vệ chống lại việc tiết lộ, chẳng hạn như sử dụng Mô-đun Nền tảng Đáng tin cậy (TPM) hoặc Mô-đun Bảo mật Phần cứng (HSM) hoặc dịch vụ Hệ điều hành có thể sử dụng bộ nhớ an toàn này. | | ✓ | ✓ | 320 | 5.1.7.2 |
| **2.9.2** | Xác minh rằng thử thách nonce có độ dài ít nhất 64 bit và duy nhất về mặt thống kê hoặc duy nhất trong suốt vòng đời của thiết bị mật mã. | | ✓ | ✓ | 330 | 5.1.7.2 |
| **2.9.3** | [MODIFIED] Xác minh rằng các thuật toán mật mã được phê duyệt được sử dụng để tạo, gieo hạt và xác minh các khóa mật mã. | | ✓ | ✓ | 327 | 5.1.7.2 |

## V2.10 Service Authentication

Phần này không thể kiểm tra thâm nhập, vì vậy không có bất kỳ yêu cầu L1 nào.

Bí mật có thể được lưu trữ an toàn bằng cách sử dụng các dịch vụ do khuôn khổ, hệ điều hành hoặc phần cứng cung cấp. Ví dụ: Java Key Store, Keychain Access và AWS Secrets Manager là những dịch vụ có thể giúp lưu trữ bí mật một cách an toàn. Để bảo mật tối ưu, nên sử dụng giải pháp phần cứng như Mô-đun Bảo mật Phần cứng hoặc Mô-đun Nền tảng Đáng tin cậy. Để phù hợp với cấp độ 2, bí mật phải được lưu trữ trong một dịch vụ bảo mật do khuôn khổ hoặc hệ điều hành cung cấp. Đối với cấp độ 3, bí mật phải được lưu trữ trong một dịch vụ hỗ trợ phần cứng.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **2.10.1** | Xác minh rằng các bí mật nội bộ dịch vụ không dựa vào thông tin đăng nhập không thay đổi như mật khẩu, khóa API hoặc tài khoản dùng chung có quyền truy cập đặc quyền. | | ✓ | ✓ | 287 | |
| **2.10.2** | [GRAMMAR] Xác minh rằng nếu phải sử dụng thông tin đăng nhập để xác thực dịch vụ, thì thông tin đăng nhập mà người tiêu dùng đang sử dụng không phải là thông tin đăng nhập mặc định (ví dụ: root/root hoặc admin/admin là mặc định trong một số dịch vụ trong quá trình cài đặt). | | ✓ | ✓ | 255 | |
| **2.10.3** | [DELETED, DUPLICATE OF 2.10.4] | | | | | |
| **2.10.4** | [GRAMMAR] Xác minh mật khẩu, tích hợp với cơ sở dữ liệu và hệ thống bên thứ ba, hạt giống và bí mật nội bộ, và khóa API được quản lý an toàn và không được bao gồm trong mã nguồn hoặc lưu trữ trong kho lưu trữ mã nguồn. Việc lưu trữ như vậy sẽ chống lại các cuộc tấn công ngoại tuyến. Việc sử dụng kho khóa phần mềm an toàn (L1), TPM phần cứng hoặc HSM (L3) được khuyến nghị để lưu trữ mật khẩu. | | ✓ | ✓ | 798 | |

## Additional US Agency Requirements

Các cơ quan Hoa Kỳ có các yêu cầu bắt buộc liên quan đến NIST SP 800-63. Tiêu chuẩn Xác minh Bảo mật Ứng dụng (ASVS) luôn hướng đến 80% biện pháp kiểm soát áp dụng cho gần 100% ứng dụng và không phải 20% biện pháp kiểm soát nâng cao cuối cùng hoặc những biện pháp kiểm soát có khả năng áp dụng hạn chế. Như vậy, ASVS là một tập con nghiêm ngặt của NIST SP 800-63, đặc biệt đối với các phân loại IAL1/2 và AAL1/2, nhưng không đủ toàn diện, đặc biệt là liên quan đến các phân loại IAL3/AAL3.

Chúng tôi khuyến khích các cơ quan chính phủ Hoa Kỳ xem xét và triển khai NIST SP 800-63 một cách đầy đủ.

## Glossary of terms

| Term | Meaning |
| -- | -- |
| CSP | Nhà cung cấp dịch vụ thông tin xác thực (Credential Service Provider) còn được gọi là Nhà cung cấp danh tính (Identity Provider). |
| Authenticator | Mã xác thực mật khẩu, mã thông báo, MFA, xác nhận liên kết, v.v. |
| Verifier | "Một thực thể xác minh danh tính của người yêu cầu bằng cách xác minh quyền sở hữu và kiểm soát của người yêu cầu đối với một hoặc hai trình xác thực bằng giao thức xác thực. Để làm điều này, trình xác minh cũng có thể cần xác thực thông tin đăng nhập liên kết (các) trình xác thực với số nhận dạng của người đăng ký và kiểm tra trạng thái của họ". |
| OTP | One-time password. |
| SFA | Trình xác thực đơn nhân tố (Single-factor authenticators), chẳng hạn như thứ bạn biết (bí mật ghi nhớ, mật khẩu, cụm mật khẩu, mã PIN), thứ bạn là (sinh trắc học, dấu vân tay, quét khuôn mặt) hoặc thứ bạn có (mã thông báo OTP, thiết bị mật mã chẳng hạn như thẻ thông minh). |
| MFA | Xác thực đa yếu tố (Multi-factor authentication), bao gồm hai hoặc nhiều yếu tố đơn lẻ. |

## References

For more information, see also:

* [NIST SP 800-63 - Digital Identity Guidelines](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63-3.pdf)
* [NIST SP 800-63A - Enrollment and Identity Proofing](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a.pdf)
* [NIST SP 800-63B - Authentication and Lifecycle Management](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b.pdf)
* [NIST SP 800-63C - Federation and Assertions](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63c.pdf)
* [NIST SP 800-63 FAQ](https://pages.nist.gov/800-63-FAQ/)
* [OWASP Testing Guide 4.0: Testing for Authentication](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/04-Authentication_Testing/README.html)
* [OWASP Cheat Sheet - Password storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
* [OWASP Cheat Sheet - Forgot password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)
* [OWASP Cheat Sheet - Choosing and using security questions](https://cheatsheetseries.owasp.org/cheatsheets/Choosing_and_Using_Security_Questions_Cheat_Sheet.html)
