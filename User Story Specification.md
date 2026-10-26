# ĐẶC TẢ USER STORIES & ACCEPTANCE CRITERIA (ANSERA PLATFORM)

## 1. Document Information & Version History

**Tác giả:** Duong Duc An  
**Phiên bản:** 3.0  
**Ngày cập nhật:** 2026-10-26  
**Phạm vi:** Learning Trial cho từng khóa học — mua một lần.  
**Trạng thái:** Bản refactor sẵn sàng BA review; BD-001–BD-008 là quyết định đã xác nhận trong prompt, Open Questions chưa phải chính sách được phê duyệt.

| Phiên bản | Nội dung |
| --- | --- |
| 2.1 | Bản trước: 6 story, trial 7 ngày/50% 3 bài; còn giả định subscription, xác thực 0đ và retry 3 lần. |
| 3.0 | Tổ chức 11 story/5 Epic; mua một lần, hủy lịch không hủy trial, mua sớm, tự mua cuối kỳ, cấp quyền; BR, trạng thái, truy vết, thông báo và ghi chú UI được đồng bộ. |

Nguồn dự án: prompt “REFACTOR ANSERA LEARNING TRIAL – USER STORY SPECIFICATION V3.0”, mục 3–14 do người dùng cung cấp ngày 2026-10-26; file v2.1 tại repository `gnuodna/trial-learning-fs`, blob `d84ce48e836a44da63e9ef725ee323e1d62b13a8`. Khi khác nhau, BD đã xác nhận trong prompt ưu tiên hơn v2.1 và ảnh. Không suy ra phê duyệt chính sách từ mockup hoặc kết quả review của agent.

## 2. Feature Overview

Học viên đủ điều kiện liên kết phương thức thanh toán, đồng ý khoản mua một lần và kích hoạt 168 giờ trial cho một khóa học. Trong hạn chỉ xem 50% đầu video của từng bài trong 3 bài đầu, xem lại không giới hạn; nội dung khác và tài liệu bảo vệ bị khóa. Học viên được hủy lịch thanh toán trước hạn và vẫn giữ trial, hoặc mua sớm để mở đầy đủ. Tại hết hạn, chỉ tự mua khi còn ủy quyền hợp lệ, chưa hủy và chưa sở hữu. Chưa có thanh toán thành công thì mất toàn bộ trial đúng hạn, kể cả khi giao dịch còn đang xử lý.

Authentication là dependency hiện hữu. Checkout mua trực tiếp/mua sau hết hạn dùng luồng mua một lần hiện hữu, áp dụng cùng kiểm tra thanh toán và cấp quyền trong tài liệu này; không thêm story ngoài baseline. Không bao gồm thiết kế mới OAuth, hoàn tiền, đa tài khoản, bundle, phiên bản khóa hoặc retry nhiều ngày. Giá trong ảnh không phải bảng giá được phê duyệt.

## 3. Confirmed Business Decisions

| ID | Quyết định đã được xác nhận |
| --- | --- |
| BD-001 | Mua một lần cho từng khóa; không thu định kỳ. |
| BD-002 | Trial đúng 168 giờ từ kích hoạt thành công; 50% đầu video của từng bài trong 3 bài đầu, replay không giới hạn trong hạn; khóa nội dung khác/tài liệu bảo vệ. |
| BD-003 | Cần phương thức hỗ trợ và consent rõ ràng cho khoản tự mua một lần sau trial; xử lý qua gateway, không mặc định xác thực 0đ. |
| BD-004 | Cho hủy thanh toán tự động trước hạn; không kết thúc trial sớm, vẫn học tới expiry ban đầu. |
| BD-005 | Cho mua sớm trong trial; thành công mở toàn bộ, vô hiệu hóa tự mua, ngăn thu trùng, giữ tiến trình; thất bại giữ trial còn lại. |
| BD-006 | Tại hết hạn chỉ tự mua khi chưa hủy/chưa sở hữu và phương thức được ủy quyền còn hợp lệ. Thành công mở khóa; thất bại không cấp paid, thu hồi trial và thông báo/đường mua thủ công. Không có grace nhiều ngày/lịch retry tự động MVP. |
| BD-007 | Hết hạn chưa mua thì mất toàn bộ quyền trial; refresh/đăng nhập lại không khôi phục. |
| BD-008 | Một lần trial cho mỗi học viên/khóa; người đã sở hữu không được trial/mua trùng. Không suy diễn chính sách nhiều tài khoản/thẻ dùng chung/bundle/phiên bản khóa. |

## 4. User Story Backlog by Epic

### Authentication

| User Story ID | Tên | Priority | Xử lý so với v2.1 |
| --- | --- | --- | --- |
| US-AUTH-001 | Đăng ký tài khoản học viên mới | P0 | KEEP |

### Trial Enrollment

| User Story ID | Tên | Priority | Xử lý so với v2.1 |
| --- | --- | --- | --- |
| US-CRS-002 | Xem thông tin khóa học và quyền học thử | P0 | KEEP / REVISE |
| US-ENR-003 | Xem và xác nhận điều kiện học thử | P1 | KEEP / REVISE |
| US-PAY-004 | Liên kết phương thức thanh toán và kích hoạt học thử | P0 | KEEP / REVISE |

### Trial Experience

| User Story ID | Tên | Priority | Xử lý so với v2.1 |
| --- | --- | --- | --- |
| US-PLAY-005 | Trải nghiệm nội dung học thử có giới hạn | P0 | KEEP / REVISE |
| US-TRIAL-007 | Xem trạng thái và thời gian học thử | P1 | NEW |

### Purchase & Payment

| User Story ID | Tên | Priority | Xử lý so với v2.1 |
| --- | --- | --- | --- |
| US-PAY-008 | Hủy thanh toán tự động sau học thử | P0 | NEW |
| US-PAY-009 | Tự động mua khóa học khi kết thúc thời hạn học thử | P0 | NEW / EXTRACT FROM US-PAY-004 |
| US-PAY-010 | Thanh toán mở khóa khóa học trước thời hạn | P0 | NEW |

### Access Management

| User Story ID | Tên | Priority | Xử lý so với v2.1 |
| --- | --- | --- | --- |
| US-EXP-006 | Tự động hết hạn học thử và thu hồi quyền truy cập | P0 | KEEP / REVISE |
| US-ACCESS-011 | Cấp quyền truy cập đầy đủ sau khi mua khóa học thành công | P0 | NEW |

## 5. Business Rules – Learning Trial

Áp dụng cho cặp học viên–khóa học. Giữ mã BR-001–BR-014 theo baseline được chỉ định; không đổi sang quy ước mã khác.

| ID | Business Rule | Nguồn |
| --- | --- | --- |
| BR-001 | Một học viên chỉ được kích hoạt trial một lần cho mỗi khóa học; kích hoạt lặp/đăng nhập lại không đặt lại lịch sử. | BD-008 |
| BR-002 | Trial bắt đầu khi kích hoạt thành công; expiry = start + 168 giờ. Quyền trial chỉ hợp lệ khi thời gian máy chủ nhỏ hơn expiry. | BD-002 |
| BR-003 | Trong trial còn hiệu lực chỉ được phát phần đầu tối đa 50% thời lượng video của từng bài trong 3 bài đầu; xem lại phần được phép không giới hạn. Bài khác và tài liệu bảo vệ bị khóa. | BD-002 |
| BR-004 | Tại expiry, nếu chưa có quyền đã mua từ thanh toán thành công, thu hồi toàn bộ quyền trial kể cả phần 50% của 3 bài đầu. | BD-006, BD-007 |
| BR-005 | Học viên đã sở hữu khóa học không được kích hoạt trial hoặc bị tạo khoản mua trùng cho khóa đó qua các luồng bình thường. | BD-005, BD-008 |
| BR-006 | Trước kích hoạt, phải có phương thức được gateway hỗ trợ và consent rõ ràng cho giá/tiền tệ, thời điểm thu tiền một lần; thay đổi điều kiện phải xác nhận lại. | BD-003 |
| BR-007 | Hủy lịch tự mua thành công trước expiry ngăn khoản tự thu, giữ nguyên trial và expiry ban đầu. | BD-004 |
| BR-008 | Mua sớm thành công vô hiệu hóa lịch tự mua cuối kỳ chưa thực thi và giữ tiến trình học nếu có. | BD-005 |
| BR-009 | Tự mua thất bại không cấp paid access; quyền trial chấm dứt tại expiry. MVP không có grace period nhiều ngày hoặc lịch tự retry. | BD-006 |
| BR-010 | Thanh toán thành công được gateway xác minh cấp quyền toàn bộ nội dung khóa đã mua, gỡ giới hạn trial và lưu ownership qua các phiên. | BD-005, BD-006 |
| BR-011 | Các luồng mua sớm/tự mua và yêu cầu/callback lặp cho cùng học viên–khóa phải phối hợp để không thực hiện khoản mua trùng. Khi giao dịch chưa rõ kết quả, không tạo khoản thu độc lập khác. | BD-005, BD-006 |
| BR-012 | Backend/media delivery thực thi quyền của đúng học viên/khóa/tài nguyên và thời hạn; sửa frontend, URL trực tiếp hoặc đăng nhập lại không vượt được quyền. | BD-002, BD-007 |
| BR-013 | Khóa học được mua một lần; sau mua không tạo khoản thu định kỳ hoặc subscription cho Learning Trial. | BD-001 |
| BR-014 | Hủy lịch tự mua không cấm học viên chủ động mua khóa học; mua thất bại không mất trial còn lại trước expiry. | BD-004, BD-005 |

## 6. State Definitions & Transition Matrix

### 6.1. Ba chiều trạng thái độc lập

| Chiều | Trạng thái | Ý nghĩa |
| --- | --- | --- |
| trial_status | NOT_STARTED | Chưa kích hoạt trial; thất bại liên kết không tiêu thụ quyền. |
| trial_status | TRIAL_ACTIVE | Đã kích hoạt, còn hạn và chưa chuyển đổi mua thành công. |
| trial_status | TRIAL_EXPIRED | Đã hết 168 giờ khi chưa mua thành công. |
| trial_status | CONVERTED | Trial đã dùng được chuyển đổi sang mua thành công, kể cả thành công xác minh về sau expiry. |
| automatic_payment_status | NONE | Chưa lập lịch tự mua. |
| automatic_payment_status | SCHEDULED | Lịch được lập và chưa có kết quả cuối; không có nghĩa giao dịch đã thành công. |
| automatic_payment_status | CANCELED | Lịch đã vô hiệu hóa do hủy thành công hoặc đã mua sớm. Không phải hủy quyền trial. |
| automatic_payment_status | COMPLETED | Khoản tự mua của lịch đã được xác minh thành công. Không dùng cho giao dịch mua chủ động. |
| automatic_payment_status | FAILED | Tự mua thất bại dứt khoát hoặc không thể thực hiện do phương thức/ủy quyền hết hiệu lực. |
| course_access | NOT_OWNED | Không có quyền trial hiệu lực hoặc ownership đã mua. |
| course_access | TRIAL_LIMITED | Chỉ có giới hạn trial hiện còn hiệu lực. |
| course_access | PAID_ACTIVE | Có ownership từ thanh toán thành công đã được xác minh. |

