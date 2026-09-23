# BOUNDED CONTEXT – CAB SYSTEM

## 1. Danh sách Bounded Context

Hệ thống CAB System được phân chia thành các Bounded Context theo từng nhóm nghiệp vụ độc lập như sau:

| STT  | Bounded Context                          | Trách nhiệm chính                                   | Đối tượng chính                                               |
| ---- | ---------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------- |
| BC01 | **Identity & Access Context**            | Đăng ký, đăng nhập, xác thực và phân quyền          | `UserAccount`, `Role`, `Permission`                           |
| BC02 | **Customer Management Context**          | Quản lý thông tin khách hàng                        | `Customer`, `CustomerProfile`                                 |
| BC03 | **Driver Management Context**            | Quản lý tài xế, phương tiện và trạng thái hoạt động | `Driver`, `Vehicle`, `DriverLocation`                         |
| BC04 | **Trip Management Context**              | Quản lý toàn bộ vòng đời chuyến đi                  | `Trip`, `TripStatus`, `PickupLocation`, `Destination`         |
| BC05 | **Driver Matching & Assignment Context** | Tìm tài xế phù hợp và phân công tài xế              | `MatchingRequest`, `DriverCandidate`, `DriverAssignment`      |
| BC06 | **Fare Management Context**              | Tính cước và quản lý chính sách giá                 | `Fare`, `FarePolicy`                                          |
| BC07 | **Payment Context**                      | Quản lý thanh toán và giao dịch                     | `PaymentTransaction`, `PaymentAttempt`                        |
| BC08 | **Notification Context**                 | Gửi thông báo đến khách hàng và tài xế              | `Notification`, `NotificationTemplate`, `NotificationChannel` |
| BC09 | **Rating & Trip History Context**        | Đánh giá chuyến đi và quản lý lịch sử               | `Rating`, `TripHistory`                                       |
| BC10 | **Operation & Reporting Context**        | Quản lý vận hành, giám sát, quản trị và báo cáo     | `Operation`, `Report`, `AuditLog`                             |

---

# 2. Chi tiết các Bounded Context

## BC01 – Identity & Access Context

### Mục đích

Quản lý tài khoản người dùng, xác thực và phân quyền truy cập hệ thống.

### Các Domain Entity

```text
Identity & Access
│
├── UserAccount
├── Role
└── Permission
```

### Trách nhiệm

* Đăng ký tài khoản.
* Đăng nhập.
* Xác thực người dùng.
* Quản lý vai trò.
* Quản lý quyền truy cập.
* Kiểm soát quyền sử dụng chức năng.

### Quan hệ

```text
UserAccount
      │
      └── N : N ── Role
                       │
                       └── N : N ── Permission
```

---

# BC02 – Customer Management Context

### Mục đích

Quản lý thông tin và hồ sơ của khách hàng sử dụng dịch vụ CAB System.

### Các Domain Entity

```text
Customer Management
│
├── Customer
└── CustomerProfile
```

### Trách nhiệm

* Quản lý thông tin khách hàng.
* Quản lý hồ sơ khách hàng.
* Cập nhật thông tin cá nhân.
* Cung cấp thông tin khách hàng cho các context cần thiết.

### Lưu ý

`Customer Management` không chịu trách nhiệm quản lý vòng đời chuyến đi.

---

# BC03 – Driver Management Context

### Mục đích

Quản lý tài xế, phương tiện và thông tin hoạt động của tài xế.

### Các Domain Entity

```text
Driver Management
│
├── Driver
├── Vehicle
└── DriverLocation
```

### Quan hệ

```text
Driver 1 ─── N Vehicle

Driver 1 ─── N DriverLocation
```

### Trách nhiệm

* Quản lý thông tin tài xế.
* Quản lý phương tiện.
* Quản lý trạng thái hoạt động của tài xế.
* Quản lý vị trí hiện tại của tài xế.
* Cung cấp thông tin tài xế cho quá trình tìm kiếm và phân công.

### Lưu ý

