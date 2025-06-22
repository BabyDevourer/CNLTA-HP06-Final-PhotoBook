
# 📦 Data Model – Greeting Card Creator App

## 🧱 1. Các Model chính

### ✅ `GreetingCard` – đại diện cho **một tấm thiệp đã hoàn thành**

```swift
struct GreetingCard: Identifiable, Codable {
    var id: UUID = UUID()
    var greetingText: String        // Lời chúc trên thiệp
    var fontName: String            // Tên font chữ đã chọn
    var fontSize: CGFloat           // Kích thước chữ
    var textColorData: Data         // Dữ liệu màu chữ (để Codable)
    var backgroundImageName: String // Tên ảnh nền đã chọn
    var dateCreated: Date           // Ngày tạo thiệp
}
```

📌 **Giải thích:**

*   `greetingText`: Nội dung lời chúc do người dùng nhập.
*   `fontName`, `fontSize`: Lưu lại thông tin font chữ đã tùy chỉnh.
*   `textColorData`: `Color` không trực tiếp `Codable`. Ta cần chuyển nó sang `Data` để lưu và tải.
*   `backgroundImageName`: Tên của ảnh nền trong `Assets.xcassets` mà người dùng đã chọn.
*   `dateCreated`: Để sắp xếp danh sách thiệp đã lưu theo thời gian.

---

### ✅ `BackgroundOption` – đại diện cho **một lựa chọn ảnh nền**

```swift
struct BackgroundOption: Identifiable, Hashable {
    let id = UUID()
    let imageName: String      // Tên ảnh trong Assets Catalog
    let displayName: String    // Tên hiển thị trong UI
}
```

📌 **Giải thích:**

*   Dùng để tạo danh sách các ảnh nền cho người dùng lựa chọn một cách có tổ chức. `Identifiable` và `Hashable` giúp nó hoạt động tốt với `ForEach` và `Picker`.

---

### ✅ `FontOption` – đại diện cho **một lựa chọn font chữ**

```swift
struct FontOption: Identifiable, Hashable {
    let id = UUID()
    let fontName: String       // Tên hệ thống của font
    let displayName: String    // Tên thân thiện hiển thị cho người dùng
}
```

📌 **Giải thích:**

*   Tương tự `BackgroundOption`, struct này giúp quản lý danh sách các font chữ có thể chọn.

---

## 📂 2. Lưu trữ dữ liệu

### ✅ Lưu danh sách `GreetingCard`:

*   Dùng `@Published var savedCards: [GreetingCard]` trong `CardViewModel`.
*   Lưu và tải với `UserDefaults` (hoặc `FileManager` cho dữ liệu lớn hơn) bằng `JSONEncoder`/`JSONDecoder`.

```swift
func saveCards() {
    // Trước khi encode, cần chuyển đổi Color sang Data nếu đang dùng
    if let encoded = try? JSONEncoder().encode(savedCards) {
        UserDefaults.standard.set(encoded, forKey: "SavedGreetingCards")
    }
}

func loadCards() {
    if let data = UserDefaults.standard.data(forKey: "SavedGreetingCards"),
       let decoded = try? JSONDecoder().decode([GreetingCard].self, from: data) {
        self.savedCards = decoded
        // Sau khi decode, cần chuyển đổi Data ngược lại thành Color để hiển thị
    }
}
```

---

## 📚 Tổng kết luồng dữ liệu

| Thành phần         | Vai trò                  | Mối quan hệ                                                         |
| ------------------ | ------------------------- | ------------------------------------------------------------------- |
| `GreetingCard`     | Thiệp hoàn chỉnh          | Lưu lại kết quả lựa chọn của người dùng (text, font, màu, ảnh nền) |
| `BackgroundOption` | Lựa chọn ảnh nền          | Cung cấp dữ liệu cho danh sách/lưới chọn ảnh nền                   |
| `FontOption`       | Lựa chọn font chữ         | Cung cấp dữ liệu cho `Picker` chọn font chữ                         |
| `CardViewModel`    | Quản lý dữ liệu           | Chứa danh sách các thiệp đã lưu, xử lý logic save/load              |
| `UserDefaults`     | Lưu trữ cục bộ            | Lưu lại mảng `[GreetingCard]` sau mỗi lần người dùng lưu thiệp       |

---

👉 **Gợi ý mở rộng:**

*   Cho phép người dùng chọn ảnh từ thư viện thay vì chỉ từ `Assets`.
*   Export thiệp đã tạo thành một file ảnh `UIImage` và lưu vào thư viện.
*   Thêm các "Sticker" (các ảnh nhỏ) có thể kéo thả lên thiệp.
*   Tạo các "Template" (`GreetingCard` mẫu) cho các dịp lễ (Sinh nhật, Giáng sinh...).