`course_access` là chiều quyền/ownership khái niệm của baseline; lịch sử đã dùng trial được lưu riêng, không xóa khi quyền về NOT_OWNED. Mua trực tiếp chưa từng trial giữ trial_status = NOT_STARTED và automatic_payment_status = NONE, đồng thời PAID_ACTIVE; không tiêu thụ trial để rồi cho mua/trial trùng.

Không thêm `PROCESSING` vào enum thanh toán tự động đã chốt. Giao dịch đang thực thi/chưa rõ kết quả có dấu vết xử lý riêng của transaction, phân biệt với lịch. Trong thời gian này lịch chưa có kết quả cuối vẫn SCHEDULED; phải kiểm tra transaction trước hủy/gửi mua. Đây là ràng buộc nhất quán dẫn xuất từ yêu cầu chống thu trùng, không phải quyết định retry hoặc hoàn tiền. Tên trường kỹ thuật, timeout và thời hạn đối soát chờ OQ-002.

### 6.2. Ma trận chuyển dịch

Ký hiệu bộ ba: `trial_status / automatic_payment_status / course_access`; “giữ” nghĩa không thay đổi chiều đó. Guards được kiểm tra bằng trạng thái backend/thời gian máy chủ. Không chỉ dựa vào nút hoặc scheduler.

| ID | Trước | Trigger / Vai trò | Preconditions / Guard | Sau | Quyền / ngoại lệ / AC truy vết |
| --- | --- | --- | --- | --- | --- |
| ST-01 | NOT_STARTED / NONE / NOT_OWNED | Kích hoạt / học viên + hệ thống | Đủ điều kiện, consent cuối khớp giá/lịch, phương thức xác nhận hỗ trợ | TRIAL_ACTIVE / SCHEDULED / TRIAL_LIMITED | 168 giờ; US-PAY-004.AC1. |
| ST-02 | NOT_STARTED / NONE / NOT_OWNED | Liên kết lỗi/chưa rõ / gateway | Chưa đủ điều kiện kích hoạt | Giữ | Không tạo quyền/lịch; US-PAY-004.AC4, AC6. |
| ST-03 | TRIAL_ACTIVE / SCHEDULED / TRIAL_LIMITED | Hủy ngày 2 / học viên | Hủy được chấp nhận trước expiry và trước khi giao dịch được gửi | TRIAL_ACTIVE / CANCELED / TRIAL_LIMITED | Giữ expiry gốc; US-PAY-008.AC1, AC4. |
| ST-04 | TRIAL_ACTIVE / CANCELED / TRIAL_LIMITED | Hủy lặp / học viên | Lịch đã vô hiệu hóa | Giữ | Không đổi thời hạn; US-PAY-008.AC2. |
| ST-05 | TRIAL_ACTIVE / SCHEDULED hoặc CANCELED / TRIAL_LIMITED | Mua sớm thành công / gateway + hệ thống | Giao dịch chủ động xác minh thành công | CONVERTED / CANCELED / PAID_ACTIVE | Vô hiệu lịch và giữ tiến trình; US-PAY-010.AC1, AC2; US-ACCESS-011.AC1. |
| ST-06 | TRIAL_ACTIVE / SCHEDULED hoặc CANCELED / TRIAL_LIMITED | Mua sớm thất bại / gateway | Thất bại dứt khoát, vẫn trước expiry | Giữ | Không hủy lịch đang hợp lệ; US-PAY-010.AC3. |
| ST-07 | TRIAL_ACTIVE / CANCELED / TRIAL_LIMITED | Đạt expiry / hệ thống | Chưa sở hữu | TRIAL_EXPIRED / CANCELED / NOT_OWNED | Không tự thu, khóa toàn bộ; US-EXP-006.AC2. |
| ST-08 | TRIAL_ACTIVE / SCHEDULED / TRIAL_LIMITED | Đạt expiry / hệ thống | Chưa sở hữu; tự mua đủ điều kiện, chưa có giao dịch cạnh tranh | TRIAL_EXPIRED / SCHEDULED / NOT_OWNED | Thực hiện một khoản mua; đang chờ không có quyền trial/paid; US-PAY-009.AC8, US-EXP-006.AC1. |
| ST-09 | TRIAL_EXPIRED / SCHEDULED / NOT_OWNED | Tự mua thành công / gateway | Kết quả xác minh khớp cùng giao dịch | CONVERTED / COMPLETED / PAID_ACTIVE | Ghi giao dịch và cấp quyền; US-PAY-009.AC1, US-ACCESS-011.AC1; lỗi cấp quyền xem ngoại lệ 6.3. |
| ST-10 | TRIAL_EXPIRED / SCHEDULED / NOT_OWNED | Tự mua thất bại / gateway hoặc kiểm tra ủy quyền | Kết quả thất bại dứt khoát hoặc không thể gửi hợp lệ | TRIAL_EXPIRED / FAILED / NOT_OWNED | Không retry/grace tự đặt; US-PAY-009.AC4, AC5. |
| ST-11 | TRIAL_EXPIRED / CANCELED hoặc FAILED / NOT_OWNED | Mua chủ động sau hạn / checkout hiện hữu | Không có giao dịch chưa rõ kết quả, mua được xác minh thành công | CONVERTED / giữ CANCELED hoặc FAILED / PAID_ACTIVE | Không viết lại lịch sử tự mua thành COMPLETED; US-ACCESS-011.AC1. |
| ST-12 | TRIAL_EXPIRED / SCHEDULED / NOT_OWNED | Mua bắt đầu trước hạn, thành công về chậm / gateway | Cùng giao dịch chủ động, chưa có khoản thu độc lập khác | CONVERTED / CANCELED / PAID_ACTIVE | Không phục hồi trial; US-PAY-010.AC5. |
| ST-13 | CONVERTED / CANCELED hoặc COMPLETED hoặc FAILED / PAID_ACTIVE | Callback/tác vụ lặp / hệ thống | Kết quả mua đã xác minh | Giữ | Không thu trùng/hạ quyền; US-ACCESS-011.AC4; US-EXP-006.AC5. |
| ST-14 | NOT_STARTED / NONE / NOT_OWNED | Mua trực tiếp / checkout hiện hữu | Chưa sở hữu; thanh toán xác minh thành công | NOT_STARTED / NONE / PAID_ACTIVE | Cấp quyền khóa mua, không tạo trial/lịch; US-ACCESS-011.AC1, AC2. |

### 6.3. Bất biến và ngoại lệ

- Trial có hiệu lực ở khoảng `[trial_start, trial_expires_at)`. Scheduler chạy muộn không kéo dài quyền. Tại đúng expiry, quyền trial kết thúc; ownership đã mua có ưu tiên khi kiểm tra truy cập.
- Không cho TRIAL_EXPIRED/CONVERTED trở lại TRIAL_ACTIVE cho cùng học viên–khóa; không cho CANCELED trở lại SCHEDULED bằng refresh/hủy lặp; không cấp PAID_ACTIVE từ client redirect hoặc gửi request.
- Hủy được chấp nhận trước hạn phải ngăn gửi thu; nếu giao dịch đã thực thi hoặc yêu cầu đến muộn, không báo thành công giả. Xử lý hoàn/void hoặc ngoại lệ tiếp nhận muộn chờ OQ-003. Không tự mở rộng quyền hủy sau hạn.
- Chậm callback/timeout không bằng FAILED. Khóa trial khi hết hạn, giữ dấu vết transaction để đối soát; không tự cấp quyền hoặc khởi tạo khoản thu mới. Callback thành công xác minh của cùng giao dịch được xử lý theo ST-09/ST-12; cách giải quyết kết quả chưa rõ kéo dài chờ OQ-002.
- Kiểm tra nguồn gateway, khóa học, học viên, số tiền/tiền tệ và giao dịch trước cấp quyền. Callback trùng không tạo thu/ownership/biên lai trùng. Callback cũ/mâu thuẫn không hạ ownership; đối soát trước thay kết quả cuối.
- Thanh toán đã thành công nhưng cập nhật quyền lỗi: giữ giao dịch thành công, MSG-020 và hoàn tất cấp quyền có thể xử lý lại không thu thêm (US-ACCESS-011.AC5). Không báo paid access đã sẵn sàng khi chưa cập nhật quyền; không đổi thanh toán thành FAILED vì lỗi nội bộ. Các bộ ba ST-09/ST-12 là trạng thái đích sau hoàn tất cấp quyền.
- Mua chủ động thành công sau lịch FAILED giữ FAILED của lịch; không đồng nhất thành công giao dịch chủ động với automatic_payment_status = COMPLETED. Không hạ PAID_ACTIVE bởi tác vụ hết hạn. Refund/chargeback không được tự thiết kế trong phạm vi này.

## 7. Message Catalog

Thông điệp có placeholder phải hiển thị giá/tiền tệ và thời gian có múi giờ thực tế. Nội dung là bản copy đặc tả, không coi dữ liệu minh họa trên ảnh là giá đã chốt.

