
# B1. Đọc và phân tích – Business Context & Business Problem

## 1. Business Context – Bối cảnh nghiệp vụ

**Công ty ABC** cung cấp dịch vụ **đặt xe trực tuyến**.

Hiện tại khách hàng có thể đặt xe bằng:
- Gọi **tổng đài**
- Sử dụng **ứng dụng đơn giản**

Tuy nhiên, hệ thống hiện tại còn nhiều hạn chế và không phù hợp khi doanh nghiệp muốn mở rộng quy mô.

---

## 2. Business Problem – Vấn đề kinh doanh

### Hệ thống hiện tại đang gặp vấn đề gì?

| Vấn đề hiện tại | Ảnh hưởng |
|---|---|
| Phân công tài xế chủ yếu thủ công | Mất thời gian, tốn nhân lực |
| Khó tìm tài xế phù hợp | Khách hàng có thể phải chờ lâu |
| Tài xế từ chối nhưng chưa có cơ chế tự động tìm người khác | Khách có thể phải đặt lại |
| Khách hàng khó theo dõi trạng thái chuyến | Trải nghiệm khách hàng kém |
| Thông tin thanh toán chưa tập trung | Khó quản lý và tra cứu |
| Thông báo chưa linh hoạt | Khó cập nhật trạng thái kịp thời |
| Nhân viên vận hành khó quản lý | Khó theo dõi chuyến, tài xế và sự cố |
| Hệ thống khó mở rộng | Không phù hợp khi số lượng user/chuyến tăng |
| Các thành phần phụ thuộc lẫn nhau | Một lỗi có thể ảnh hưởng toàn hệ thống |
| Khó tích hợp dịch vụ mới | Khó phát triển trong tương lai |

### Vấn đề cốt lõi

> Hệ thống cũ phù hợp với việc **đặt xe cơ bản**, nhưng không đáp ứng được yêu cầu về **tự động hóa, quản lý, khả năng mở rộng và phát triển lâu dài** của doanh nghiệp.

---

## 3. KH muốn giải quyết vấn đề gì?

Khách hàng muốn xây dựng một **CAB System mới** nhằm:

1. **Tự động hóa quy trình đặt và phân công xe**
2. **Giúp khách hàng theo dõi chuyến đi rõ ràng**
3. **Quản lý thanh toán tập trung**
4. **Hỗ trợ nhân viên vận hành quản lý toàn bộ hoạt động**
5. **Phục vụ số lượng lớn khách hàng và tài xế**
6. **Đảm bảo hệ thống ổn định và bảo mật**
7. **Có khả năng mở rộng và phát triển thêm tính năng trong tương lai**

---

## 4. Tại sao hệ thống hiện tại không đáp ứng?

Hệ thống cũ chủ yếu đáp ứng nhu cầu **đặt xe cơ bản**, nhưng chưa đáp ứng được yêu cầu về **tự động hóa, quản lý và mở rộng**.

### Các hạn chế chính:

- Phân công tài xế còn **thủ công**
- Chưa hỗ trợ tốt việc **tìm tài xế gần và phù hợp**
- Chưa có cơ chế **tự động tìm tài xế khác khi tài xế từ chối**
- Khách hàng **khó theo dõi chuyến**
- Thanh toán **chưa được quản lý tập trung**
- Nhân viên vận hành **khó kiểm soát hoạt động**
- Hệ thống **khó mở rộng khi tải tăng**
- Khó thêm **dịch vụ, phương thức thanh toán và kênh thông báo**
- Một lỗi ở một chức năng có thể **ảnh hưởng đến toàn bộ hệ thống**

---

# 5. Mục tiêu kinh doanh – Business Goals

## 5.1. Tự động hóa

Tự động hóa toàn bộ quy trình:

> Đặt xe → Tìm tài xế → Phân công → Thực hiện chuyến → Tính cước → Thanh toán → Đánh giá

## 5.2. Nâng cao trải nghiệm khách hàng

Khách hàng có thể:

- Biết yêu cầu đã được tiếp nhận
- Biết hệ thống đang tìm tài xế
- Biết tài xế nào nhận chuyến
- Theo dõi trạng thái chuyến
- Biết thời gian dự kiến tài xế đến
- Xem cước phí
- Thanh toán
- Xem lịch sử chuyến
- Đánh giá tài xế

## 5.3. Tăng hiệu quả vận hành

Nhân viên vận hành có thể:

- Quản lý khách hàng
- Quản lý tài xế
- Quản lý phương tiện
- Theo dõi chuyến
- Xử lý chuyến lỗi
- Tra cứu giao dịch
- Xem báo cáo

## 5.4. Tăng khả năng mở rộng