`Driver Management` **không chịu trách nhiệm tìm và lựa chọn tài xế**.

Việc tìm tài xế và phân công tài xế thuộc:

> **Driver Matching & Assignment Context**

---

# BC04 – Trip Management Context

## Mục đích

Quản lý toàn bộ vòng đời của một chuyến đi.

Đây là một trong những **Core Domain** của CAB System.

### Aggregate chính

```text
Trip
│
├── TripId
├── CustomerId
├── DriverId
├── VehicleId
├── PickupLocation
├── Destination
├── VehicleType
└── TripStatus
```

### Vòng đời Trip

```text
REQUESTED
    ↓
SEARCHING_DRIVER
    ↓
DRIVER_ASSIGNED
    ↓
DRIVER_ARRIVING
    ↓
DRIVER_ARRIVED
    ↓
PASSENGER_PICKED_UP
    ↓
IN_PROGRESS
    ↓
COMPLETED
```

Ngoài ra có thể phát sinh các trạng thái ngoại lệ:

```text
NO_DRIVER
CANCELLED
```

### Trách nhiệm

* Tạo chuyến.
* Quản lý thông tin chuyến.
* Quản lý trạng thái chuyến.
* Cập nhật trạng thái theo từng bước của hành trình.
* Hoàn thành chuyến.
* Phát sinh các Domain Event liên quan đến Trip.

### Nguyên tắc thiết kế

Không nên thiết kế:

```text
Trip
├── Customer
├── Driver
├── Vehicle
├── Fare
└── Payment
```

Thay vào đó nên sử dụng ID tham chiếu:

```text
Trip
├── CustomerId
├── DriverId
└── VehicleId
```

Điều này giúp `Trip Management` không phụ thuộc trực tiếp vào các Domain Model của Bounded Context khác.

---

# BC05 – Driver Matching & Assignment Context

## Mục đích

Tìm kiếm tài xế phù hợp và thực hiện quá trình phân công tài xế cho chuyến đi.

Đây là một trong những **Core Domain** của CAB System.

### Các Domain Entity

```text
Driver Matching & Assignment
│
├── MatchingRequest
├── DriverCandidate
└── DriverAssignment
```

### Luồng nghiệp vụ

```text
Trip Created
      ↓
MatchingRequest
      ↓
DriverCandidate
      ↓
DriverAssignment
      ↓
Driver Response
      ↓
Driver Assigned
```

### Ví dụ

Một chuyến đi có thể có nhiều lần phân công:

```text
Trip #1001
│
├── Assignment #1 → Driver A → REJECTED
│
├── Assignment #2 → Driver B → TIMEOUT
│
└── Assignment #3 → Driver C → ACCEPTED
```

### Trách nhiệm

* Nhận yêu cầu tìm tài xế.
* Xác định danh sách tài xế phù hợp.
* Tạo ứng viên tài xế.
* Gửi yêu cầu nhận chuyến.
* Theo dõi phản hồi của tài xế.
* Phân công tài xế.
* Xử lý trường hợp tài xế từ chối hoặc không phản hồi.

### Lưu ý

Không nên đặt logic matching trực tiếp vào `Trip Management`.

---

# BC06 – Fare Management Context

## Mục đích

Tính toán giá chuyến đi và quản lý chính sách tính cước.

### Các Domain Entity

```text
Fare Management
│
├── Fare
└── FarePolicy
```

### Luồng

```text
Trip Completed
       ↓
Fare Management
       ↓
Calculate Fare
       ↓
Fare
```

### Trách nhiệm

* Tính giá chuyến.
* Áp dụng chính sách giá.
* Xác định số tiền khách hàng cần thanh toán.
* Quản lý thông tin Fare.

### Phân biệt Fare và Payment

```text
Fare
│
└── Khách hàng phải trả bao nhiêu?
```

```text
Payment
│
└── Khách hàng đã thanh toán hay chưa?
```

Hai nghiệp vụ này phải được tách thành hai Bounded Context khác nhau.

---

# BC07 – Payment Context