| MSG ID | Type | Nội dung tiếng Việt | Trigger condition |
| --- | --- | --- | --- |
| MSG-001 | Lỗi | Vui lòng nhập thông tin | Thiếu trường bắt buộc khi gửi đăng ký hoặc liên kết phương thức. |
| MSG-002 | Cảnh báo | Tên người dùng đã tồn tại | Username đăng ký bị trùng; gắn tại username, không tại password. |
| MSG-003 | Lỗi | Thông tin chưa hợp lệ | Password dưới 8 ký tự/xác nhận không khớp; email hoặc dữ liệu thanh toán sai quy tắc của phương thức/gateway đã chọn. |
| MSG-004 | Thông báo | Bạn đã sở hữu khóa học này. Hãy vào học để tiếp tục. | Người đã mua yêu cầu trial/mua lại; giữ ID chống trùng sở hữu từ v2.1. |
| MSG-005 | Thông báo | Bạn đã hoàn thành thời lượng học thử của bài học này. Vui lòng mở khóa để xem tiếp toàn bộ nội dung. | Chạm/tua tới giới hạn 50% video được trial cho phép. |
| MSG-006 | Cảnh báo | Thời gian học thử 7 ngày của bạn cho khóa học này đã kết thúc. Vui lòng thanh toán để tiếp tục học tập. | Trial đã hết hạn và chưa sở hữu; không dùng khi chỉ hủy thanh toán trước hạn. |
| MSG-007 | Thành công | Đã kích hoạt học thử. Bạn có thể học đến {expires_at}. Khoản mua khóa học một lần {amount} {currency} dự kiến được thanh toán lúc {payment_at}, trừ khi bạn hủy trước hạn. | Kích hoạt và lập lịch thành công; thời gian có múi giờ. |
| MSG-008 | Thành công | Đã hủy thanh toán tự động sau học thử. Bạn vẫn được học thử đến {expires_at} và có thể chủ động mua khóa học. | Hủy đã được ghi nhận thành công, kể cả yêu cầu lặp. |
| MSG-009 | Thành công | Mua khóa học thành công. Bạn đã có toàn bộ nội dung; khoản mua tự động cuối kỳ đã được vô hiệu hóa. | Mua sớm và cấp quyền hoàn tất. |
| MSG-010 | Thành công | Khoản mua khóa học một lần sau học thử đã thanh toán thành công. Bạn có thể tiếp tục học toàn bộ khóa học. | Tự mua và cấp quyền hoàn tất. |
| MSG-011 | Lỗi | Không thể hoàn tất thanh toán tự động sau học thử. Quyền học thử đã hết hạn. Bạn có thể chủ động mua khóa học để tiếp tục. | Tại/sau expiry có kết quả thất bại xác minh hoặc phương thức/ủy quyền không đủ điều kiện. |
| MSG-012 | Đang xử lý | Yêu cầu đang được kiểm tra kết quả. Vui lòng kiểm tra trạng thái trước khi thực hiện thanh toán khác. | Liên kết/giao dịch chưa rõ kết quả hoặc yêu cầu mua lặp khi đang xử lý; không ngụ ý cấp quyền. |
| MSG-013 | Cảnh báo | Chưa thể xác nhận hủy: thời hạn hủy đã kết thúc hoặc giao dịch đang được xử lý. Vui lòng kiểm tra trạng thái thanh toán. | Yêu cầu hủy tới hạn/đang có giao dịch thực thi; không hứa hủy/hoàn tiền. |
| MSG-014 | Thông báo | Bạn đã sử dụng quyền học thử của khóa học này. Mỗi học viên chỉ được học thử một lần cho mỗi khóa học. | Ngăn trial lặp; với trial còn hạn vẫn cho tiếp tục học. |
| MSG-015 | Cảnh báo | Vui lòng xác nhận điều kiện học thử và khoản mua khóa học một lần sau học thử trước khi tiếp tục. | Chưa có consent hợp lệ. |
| MSG-016 | Lỗi | Không thể xác thực hoặc liên kết phương thức thanh toán. Vui lòng kiểm tra hoặc chọn phương thức được hỗ trợ khác. | Gateway từ chối liên kết/ủy quyền, chưa kích hoạt trial. |
| MSG-017 | Thông báo | Nội dung này chỉ được mở sau khi mua khóa học thành công. | Trial yêu cầu bài ngoài 3 bài đầu hoặc tài liệu bảo vệ. |
| MSG-018 | Lỗi | Chưa thể xác nhận hủy thanh toán tự động. Vui lòng kiểm tra lại trạng thái trước thời điểm hết hạn. | Lỗi ghi nhận/vô hiệu hóa lịch, chưa được xác nhận CANCELED. |
| MSG-019 | Lỗi | Thanh toán mua khóa học chưa thành công. Bạn vẫn có thể học thử đến {expires_at} nếu thời hạn chưa kết thúc. | Mua chủ động thất bại dứt khoát; không dùng cho giao dịch chưa rõ kết quả. |
| MSG-020 | Đang xử lý | Thanh toán đã thành công, hệ thống đang hoàn tất cấp quyền khóa học. Bạn không cần thanh toán lại. | Thành công đã xác minh nhưng cập nhật entitlement chưa hoàn tất. |

## 8. Detailed User Story Specifications

### 8.1. US-AUTH-001 – Đăng ký tài khoản học viên mới

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-AUTH-001 |
| User Story Name | Đăng ký tài khoản học viên mới |
| Epic | Authentication |
| Priority | P0 |
| User Role | khách truy cập mới chưa có tài khoản trên ANSERA |

#### B. User Story Statement

**As a** khách truy cập mới chưa có tài khoản trên ANSERA  
**I want to** đăng ký tài khoản bằng username và mật khẩu cá nhân  
**So that** tôi có tài khoản định danh để học tập và lưu tiến trình cá nhân.

#### C. Business Context

Dependency xác thực của Learning Trial; giữ hành vi đăng ký hiện hữu, không thiết kế lại Authentication.

#### D. Preconditions

Khách chưa đăng nhập và đang ở trang đăng ký.

#### E. Acceptance Criteria

**AC1: Đăng ký thành công — Happy Path**

- **Given** khách ở trang đăng ký và username chưa tồn tại.
- **When** nhập username, password tối thiểu 8 ký tự, xác nhận trùng khớp và nhấn Đăng ký.
- **Then** tạo tài khoản ở trạng thái kích hoạt; tự động đăng nhập và điều hướng về trang chủ.

**AC2: Thiếu dữ liệu — Negative Path**

- **Given** khách ở form đăng ký.
- **When** bỏ trống username, password hoặc xác nhận rồi gửi.
- **Then** không tạo tài khoản; hiển thị MSG-001 tại từng trường thiếu, giữ các giá trị đã nhập phù hợp.

**AC3: Trùng username — Negative Path**

- **Given** username đã được một tài khoản sử dụng.
- **When** gửi đăng ký với username đó.
- **Then** không tạo tài khoản trùng; hiển thị MSG-002 tại username.

**AC4: Mật khẩu dưới giới hạn — Boundary**

- **Given** username chưa tồn tại và xác nhận khớp.
- **When** gửi password có dưới 8 ký tự.
- **Then** chặn đăng ký, đánh dấu trường lỗi và hiển thị MSG-003; password đúng 8 ký tự không bị từ chối vì độ dài.

**AC5: Xác nhận khác mật khẩu — Negative Path**

- **Given** password có ít nhất 8 ký tự.
- **When** gửi xác nhận không trùng password.
- **Then** chặn đăng ký, đánh dấu trường xác nhận lỗi và hiển thị MSG-003.

#### F. UI Component Specification

![US-AUTH-001_ Homepage khi truy cập vào trang trước khi đăng ký](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-AUTH-001_%20Homepage%20khi%20truy%20c%E1%BA%ADp%20v%C3%A0o%20trang%20tr%C6%B0%E1%BB%9Bc%20khi%20%C4%91%C4%83ng%20k%C3%AD.png)

![US-AUTH-001_ Đăng ký tài khoản học viên mới](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-AUTH-001_%20%C4%90%C4%83ng%20k%C3%BD%20t%C3%A0i%20kho%E1%BA%A3n%20h%E1%BB%8Dc%20vi%C3%AAn%20m%E1%BB%9Bi.png)

![US-AUTH-001_ Đăng ký (Lỗi validation MSG-001, MSG-002, MSG-003)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-AUTH-001_%20%C4%90%C4%83ng%20k%C3%BD%20(L%E1%BB%97i%20validation%20MSG-001,%20MSG-002,%20MSG-003).png)

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| :---: | --- | :---: | :---: | :---: | :---: | --- |
| 1 | Button tham gia miễn phí | Button | N/A | N/A | N/A | Nút kêu gọi hành động trên header/banner trang chủ. |
| 2 | Button tham gia miễn phí | Button | N/A | N/A | N/A | Nút kêu gọi hành động ở phần thân trang chủ. |
| 3 | Trường thông tin username | Text | Yes | Yes | N/A | - Bắt buộc nhập.<br>- Bỏ trống và bấm gửi: hiển thị **MSG-001** và đổi viền khung đỏ.<br>- Username đã tồn tại: hiển thị **MSG-002**. |
| 4 | Trường thông tin password | Text | Yes | Yes | N/A | - Mật khẩu bắt buộc nhập, ẩn ký tự dạng `*`.<br>- Tối thiểu 8 ký tự.<br>- Nhấn giữ biểu tượng con mắt để xem mật khẩu.<br>- Bỏ trống: hiển thị **MSG-001**.<br>- Dưới 8 ký tự: hiển thị **MSG-003**. |
| 5 | Trường nhập lại mật khẩu | Text | Yes | Yes | N/A | - Phải trùng khớp 100% với mật khẩu đã nhập.<br>- Bỏ trống: hiển thị **MSG-001**.<br>- Không trùng khớp: hiển thị **MSG-003** và viền đỏ. |
| 6 | Button đăng ký | Button | N/A | N/A | N/A | Gửi thông tin đăng ký tài khoản. Đăng ký thành công điều hướng về trang chủ với trạng thái đăng nhập. |
| 7 | Button đăng ký Google | Button | N/A | N/A | N/A | Chuyển hướng tới đăng ký bằng tài khoản Google. |
| 8 | Button đăng ký Facebook | Button | N/A | N/A | N/A | Chuyển hướng tới đăng ký bằng tài khoản Facebook. |
| 9 | Link đăng nhập | Link | N/A | N/A | N/A | Điều hướng sang trang Đăng nhập nếu đã có tài khoản. |

Giữ nguyên các nút điều hướng/Google/Facebook của module hiện hữu; không bổ sung chính sách Authentication mới.

#### G. Related Business Rules

N/A — quy tắc đăng ký giữ từ v2.1.

#### H. Dependencies

Module Authentication hiện hữu; các nút Google/Facebook và link đăng nhập dùng luồng hiện hữu.

### 8.2. US-CRS-002 – Xem thông tin khóa học và quyền học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-CRS-002 |
| User Story Name | Xem thông tin khóa học và quyền học thử |
| Epic | Trial Enrollment |
| Priority | P0 |
| User Role | học viên đã đăng nhập |

#### B. User Story Statement

**As a** học viên đã đăng nhập  
**I want to** xem thông tin khóa học và quyền học thử tương ứng trạng thái của tôi  
**So that** tôi có đủ thông tin để chọn học thử hoặc mua khóa học.

#### C. Business Context

Giữ thông tin đề cương, giảng viên, đánh giá, trailer và accordion; CTA phụ thuộc quyền sở hữu và lịch sử trial.

#### D. Preconditions

Khóa học được truy cập qua trang chi tiết; trạng thái của đúng học viên và khóa học được kiểm tra.

#### E. Acceptance Criteria

**AC1: Thông tin và quyền học thử — Happy Path**

- **Given** học viên chưa sở hữu và chưa từng trial khóa học.
- **When** mở chi tiết khóa học.
- **Then** hiển thị thông tin khóa, đơn vị phát hành, rating, số học viên, cấp độ, giảng viên, đánh giá, trailer; đánh dấu 3 bài đầu chỉ xem 50% video, các bài còn lại và tài liệu bảo vệ bị khóa; hiển thị Trải nghiệm 7 ngày và Mua ngay.

**AC2: Accordion — Alternative Flow**

- **Given** danh mục bài học đang hiển thị.
- **When** nhấn mũi tên tại bài học.
- **Then** mở hoặc thu tóm tắt bài học mà không tải lại trang.

**AC3: Đã sở hữu — Negative Path**

- **Given** học viên có PAID_ACTIVE.
- **When** mở trang hoặc gửi yêu cầu học thử/mua từ liên kết cũ.
- **Then** CTA chính là Vào học; không cho trial hay tạo thanh toán mua trùng; yêu cầu mua cũ nhận MSG-004.

**AC4: Trial đang hoạt động — Alternative Flow**

- **Given** học viên có TRIAL_ACTIVE và chưa sở hữu.
- **When** mở trang.
- **Then** hiển thị Tiếp tục học thử, trạng thái/thời gian còn lại theo US-TRIAL-007 và lựa chọn mua; không khởi tạo trial thứ hai.

**AC5: Trial đã dùng — Boundary**

- **Given** trial đã hết hạn và chưa sở hữu.
- **When** mở lại hoặc đăng nhập lại.
- **Then** không cho kích hoạt lại; giải thích bằng MSG-014 và cho phép thanh toán mua một lần.

#### F. UI Component Specification

![US-CRS-002_ Chi tiết khóa học (Huy hiệu Học thử 50% & CTA Trải nghiệm 7 ngày)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-CRS-002_%20Chi%20ti%E1%BA%BFt%20kh%C3%B3a%20h%E1%BB%8Dc%20(Huy%20hi%E1%BB%87u%20H%E1%BB%8Dc%20th%E1%BB%AD%2050%25%20&%20CTA%20Tr%E1%BA%A3i%20nghi%E1%BB%87m%207%20ng%C3%A0y).png)

