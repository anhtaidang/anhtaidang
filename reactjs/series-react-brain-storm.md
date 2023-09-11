---
<h1 align="center">Series ReactJS - State Management Brainstorm</h1>

#### Made by <a href="https://www.facebook.com/anhtaidang.developer">anhtaidang</a>

![logoJSpng](../assets/images/logoReactJS.webp)
---
# Table of Contents
- [Explain Virtual DOM](#-explain-virtual-dom)

---
## 🧠 Explain Virtual DOM.

Virtual DOM (Document Object Model)
Virtual DOM (DOM ảo) là một mô hình dữ liệu đại diện cho DOM thực.<br /> 
Virtual DOM là một biểu diễn ảo của cây DOM thực tế của trang web. Nó được sử dụng để tối ưu hóa hiệu suất và cải thiện tính năng khi làm việc với DOM thật trong ứng dụng web.

Dưới đây là cách Virtual DOM hoạt động:

**1. Tạo một biểu diễn ảo của DOM**: Khi một thay đổi xảy ra trong ứng dụng web (ví dụ: sự kiện người dùng hoặc dữ liệu thay đổi), React và các thư viện tương tự tạo ra một bản sao ảo của cây DOM hiện tại. Cây này được gọi là Virtual DOM.<br/>
**2. So sánh với DOM thật**: Virtual DOM sau đó được so sánh với DOM thật để tìm ra sự khác biệt giữa chúng. Nói cách khác, React xác định xem nội dung thực tế của trang web đã thay đổi như thế nào so với biểu diễn ảo.<br/>
**3. Tính toán các thay đổi cần thiết**: Dựa trên sự khác biệt, React tính toán các thay đổi cần thiết để đưa DOM thực tế về trạng thái mới, chứa tất cả các thay đổi từ Virtual DOM.<br/>
**4. Áp dụng thay đổi vào DOM thật**: Cuối cùng, React áp dụng các thay đổi đã tính toán vào DOM thật, cập nhật giao diện người dùng theo cách hiệu quả nhất.<br/>

Lợi ích của Virtual DOM bao gồm:

- **Tối ưu hóa hiệu suất**: Virtual DOM giúp giảm thiểu số lượng thao tác trực tiếp trên DOM thật, giúp cải thiện hiệu suất của ứng dụng web.
- **Tự động xác định thay đổi**: Virtual DOM tự động xác định các phần của trang cần được cập nhật, giúp tránh việc cập nhật toàn bộ trang.
- **Giảm khả năng xảy ra lỗi**: Bằng cách sử dụng Virtual DOM, bạn có thể tránh được nhiều lỗi phổ biến liên quan đến việc thao tác trực tiếp trên DOM.

[[↑] Back to top](#table-of-contents)