## Mục đích

Quản lý quá trình thanh toán và các giao dịch thanh toán.

### Các Domain Entity

```text
Payment
│
├── PaymentTransaction
└── PaymentAttempt
```

### Ví dụ

```text
PaymentTransaction
│
├── Attempt #1 → FAILED
├── Attempt #2 → FAILED
└── Attempt #3 → SUCCESS
```

### Trách nhiệm

* Tạo giao dịch thanh toán.
* Xử lý thanh toán.
* Theo dõi trạng thái thanh toán.
* Xử lý thanh toán thất bại.
* Thực hiện lại giao dịch khi cần.
* Lưu lịch sử giao dịch.

---

# BC08 – Notification Context

## Mục đích

Quản lý việc gửi thông báo đến khách hàng, tài xế và các đối tượng liên quan.

### Các Domain Entity

```text
Notification
│
├── Notification
├── NotificationTemplate
└── NotificationChannel
```

### Các kênh thông báo

```text
Notification
      │
      ├── Push Notification
      ├── SMS
      └── Email
```

### Ví dụ

Khi tài xế được phân công:

```text
DriverAssigned
       ↓
Notification Context
       ↓
Thông báo khách hàng
```

### Trách nhiệm

* Tạo thông báo.
* Quản lý mẫu thông báo.
* Xác định kênh gửi.
* Gửi thông báo.
* Theo dõi trạng thái gửi.

---

# BC09 – Rating & Trip History Context

## Mục đích

Quản lý đánh giá và lịch sử chuyến đi.

### Các Domain Entity

```text
Rating & Trip History
│
├── Rating
└── TripHistory
```

### Luồng

```text
Trip Completed
       │
       ├──────────→ TripHistory
       │
       └──────────→ Rating
```

### Trách nhiệm

* Lưu lịch sử chuyến đi.
* Cho phép khách hàng đánh giá chuyến.
* Lưu điểm đánh giá.
* Lưu nhận xét.
* Tra cứu lịch sử chuyến.

Một chuyến đi có thể chưa có đánh giá:

```text
Trip 1 ─── 0..1 Rating
```

---

# BC10 – Operation & Reporting Context

## Mục đích

Phục vụ hoạt động vận hành, quản trị và báo cáo của hệ thống.

### Các Domain Entity

```text
Operation & Reporting
│
├── Operation
├── Report
└── AuditLog
```

### Trách nhiệm

* Theo dõi hoạt động hệ thống.
* Giám sát chuyến đi.
* Quản lý hoạt động vận hành.
* Quản lý Audit Log.
* Tổng hợp dữ liệu báo cáo.
* Cung cấp báo cáo cho quản trị viên.

---

# 3. Phân loại Core Domain và Supporting Domain

## Core Domain

```text
┌───────────────────────────────────────────┐
│                CORE DOMAIN                 │
├───────────────────────────────────────────┤
│                                           │
│  1. Trip Management                       │
│  2. Driver Matching & Assignment          │
│                                           │
└───────────────────────────────────────────┘
```

Đây là hai Bounded Context trực tiếp tạo nên nghiệp vụ cốt lõi của hệ thống đặt xe.

## Supporting Domain

```text
┌───────────────────────────────────────────┐
│             SUPPORTING DOMAIN              │
├───────────────────────────────────────────┤
│                                           │
│  1. Identity & Access                     │
│  2. Customer Management                   │
│  3. Driver Management                     │
│  4. Fare Management                       │
│  5. Payment                               │
│  6. Notification                          │
│  7. Rating & Trip History                 │
│  8. Operation & Reporting                 │
│                                           │
└───────────────────────────────────────────┘
```

---

# 4. Context Map tổng thể