**UI Update Required:** Giữ ảnh; bổ sung CTA theo trạng thái và thông tin 168 giờ. Giá 399.000đ trong ảnh là dữ liệu minh họa, không phải giá cố định của mọi khóa học.

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Card thông tin khóa học | Card | No | N/A | Theo khóa học | Tên khóa, đơn vị phát hành, rating, số học viên, cấp độ; giữ khối giảng viên và đánh giá. |
| 2 | Video trailer giới thiệu | Media | No | N/A | Chưa phát | Giới thiệu tổng quan; không thay thế kiểm tra quyền video bài học. |
| 3 | Trải nghiệm 7 ngày / Tiếp tục học thử / Vào học | Button | No | N/A | Theo trạng thái | Điều hướng US-ENR-003, US-PLAY-005 hoặc nội dung đã mua; không cho trial lặp lại. |
| 4 | Mua ngay | Button | No | N/A | Giá hiện hành | Mua một lần; không hiển thị cho người đã sở hữu. |
| 5 | Huy hiệu Học thử 50% | Badge | No | N/A | Bài 1–3 | Giới hạn video của từng bài; không thể hiện quyền đã mua. |
| 6 | Biểu tượng Khóa | Icon | No | N/A | Theo quyền | Các bài từ 4 và bài tập/quiz/tài liệu bảo vệ khóa với trial; sau hết hạn khóa cả 3 bài đầu nếu chưa mua. |
| 7 | Accordion bài học | Accordion | Yes | No | Thu gọn | Xem tóm tắt nội dung, không mở tài nguyên được bảo vệ. |

#### G. Related Business Rules

BR-001, BR-003, BR-005, BR-010, BR-014

#### H. Dependencies

US-AUTH-001; US-ENR-003; US-TRIAL-007; US-ACCESS-011; checkout mua một lần hiện hữu.

### 8.3. US-ENR-003 – Xem và xác nhận điều kiện học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-ENR-003 |
| User Story Name | Xem và xác nhận điều kiện học thử |
| Epic | Trial Enrollment |
| Priority | P1 |
| User Role | học viên đủ điều kiện học thử khóa học |

#### B. User Story Statement

**As a** học viên đủ điều kiện học thử khóa học  
**I want to** xem và chủ động đồng ý các điều kiện học thử cùng khoản mua một lần sau trial  
**So that** tôi hiểu quyền truy cập và khoản thanh toán trước khi liên kết phương thức.

#### C. Business Context

Consent phải thể hiện đúng khóa học, giá, thời điểm thu tiền và quyền hủy. Không coi thao tác xem modal là đồng ý.

#### D. Preconditions

Đã đăng nhập, chưa sở hữu, chưa từng kích hoạt trial cho khóa học.

#### E. Acceptance Criteria

**AC1: Hiển thị điều kiện — Happy Path**

- **Given** học viên đủ điều kiện đang ở chi tiết khóa học.
- **When** nhấn Trải nghiệm 7 ngày.
- **Then** modal nêu 168 giờ từ kích hoạt thành công; chỉ 50% video của từng bài trong 3 bài đầu, xem lại không giới hạn trong trial; giá mua một lần và ngày/giờ dự kiến thu tiền có múi giờ; giải thích không thu định kỳ và cách Hủy thanh toán tự động sau học thử mà vẫn học tới hạn.

**AC2: Đồng ý rõ ràng — Happy Path**

- **Given** đã xem điều kiện và consent chưa được chọn sẵn.
- **When** chủ động chọn đồng ý và tiếp tục.
- **Then** ghi nhận sự đồng ý với khóa học, giá và lịch dự kiến; chuyển US-PAY-004; chưa kích hoạt trial tại bước này.

**AC3: Chưa đồng ý — Negative Path**

- **Given** consent chưa được chọn.
- **When** yêu cầu tiếp tục.
- **Then** chặn chuyển tiếp và hiển thị MSG-015; đóng modal không tạo trial hoặc lịch thanh toán.

**AC4: Điều kiện thay đổi trước kích hoạt — Edge Case**

- **Given** giá hoặc thời điểm đã trình bày không còn khớp điều kiện kích hoạt cuối cùng.
- **When** tiếp tục kích hoạt.
- **Then** hiển thị lại giá và ngày/giờ chính xác, yêu cầu xác nhận mới trước khi kích hoạt; không dùng consent cũ cho khoản hoặc lịch khác.

**AC5: Không còn đủ điều kiện — Negative Path**

- **Given** đã dùng trial hoặc đã sở hữu từ phiên khác.
- **When** gửi xác nhận.
- **Then** kiểm tra lại và từ chối trial với MSG-014 hoặc MSG-004; không tạo lịch thanh toán.

#### F. UI Component Specification

![US-ENR-003_ Modal cam kết trải nghiệm học thử 7 ngày](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-ENR-003_%20Modal%20cam%20k%E1%BA%BFt%20tr%E1%BA%A3i%20nghi%E1%BB%87m%20h%E1%BB%8Dc%20th%E1%BB%AD%207%20ng%C3%A0y.png)

**UI Update Required:** Modal hiện tại ghi “$20 USD mỗi tháng”, quyền mọi khóa/chứng chỉ và “Hủy bất cứ lúc nào”. Thay bằng quyền của một khóa, giá mua một lần, lịch thu chính xác và quyền hủy trước hết hạn; không kế thừa cam kết chứng chỉ trong ảnh.

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Trải nghiệm 7 ngày | Button | No | N/A | Theo đủ điều kiện | Mở modal điều kiện. |
| 2 | Modal điều kiện học thử | Modal | No | Yes | Chưa mở | Hiển thị đầy đủ thời hạn, nội dung, giá một lần, thời điểm và múi giờ thanh toán, cách hủy và quyền còn lại. |
| 3 | Đồng ý thanh toán một lần sau học thử | Checkbox | Yes | Yes | Chưa chọn | Đồng ý rõ ràng, liên kết đúng phiên bản điều kiện; không chọn sẵn. |
| 4 | Bắt đầu dùng thử miễn phí | Button | No | N/A | Chưa cho tiếp tục | Chỉ chuyển sang liên kết phương thức khi consent hợp lệ; bản thân nút không kích hoạt trial. |

#### G. Related Business Rules

BR-001, BR-002, BR-003, BR-006, BR-007, BR-013

#### H. Dependencies

US-CRS-002; US-PAY-004; US-PAY-008.

### 8.4. US-PAY-004 – Liên kết phương thức thanh toán và kích hoạt học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-PAY-004 |
| User Story Name | Liên kết phương thức thanh toán và kích hoạt học thử |
| Epic | Trial Enrollment |
| Priority | P0 |
| User Role | học viên đã đồng ý điều kiện học thử |

#### B. User Story Statement

**As a** học viên đã đồng ý điều kiện học thử  
**I want to** liên kết phương thức thanh toán được hỗ trợ và kích hoạt trial  
**So that** tôi bắt đầu trải nghiệm với lịch mua một lần đã được ủy quyền.

#### C. Business Context

Gateway xác thực và lưu token/phương thức tham chiếu; không tạo subscription. Chỉ kích hoạt sau khi đủ điều kiện và consent hợp lệ.

#### D. Preconditions

Đã đăng nhập, chưa sở hữu/chưa dùng trial; đã xem điều kiện US-ENR-003.

#### E. Acceptance Criteria

**AC1: Kích hoạt thành công — Happy Path**

- **Given** gateway xác nhận phương thức hỗ trợ khoản mua tự động một lần và consent khớp giá/lịch cuối cùng.
- **When** học viên xác nhận kích hoạt và các điều kiện đều thành công.
- **Then** ghi trial_start tại thời điểm kích hoạt thành công, trial_expires_at = trial_start + 168 giờ; tạo đúng một lịch SCHEDULED cho đúng khóa/giá được đồng ý; đặt TRIAL_ACTIVE / TRIAL_LIMITED, hiển thị MSG-007, gửi email xác nhận và điều hướng Bài 1.

**AC2: Thiếu trường bắt buộc — Validation**

- **Given** đang liên kết phương thức.
- **When** gửi khi trường bắt buộc của phương thức bị trống.
- **Then** không kích hoạt; hiển thị MSG-001 tại trường thiếu.

**AC3: Sai định dạng — Negative Path**

- **Given** đang dùng form phương thức được hỗ trợ.
- **When** gửi dữ liệu không hợp lệ theo quy tắc của phương thức đó.
- **Then** không kích hoạt; hiển thị MSG-003; với form thẻ, giữ kiểm tra email, số thẻ, hạn thẻ và mã bảo vệ theo gateway, không áp quy tắc của một loại thẻ cho mọi phương thức.

**AC4: Gateway từ chối — Negative Path**

- **Given** dữ liệu đúng định dạng.
- **When** gateway từ chối liên kết hoặc quyền thu tiền.
- **Then** hiển thị MSG-016, cho kiểm tra hoặc đổi phương thức; không tiêu thụ quyền trial, không tạo trial hoạt động hoặc lịch thu tiền.

**AC5: Lặp yêu cầu/kết quả — Edge Case**

- **Given** trial cho học viên/khóa học đã kích hoạt thành công.
- **When** bấm kích hoạt nhiều lần hoặc nhận lại kết quả gateway.
- **Then** trả trạng thái đã có; giữ nguyên start/expiry và một lịch duy nhất, không kéo dài hoặc bắt đầu trial mới.

**AC6: Chưa có kết quả chắc chắn — Edge Case**

- **Given** yêu cầu liên kết đã gửi nhưng gateway chưa xác nhận.
- **When** trang được tải lại hoặc kết nối gián đoạn.
- **Then** không hiển thị kích hoạt thành công; hiển thị MSG-012 và kiểm tra kết quả của cùng yêu cầu; không tạo trial/lịch mới chỉ vì gửi lại.

**AC7: Consent/quyền sở hữu đổi — Negative Path**

- **Given** consent không còn khớp hoặc khóa đã được mua ở phiên khác.
- **When** hoàn tất liên kết.
- **Then** không kích hoạt với consent cũ hoặc tạo mua trùng; yêu cầu xác nhận mới theo US-ENR-003 hoặc hiển thị MSG-004.

#### F. UI Component Specification

![US-PAY-004_ Liên kết thẻ thanh toán quốc tế & Kích hoạt học thử 7 ngày](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-PAY-004_%20Li%C3%AAn%20k%E1%BA%BFt%20th%E1%BA%BB%20thanh%20to%C3%A1n%20qu%E1%BB%91c%20t%E1%BA%BF%20&%20K%C3%ADch%20ho%E1%BA%A1t%20h%E1%BB%8Dc%20th%E1%BB%AD%207%20ng%C3%A0y.png)

![US-PAY-004_ Điền thẻ thanh toán (Lỗi validation AC2 MSG-001 & AC3 MSG-003)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-PAY-004_%20%C4%90i%E1%BB%81n%20th%E1%BA%BB%20thanh%20to%C3%A1n%20(L%E1%BB%97i%20validation%20AC2%20MSG-001%20&%20AC3%20MSG-003).png)

