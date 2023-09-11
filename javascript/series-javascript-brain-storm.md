---
<h1 align="center">Series JavaScript Brainstorm</h1>

#### Made by <a href="https://www.facebook.com/anhtaidang.developer">anhtaidang</a>

![logoJSpng](../assets/images/logoJS.png)
---
# Table of Contents
- [Explain How to `this` work in Javascript](#-explain-how-to-this-work-in-javascript)
- [Explain Bind Call method in Javascript](#-explain-bind-call-method-in-javascript)
- [Explain `let`,`const`,`var` in Javascript](#-explain-letconstvar-in-javascript)
- [Explain Cache-control](#-explain-cache-control)
- [Explain HSTS](#-explain-hsts)
- [Explain HTTPS](#-explain-https)
- [Explain Truly & Faulty](#-explain-truly--faulty)
- [Explain difference between `.forEach` & `.map` - `.find()`, `.findIndex()` & `.filter()`](#-explain-difference-between-foreach--map---find-findindex--filter)
- [Explain Closure in Javascript](#-explain-closure-in-javascript)
- [Explain Promise in Javascript](#-explain-promise-in-javascript)
- [Explain Callback in Javascript](#-explain-callback-in-javascript)
- [Explain Hoisting in Javascript](#-explain-hoisting-in-javascript)
- [Explain Design Pattern](#-explain-design-pattern)
- [Explain Cookies Session Storage và Local Storage](#-explain-cookies-session-storage-v-local-storage)
- [Explain BEM? Naming standard CSS follow BEM](#-explain-bem-naming-standard-css-follow-bem)
---
## 🧠 Explain How to `this` work in Javascript.
Trong JavaScript, `this` là một từ khóa đặc biệt được sử dụng để tham chiếu đến đối tượng hiện tại, tức là đối tượng phương thức hoặc thuộc tính được gọi.

Cách hoạt động của this được xác định bởi cách mà một phương thức hoặc hàm được gọi. 
Có 4 cách thường được sử dụng để thiết lập giá trị của `this`:

#### 1. Khi gọi phương thức trên một đối tượng, `this` được thiết lập thành đối tượng đó:
```js
const person = {
  name: 'John',
  sayHello() {
    console.log('Hello, ' + this.name);
  }
};

person.sayHello(); // Hello, John
```

Trong ví dụ này, khi `sayHello()` được gọi trên đối tượng `person`, `this` được thiết lập thành `person`.

#### 2. Khi gọi hàm không được gọi trên đối tượng, `this` được thiết lập thành đối tượng toàn cục (`window` trong trình duyệt hoặc `global` trong Node.js):

```js
function sayHello() {
  console.log('Hello, ' + this.name);
}

window.name = 'John';

sayHello(); // Hello, John
```

Trong ví dụ này, khi `sayHello()` được gọi, this được thiết lập thành `window` và `name` được lấy từ `window.name`.

#### 3. Khi sử dụng phương thức `call()` hoặc `apply()`, this được thiết lập thành đối tượng được truyền vào làm tham số đầu tiên:

```js
function sayHello() {
  console.log('Hello, ' + this.name);
}

const person = {
  name: 'John'
};

sayHello.call(person); // Hello, John
```

Trong ví dụ này, khi `call()` được sử dụng để gọi `sayHello()` và truyền vào person làm tham số đầu tiên, `this` được thiết lập thành person.

#### 4. Khi sử dụng hàm arrow, `this` được liên kết với ngữ cảnh của hàm đó, tức là nó được thiết lập từ hàm bao bọc nó:

```js
const person = {
  name: 'John',
  sayHello: () => {
    console.log('Hello, ' + this.name);
  }
};

person.sayHello(); // Hello, undefined
```

Trong ví dụ này, `this` không được thiết lập thành person, mà là từ hàm bao bọc nó. Do đó, `this.name` trả về `undefined`.

Trong ngữ cảnh của một hàm hay phương thức, giá trị của this có thể thay đổi tùy vào cách hàm hay phương thức đó được gọi.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Bind Call method in Javascript.

> Trong JavaScript, `bind()`, `call()`, `apply()` đều là các phương thức dùng để thay đổi `context (ngữ cảnh)` và được sử dụng để thiết lập giá trị  `this` của một hàm. Tuy nhiên, cách thực hiện và cách sử dụng của chúng khác nhau như sau:

#### 1. Phương thức `call()`: Sử dụng phương thức `call()` để gọi hàm và thiết lập giá trị `this` trong hàm. Giá trị của `this` được truyền vào làm tham số đầu tiên của phương thức `call()`, còn các tham số tiếp theo là các tham số của hàm được gọi.

```js
function.call(thisArg, arg1, arg2, ...)
```````

- function là hàm cần gọi.
- thisArg là giá trị mà this sẽ được thiết lập thành.
- arg1, arg2, ... là các đối số của hàm.

Ví dụ:

```js
const person1 = { name: 'Alice' };
const person2 = { name: 'Bob' };

function greet() {
  console.log(`Hello, ${this.name}`);
}

greet.call(person1); // Hello, Alice
greet.call(person2); // Hello, Bob
```
#### 2. Phương thức `bind()`: Sử dụng phương thức `bind()` để tạo ra một hàm mới với giá trị `this` được thiết lập sẵn. Phương thức `bind()` trả về một hàm mới, không gọi hàm đó ngay lập tức, mà chỉ trả về một tham chiếu đến hàm mới đó. Khi hàm mới được gọi, giá trị this được thiết lập sẵn theo giá trị đã được đặt trong phương thức bind(), còn các tham số sẽ được truyền vào hàm khi hàm mới được gọi.

```js
function.bind(thisArg, arg1, arg2, ...)
`````

- `function` là hàm cần tạo phiên bản mới.
- `thisArg` là giá trị mà this sẽ được thiết lập thành.
- `arg1`, `arg2, ...` là các đối số của hàm.

Ví dụ:

```js
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

```js
function greet(greeting, name) {
    console.log(`${greeting}, ${name}! My name is ${this.name}.`);
}

const person = {
    name: 'John'
};

const greetPerson = greet.bind(person, 'Hello');
greetPerson('Mary'); // Hello, Mary! My name is John.
```
Trong ví dụ này, phương thức `bind()` được sử dụng để tạo ra một hàm mới greetPerson với giá trị this được thiết lập sẵn là đối tượng person. Khi hàm `greetPerson()` được gọi, giá trị `this`

#### 3. Phương thức `apply()`:Sử dụng phương thức `apply()` để gọi hàm và thiết lập giá trị `this` trong hàm. Giá trị của `this` được truyền vào làm tham số đầu tiên của phương thức `apply()`, còn tham số thứ hai là một mảng các tham số của hàm được gọi.

Ví dụ:

```js
function greet(greeting, name) {
  console.log(`${greeting}, ${name}! My name is ${this.name}.`);
}

const person = {
  name: 'John'
};

greet.apply(person, ['Hello', 'Mary']); // Hello, Mary! My name is John.
```
---
> Notes:<br/>
> - Tóm lại, `call()`, `apply()` được sử dụng để gọi hàm và thiết lập context ngay lúc đó, trong khi `bind()` được sử dụng để tạo ra một phiên bản mới của hàm với context đã được thiết lập sẵn.
> <br/><br/>
> - Tham số truyền vào: Trong phương thức `call()`, các tham số của hàm được gọi được truyền vào theo cách riêng biệt, trong khi đó, trong phương thức `apply()`, các tham số được truyền vào dưới dạng một mảng.
> <br/><br/>
> - Hiệu suất: Phương thức call() có hiệu suất tốt hơn so với phương thức apply(). Do phương thức call() truyền các tham số một cách riêng biệt nên nó nhanh hơn khi xử lý các tham số, trong khi phương thức apply() phải xử lý một mảng các tham số.
> <br/><br/>
> - Sử dụng: Phương thức `call()` thường được sử dụng khi số lượng tham số được truyền vào hàm là biết trước, còn phương thức `apply()` thường được sử dụng khi số lượng tham số là không biết trước và được lưu trữ trong một mảng.
> 

[[↑] Back to top](#table-of-contents)

## 🧠 Explain `let`,`const`,`var` in Javascript

Trong Javascript, `let`, `const`, và `var` đều được sử dụng để khai báo biến. Tuy nhiên, chúng có những sự khác nhau quan trọng về phạm vi, cách thức hoạt động, và tính chất bảo vệ giá trị.

`var` được sử dụng để khai báo biến toàn cục hoặc cục bộ trong một hàm. Trong khi đó, `let` và `const` được sử dụng để khai báo biến cục bộ trong một khối mã, như một khối lệnh hoặc một hàm.

Về cách thức hoạt động, `var` sẽ có phạm vi là toàn bộ hàm hoặc tệp tin mà nó được khai báo, trong khi `let` và `const` sẽ có phạm vi là khối mã bao quanh nó. Điều này có nghĩa là biến được khai báo bằng let hoặc const chỉ có thể được truy cập trong khối mã bao quanh nó, trong khi biến được khai báo bằng var có thể được truy cập từ bất kỳ đâu trong hàm hoặc tệp tin.

Tính chất bảo vệ giá trị của `let` và `const` khác với `var`. Khi một biến được khai báo bằng `let` hoặc `const`, giá trị của nó có thể được gán lại nhưng không thể khai báo lại trong cùng một khối mã. Trong khi đó, biến được khai báo bằng var có thể khai báo lại và gán giá trị mới một cách dễ dàng.

Một sự khác biệt quan trọng khác giữa `let` và `const` đó là `let` cho phép gán giá trị mới cho biến, trong khi `const` không cho phép. Nếu một biến được khai báo bằng `const`, giá trị của nó không thể thay đổi sau khi được gán.

Tóm lại, `var` có phạm vi toàn cục hoặc cục bộ trong hàm, có thể khai báo lại và gán giá trị mới. `let` và `const` chỉ có phạm vi trong khối mã bao quanh nó, không thể khai báo lại nhưng let có thể gán giá trị mới, trong khi `const` không thể thay đổi giá trị đã gán.

Chúng ta hãy xem qua một số ví dụ để hiểu rõ hơn về sự khác nhau giữa `let`, `const`, và `var` trong JavaScript.

#### 1. Ví dụ về phạm vi (scope):

```js
function example() {
  var a = 1;
  let b = 2;
  const c = 3;
  
  if (true) {
    var a = 4;
    let b = 5;
    const c = 6;
    console.log(a, b, c); // output: 4 5 6
  }
  
  console.log(a, b, c); // output: 4 2 3
}

example();
```

Ở đây, biến `a` được khai báo bằng `var` và có thể truy cập từ bất kỳ đâu trong hàm `example()`. Trong khi đó, biến `b` và `c` được khai báo bằng `let` và `const` và chỉ có thể truy cập trong khối mã bao quanh nó, do đó, giá trị của `b` và `c` sẽ không bị ảnh hưởng bởi việc khai báo lại trong khối mã `if`.

#### 2. Ví dụ về tính chất bảo vệ giá trị:

```js
let x = 1;
const y = 2;

x = 3;
// y = 4; // không thể gán lại giá trị cho biến đã khai báo bằng const

console.log(x, y); // output: 3 2
```

Ở đây, biến `x` được khai báo bằng let, cho phép gán lại giá trị mới cho biến. Trong khi đó, biến `y` được khai báo bằng const và không thể gán lại giá trị mới, do đó, khi ta thử gán giá trị mới cho `y`, chương trình sẽ bị lỗi.

#### 3. Ví dụ về hoisting (nâng cao):

```js
console.log(a); // output: undefined
var a = 1;

console.log(b); // Uncaught ReferenceError: b is not defined
let b = 2;
```

Ở đây, biến `a` được khai báo bằng `var` được hoisting lên đầu phạm vi và có giá trị là `undefined` trước khi được gán giá trị. Trong khi đó, biến `b` được khai báo bằng `let` không được hoisting, do đó, khi ta cố gắng truy cập b trước khi khai báo, chương trình sẽ bị lỗi.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Cache-control.

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

## 🧠 Explain HSTS

`HSTS` là viết tắt của "HTTP Strict Transport Security". Đây là một chính sách bảo mật được sử dụng trên các trình duyệt web để đảm bảo rằng các kết nối truy cập trang web của người dùng luôn được mã hóa và được gửi qua một kênh an toàn.

Khi một trình duyệt được cấu hình để sử dụng HSTS, nó sẽ nhận dạng trang web và yêu cầu các yêu cầu tiếp theo đến trang web đó phải sử dụng HTTPS (HTTP Secure) thay vì HTTP. Nếu trình duyệt không thể kết nối đến trang web qua HTTPS, nó sẽ hiển thị một thông báo lỗi để ngăn chặn người dùng tiếp tục truy cập trang web bằng HTTP.

HSTS được sử dụng để bảo vệ truyền thông trang web khỏi các cuộc tấn công như tấn công giả mạo trang web và tấn công man-in-the-middle. Nó cũng giúp tăng cường tính riêng tư của người dùng bằng cách đảm bảo rằng các thông tin nhạy cảm không được truyền trên kênh truyền thông không an toàn.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain HTTPS

`HTTPS` là viết tắt của "Hypertext Transfer Protocol Secure". Đây là một phiên bản bảo mật của giao thức HTTP, được sử dụng để truyền tải dữ liệu giữa máy tính và máy chủ trên mạng internet.

Khi sử dụng HTTPS, dữ liệu được mã hóa trước khi được truyền qua mạng, điều này làm cho nó khó khăn để người khác có thể đánh cắp thông tin của bạn hoặc thay đổi dữ liệu trên đường truyền. Điều này đặc biệt quan trọng đối với các trang web yêu cầu thông tin nhạy cảm từ người dùng, chẳng hạn như thông tin tài khoản ngân hàng, thông tin thẻ tín dụng hoặc thông tin đăng nhập. Khi trang web sử dụng HTTPS, trình duyệt web sẽ hiển thị một biểu tượng khóa màu xanh lá cây hoặc một biểu tượng "https://" trên thanh địa chỉ của trình duyệt.

### SSL

`SSL` là viết tắt của "Secure Sockets Layer". SSL là một công nghệ bảo mật được sử dụng để bảo vệ dữ liệu truyền tải giữa máy tính của bạn và máy chủ trên mạng internet.

`SSL` sử dụng một cơ chế mã hóa để mã hóa dữ liệu trước khi truyền qua mạng. Khi máy tính của bạn gửi yêu cầu đến một trang web được bảo vệ bằng SSL, máy chủ sẽ gửi một chứng chỉ SSL để xác minh tính hợp lệ của trang web. Sau khi xác minh tính hợp lệ của chứng chỉ SSL, máy tính của bạn và máy chủ sẽ thiết lập một kết nối an toàn để truyền tải dữ liệu giữa chúng.

`SSL` đã được thay thế bởi `TLS` (Transport Layer Security), nhưng thuật ngữ SSL vẫn được sử dụng phổ biến để chỉ đến các giao thức bảo mật được sử dụng để bảo vệ dữ liệu truyền tải trên mạng.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Truly & Faulty

`Truly` và `faulty` là các giá trị boolean trong JavaScript, có ý nghĩa tương ứng với `true` và `false`.

Trong JavaScript, các giá trị `truly` là các giá trị được xem là `true` khi được sử dụng trong một phép so sánh boolean. Các giá trị `truly`bao gồm:

>- Giá trị boolean `true`
>- Các chuỗi khác rỗng `(ví dụ: "hello", "123")`
>- Số khác `0 (ví dụ: 42, -3.14)`
>- Một đối tượng được xem là `truthy` - tức là, một đối tượng không phải là `null, undefined, false, 0` hoặc rỗng chuỗi.

Ví dụ, các biểu thức sau đây đều trả về giá trị boolean `true`:

```js
Boolean(true); // true
Boolean("hello"); // true
Boolean(42); // true
Boolean({}); // true
```
Ngược lại, các giá trị `faulty` là các giá trị được xem là `false` khi được sử dụng trong một phép so sánh boolean. Các giá trị `faulty` bao gồm:

>- Giá trị boolean `false`
>- Chuỗi rỗng `""`
>- Số `0`
>- Giá trị `null` hoặc `undefined`
>- Một đối tượng được xem là `falsy` - tức là, một đối tượng có giá trị là `null` hoặc `undefined`.
> 
Ví dụ, các biểu thức sau đây đều trả về giá trị boolean false:

```js
Boolean(false); // false
Boolean(""); // false
Boolean(0); // false
Boolean(null); // false
```
Lưu ý rằng các giá trị khác false hoặc rỗng chuỗi có thể được coi là `truly` hoặc `faulty` tùy thuộc vào ngữ cảnh sử dụng của chúng trong phép so sánh boolean.

### ứng dụng

Các giá trị `truly` và `faulty` trong JavaScript thường được sử dụng trong các biểu thức logic và điều kiện trong chương trình.

Ví dụ, trong một biểu thức logic đơn giản, chúng ta có thể sử dụng các giá trị `truly` và `faulty` để kiểm tra xem một biến có giá trị hay không:

```javascript
var name = "John";
if (name) {
console.log("Hello, " + name); // Hiển thị "Hello, John"
} else {
console.log("Please enter your name");
}
```

Trong ví dụ trên, biến name có giá trị là "John", được xem là một giá trị "truly", do đó điều kiện if được đánh giá là đúng và câu lệnh trong khối if được thực thi.

Một ví dụ khác, chúng ta có thể sử dụng các giá trị "faulty" để kiểm tra xem một biến có giá trị hay không:

```js
var age;
if (age) {
console.log("Your age is " + age);
} else {
console.log("Please enter your age"); // Hiển thị "Please enter your age"
}
```

Trong ví dụ trên, biến age không được gán giá trị nào, do đó nó được xem là một giá trị "faulty". Do đó, điều kiện if được đánh giá là sai và câu lệnh trong khối else được thực thi.

Các giá trị "truly" và "faulty" cũng được sử dụng để kiểm tra tính đúng đắn của dữ liệu được nhập vào từ người dùng hoặc được trả về từ các API. Nếu một giá trị là "truly", nó được xem là dữ liệu hợp lệ và có thể được sử dụng, ngược lại, nếu nó là "faulty", thì nó được xem là dữ liệu không hợp lệ và cần được xử lý hoặc báo lỗi.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain difference between `.forEach` & `.map` - `.find()`, `.findIndex()` & `.filter()`
### `.forEach` & `.map`
Cả hai phương thức `.forEach` và `.map` đều được sử dụng để lặp qua các phần tử trong một mảng trong JavaScript. Tuy nhiên, có một số sự khác biệt quan trọng giữa chúng.

#### - Phương thức `.forEach()` được sử dụng để lặp qua một mảng và thực hiện một hành động cho mỗi phần tử. Nó sẽ không trả về một mảng mới, mà chỉ thực hiện một hành động trên mỗi phần tử.
Ví dụ:
```js
const arr = [1, 2, 3, 4];

arr.forEach((num) => console.log(num * 2));

// Kết quả sẽ là:
2
4
6
8
```

#### - Phương thức `.map()` cũng được sử dụng để lặp qua một mảng, nhưng nó trả về một mảng mới được tạo ra bằng cách thực hiện một hành động trên mỗi phần tử của mảng ban đầu. Kết quả trả về là một mảng mới với các giá trị được biến đổi theo cách mong muốn.
Ví dụ:
```js
const arr = [1, 2, 3, 4];

const newArr = arr.map((num) => num * 2);

console.log(newArr);

// Kết quả sẽ là:
[2, 4, 6, 8]
```
---
> - Vì `.map()` trả về một mảng mới, nên nó thường được sử dụng để biến đổi dữ liệu trong mảng ban đầu để tạo ra một mảng mới với các giá trị được xử lý theo cách khác nhau.
> - Tóm lại, `.forEach()` và `.map()` đều là phương thức lặp qua một mảng trong JavaScript. Tuy nhiên, `.forEach()` được sử dụng để thực hiện mutable trên mỗi phần tử trong mảng ban đầu, trong khi đó, `.map()` được sử dụng để biến đổi các giá trị trong mảng ban đầu và trả về một mảng mới.
> - Về mặt hiệu suất, phương thức .map() có thể nhanh hơn phương thức `.forEach()`, tuy nhiên sự khác biệt không đáng kể và phụ thuộc vào từng trường hợp sử dụng.
> 
---
### `.find()`, `.findIndex()` và `.filter()`
Trong JavaScript, `.find` và `.filter` đều là các phương thức cho phép bạn tìm kiếm và lọc các phần tử trong một mảng.

#### - Phương thức `.find` sẽ trả về giá trị đầu tiên trong mảng. Nếu không có phần tử nào thỏa mãn điều kiện, phương thức sẽ trả về `undefined`.
#### - Phương thức `.findIndex` sẽ trả về chỉ số của giá trị đầu tiên trong mảng. Nếu không có phần tử nào thỏa mãn điều kiện, phương thức sẽ trả về `-1`.
#### - Phương thức `.filter` sẽ trả về một mảng mới chứa tất cả các phần tử trong mảng ban đầu.

> - Tóm lại, `.find` được sử dụng để tìm kiếm và trả về phần tử đầu tiên trong mảng thỏa mãn điều kiện, trong khi `.filter` được sử dụng để lọc các phần tử trong mảng theo điều kiện và trả về một mảng mới chứa các phần tử đó.
> - Nếu so sánh 2 phương thức này về cấu trúc code, thì phương thức `.find` thường sẽ nhanh hơn phương thức `.filter`, vì `.find` sẽ chỉ trả về phần tử đầu tiên trong mảng thỏa mãn điều kiện, trong khi `.filter` sẽ duyệt qua toàn bộ mảng và trả về một mảng mới.

[[↑] Back to top](#table-of-contents)

### 🧠 Explain Closure in Javascript
Closure trong JavaScript là một tính năng cho phép một hàm có thể truy cập và sử dụng các biến bên ngoài phạm vi của nó, bao gồm các biến được định nghĩa trong hàm cha hoặc các biến toàn cục.

Khi một hàm được định nghĩa bên trong một hàm khác, hàm con được tạo ra sẽ được kết nối với phạm vi của hàm cha, do đó các biến bên ngoài phạm vi của hàm con vẫn có thể được truy cập và sử dụng.

```js
function greeting(name) {
  var message = "Hello, " + name + "!";
  function sayHello() {
    console.log(message);
  }
  return sayHello;
}

var helloBob = greeting("Bob");
helloBob(); // "Hello, Bob!"
```

> Các đặc tính của closure trong JavaScript bao gồm:
> - Closure cho phép các biến nằm trong phạm vi của một hàm cha có thể được sử dụng bởi các hàm con bên trong đó.
> - Closure được tạo ra khi một hàm bên trong được tạo ra bên trong một hàm khác và có thể truy cập các biến của hàm cha.
> - Các biến bên ngoài phạm vi của hàm con được giữ lại bởi closure, do đó chúng có thể được sử dụng lại sau khi hàm cha đã thực thi xong.
> - Closure giúp cho các biến và hàm được sử dụng lại và tái sử dụng một cách dễ dàng, làm cho mã JavaScript trở nên dễ đọc và dễ bảo trì hơn.
> - Việc sử dụng closure cần được cẩn thận để tránh gây ra các vấn đề về hiệu suất và quản lý bộ nhớ, do closure giữ các biến trong bộ nhớ, dẫn đến tiêu tốn bộ nhớ và tăng thời gian hoạt động của chương trình.
> - Closure là một tính năng quan trọng của JavaScript và được sử dụng rộng rãi trong nhiều thư viện và khung làm việc của JavaScript.

[[↑] Back to top](#table-of-contents)

### 🧠 Explain Promise in Javascript
Promise trong JavaScript là một đối tượng được sử dụng để xử lý các tác vụ bất đồng bộ. Nó là một cơ chế để quản lý và kiểm soát các hoạt động không đồng bộ như gọi API, tải tệp, truy vấn cơ sở dữ liệu, và các hoạt động khác mà có thể mất thời gian để hoàn thành.

Promise có ba trạng thái chính:

<b>1. Pending (Chờ)</b>: Trạng thái ban đầu khi một Promise được tạo. Tại thời điểm này, tác vụ bất đồng bộ chưa hoàn thành.

<b>2.Resolved - Fulfilled (Thành công)</b>: Trạng thái này xảy ra khi tác vụ bất đồng bộ hoàn thành thành công. Dữ liệu kết quả của tác vụ sẽ được trả về.

<b>3. Rejected (Từ chối)</b>: Trạng thái này xảy ra khi tác vụ bất đồng bộ gặp lỗi hoặc không thể hoàn thành. Một lỗi (error) sẽ được trả về.

Promise có cú pháp như sau:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Xử lý tác vụ bất đồng bộ ở đây
  if (/* tác vụ thành công */) {
    resolve("Kết quả thành công");
  } else {
    reject("Lỗi xảy ra");
  }
});

myPromise
  .then((result) => {
    console.log("Thành công: " + result);
  })
  .catch((error) => {
    console.error("Lỗi: " + error);
  });
```

Trong ví dụ trên, `myPromise` là một Promise. Nó có thể chuyển từ trạng thái "Chờ" sang "Thành công" bằng cách sử dụng `resolve`, hoặc sang trạng thái "Từ chối" bằng cách sử dụng `reject`. Sau đó, bạn có thể sử dụng `.then()` để xử lý kết quả thành công hoặc `.catch()` để xử lý lỗi.

Promise giúp mã nguồn xử lý các tác vụ bất đồng bộ trở nên dễ đọc hơn và quản lý tốt hơn, bởi vì nó loại bỏ sự lồng ghép (nesting) nhiều callback và giúp tạo ra một luồng xử lý tuyến tính hơn.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Callback in Javascript

Callback trong JavaScript là một hàm (function) được truyền làm tham số cho một hàm khác và được gọi sau khi hàm đó hoàn thành công việc của nó.

Callback thường được sử dụng để xử lý các tác vụ bất đồng bộ, như đọc/ghi tệp, gọi API, hoặc xử lý sự kiện, mà có thể mất thời gian để hoàn thành.<br />
Callback giúp đảm bảo rằng mã nguồn không bị chặn (blocked) và có thể tiếp tục thực thi trong khi tác vụ bất đồng bộ đang chạy.<br />
Callback có thể được truyền dưới dạng hàm nặc danh (anonymous function) hoặc hàm đã được định nghĩa trước, tùy thuộc vào tình huống cụ thể.<br />
Callback là một cơ chế quan trọng trong lập trình JavaScript và được sử dụng rộng rãi để xử lý các tác vụ không đồng bộ.



```javascript
function fetchData(callback) {
  // Giả lập việc gọi API bất đồng bộ
  setTimeout(() => {
    const data = "Dữ liệu từ máy chủ";
    callback(data); // Gọi callback khi tác vụ hoàn thành
  }, 1000);
}

function processData(data) {
  console.log("Dữ liệu đã xử lý: " + data);
}

fetchData(processData); // Truyền hàm processData làm callback

```

Trong ví dụ này, `fetchData` là một hàm có nhiệm vụ giả lập việc gọi API bất đồng bộ và sau đó gọi callback `processData` khi tác vụ hoàn thành.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Hoisting in Javascript

Hoisting là một cơ chế của JavaScript trong đó các biến và hàm được khai báo được di chuyển lên đầu phạm vi hiện tại của chúng.<br/> 
Điều này có nghĩa là các biến và hàm có thể được sử dụng ngay cả khi chúng được khai báo sau khi chúng được sử dụng.

Cụ thể, hoisting có các đặc điểm sau:
**1. Biến được khai báo với var**: Khi bạn sử dụng từ khóa var để khai báo biến, biến đó sẽ được nâng lên (hoisted) lên đầu phạm vi của nó, tức là nó được đưa lên phía trên mọi mã nguồn khác trong phạm vi đó.

Ví dụ:
```javascript
console.log(x); // undefined
var x = 5;
```

Trong ví dụ trên, biến `x` được nâng lên đầu phạm vi của nó và có giá trị `undefined` khi bạn cố gắng truy cập nó trước khi gán giá trị.

**2. Hàm được định nghĩa với function**: Các hàm được định nghĩa bằng từ khóa `function` cũng được nâng lên lên đầu phạm vi của nó, nghĩa là bạn có thể gọi hàm trước khi nó được định nghĩa trong mã nguồn.

Ví dụ:
```javascript
myFunction(); // "Hello, world!"

function myFunction() {
  console.log("Hello, world!");
}
```

Tuy hoisting có tính năng này, tuy nhiên, khuyến cáo là nên khai báo biến và định nghĩa hàm trước khi sử dụng để tạo mã nguồn dễ đọc và hiểu hơn.<br/>
Sử dụng `let` và `const` thay thế cho `var` cho biến để tránh một số lỗi logic liên quan đến hoisting, và sử dụng các quy tắc tốt trong việc đặt thứ tự khai báo biến và hàm trong mã nguồn.

> Hoisting có một số ưu điểm, bao gồm:
> - Giúp code dễ đọc và dễ hiểu hơn: Hoisting cho phép bạn khai báo các biến và hàm ở bất cứ đâu trong phạm vi hiện tại của chúng. Điều này giúp code dễ đọc và dễ hiểu hơn.
> - Giúp tránh lỗi: Hoisting giúp tránh lỗi do sử dụng biến hoặc hàm trước khi chúng được khai báo.

> Tuy nhiên, hoisting cũng có một số nhược điểm, bao gồm:
> - Có thể gây hiểu lầm: Hoisting có thể gây hiểu lầm nếu bạn không hiểu cách thức hoạt động của nó.
> - Có thể gây ra lỗi: Hoisting có thể gây ra lỗi nếu bạn sử dụng biến hoặc hàm theo cách không mong muốn.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Design Pattern


Design pattern là một kỹ thuật giải pháp chung cho một vấn đề chung trong lập trình. Các design pattern được mô tả dưới dạng các mẫu code có thể được sử dụng lại trong các ứng dụng khác nhau.

Design Pattern thường chia thành các loại cơ bản sau:

<b>1. Creational Patterns (Mẫu tạo đối tượng)</b>: Loại mẫu này liên quan đến việc tạo ra đối tượng. Các mẫu trong loại này giúp kiểm soát quá trình tạo đối tượng và đảm bảo rằng mã nguồn dễ mở rộng và bảo trì. Ví dụ: Singleton, Factory, Builder.

<b>2. Structural Patterns (Mẫu cấu trúc)</b>: Loại mẫu này tập trung vào cách các đối tượng được kết hợp lại để tạo ra các cấu trúc lớn hơn. Các mẫu trong loại này giúp bạn tạo ra các cấu trúc phức tạp bằng cách kết hợp các đối tượng một cách hiệu quả. Ví dụ: Adapter, Composite, Proxy.

<b>3. Behavioral Patterns (Mẫu hành vi)</b>: Loại mẫu này liên quan đến cách các đối tượng tương tác và trao đổi thông tin với nhau. Các mẫu trong loại này giúp bạn quản lý các mẫu tương tác phức tạp trong mã nguồn. Ví dụ: Observer, Strategy, Command.

Một số ví dụ cụ thể của Design Pattern bao gồm:

- <b>Singleton Pattern</b>: Đảm bảo rằng một lớp chỉ có một thể hiện và cung cấp một điểm truy cập toàn cục đến nó.

- <b>Factory Method Pattern</b>: Định nghĩa một giao diện cho việc tạo đối tượng, nhưng để các lớp con quyết định lớp cụ thể nào sẽ được tạo.

- <b>Observer Pattern</b>: Định nghĩa một phương thức một-đến-nhiều giữa các đối tượng để thông báo về sự thay đổi trạng thái.

Mục tiêu của Design Pattern là cung cấp một phong cách cấu trúc cho mã nguồn và giúp cải thiện tính hiệu quả, bảo trì và mở rộng của mã nguồn.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain Cookies Session Storage và Local Storage
Cookies, Session Storage và Local Storage là cách để lưu trữ dữ liệu trong trình duyệt web, nhưng chúng có sự khác nhau về cách hoạt động, thời gian tồn tại, và mục đích sử dụng:

| Tính năng        | Cookies  | Session Storage  | Local Storage  |
| -------          | --- | --- | --- |
| Tính năng        | Máy chủ web | Bộ nhớ cục bộ của trình duyệt | Bộ nhớ cục bộ của trình duyệt |
| Thời hạn sử dụng | Tùy chỉnh | Kết thúc phiên trình duyệt | Không giới hạn (trừ khi người dùng xóa thủ công) |
| Kích thước       | 4kb | 5MB | 10MB |
| Sự riêng tư      | Có thể truy cập được bởi các trang web khác | Có thể truy cập được bởi trang web hiện tại | Có thể truy cập được bởi trang web hiện tại |
| Sử dụng          | Lưu trữ dữ liệu nhỏ, chẳng hạn như thông tin đăng nhập, trạng thái mua sắm, v.v. | Lưu trữ dữ liệu tạm thời, chẳng hạn như danh sách các mặt hàng đã xem | Lưu trữ dữ liệu lâu dài, chẳng hạn như danh sách yêu thích, cài đặt, v.v. |

>1. Cookies:
>- Cookies là một cách lưu trữ dữ liệu nhỏ dưới dạng chuỗi văn bản trên máy tính của người dùng.
>- Cookies được gửi cùng với mỗi yêu cầu HTTP đến máy chủ, điều này có thể làm cho yêu cầu trở nên chậm nếu dữ liệu lớn.
>- Cookies có thời gian sống và có thể được đặt để tồn tại trong một số ngày hoặc thậm chí là lâu hơn.
>- Cookies thường được sử dụng để lưu trữ thông tin đăng nhập, theo dõi hoạt động trang web, và mục đích theo dõi.

>2. Session Storage:
>- Session Storage là một cách lưu trữ dữ liệu tương tự như Cookies, nhưng dữ liệu chỉ tồn tại trong suốt phiên làm việc của trình duyệt (session).
>- Dữ liệu trong Session Storage không được gửi cùng với mỗi yêu cầu HTTP đến máy chủ và chỉ tồn tại trong cửa sổ hoặc tab trình duyệt mà bạn đang làm việc. Khi bạn đóng cửa sổ hoặc tab, dữ liệu sẽ bị xóa.

>3. Local Storage:
>- Local Storage cũng giống như Session Storage, nhưng dữ liệu tồn tại lâu hơn, vượt qua phiên làm việc và cả khi bạn tắt máy tính và mở lại trình duyệt.
>- Dữ liệu trong Local Storage không bao giờ được tự động xóa, trừ khi bạn xóa nó bằng mã JavaScript hoặc bằng tay thông qua cài đặt trình duyệt.

Lựa chọn giữa Cookies, Session Storage và Local Storage phụ thuộc vào mục đích sử dụng:
- Sử dụng `Cookies` khi bạn cần lưu trữ thông tin trên máy chủ và truy cập từ mọi nơi, hoặc khi bạn cần lưu trữ thông tin trong thời gian dài hơn.
- Sử dụng `Session Storage` khi bạn cần lưu trữ thông tin chỉ trong suốt phiên làm việc của trình duyệt, chẳng hạn như trong quá trình điều hướng giữa các trang web hoặc tab.
- Sử dụng `Local Storage` khi bạn cần lưu trữ thông tin vượt qua phiên làm việc, ngay cả khi trình duyệt đã được tắt và mở lại.

[[↑] Back to top](#table-of-contents)

## 🧠 Explain BEM? Naming standard CSS follow BEM

### BEM là gì?
BEM là viết tắt của cụm `Block – Element – Modifier`, là tiêu chuẩn quy ước đặt tên cho các tên lớp CSS. BEM giúp việc lập trình Front-end trở nên dễ hiểu, dễ đọc hơn, dễ làm việc và dễ mở rộng cũng như bảo trì khi làm việc với CSS.
Việc đặt tên theo tiêu chuẩn giúp các lập trình viên frontend hiểu được đoạn code đó có nghĩa là gì, nó thực hiện nhiệm vụ gì? Từ đó những lập tình viên khác khi đọc code của họ cũng hiểu được bạn đang làm gì, từ đó dễ dàng phân tích, thay đổi và quản lý.

### Tại sao nên dùng BEM?
Đối với những dự án nhỏ thì BEM có thể chưa cần đến, tuy nhiên các dự án lớn và làm việc nhóm thì BEM rất quan trọng.
- <b>Giúp cho team làm việc với nhau dễ dàng hơn</b>: Khi làm Teamwork với nhau, mỗi người đều sẽ có một cách đặt tên class riêng và sẽ bị conflict với nhau. Việc sử dụng BEM sẽ bị loại bỏ vấn đề này vì có cấu trúc rõ ràng và dễ dàng tuân thủ khi sử dụng.
- <b>Modules</b>: Các class của mỗi block sẽ không bị ảnh hưởng gì bởi các yếu tố khác, vì thế bạn sẽ không cần quá lo CSS của class này sẽ gây ảnh hưởng đến class khác.
- <b>Tái sử dụng lại</b>: Bạn có thể soạn các block riêng biệt và sử dụng lại chúng một cách thuận tiện và giảm số lượng code CSS.
- <b>Cấu trúc</b>: BEM cung cấp cho CSS một cấu hình vững chắc, đơn giản và rất dễ hiểu.

### Quy ước đặt tên của BEM

```css
.block {} /* Block */
.block__element {} /* Element */
.block--modifier {} /* Modifier */
```
<b>1. Block</b>: Là một thành phần của trang web hay ứng dụng đó, các thành phần của DOM cũng có thể là các block. Block ở đây thường là các thành phần header, body, content, footer. Ví dụ section td bên dưới tập hợp các block sau:
- `.td__container` làm nhiệm vụ cân max width và padding left right.<br/>
  `.td__inner` làm nhiệm vụ cân padding top bottom và điểm bám cho các element absolute. VD: chỉnh một button…<br/>
  `.td__header` chứa Sub-title.<br/>
  `.td__content` chứa Headline và Description.<br/>
  `.td__footer` chứa button CTA.<br/>

Các prefix của các class đều là td giúp chúng ta có thể nhận diện section khi muốn update mục tương ứng trong css.

<b>2. Elements</b>: Là một thành phần của một block và sẽ không tồn tại độc lập mà không có block vì được đặt bên trong nó, và chúng phụ thuộc vào parent block của nó. Trong BEM, các phần tử được biểu thị bằng dấu gạch dưới kép `__`.
- `.td__headline` là Text cỡ lớn. Style thường là H1 hoặc H2.<br/>
  `.td__intro`, `.td__description` làm mô tả content.<br/>
  `.td__image` chứa ảnh.<br/>
  `.td__button` với style riêng cho button trong section này.<br/>

<b>3. Modifers</b>: Được dùng để thao tác thay đổi cách hiển thị trên block hoặc phần tử. Ví dụ mình muốn tạo thêm một block `.block__elem` khác nữa và muốn làm nổi bật nó thì sẽ thêm một class `.block__elem--hightlight` để tạo sự khác biệt đó.

### Lợi ích khi sử dụng BEM
- Style của block không phụ thuộc vào các phần tử khác trên một trang, vì vậy bạn sẽ không bao giờ gặp vấn đề từ việc xếp tầng. Bạn cũng có thể chuyển các block từ dự án đã hoàn thành của mình sang các dự án mới.
- Có thể tạo ra các block độc lập, xây dựng thành một thư viện các block để tái sử dụng chúng. Điều này sẽ giúp cho CSS của bạn trở nên hiệu quả hơn và làm giảm lượng code CSS mà bạn sẽ phải bảo trì.
- BEM cung cấp cho code CSS của bạn một cấu trúc vững chắc mà vẫn đơn giản và dễ hiểu.

### Quy tắc, cách sử dụng BEM trong Block, Element, Modifier
<i>ĐỐI VỚI BLOCK</i>
<h4><b>Quy tắc đặt tên</b></h3>
- Tên của block có thể bao gồm các chữ cái Latinh, chữ số và cả dấu gạch ngang
- Tạo CSS class: thêm một tiền tố ở phía trước. VD như: .block
- Bất kỳ node DOM nào cũng có thể là một block nếu như nó có một class name 

VD như: `<div class=”block”>…</div>`

<h4><b>Cách sử dụng trong CSS</b></h4>
- Chỉ sử dụng bộ chọn của class
- Không dùng tên thẻ hoặc id
- Không phụ thuộc vào các block/element trên 1 trang

VD như: .block { color: #042; }

<i>ĐỐI VỚI ELEMENT</i>
<h4><b>Quy tắc đặt tên</b></h4>
- Tên Element có thể bao gồm các chữ số, chữ cái Latinh, dấu gạch ngang, gạch dưới.
- Tạo class CSS: tên block cộng với 2 dấu gạch dưới và tên Element.

VD như: .block__elem

- Bất kỳ một node DOM nào trong một block cũng đều có thể là một element
- Trong một block nhất định, tất cả các element cũng đều bằng nhau về mặt ngữ nghĩa

```html
<div class=”block”>
    …
    <span class=”block__elem”> </span>
</div>
```

<h4><b>Cách sử dụng trong CSS</b></h4>

- Chỉ sử dụng được bộ chọn class
- Không thể sử dụng tên thẻ hoặc id
- Không phụ thuộc vào các block/ element trên các trang mạng khác


```css
Nên: 
    .block__elem { color: #042; }
Không nên: 
    .block .block__elem { color: #042; }
    div.block__elem { color: #042; }
```

<i>ĐỐI VỚI MODIFIER</i>
<h4><b>Quy tắc đặt tên</b></h4>
- Tên của Modifier có thể gồm các chữ cái Latinh, dấu gạch ngang, chữ số và dấu gạch dưới
- Tạo class CSS: tên của block hoặc element cộng hai dấu gạch ngang, cộng với tên của Modifier
- Dấu cách trong các Modifier dài sẽ được thay thế bằng dấu gạch ngang.


```css
.block–mod { }
.block__elem–mod { }
.block–color-black { }
.block–color-red { }
```

- Modifier là tên class mà bạn thêm vào node DOM block/ element
- Tăng thêm các Modifier class vào các nhóm block/ element mà chúng ta cần sửa đổi và giữ lại class ban đầu của block/element đó.

VD như: <br/>
```html
Nên: 
    <div class=”block block–mod”>…</div>
    <div class=”block block–size-big block–shadow-yes”>…</div>
Không nên: 
    <div class=”block–mod”>…</div>
```

<h4><b>Cách sử dụng trong CSS</b></h4>
- Sử dụng Modifier class với bộ CSS


```css
.block–hidden { }
```

- Thay đổi các element dựa trên các block có chứa modifier

```css
.block–mod .block__elem { }
```

- Element có Modifier

```css
.block__elem–mod { }
```

### Một số lưu ý khi sử dụng BEM

BEM không có khả năng phản ánh cấu trúc lồng nhau của các block và các element. Giả sử: Một block có chứa element 1, element 1 chứa element 2, element 2 chứa element 3. Khi đó, tên của class của block và element nên đặt như sau:

HTML
```html
<div class=”block”>
    <div class=”block__elem1″>
        <div class=”block__elem2″>
            <div class=”block__elem3″></div>
        </div>
    </div>
</div>
```

CSS
```css
.block {}
.block__elem1 {}
.block__elem2 {}
.block__elem3 {}
```

Đặt class như vậy, sẽ làm cho các element chỉ phục thuộc vào với block mà thôi. Sau này, nếu bạn muốn thay đổi giao diện, bạn sẽ có thể dễ dàng di chuyển vị trí của các element trong block cũng như cấu trúc của block DOM lúc này tuy đã thay đổi nhưng bạn không cần quá lo lắng về việc sửa code CSS ban đầu.

[[↑] Back to top](#table-of-contents)