```text
                         ┌──────────────────────┐
                         │  Identity & Access   │
                         └──────────┬───────────┘
                                    │
                     ┌──────────────┴──────────────┐
                     ↓                             ↓
          ┌────────────────────┐       ┌────────────────────┐
          │ Customer Management│       │ Driver Management  │
          └─────────┬──────────┘       └─────────┬──────────┘
                    │                            │
                    └──────────────┬─────────────┘
                                   ↓
                    ┌───────────────────────────┐
                    │     TRIP MANAGEMENT        │
                    │       CORE DOMAIN          │
                    └─────────────┬─────────────┘
                                  │
                           TripCreated
                                  ↓
                    ┌───────────────────────────┐
                    │ Driver Matching &          │
                    │ Assignment                 │
                    │ CORE DOMAIN                 │
                    └─────────────┬─────────────┘
                                  │
                           DriverAssigned
                                  ↓
                    ┌───────────────────────────┐
                    │     TRIP MANAGEMENT        │
                    └─────────────┬─────────────┘
                                  │
                    ┌─────────────┼──────────────┐
                    ↓             ↓              ↓
             ┌────────────┐ ┌────────────┐ ┌──────────────┐
             │    Fare    │ │  Payment   │ │Notification  │
             │ Management │ │            │ │              │
             └─────┬──────┘ └─────┬──────┘ └──────┬───────┘
                   │              │               │
                   └──────────────┼───────────────┘
                                  ↓
                    ┌───────────────────────────┐
                    │ Rating & Trip History     │
                    └─────────────┬─────────────┘
                                  ↓
                    ┌───────────────────────────┐
                    │ Operation & Reporting     │
                    └───────────────────────────┘
```

---

# 5. Luồng giao tiếp giữa các Bounded Context

```text
Customer
   │
   │ Create Booking
   ↓
Trip Management
   │
   │ TripCreated
   ↓
Driver Matching & Assignment
   │
   │ DriverAssigned
   ↓
Trip Management
   │
   │ TripCompleted
   ├──────────────────→ Fare Management
   │                         │
   │                         ↓
   │                       Fare
   │
   ├──────────────────→ Payment
   │                         │
   │                         ↓
   │                  PaymentSucceeded
   │
   ├──────────────────→ Notification
   │
   └──────────────────→ Rating & Trip History
```

---

# 6. Tổng hợp Bounded Context

| Bounded Context                  | Loại       | Aggregate/Entity chính                    |
| -------------------------------- | ---------- | ----------------------------------------- |
| Identity & Access                | Supporting | `UserAccount`, `Role`, `Permission`       |
| Customer Management              | Supporting | `Customer`, `CustomerProfile`             |
| Driver Management                | Supporting | `Driver`, `Vehicle`, `DriverLocation`     |
| **Trip Management**              | **Core**   | **`Trip`**                                |
| **Driver Matching & Assignment** | **Core**   | **`MatchingRequest`, `DriverAssignment`** |
| Fare Management                  | Supporting | `Fare`, `FarePolicy`                      |
| Payment                          | Supporting | `PaymentTransaction`, `PaymentAttempt`    |
| Notification                     | Supporting | `Notification`, `NotificationTemplate`    |
| Rating & Trip History            | Supporting | `Rating`, `TripHistory`                   |
| Operation & Reporting            | Supporting | `Operation`, `Report`, `AuditLog`         |

## 7. Nguyên tắc thiết kế

1. Mỗi Bounded Context có **domain model riêng**.
2. Không dùng chung Entity giữa các Bounded Context.
3. Không dùng chung Database giữa các Microservice nếu triển khai theo Microservices.
4. Khi Context khác cần tham chiếu dữ liệu, sử dụng **ID** thay vì truyền trực tiếp Domain Object.
5. `Trip Management` không chứa `Payment`, `Fare`, `DriverAssignment` dưới dạng Entity của chính nó.
6. `Driver Management` quản lý tài xế; `Driver Matching & Assignment` chịu trách nhiệm tìm và phân công tài xế.
7. `Fare Management` tính tiền; `Payment` xử lý thanh toán.
8. Các Context có thể giao tiếp thông qua **API hoặc Domain Event**.
9. `Trip Management` và `Driver Matching & Assignment` là hai Context quan trọng nhất của nghiệp vụ CAB System.