![US-PAY-004_ Điền thẻ thanh toán (Lỗi thẻ bị từ chối AC4 Gateway Decline)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-PAY-004_%20%C4%90i%E1%BB%81n%20th%E1%BA%BB%20thanh%20to%C3%A1n%20(L%E1%BB%97i%20th%E1%BA%BB%20b%E1%BB%8B%20t%E1%BB%AB%20ch%E1%BB%91i%20AC4%20Gateway%20Decline).png)

**UI Update Required:** Giữ 3 ảnh form/kết quả lỗi; cập nhật consent và lịch mua một lần, thống nhất giá theo khóa. Không coi hình logo Visa/Mastercard, xác thực 0đ hoặc mẫu CVV là danh sách phương thức/quy tắc gateway đã được chốt.

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Họ và tên trên thẻ | Text / gateway-hosted | Yes | Theo phương thức | Trống | Giữ trường nếu gateway yêu cầu; tên theo quy tắc gateway, không mặc định cấm mọi ký tự đặc biệt. MSG-001/MSG-003. |
| 2 | Email | Text | Yes | Yes với form hiện hữu | Trống | Email nhận xác nhận trial và biên lai mua một lần; kiểm tra cú pháp, MSG-001/MSG-003. |
| 3 | Quốc gia | List / gateway-hosted | Yes | Theo phương thức | Chưa chọn | Quốc gia theo yêu cầu nhà cung cấp, không mặc định mọi phương thức đều cần. |
| 4 | Số thẻ | Gateway-hosted field | Yes | Theo phương thức thẻ | Trống | Do gateway thu nhận và kiểm tra định dạng/Luhn khi áp dụng; không lưu số thẻ đầy đủ trực tiếp tại ANSERA. |
| 5 | Ngày hết hạn | Gateway-hosted field | Yes | Theo phương thức thẻ | MM/YY nếu hỗ trợ | Kiểm tra định dạng và hiệu lực theo gateway; MSG-001/MSG-003. |
| 6 | Mã bảo vệ (CVV) | Gateway-hosted field | Yes | Theo gateway | Trống | Độ dài theo loại thẻ/gateway; không mặc định luôn 3 chữ số; không yêu cầu ANSERA lưu CVV. |
| 7 | Kích hoạt học thử 7 ngày | Button | No | N/A | Chưa gửi | Liên kết an toàn, kiểm tra consent cuối cùng, kích hoạt và lập lịch một lần; không suy ra thành công từ việc gửi yêu cầu. |
| 8 | Tóm tắt giá và lịch thu tiền | Summary | No | Yes | Theo điều kiện đã đồng ý | Hiển thị giá, tiền tệ, giờ và múi giờ chính xác; nếu thay đổi phải xác nhận lại trước kích hoạt. |

#### G. Related Business Rules

BR-001, BR-002, BR-005, BR-006, BR-012, BR-013

#### H. Dependencies

US-ENR-003; gateway được chọn; US-PLAY-005; US-PAY-009.

### 8.5. US-PLAY-005 – Trải nghiệm nội dung học thử có giới hạn

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-PLAY-005 |
| User Story Name | Trải nghiệm nội dung học thử có giới hạn |
| Epic | Trial Experience |
| Priority | P0 |
| User Role | học viên đang có trial còn hiệu lực |

#### B. User Story Statement

**As a** học viên đang có trial còn hiệu lực  
**I want to** xem và xem lại phần video được cho phép cùng Paywall tại giới hạn  
**So that** tôi đánh giá chất lượng giảng dạy trước khi mua khóa học.

#### C. Business Context

Giữ Seek Guard, Paywall và replay hiện hữu; quyền phải được kiểm tra khi cấp dữ liệu media, không chỉ che giao diện.

#### D. Preconditions

TRIAL_ACTIVE, chưa PAID_ACTIVE và thời gian máy chủ nhỏ hơn trial_expires_at.

#### E. Acceptance Criteria

**AC1: Dừng đúng giới hạn — Happy Path**

- **Given** đang xem video thuộc Bài 1, 2 hoặc 3, trial còn hạn.
- **When** đạt 50% tổng thời lượng video của bài đó.
- **Then** dừng phát ở ranh giới, không phát nội dung sau ranh giới; hiển thị Paywall và MSG-005.

**AC2: Tua vượt giới hạn — Boundary**

- **Given** trial còn hạn và video thuộc 3 bài đầu.
- **When** kéo tua tới thời điểm lớn hơn 50% thời lượng.
- **Then** không tải/phát phần vượt giới hạn; đưa vị trí về ranh giới 50% và hiển thị Paywall; backend/media delivery từ chối phần không được cấp quyền.

**AC3: Bài/tài nguyên bị khóa — Negative Path**

- **Given** chỉ có quyền trial.
- **When** mở Bài 4 trở đi hoặc bài tập/quiz/tài liệu bảo vệ kể cả qua URL trực tiếp.
- **Then** từ chối dữ liệu bảo vệ và hiển thị Paywall với MSG-017 khi có giao diện.

**AC4: Xem lại — Alternative Flow**

- **Given** Paywall đang hiện và trial còn hiệu lực.
- **When** chọn Xem lại đoạn học thử.
- **Then** đóng Paywall, tua về 00:00; cho xem lại phần đầu được phép không giới hạn số lần, không kéo dài trial.

**AC5: Hết hạn trong lúc phát — Edge Case**

- **Given** video đang phát với trial còn hiệu lực trước đó và chưa mua.
- **When** thời gian máy chủ đạt trial_expires_at.
- **Then** thu hồi quyền kể cả phần video đã được trial cho phép; dừng phát và chặn yêu cầu media tiếp theo theo US-EXP-006, hiển thị MSG-006.

**AC6: Mua thành công — Alternative Flow**

- **Given** đang có giới hạn trial.
- **When** thanh toán được gateway xác nhận thành công và quyền được cập nhật.
- **Then** bỏ giới hạn 50% và mở toàn bộ nội dung theo US-ACCESS-011; giữ tiến trình đã có.

#### F. UI Component Specification

![US-PLAY-005_ Trình phát video học thử 50% & Chặn tua (Seek Guard)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-PLAY-005_%20Tr%C3%ACnh%20ph%C3%A1t%20video%20h%E1%BB%8Dc%20th%E1%BB%AD%2050%25%20&%20Ch%E1%BA%B7n%20tua%20(Seek%20Guard).png)

![US-PLAY-005_ Lớp phủ Paywall Modal khi chạm mốc 50% (MSG-005)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-PLAY-005_%20L%E1%BB%9Bp%20ph%E1%BB%A7%20Paywall%20Modal%20khi%20ch%E1%BA%A1m%20m%E1%BB%91c%2050%25%20(MSG-005).png)

**UI Update Required:** Giữ 2 ảnh player/Paywall; thay lời nhắc lịch thu tiền, bổ sung trạng thái đã hủy. Giá/giảm giá, hoàn tiền 7 ngày, chứng chỉ, sở hữu trọn đời và cập nhật miễn phí trong ảnh chưa được BD xác nhận; không dùng làm yêu cầu mặc định.

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Khung trình phát video | Video | Yes | N/A | Chưa phát | Phát trong quyền hiện tại; không coi player là lớp kiểm soát duy nhất. |
| 2 | Thanh tua Seek-bar | Slider | Yes | No | 00:00 | Phân biệt 50% đầu được phép và phần sau bị khóa; không phát/tải vượt giới hạn. |
| 3 | Banner đếm ngược | Banner | No | N/A | Theo máy chủ | Thời gian còn lại và lịch mua một lần/trạng thái đã hủy theo US-TRIAL-007. |
| 4 | Paywall Modal Overlay | Modal | No | N/A | Đóng | Xuất hiện ở giới hạn 50% hoặc nội dung khóa; phân biệt MSG-005 và MSG-017. |
| 5 | Mở khóa toàn bộ khóa học | Button | No | N/A | Giá hiện tại | Dẫn tới xác nhận mua một lần US-PAY-010, không tự cấp quyền. |
| 6 | Xem lại đoạn học thử | Button | No | N/A | Theo trial | Chỉ cho replay khi còn hạn; hết hạn không cho xem lại. |

#### G. Related Business Rules

BR-002, BR-003, BR-004, BR-007, BR-010, BR-012

#### H. Dependencies

US-PAY-004; US-TRIAL-007; US-PAY-010; US-EXP-006; US-ACCESS-011; backend/media delivery.

### 8.6. US-TRIAL-007 – Xem trạng thái và thời gian học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-TRIAL-007 |
| User Story Name | Xem trạng thái và thời gian học thử |
| Epic | Trial Experience |
| Priority | P1 |
| User Role | học viên đã kích hoạt trial |

#### B. User Story Statement

**As a** học viên đã kích hoạt trial  
**I want to** xem thời gian còn lại, hạn và trạng thái khoản mua tự động  
**So that** tôi chủ động quyết định hủy thanh toán hoặc mua khóa học.

#### C. Business Context

Một nguồn trạng thái thống nhất cho trang khóa học và player; không suy ra quyền từ đồng hồ phía trình duyệt.

#### D. Preconditions

Đã đăng nhập, đang xem đúng khóa học có lịch sử trial.

#### E. Acceptance Criteria

**AC1: Xem thông tin — Happy Path**

- **Given** trial còn hạn và lịch SCHEDULED.
- **When** mở trạng thái khóa học.
- **Then** hiển thị thời gian còn lại không âm, thời điểm hết hạn có múi giờ, số tiền/tiền tệ mua một lần và lịch thu đã được đồng ý.

**AC2: Hủy thanh toán — Alternative Flow**

- **Given** hủy thành công trước hạn.
- **When** xem lại trạng thái.
- **Then** hiển thị CANCELED và không tự thu; vẫn giữ hạn ban đầu và thời gian học thử còn lại, không hiển thị lịch là khoản chắc chắn sẽ thu.

**AC3: Mua thành công — Alternative Flow**

- **Given** quyền đã PAID_ACTIVE.
- **When** cập nhật trang.
- **Then** hiển thị đã sở hữu, không còn đếm ngược như giới hạn truy cập hoặc lịch tự thu đang chờ; dùng trạng thái thanh toán thực tế.

**AC4: Hết hạn/đang xử lý — Boundary**

- **Given** chưa có thanh toán thành công.
- **When** đạt hạn hoặc tải lại sau hạn.
- **Then** thời gian còn lại bằng 0, trial hết hạn; nếu giao dịch chưa rõ kết quả hiển thị MSG-012, nếu thất bại hiển thị MSG-011; không coi đang xử lý là đã mua.

**AC5: Không được đọc dữ liệu người khác — Negative Path**

- **Given** đang đăng nhập học viên A.
- **When** yêu cầu dữ liệu trial/thanh toán của học viên B.
- **Then** backend từ chối và không tiết lộ số tiền, phương thức hoặc lịch của B.