Hệ thống có thể mở rộng:

- Số lượng khách hàng
- Số lượng tài xế
- Số lượng chuyến
- Loại dịch vụ
- Phương thức thanh toán
- Kênh thông báo
- Nhà cung cấp bên thứ ba

## 5.5. Đảm bảo an toàn và ổn định

- Xác thực người dùng
- Phân quyền nhân viên
- Bảo vệ dữ liệu cá nhân
- Bảo vệ dữ liệu vị trí
- Bảo vệ dữ liệu giao dịch
- Lưu vết các thao tác quan trọng
- Một chức năng bị lỗi không làm toàn bộ hệ thống ngừng hoạt động

---

# 6. Ai sử dụng hệ thống?

| Actor | Vai trò / Nhu cầu |
|---|---|
| **Khách hàng (KH)** | Đăng ký, đăng nhập, đặt xe, theo dõi chuyến, thanh toán, đánh giá |
| **Tài xế (TX)** | Quản lý hồ sơ, nhận/từ chối chuyến, cập nhật trạng thái và vị trí |
| **Nhân viên vận hành (NHVH)** | Quản lý KH, TX, phương tiện, chuyến đi, giao dịch và sự cố |
| **Nhà cung cấp thanh toán** | Xử lý thanh toán điện tử |
| **Nhà cung cấp thông báo** | Gửi thông báo và có thể mở rộng thêm trong tương lai |

---

# 7. Giá trị hệ thống mới so với hệ thống cũ

| Khía cạnh | Hệ thống cũ | Hệ thống CAB mới |
|---|---|---|
| Đặt xe | Có | Có |
| Tìm tài xế | Chủ yếu thủ công | Tự động |
| Phân công tài xế | Thủ công | Tự động theo tiêu chí |
| Tài xế từ chối | Xử lý hạn chế | Tự động tìm tài xế khác |
| Theo dõi chuyến | Hạn chế | Theo dõi trạng thái rõ ràng |
| Vị trí tài xế | Chưa đáp ứng tốt | Lưu và sử dụng để tìm tài xế |
| Thanh toán | Chưa tập trung | Quản lý tập trung + tích hợp payment |
| Thông báo | Hạn chế | Thông báo theo từng sự kiện |
| Quản trị | Hạn chế | Có hệ thống quản trị |
| Báo cáo | Hạn chế | Có báo cáo vận hành |
| Phân quyền | Chưa đầy đủ | Có kiểm soát quyền |
| Mở rộng | Khó | Có khả năng mở rộng |
| Tích hợp | Khó | Dễ thêm provider/dịch vụ |
| Khả năng chịu tải | Hạn chế | Có khả năng phục vụ lượng lớn |
| Xử lý lỗi | Có thể ảnh hưởng hệ thống | Các thành phần có khả năng hoạt động độc lập |

---

# 8. Giá trị tạo ra cho từng nhóm người dùng

## 8.1. Khách hàng

**Giá trị:**
- Đặt xe thuận tiện hơn
- Biết rõ trạng thái chuyến
- Biết tài xế đã nhận chuyến
- Theo dõi thời gian dự kiến tài xế đến
- Thanh toán dễ dàng
- Xem lịch sử và đánh giá tài xế

### Quy trình

> Đặt xe → Biết đang tìm tài xế → Biết tài xế → Theo dõi chuyến → Thanh toán → Đánh giá

---

## 8.2. Tài xế

**Giá trị:**
- Nhận được thông báo chuyến phù hợp
- Có thể chấp nhận hoặc từ chối chuyến
- Chủ động cập nhật trạng thái
- Hệ thống sử dụng vị trí để hỗ trợ tìm chuyến phù hợp
- Quản lý chuyến thuận tiện hơn

---

## 8.3. Nhân viên vận hành

**Giá trị:**
- Quản lý tập trung
- Theo dõi chuyến đang diễn ra
- Kiểm tra trạng thái tài xế
- Xử lý các chuyến bị lỗi
- Tra cứu giao dịch
- Xem báo cáo
- Giảm thao tác thủ công

---

## 8.4. Doanh nghiệp

**Giá trị:**
- Tăng khả năng phục vụ khách hàng
- Giảm chi phí và công việc thủ công
- Tăng hiệu quả vận hành
- Quản lý dữ liệu tập trung
- Có khả năng mở rộng hệ thống
- Dễ phát triển tính năng mới
- Hỗ trợ doanh nghiệp phát triển lâu dài

---

# 9. Business Goal → Business Value

