---
Title: JavaScript Questions
---
#### Made by <a href="https://www.facebook.com/anhtaidang.developer">anhtaidang</a>

# Table of Contents
- [Bind Call method in Javascript](#bind-call-method-in-javascript)
- [Explain Cache-control](#explain-cache-control)
- [Explain HSTS](#explain-hsts)
- [Explain HTTPS](#explain-https)

>## Bind Call method in Javascript.

Trong JavaScript, `bind()` và `call()` đều là các phương thức dùng để thay đổi context (ngữ cảnh) của một hàm. Tuy nhiên, cách thực hiện và cách sử dụng của chúng khác nhau như sau:

1. `call()`: phương thức này cho phép gọi một hàm và thiết lập context cho hàm đó ngay lúc đó. Cú pháp của `call()` như sau:

```javascript
function.call(thisArg, arg1, arg2, ...)
```````

- function là hàm cần gọi.
- thisArg là giá trị mà this sẽ được thiết lập thành.
- arg1, arg2, ... là các đối số của hàm.

Ví dụ:

```javascript
const person1 = { name: 'Alice' };
const person2 = { name: 'Bob' };

function greet() {
  console.log(`Hello, ${this.name}`);
}

greet.call(person1); // Hello, Alice
greet.call(person2); // Hello, Bob
```
2. `bind()`: phương thức này cho phép tạo ra một phiên bản mới của hàm, với context đã được thiết lập sẵn. Cú pháp của bind() như sau:

```javascript
function.bind(thisArg, arg1, arg2, ...)
`````

- `function` là hàm cần tạo phiên bản mới.
- `thisArg` là giá trị mà this sẽ được thiết lập thành.
- `arg1`, `arg2, ...` là các đối số của hàm.

Ví dụ:

```javascript
const person1 = { name: 'Alice' };
const person2 = { name: 'Bob' };

function greet() {
  console.log(`Hello, ${this.name}`);
}

const greetPerson1 = greet.bind(person1);
const greetPerson2 = greet.bind(person2);

greetPerson1(); // Hello, Alice
greetPerson2(); // Hello, Bob
```

Tóm lại, `call()` được sử dụng để gọi hàm và thiết lập context ngay lúc đó, trong khi `bind()` được sử dụng để tạo ra một phiên bản mới của hàm với context đã được thiết lập sẵn.

[[↑] Back to top](#table-of-contents)

>## Explain Cache-control.

Cache-Control là một trường trong tiêu đề HTTP được sử dụng để kiểm soát bộ nhớ cache của trình duyệt hoặc proxy. Nó xác định cách thức mà các trang web được lưu trữ và sử dụng trong bộ nhớ đệm (cache) của các máy khách và proxy.

Các giá trị của trường Cache-Control có thể bao gồm:

- `public`: Cho phép bộ nhớ cache công khai, có thể được lưu trữ bởi các máy khách và proxy.
- `private`: Không cho phép bộ nhớ cache công khai, chỉ có thể được lưu trữ bởi trình duyệt của người dùng.
- `no-cache`: Bắt buộc các máy khách và proxy phải yêu cầu phiên bản mới nhất từ máy chủ trước khi trả về nội dung cho người dùng.
- `no-store`: Các trang web không được lưu trữ trong bộ nhớ cache của máy khách hoặc proxy.
- `max-age`: Xác định thời gian tối đa mà nội dung được lưu trữ trong bộ nhớ cache trước khi nó phải được yêu cầu lại từ máy chủ.
- `s-maxage`: Tương tự như max-age, nhưng chỉ áp dụng cho các proxy chia sẻ.
Các giá trị này có thể được sử dụng độc lập hoặc kết hợp với nhau để kiểm soát cách thức lưu trữ và sử dụng bộ nhớ cache.

[[↑] Back to top](#table-of-contents)

>## Explain HSTS

`HSTS` là viết tắt của "HTTP Strict Transport Security". Đây là một chính sách bảo mật được sử dụng trên các trình duyệt web để đảm bảo rằng các kết nối truy cập trang web của người dùng luôn được mã hóa và được gửi qua một kênh an toàn.

Khi một trình duyệt được cấu hình để sử dụng HSTS, nó sẽ nhận dạng trang web và yêu cầu các yêu cầu tiếp theo đến trang web đó phải sử dụng HTTPS (HTTP Secure) thay vì HTTP. Nếu trình duyệt không thể kết nối đến trang web qua HTTPS, nó sẽ hiển thị một thông báo lỗi để ngăn chặn người dùng tiếp tục truy cập trang web bằng HTTP.

HSTS được sử dụng để bảo vệ truyền thông trang web khỏi các cuộc tấn công như tấn công giả mạo trang web và tấn công man-in-the-middle. Nó cũng giúp tăng cường tính riêng tư của người dùng bằng cách đảm bảo rằng các thông tin nhạy cảm không được truyền trên kênh truyền thông không an toàn.

[[↑] Back to top](#table-of-contents)

> ## Explain HTTPS

`HTTPS` là viết tắt của "Hypertext Transfer Protocol Secure". Đây là một phiên bản bảo mật của giao thức HTTP, được sử dụng để truyền tải dữ liệu giữa máy tính và máy chủ trên mạng internet.

Khi sử dụng HTTPS, dữ liệu được mã hóa trước khi được truyền qua mạng, điều này làm cho nó khó khăn để người khác có thể đánh cắp thông tin của bạn hoặc thay đổi dữ liệu trên đường truyền. Điều này đặc biệt quan trọng đối với các trang web yêu cầu thông tin nhạy cảm từ người dùng, chẳng hạn như thông tin tài khoản ngân hàng, thông tin thẻ tín dụng hoặc thông tin đăng nhập. Khi trang web sử dụng HTTPS, trình duyệt web sẽ hiển thị một biểu tượng khóa màu xanh lá cây hoặc một biểu tượng "https://" trên thanh địa chỉ của trình duyệt.

### SSL

`SSL` là viết tắt của "Secure Sockets Layer". SSL là một công nghệ bảo mật được sử dụng để bảo vệ dữ liệu truyền tải giữa máy tính của bạn và máy chủ trên mạng internet.

`SSL` sử dụng một cơ chế mã hóa để mã hóa dữ liệu trước khi truyền qua mạng. Khi máy tính của bạn gửi yêu cầu đến một trang web được bảo vệ bằng SSL, máy chủ sẽ gửi một chứng chỉ SSL để xác minh tính hợp lệ của trang web. Sau khi xác minh tính hợp lệ của chứng chỉ SSL, máy tính của bạn và máy chủ sẽ thiết lập một kết nối an toàn để truyền tải dữ liệu giữa chúng.

`SSL` đã được thay thế bởi `TLS` (Transport Layer Security), nhưng thuật ngữ SSL vẫn được sử dụng phổ biến để chỉ đến các giao thức bảo mật được sử dụng để bảo vệ dữ liệu truyền tải trên mạng.

[[↑] Back to top](#table-of-contents)