#### F. UI Component Specification

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Trạng thái học thử và quyền sở hữu | Status | No | N/A | Theo backend | Tách trial_status, automatic_payment_status, course_access. |
| 2 | Thời gian còn lại / Hết hạn lúc | Countdown / Text | No | N/A | Theo máy chủ | Hiển thị giờ/ngày và múi giờ; không thể gia hạn bằng sửa đồng hồ máy. |
| 3 | Giá mua một lần / lịch thanh toán | Summary | No | N/A | Theo consent | Thể hiện rõ đã hủy, hoàn tất, thất bại hoặc đang xử lý; lịch cũ chỉ là lịch sử khi đã hủy. |
| 4 | Hủy thanh toán tự động sau học thử | Button | No | N/A | Theo điều kiện US-PAY-008 | Chỉ cho hủy lịch còn đủ điều kiện. |
| 5 | Mua khóa học / Vào học | Button | No | N/A | Theo quyền | CTA mua chịu kiểm tra giao dịch đang xử lý, không tạo thu trùng. |

#### G. Related Business Rules

BR-002, BR-004, BR-006, BR-007, BR-008, BR-009, BR-010

#### H. Dependencies

US-PAY-004; US-PAY-008; US-PAY-009; US-PAY-010; US-EXP-006; US-ACCESS-011.

### 8.7. US-PAY-008 – Hủy thanh toán tự động sau học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-PAY-008 |
| User Story Name | Hủy thanh toán tự động sau học thử |
| Epic | Purchase & Payment |
| Priority | P0 |
| User Role | học viên đang học thử có lịch thanh toán tự động |

#### B. User Story Statement

**As a** học viên đang học thử có lịch thanh toán tự động  
**I want to** hủy khoản mua tự động trước khi trial hết hạn  
**So that** tôi tránh khoản thu đã lên lịch và vẫn sử dụng phần trial còn lại.

#### C. Business Context

Hủy lịch thu tiền, không hủy trial. Phải phân biệt xác nhận hủy thành công với yêu cầu hủy đang xử lý.

#### D. Preconditions

Đã đăng nhập, TRIAL_ACTIVE, chưa sở hữu, lịch SCHEDULED, thời gian máy chủ trước expiry.

#### E. Acceptance Criteria

**AC1: Hủy ngày 2 — Happy Path**

- **Given** trial bắt đầu ngày 1 và còn hiệu lực ngày 2, lịch chưa được thực thi.
- **When** học viên xác nhận Hủy thanh toán tự động sau học thử và hệ thống ghi nhận thành công.
- **Then** lịch thành CANCELED, hiển thị MSG-008; giữ TRIAL_ACTIVE / TRIAL_LIMITED và expiry ban đầu ngày 7; không tự thu khi đến hạn.

**AC2: Hủy lại — Edge Case**

- **Given** lịch đã CANCELED.
- **When** gửi yêu cầu hủy lặp lại.
- **Then** trả cùng trạng thái/MSG-008, không đổi hạn trial, không tạo lịch mới hoặc phát sinh giao dịch.

**AC3: Hủy rồi mua — Alternative Flow**

- **Given** lịch CANCELED và trial còn hạn.
- **When** học viên chọn mua khóa học.
- **Then** cho luồng US-PAY-010; hủy trước đó không ngăn mua chủ động.

**AC4: Yêu cầu hủy thắng cạnh tranh — Edge Case**

- **Given** yêu cầu hủy được hệ thống chấp nhận trước expiry và trước khi giao dịch được gửi.
- **When** tác vụ tự động kiểm tra lịch đồng thời.
- **Then** chỉ kết quả hủy có hiệu lực, không gửi giao dịch; không trả xác nhận hủy thành công rồi vẫn tự thu.

**AC5: Đã tới hạn/giao dịch đang xử lý — Negative Path**

- **Given** thời gian máy chủ đã tới expiry hoặc khoản thu đã được gửi trước khi hủy được chấp nhận.
- **When** học viên yêu cầu hủy.
- **Then** không báo đã hủy thành công hoặc đổi sai CANCELED; trả trạng thái hiện tại với MSG-013; cách xử lý yêu cầu đến muộn theo OQ-003, không tự hứa hoàn tiền.

**AC6: Lỗi ghi nhận hủy — Negative Path**

- **Given** lịch còn SCHEDULED.
- **When** hệ thống chưa thể xác nhận vô hiệu hóa lịch thu.
- **Then** hiển thị MSG-018; không hiển thị MSG-008 hoặc giả định không thu, giữ trạng thái đã xác minh và cho kiểm tra lại.

#### F. UI Component Specification

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Hủy thanh toán tự động sau học thử | Button | No | N/A | Theo SCHEDULED/còn hạn | Mở xác nhận; không đặt tên Hủy gia hạn. |
| 2 | Xác nhận hủy | Dialog | No | N/A | Chưa xác nhận | Nêu sẽ không tự mua; trial vẫn dùng tới hạn ban đầu. |
| 3 | Kết quả hủy | Status / Message | No | N/A | Theo kết quả backend | MSG-008 chỉ sau hủy thành công; MSG-013/MSG-018 cho trường hợp chưa thể hủy. |
| 4 | Mua khóa học | Button | No | N/A | Theo quyền | Vẫn mua chủ động được sau hủy; kiểm tra thanh toán đang xử lý. |

#### G. Related Business Rules

BR-002, BR-004, BR-007, BR-011, BR-014

#### H. Dependencies

US-TRIAL-007; US-PAY-009; US-PAY-010; gateway/lịch thanh toán.

### 8.8. US-PAY-009 – Tự động mua khóa học khi kết thúc thời hạn học thử

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-PAY-009 |
| User Story Name | Tự động mua khóa học khi kết thúc thời hạn học thử |
| Epic | Purchase & Payment |
| Priority | P0 |
| User Role | học viên đã ủy quyền mua tự động sau trial |

#### B. User Story Statement

**As a** học viên đã ủy quyền mua tự động sau trial  
**I want to** hệ thống thực hiện khoản mua một lần khi trial hết hạn nếu tôi vẫn đủ điều kiện  
**So that** tôi có toàn bộ khóa học sau khi thanh toán được xác nhận thành công.

#### C. Business Context

Tách tác vụ cuối kỳ khỏi US-PAY-004; mỗi lịch chỉ thực hiện một khoản mua, không có gia hạn định kỳ hoặc lịch tự retry MVP.

#### D. Preconditions

Thời gian máy chủ đạt/vượt expiry; trial đã được kích hoạt; tác vụ chỉ được thu nếu chưa sở hữu, chưa hủy và phương thức/ủy quyền còn hợp lệ.

#### E. Acceptance Criteria

**AC1: Thanh toán tự động thành công — Happy Path**

- **Given** đã tới hạn, chưa sở hữu, lịch SCHEDULED, phương thức và ủy quyền hợp lệ.
- **When** khoản mua một lần được thực thi và gateway xác nhận thành công.
- **Then** ghi kết quả giao dịch, đặt automatic_payment_status = COMPLETED; cấp quyền qua US-ACCESS-011, trial CONVERTED và hiển thị/gửi MSG-010 khi thông báo cho học viên.

**AC2: Lịch đã hủy — Alternative Flow**

- **Given** lịch CANCELED.
- **When** tác vụ tới hạn chạy.
- **Then** không gửi giao dịch; giữ CANCELED và thu hồi trial nếu chưa mua theo US-EXP-006.

**AC3: Đã mua trước hạn — Alternative Flow**

- **Given** đã PAID_ACTIVE.
- **When** tác vụ tới hạn hoặc tác vụ lặp chạy.
- **Then** không thu thêm; giữ quyền đã mua và kết quả lịch đã vô hiệu hóa/hoàn tất thực tế.

**AC4: Gateway thất bại dứt khoát — Negative Path**

- **Given** khoản tự mua đủ điều kiện đã được gửi.
- **When** gateway xác nhận thất bại.
- **Then** ghi FAILED, không cấp paid access; trial hết hiệu lực tại expiry, thông báo MSG-011 và đường mua chủ động; không tự chạy lịch retry nhiều lần hoặc cho grace period.

**AC5: Phương thức không còn đủ điều kiện — Negative Path**

- **Given** đã tới hạn nhưng ủy quyền/phương thức không còn hợp lệ.
- **When** tác vụ kiểm tra trước thu.
- **Then** không gửi khoản thu không được phép; ghi FAILED cùng lý do không thể thực hiện, thông báo MSG-011; không cấp paid access.

**AC6: Lặp tác vụ/callback — Edge Case**

- **Given** đã có giao dịch của cùng lịch hoặc kết quả đã xử lý.
- **When** scheduler chạy lại hoặc callback hợp lệ trùng lặp tới.
- **Then** không gửi khoản thu thứ hai, không tạo ownership/biên lai trùng; đối chiếu cùng giao dịch và giữ kết quả đã xác minh.

**AC7: Cạnh tranh mua sớm — Edge Case**

- **Given** mua chủ động và tác vụ cuối kỳ cùng muốn thanh toán một học viên/khóa.
- **When** hai yêu cầu được xử lý đồng thời.
- **Then** chỉ cho một giao dịch mua được thực thi; yêu cầu còn lại nhận trạng thái hiện có/MSG-012 hoặc MSG-004 sau thành công, không tạo khoản thu độc lập.

**AC8: Callback chậm/timeout — Edge Case**

- **Given** giao dịch đã gửi nhưng chưa có kết quả xác thực khi trial hết hạn.
- **When** gateway trả chậm hoặc kết nối mất.
- **Then** ghi nhận kết quả giao dịch chưa xác định riêng, không gán FAILED/COMPLETED chỉ vì timeout; trial TRIAL_EXPIRED / NOT_OWNED và MSG-012; không gửi mua mới khi chưa làm rõ, theo OQ-002.

**AC9: Callback không hợp lệ — Negative Path**

- **Given** có thông báo thành công không khớp giao dịch/khóa/giá/tiền tệ hoặc không xác thực được nguồn.
- **When** xử lý thông báo.
- **Then** không đánh dấu hoàn tất, không cấp quyền; ghi nhận để đối soát, tiếp tục dựa trên kết quả đã xác minh.

#### F. UI Component Specification

N/A — tác vụ tự động, không tạo màn hình riêng. Kết quả dùng trang trạng thái US-TRIAL-007, trang khóa học và thông báo MSG-010/MSG-011/MSG-012.

#### G. Related Business Rules

BR-004, BR-005, BR-006, BR-008, BR-009, BR-010, BR-011, BR-013

#### H. Dependencies

US-PAY-004; US-PAY-008; US-PAY-010; US-EXP-006; US-ACCESS-011; gateway.

### 8.9. US-PAY-010 – Thanh toán mở khóa khóa học trước thời hạn

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-PAY-010 |
| User Story Name | Thanh toán mở khóa khóa học trước thời hạn |
| Epic | Purchase & Payment |
| Priority | P0 |
| User Role | học viên đang có trial còn hiệu lực và chưa sở hữu khóa học |

#### B. User Story Statement

**As a** học viên đang có trial còn hiệu lực và chưa sở hữu khóa học  
**I want to** chủ động thanh toán mua khóa học ngay  
**So that** tôi học toàn bộ nội dung mà không phải đợi hết trial.

#### C. Business Context

Mua một lần kể cả đã hủy lịch; khi thanh toán thất bại, chỉ giữ trial trong phần thời gian còn lại ban đầu.

#### D. Preconditions

Đã đăng nhập, chưa sở hữu, trial còn hạn tại lúc bắt đầu; không có giao dịch mua khác chưa rõ kết quả.

#### E. Acceptance Criteria

**AC1: Mua sớm thành công — Happy Path**

