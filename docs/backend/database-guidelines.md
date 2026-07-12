# Database Guidelines

## 1. Primary Key

- Tất cả bảng sử dụng UUID làm Primary Key.
- Không sử dụng Auto Increment ID.

Example

```sql
id UUID PRIMARY KEY
```

---

## 2. Naming Convention

### Table

- Sử dụng PascalCase hoặc snake_case (thống nhất toàn dự án).
- Tên bảng ở dạng số ít.

Ví dụ

- User
- BankAccount
- Transaction
- ImportBatch
- Category

Không dùng

- Users
- Transactions

---

### Column

- Sử dụng camelCase.

Ví dụ

- userId
- bankAccountId
- transactionDate
- balanceAfter

---

## 3. Foreign Key

Tên Foreign Key phải theo format

```
<entityName>Id
```

Ví dụ

- userId
- categoryId
- importBatchId

Không dùng

- uid
- bank_id
- catId

---

## 4. Money

Không sử dụng FLOAT hoặc DOUBLE.

Luôn sử dụng

```
DECIMAL(18,2)
```

Áp dụng cho

- amount
- balanceAfter

---

## 5. Date & Time

Audit Fields

```
createdAt
updatedAt
deletedAt
```

Business Date

```
transactionDate
transactionTime
```

Không lưu Date dưới dạng String.

---

## 6. Enum

Các giá trị cố định phải sử dụng Enum.

Ví dụ

TransactionType

- INCOME
- EXPENSE

ImportStatus

- PENDING
- PROCESSING
- SUCCESS
- FAILED

---

## 7. Audit Fields

Mọi bảng đều phải có

```
createdAt
updatedAt
```

Các bảng cần hỗ trợ xóa mềm sẽ có

```
deletedAt
```

---

## 8. Soft Delete

Ưu tiên sử dụng

```
deletedAt
```

Không sử dụng

```
isDeleted
```

---

## 9. Unique Constraint

Chỉ tạo Unique khi Business yêu cầu.

Ví dụ

User

```
email
```

Category

```
(userId, name)
```

---

## 10. Index

Tạo Index cho các cột thường xuyên

- JOIN
- WHERE
- ORDER BY

Ví dụ

```
userId
bankAccountId
transactionDate
categoryId
```

Không tạo Index cho mọi cột.

---

## 11. Normalization

Database chỉ lưu dữ liệu đã được chuẩn hóa.

Parser chịu trách nhiệm chuyển đổi dữ liệu từ các ngân hàng sang format chung.

Không lưu dữ liệu phụ thuộc vào định dạng của từng ngân hàng.

---

## 12. Business First

Mỗi cột phải phục vụ một nghiệp vụ cụ thể.

Không thêm cột nếu chưa có Business Requirement.

---

## 13. Source of Truth

Dữ liệu gốc từ ngân hàng phải được lưu đầy đủ.

Ví dụ

- transactionDate
- transactionTime
- description
- amount
- balanceAfter

Không tự ý loại bỏ dữ liệu gốc nếu chưa có lý do rõ ràng.

---

## 14. Calculated Data

Không lưu dữ liệu có thể tính toán.

Ví dụ

Không lưu

- totalExpense
- totalIncome
- monthlyBalance

Các giá trị này sẽ được tính từ Transaction.

---

## 15. Relationship

Luôn ưu tiên sử dụng Foreign Key.

Không lưu dữ liệu trùng lặp.

Ví dụ

Đúng

```
Transaction
    bankAccountId
```

Sai

```
Transaction
    bankName
    accountNumber
```

---

## 16. Extensibility

Thiết kế Database không phụ thuộc vào một ngân hàng cụ thể.

Mọi khác biệt của file import sẽ được xử lý tại Parser.

Database chỉ lưu dữ liệu theo mô hình chuẩn của hệ thống.

###### RULE sernior BE

## 17. Single Responsibility

Mỗi bảng chỉ đại diện cho một Entity.

Không lưu dữ liệu thuộc Entity khác nếu đã có quan hệ.

Ví dụ

Đúng

Transaction
- bankAccountId

Sai

Transaction
- bankName
- accountNumber

---

## 18. Extensibility

Database phải dễ mở rộng.

Không thiết kế phụ thuộc vào một ngân hàng cụ thể.

Ví dụ

Đúng

Transaction
- amount
- type

Sai

Transaction
- debit
- credit

---

## 19. Nullable

Chỉ cho phép NULL khi Business chấp nhận.

Nếu dữ liệu luôn tồn tại thì NOT NULL.

Ví dụ

transactionDate      ✅ NOT NULL
description          ✅ NOT NULL
categoryId           ✅ NULL
transactionTime      ✅ NULL

---

## 20. Default Value

Những field có giá trị mặc định phải khai báo rõ.

Ví dụ

createdAt = NOW()

updatedAt = NOW()

status = PENDING

Không xử lý mặc định trong code nếu Database có thể đảm nhiệm.

---

## 21. Cascade Rules

Không sử dụng CASCADE một cách tùy tiện.

Luôn xác định rõ hành vi khi xóa dữ liệu.

Ví dụ

User
    ↓
BankAccount

=> RESTRICT

Category
    ↓
Transaction

=> SET NULL

ImportBatch
    ↓
Transaction

=> RESTRICT

---

## 22. Data Integrity

Luôn ưu tiên đảm bảo tính toàn vẹn dữ liệu.

Không lưu dữ liệu mồ côi (Orphan Data).

Ví dụ

Không được có

Transaction

categoryId = abc

trong khi Category không tồn tại.

---

## 23. Duplicate Prevention

Database phải có cơ chế chống dữ liệu trùng.

Không chỉ kiểm tra ở Frontend.

Không chỉ kiểm tra ở Backend.

Ưu tiên sử dụng

- Unique Constraint
- Composite Unique
- Hash Key

---

## 24. Business Validation

Validation nghiệp vụ thuộc Backend.

Database chỉ đảm bảo tính toàn vẹn dữ liệu.

Ví dụ

Database

amount > 0

Backend

Income không được có Category "Ăn uống"

---

## 25. Data Consistency

Một dữ liệu chỉ có một nguồn sự thật (Single Source of Truth).

Ví dụ

Tên ngân hàng chỉ lưu trong BankAccount.

Transaction chỉ lưu bankAccountId.

Không lưu thêm bankName trong Transaction.

---

## 26. Naming Consistency

Tên field phải thống nhất trên toàn hệ thống.

Ví dụ

createdAt
updatedAt
deletedAt

Không dùng lẫn lộn

created_date
CreateTime
create_at

---

## 27. Versioning

Không sửa trực tiếp dữ liệu gốc nếu cần lưu lịch sử.

Ưu tiên tạo Version hoặc Audit Log khi Business yêu cầu.

(MVP chưa cần triển khai.)

---

## 28. Performance

Thiết kế ưu tiên đúng Business trước.

Chỉ tối ưu khi có dữ liệu thực tế.

Không tối ưu quá sớm (Premature Optimization).

---

## 29. Documentation

Mỗi bảng cần mô tả

- Purpose
- Relationships
- Business Rules

Không chỉ tạo bảng mà không có tài liệu.

---

## 30. Think Business First

Trước khi thêm bất kỳ bảng hoặc cột nào, luôn tự hỏi:

- Business cần gì?
- User sử dụng dữ liệu này để làm gì?
- Nếu bỏ field này thì chức năng nào sẽ không hoạt động?

Chỉ thêm khi có câu trả lời rõ ràng.