```text
HỆ THỐNG CŨ
    ↓
Phân công tài xế thủ công
Khó theo dõi chuyến
Thanh toán chưa tập trung
Khó quản lý
Khó mở rộng
    ↓
BUSINESS PROBLEM
    ↓
XÂY DỰNG CAB SYSTEM MỚI
    ↓
Tự động hóa
Theo dõi chuyến
Quản lý thanh toán
Quản lý vận hành
Bảo mật
Khả năng mở rộng
    ↓
BUSINESS VALUE
    ↓
Trải nghiệm khách hàng tốt hơn
Vận hành hiệu quả hơn
Phục vụ được nhiều người dùng hơn
Dễ phát triển tính năng mới
Dễ tích hợp hệ thống bên ngoài
Hỗ trợ doanh nghiệp phát triển lâu dài

```
# B2. Xác định Stakeholder

## 1. Danh sách Stakeholder

| Stakeholder nào | Vai trò |
|---|---|
| **Ban giám đốc / Chủ doanh nghiệp** | Đưa ra mục tiêu kinh doanh, phê duyệt phạm vi và định hướng phát triển hệ thống |
| **Khách hàng (Customer)** | Đăng ký, đặt xe, theo dõi chuyến, thanh toán và đánh giá tài xế |
| **Tài xế (Driver)** | Nhận và thực hiện chuyến, cập nhật trạng thái chuyến và vị trí |
| **Nhân viên vận hành (Operator)** | Quản lý khách hàng, tài xế, phương tiện, chuyến đi; theo dõi và xử lý sự cố |
| **Quản trị viên hệ thống (Admin)** | Quản lý tài khoản, phân quyền và các thao tác quản trị nhạy cảm |
| **Nhà cung cấp thanh toán (Payment Provider)** | Xử lý các giao dịch thanh toán điện tử |
| **Nhà cung cấp dịch vụ thông báo (Notification Provider)** | Gửi thông báo đến khách hàng và tài xế |
| **Business Analyst (BA)** | Thu thập, phân tích và làm rõ yêu cầu; xác định quy trình nghiệp vụ và các vấn đề chưa rõ |
| **Đội phát triển hệ thống (Development Team)** | Thiết kế, xây dựng, tích hợp và triển khai hệ thống |
| **Đội vận hành kỹ thuật / IT** | Giám sát hệ thống, đảm bảo tính ổn định, hiệu năng, bảo mật và khả năng mở rộng |

---

# 2. Mức độ ảnh hưởng của Stakeholder

Đánh giá theo 2 tiêu chí:

- **Mức độ ảnh hưởng (Power/Influence):** Khả năng quyết định hoặc tác động đến dự án.
- **Mức độ quan tâm (Interest):** Mức độ stakeholder quan tâm và sử dụng kết quả của hệ thống.

| Stakeholder | Ảnh hưởng | Quan tâm | Mức độ |
|---|---|---|---|
| **Ban giám đốc** | 🔴 Cao | 🔴 Cao | Rất cao |
| **Nhân viên vận hành** | 🔴 Cao | 🔴 Cao | Rất cao |
| **Admin** | 🔴 Cao | 🔴 Cao | Rất cao |
| **BA** | 🔴 Cao | 🔴 Cao | Rất cao |
| **IT / Technical Operation** | 🔴 Cao | 🔴 Cao | Rất cao |
| **Khách hàng** | 🟡 Trung bình | 🔴 Cao | Cao |
| **Tài xế** | 🟡 Trung bình | 🔴 Cao | Cao |
| **Development Team** | 🟡 Trung bình | 🔴 Cao | Cao |
| **Payment Provider** | 🟡 Trung bình | 🟡 Trung bình | Trung bình |
| **Notification Provider** | 🟢 Thấp | 🟡 Trung bình | Thấp – Trung bình |

---

# 3. Ma trận Stakeholder – Power / Interest

```text
                    MỨC ĐỘ QUAN TÂM (INTEREST)
                THẤP                         CAO
                  │                            │
                  │                            │
       ┌──────────┼────────────────────────────┐
       │          │                            │
       │          │    QUẢN LÝ CHẶT CHẼ       │
       │          │                            │
  CAO  │          │    • Ban giám đốc          │
       │          │    • Nhân viên vận hành    │
       │          │    • Admin                 │
       │          │    • BA                    │
       │          │    • IT / Technical        │
       │          │                            │
MỨC    ├──────────┼────────────────────────────┤
ĐỘ     │          │                            │
ẢNH    │  GIỮ    │    THAM GIA / LẤY FEEDBACK│
HƯỞNG  │  HÀI LÒNG│                            │
       │          │    • Khách hàng            │
  THẤP │          │    • Tài xế                │
       │          │    • Development Team      │
       │          │    • Payment Provider      │
       │          │    • Notification Provider │
       └──────────┴────────────────────────────┘