- **Given** trial còn hạn, chưa sở hữu và chưa có khoản mua đang xử lý.
- **When** học viên xác nhận giá mua một lần, gateway xác nhận thanh toán thành công.
- **Then** ghi giao dịch, cấp PAID_ACTIVE qua US-ACCESS-011, đổi trial CONVERTED, vô hiệu hóa lịch SCHEDULED thành CANCELED với lý do đã mua sớm; hiển thị MSG-009, không thu tự động cuối kỳ.

**AC2: Mua sau khi hủy — Alternative Flow**

- **Given** trial còn hạn, lịch CANCELED.
- **When** học viên mua chủ động thành công.
- **Then** cấp quyền như AC1, giữ lịch CANCELED, không khôi phục thu tự động.

**AC3: Thanh toán thất bại — Negative Path**

- **Given** trial còn hạn và chưa mua.
- **When** gateway xác nhận mua chủ động thất bại.
- **Then** hiển thị MSG-019; không cấp paid access, giữ trial tới expiry ban đầu; không hủy lịch tự động đang hợp lệ hoặc phục hồi lịch đã hủy.

**AC4: Bấm lặp/cạnh tranh — Edge Case**

- **Given** mua đang xử lý hoặc tự mua cuối kỳ đã chiếm quyền thực thi cùng khoản mua.
- **When** học viên bấm trả tiền lại hoặc luồng khác chạy đồng thời.
- **Then** không tạo khoản thu thứ hai; hiển thị MSG-012 để đối soát giao dịch hiện có, hoặc MSG-004 nếu đã sở hữu.

**AC5: Qua hạn khi chờ kết quả — Boundary**

- **Given** mua bắt đầu trước expiry nhưng gateway chưa xác nhận.
- **When** thời gian máy chủ đạt expiry.
- **Then** thu hồi quyền trial nếu chưa paid; không tự thu một giao dịch cạnh tranh khác, hiển thị MSG-012; xác nhận thành công về sau chỉ cấp quyền qua US-ACCESS-011, không khôi phục trial.

**AC6: Chưa xác nhận giá/đã sở hữu — Negative Path**

- **Given** chưa đồng ý khoản mua hoặc đã PAID_ACTIVE.
- **When** gửi yêu cầu mua.
- **Then** không thực hiện khoản thu chưa được xác nhận; người đã sở hữu nhận MSG-004 và Vào học.

#### F. UI Component Specification

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Giá mua khóa học | Summary | No | Yes | Giá khóa học hiện hành | Hiển thị số tiền, tiền tệ và mua một lần; thay đổi giá phải xác nhận lại, không tự suy ra bằng giá lịch tự động. |
| 2 | Xác nhận thanh toán | Button | No | N/A | Chưa gửi | Chỉ gửi sau đồng ý giá; khi đang xử lý không tạo giao dịch mới. |
| 3 | Phương thức thanh toán | Gateway component | Yes | Yes | Theo lựa chọn hợp lệ | Thu nhận an toàn qua gateway; không yêu cầu lưu dữ liệu thẻ nhạy cảm ở ANSERA. |
| 4 | Kết quả mua | Status / Message | No | N/A | Theo gateway | MSG-009/MSG-019/MSG-012/MSG-004; mua thất bại vẫn thể hiện trial còn lại nếu còn hạn. |

#### G. Related Business Rules

BR-004, BR-005, BR-008, BR-010, BR-011, BR-013, BR-014

#### H. Dependencies

US-PLAY-005; US-TRIAL-007; US-PAY-008; US-PAY-009; US-ACCESS-011; checkout một lần hiện hữu.

### 8.10. US-EXP-006 – Tự động hết hạn học thử và thu hồi quyền truy cập

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-EXP-006 |
| User Story Name | Tự động hết hạn học thử và thu hồi quyền truy cập |
| Epic | Access Management |
| Priority | P0 |
| User Role | quản trị viên vận hành nền tảng ANSERA |

#### B. User Story Statement

**As a** quản trị viên vận hành nền tảng ANSERA  
**I want to** hệ thống thu hồi toàn bộ quyền trial đúng hạn nếu học viên chưa mua thành công  
**So that** tôi bảo vệ nội dung khóa học và thực thi đúng thời hạn đã công bố.

#### C. Business Context

Thu hồi tại đủ 168 giờ độc lập với độ trễ scheduler/gateway; hủy lịch không làm hết trial sớm.

#### D. Preconditions

Trial đã kích hoạt; hệ thống có start/expiry và quyền sở hữu đã xác minh.

#### E. Acceptance Criteria

**AC1: Hết hạn chính xác — Happy Path**

- **Given** trial còn hoạt động và chưa PAID_ACTIVE.
- **When** thời gian máy chủ đạt trial_expires_at.
- **Then** trial thành TRIAL_EXPIRED và course_access = NOT_OWNED; chặn toàn bộ nội dung trial kể cả 50% đầu của Bài 1–3, không đợi retry hoặc kết quả tự mua.

**AC2: Đã hủy thanh toán — Alternative Flow**

- **Given** lịch CANCELED từ ngày 2.
- **When** trước hạn rồi tới đúng expiry ban đầu.
- **Then** giữ quyền trial trước hạn; tại hạn thu hồi toàn bộ nếu chưa mua, không gửi khoản tự thu.

**AC3: Thanh toán lỗi hoặc đang xử lý — Negative Path**

- **Given** đã tới expiry và chưa có thành công xác minh.
- **When** gateway trả thất bại hoặc còn chờ.
- **Then** không cấp paid/grace access; hiển thị MSG-011 hoặc MSG-012 đúng kết quả, không kéo dài trial.

**AC4: Truy cập lại — Negative Path**

- **Given** trial đã hết hạn, chưa sở hữu.
- **When** mở bất cứ bài/tài nguyên được bảo vệ, tải lại, đăng nhập lại hoặc dùng URL media cũ.
- **Then** backend/media từ chối truy cập; giao diện hiển thị MSG-006 và đường thanh toán chủ động; không mở trial lần hai.

**AC5: Đã sở hữu — Edge Case**

- **Given** đã PAID_ACTIVE.
- **When** tác vụ hết hạn cũ chạy.
- **Then** không hạ quyền đã mua hoặc đổi CONVERTED về TRIAL_EXPIRED; giữ quyền đầy đủ.

**AC6: Tác vụ chậm/đồng hồ máy sai — Boundary**

- **Given** scheduler chưa cập nhật hàng dữ liệu hoặc máy học viên chỉnh giờ.
- **When** yêu cầu nội dung tại/sau expiry.
- **Then** backend dùng thời gian máy chủ và ownership để từ chối ngay nếu chưa mua; không dựa vào banner hoặc thời gian máy học viên để giữ quyền.

#### F. UI Component Specification

![US-EXP-006_ Chi tiết khóa học khi Hết hạn học thử 7 ngày (MSG-006 & Khóa toàn bộ 🔒)](./H%E1%BB%8Dc%20th%E1%BB%AD%20screen./US-EXP-006_%20Chi%20ti%E1%BA%BFt%20kh%C3%B3a%20h%E1%BB%8Dc%20khi%20H%E1%BA%BFt%20h%E1%BA%A1n%20h%E1%BB%8Dc%20th%E1%BB%AD%207%20ng%C3%A0y%20(MSG-006%20&%20Kh%C3%B3a%20to%C3%A0n%20b%E1%BB%99%20%F0%9F%94%92).png)

**UI Update Required:** Giữ ảnh hết hạn; giá 399.000đ là minh họa. Phân biệt hết hạn với thanh toán thất bại/đang xử lý; không dùng CTA mua mới để tạo thu trùng khi giao dịch trước chưa rõ kết quả.

| STT | Tên thành phần | Type | Được chỉnh sửa | Bắt buộc | Giá trị mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Banner hết hạn | Banner | No | N/A | Theo backend | MSG-006; kết quả thanh toán thể hiện riêng, không gọi hết trial là hủy trial. |
| 2 | Khóa toàn bộ bài/tài liệu bảo vệ | Icon | No | N/A | Khóa nếu chưa mua | Bao gồm Bài 1–3, ngăn URL trực tiếp. |
| 3 | Thanh toán để tiếp tục học | Button | No | N/A | Giá khóa học | Dẫn checkout một lần hiện hữu; nếu giao dịch chưa rõ kết quả, kiểm tra giao dịch trước khi mở khoản thu mới. |
| 4 | Đã sử dụng quyền học thử | Button / Note | No | N/A | Không cho kích hoạt lại | MSG-014; lịch sử đã dùng không bị xóa khi đăng nhập lại. |

#### G. Related Business Rules

BR-001, BR-002, BR-003, BR-004, BR-007, BR-009, BR-010, BR-012

#### H. Dependencies

US-PAY-004; US-PAY-008; US-PAY-009; US-PAY-010; US-ACCESS-011; backend/media delivery.

### 8.11. US-ACCESS-011 – Cấp quyền truy cập đầy đủ sau khi mua khóa học thành công

#### A. General Information

| Thuộc tính | Giá trị |
| --- | --- |
| User Story ID | US-ACCESS-011 |
| User Story Name | Cấp quyền truy cập đầy đủ sau khi mua khóa học thành công |
| Epic | Access Management |
| Priority | P0 |
| User Role | học viên đã thanh toán mua khóa học thành công |

#### B. User Story Statement

**As a** học viên đã thanh toán mua khóa học thành công  
**I want to** được truy cập toàn bộ nội dung khóa học đã mua trên các phiên đăng nhập  
**So that** tôi tiếp tục học đầy đủ và giữ tiến trình đã có.

#### C. Business Context

Dùng chung cho mua sớm, mua tự động và checkout một lần hiện hữu; ownership không đồng nhất với trạng thái trial hoặc lịch thu tiền.

#### D. Preconditions

Gateway xác nhận thanh toán thành công cho đúng học viên, khóa học, số tiền và tiền tệ; kiểm tra nguồn xác nhận.

#### E. Acceptance Criteria

**AC1: Cấp quyền đầy đủ — Happy Path**

- **Given** thành công thanh toán đã được xác thực.
- **When** xử lý kết quả mua đúng học viên/khóa.
- **Then** ghi ownership bền vững và PAID_ACTIVE; cho toàn bộ video, bài học và tài liệu bảo vệ của khóa đã mua, gỡ giới hạn 50%, giữ tiến trình hiện có nếu áp dụng; trial đã dùng chuyển CONVERTED.

**AC2: Đăng nhập lại — Alternative Flow**

- **Given** ownership đã được ghi.
- **When** học viên đăng xuất rồi đăng nhập hoặc mở phiên khác.
- **Then** backend trả quyền đã mua; không áp trial limit, không mời trial hoặc thu tiền mua lại.

**AC3: Không có xác nhận thành công — Negative Path**

- **Given** chỉ có redirect trình duyệt, yêu cầu gửi đi hoặc giao dịch chưa xác minh.
- **When** client yêu cầu mở toàn bộ khóa.
- **Then** không cấp PAID_ACTIVE; backend tiếp tục quyền trial còn hạn hoặc không cho truy cập nếu hết hạn.

**AC4: Callback trùng/sai thứ tự — Edge Case**

- **Given** đã có thành công xác minh và ownership.
- **When** nhận lại callback cùng giao dịch hoặc thông báo chậm chưa đối soát.
- **Then** không tạo ownership/thu tiền trùng, không hạ quyền đã mua dựa trên callback cũ; đối chiếu kết quả với gateway.

**AC5: Không cấp được quyền sau thu tiền — Exception**

- **Given** giao dịch thành công đã được ghi nhưng bước cập nhật quyền chưa hoàn tất.
- **When** đọc trạng thái hoặc xử lý lại kết quả.
- **Then** hiển thị MSG-020, giữ dấu vết giao dịch để hoàn tất cấp quyền có thể xử lý lại mà không thu thêm; không báo thanh toán thất bại hoặc yêu cầu trả tiền lần nữa.

**AC6: Tài nguyên khác khóa — Negative Path**

- **Given** học viên chỉ sở hữu khóa A.
- **When** yêu cầu tài liệu bảo vệ của khóa B chưa được cấp quyền.
- **Then** backend từ chối; ownership A không mở rộng sang B.

#### F. UI Component Specification

N/A — cấp quyền do hệ thống xử lý, không tạo màn hình riêng. Trang khóa học/player hiện hữu nhận quyền đầy đủ, CTA Vào học; kết quả cấp quyền chậm dùng MSG-020.

#### G. Related Business Rules

BR-005, BR-008, BR-010, BR-011, BR-012, BR-013

#### H. Dependencies

US-PAY-009; US-PAY-010; checkout một lần hiện hữu; US-PLAY-005; backend/media delivery.

## 9. User Story / Business Rule Traceability Matrix

AC được định danh đầy đủ bằng `User Story ID.ACn`. Bảng ánh xạ hỗ trợ kiểm tra tác động và dẫn xuất test case; không phải chứng nhận UAT. Quy tắc nghiệp vụ được dẫn tại G của từng story.

| Business Rule | User Stories tham chiếu |
| --- | --- |
| BR-001 | US-CRS-002, US-ENR-003, US-PAY-004, US-EXP-006 |
| BR-002 | US-ENR-003, US-PAY-004, US-PLAY-005, US-TRIAL-007, US-PAY-008, US-EXP-006 |
| BR-003 | US-CRS-002, US-ENR-003, US-PLAY-005, US-EXP-006 |
| BR-004 | US-PLAY-005, US-TRIAL-007, US-PAY-008, US-PAY-009, US-PAY-010, US-EXP-006 |
| BR-005 | US-CRS-002, US-PAY-004, US-PAY-009, US-PAY-010, US-ACCESS-011 |
| BR-006 | US-ENR-003, US-PAY-004, US-TRIAL-007, US-PAY-009 |
| BR-007 | US-ENR-003, US-PLAY-005, US-TRIAL-007, US-PAY-008, US-EXP-006 |
| BR-008 | US-TRIAL-007, US-PAY-009, US-PAY-010, US-ACCESS-011 |
| BR-009 | US-TRIAL-007, US-PAY-009, US-EXP-006 |
| BR-010 | US-CRS-002, US-PLAY-005, US-TRIAL-007, US-PAY-009, US-PAY-010, US-EXP-006, US-ACCESS-011 |
| BR-011 | US-PAY-008, US-PAY-009, US-PAY-010, US-ACCESS-011 |
| BR-012 | US-PAY-004, US-PLAY-005, US-EXP-006, US-ACCESS-011 |
| BR-013 | US-ENR-003, US-PAY-004, US-PAY-009, US-PAY-010, US-ACCESS-011 |
| BR-014 | US-CRS-002, US-PAY-008, US-PAY-010 |

| Quyết định | Story / AC trọng tâm |
| --- | --- |
| BD-001 | US-ENR-003.AC1; US-PAY-009.AC1, AC4; US-PAY-010.AC1; US-ACCESS-011.AC2 |
| BD-002 | US-PAY-004.AC1; US-PLAY-005.AC1–AC4; US-EXP-006.AC1, AC6 |
| BD-003 | US-ENR-003.AC1–AC4; US-PAY-004.AC1–AC4, AC6, AC7 |
| BD-004 | US-PAY-008.AC1–AC6; US-TRIAL-007.AC2; US-EXP-006.AC2 |
| BD-005 | US-PAY-010.AC1–AC5; US-ACCESS-011.AC1, AC4, AC5 |
| BD-006 | US-PAY-009.AC1–AC9; US-EXP-006.AC3; US-ACCESS-011.AC3 |
| BD-007 | US-EXP-006.AC1, AC4, AC6; US-PLAY-005.AC5 |
| BD-008 | US-CRS-002.AC3–AC5; US-ENR-003.AC5; US-PAY-004.AC5, AC7 |

**INVEST review:** 11 story giữ baseline đã chỉ định. Mỗi story có mục tiêu/giá trị và AC quan sát được; dependencies được nêu thay vì khẳng định độc lập tuyệt đối. US-PAY-009 có nhiều nhánh cạnh tranh/đối soát, cần đội Dev ước lượng trước khi nhận sprint; chưa khẳng định Small/Estimable đạt khi OQ-001–OQ-003 chưa chốt. Không tự tách hoặc thêm story. Ngưỡng video nhiều video/bài chờ OQ-005.

## 10. UI Change Log

Tất cả 11 tham chiếu ảnh từ v2.1 được giữ nguyên URL/alt text. Đã xem nội dung 11 ảnh; không sửa, xóa hoặc ghi đè asset. Ảnh là minh họa hiện trạng, phần đặc tả/BD mới có ưu tiên khi có mâu thuẫn. Không tạo đường dẫn ảnh mới cho 5 story bổ sung.

| Nhóm màn hình | Số ảnh | Đánh giá / cập nhật cần làm |
| --- | --- | --- |
| US-AUTH-001 | 3 | Giữ homepage/form/lỗi; sửa lỗi bảng v2.1 gắn MSG-002 tại password sang username. Copy bảo mật/OAuth trong ảnh không được suy rộng thành thiết kế mới. |
| US-CRS-002 | 1 | Giữ cấu trúc chi tiết, huy hiệu và CTA; bổ sung các trạng thái trial/đã mua. Giá minh họa không cố định. |
| US-ENR-003 | 1 | **UI Update Required:** bỏ $20 USD mỗi tháng và quyền mọi khóa/chứng chỉ, thay bằng khóa đang chọn, giá một lần, lịch thu và consent chủ động; mô tả hủy lịch mà vẫn học tới hạn. |
| US-PAY-004 | 3 | **UI Update Required:** thể hiện mua một lần/consent cuối, ngày giờ có múi giờ, thống nhất giá với khóa; form/validation theo gateway; không mặc định 0đ, CVV 3 số hoặc một tập thẻ áp dụng cho mọi phương thức. |
| US-PLAY-005 | 2 | **UI Update Required:** cập nhật banner theo lịch/cancellation, bỏ nội dung chưa chốt về giảm giá, hoàn tiền 7 ngày, chứng chỉ, trọn đời/cập nhật miễn phí; giữ Seek Guard/Paywall/replay. |
| US-EXP-006 | 1 | **UI Update Required:** phân biệt hết hạn, thất bại và đang xử lý; CTA tránh tạo thu mới khi giao dịch chưa rõ. Giá theo khóa. |
| US-TRIAL-007, US-PAY-008, US-PAY-010 | 0 | Chưa có screenshot trong repo; đặc tả component tại F để thiết kế sau, không tuyên bố đã tạo UI. |
| US-PAY-009, US-ACCESS-011 | 0 | System-triggered, F = N/A; dùng thông báo/trang trạng thái hiện hữu. |

## 11. Open Questions & Assumptions

Không biến câu hỏi sau thành điều kiện hoặc cam kết kinh doanh đã được phê duyệt. BD-001–BD-008 vẫn áp dụng trong khi chưa có quyết định bổ sung.

| ID | Cần xác nhận | Tác động / ranh giới hiện dùng |
| --- | --- | --- |
| OQ-001 | Gateway/phương thức nào hỗ trợ lưu tham chiếu và khoản mua một lần ngoài phiên sau 168 giờ? Luồng xác thực/ủy quyền nào, có giữ khoản tạm thời hay cần xác thực bổ sung? | US-PAY-004/009 chưa thể chốt tích hợp/validation. Không mặc định 0đ hoặc hỗ trợ mọi thẻ; phải công bố điều kiện thực tế trước consent. |
| OQ-002 | Đối soát giao dịch pending quá lâu thế nào: thời hạn, cách kiểm tra kết quả, thông báo và thời điểm cho phép mua thủ công sau khi chứng minh khoản cũ không thể thu? | US-PAY-009.AC8, US-PAY-010.AC5; không thêm retry/grace. Trong khi chưa rõ: hết hạn khóa trial, không cấp paid, không tạo khoản thu độc lập khác; callback thành công xác minh cùng giao dịch vẫn cấp quyền. |
| OQ-003 | Xử lý yêu cầu hủy đến muộn/đồng thời khi khoản thu đã được gateway nhận: có void/refund không, ai giải quyết, thông báo thế nào? | Không báo hủy thành công nếu chưa ngăn thu; không cam kết hoàn tiền. Yêu cầu được chấp nhận trước hạn/phát lệnh phải ngăn thu theo BR-007. |
| OQ-004 | Giá/thuế/tiền tệ nào áp dụng, khóa giá tự mua đã consent trong 168 giờ thế nào khi bảng giá thay đổi? | Không tự coi 399.000đ, 1.200.000đ hoặc $20/tháng trong ảnh là giá chuẩn. Không thu số tiền/lịch khác consent; đổi trước kích hoạt cần đồng ý lại. Giá mua chủ động phải được xác nhận riêng. |
| OQ-005 | Khóa ít hơn 3 bài, bài nhiều video, thay đổi thứ tự/nội dung/thời lượng trong trial được tính phạm vi và mốc 50% thế nào? | Baseline cho 3 bài đầu và video từng bài; không suy diễn quota gộp, làm tròn hoặc áp dụng cho khóa cấu trúc khác trước khi xác nhận. |
| OQ-006 | Thời hạn sở hữu sau mua, nội dung chứng chỉ, hỗ trợ giảng viên, cập nhật miễn phí và chính sách hoàn tiền có được chốt không? | Không kế thừa “trọn đời”, ưu đãi hoặc hoàn tiền từ ảnh. Cam kết hiện tại chỉ là full access khóa đã mua, bền vững qua phiên. |

**Giả định kỹ thuật để kiểm chứng:** có thể xác minh kết quả gateway và lưu lịch/transaction/ownership nhất quán; đây là điều kiện cần kiểm chứng khi chọn tích hợp, chưa phải bằng chứng runtime. Backend dùng thời gian máy chủ; hiển thị timestamp có múi giờ, chưa áp đặt một múi giờ kinh doanh hoặc ngưỡng hiệu năng cụ thể.

**Kiểm tra tài liệu v3.0:** 11 story / 5 Epic; mỗi story đủ A–H và AC Given–When–Then; 14 BR có truy vết; MSG-001–MSG-020 có trigger và tham chiếu nhất quán; ba chiều trạng thái tách biệt, bao phủ hủy ngày 2, mua sớm, hết hạn, thất bại, callback lặp/chậm và cạnh tranh. Giữ 11 link ảnh; không thay asset. Đây là review cấu trúc/ngữ nghĩa của đặc tả, chưa phải test ứng dụng/gateway hoặc nghiệm thu stakeholder; các OQ cần review trước thiết kế tích hợp và triển khai nhánh tương ứng.
