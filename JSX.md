# Hướng dẫn JSX

Xem khai báo biến dưới đây

```sh 
const element = <h1>Hello, world!</h1>; 
```

Đây không phải là cú pháp của 1 chuỗi cũng như của HTML

Nó gọi là JSX và nó là cú pháp mở rộng của JS. Chúng tôi khuyên bạn nên dùng nó với React để mô tả giao diện người dùng trông như thế nào.
JSX có thể nhắc bạn về 1 ngôn ngữ mẫu, nhưng nó đi kèm với toàn bộ sức mạnh của JS

JSX xuất ra React "Element". Chúng ta sẽ tìm hiểu cách rendering chúng cho DOM trong phần tiếp theo. Dưới đây, bạn có thể tìm hiểu cơ bản về JSX, cần thiết cho sự bắt đầu

### Why JSX?

JSX thực tế là rendering logic vốn đã ghép đôi với UI logic khác: Cách sử lý sự kiện, cách thay đổi trạng thái thời gian, và cách chuẩn bị dữ liệu hiển thị

Thay vì tách nhân tạo technologies bởi đánh dấu và logic trong file riêng biệt. React tách riêng sự liên quan với các units ghép lỏng lẻo gọi là "components" chứa cả hai.
Chúng ta sẽ quay lại components ở chương tiếp, nhưng nếu bạn không cảm thấy thoải mái đặt markup trong JS. Cuội nói chuyện này sẽ thuyết phục bạn(thằng Pete Hunt nói)

React không bắt buộc dùng JSX, nhưng hầu hết mọi người tìm sự giúp đỡ như hỗ trợ trực quan khi làm việc với UI bên trong code JS. Nó hầu như cho phép React hiển thị error và warning message hữu ích hơn

### Embedding Expressions in JSX

Trong ví dụ dưới đây, chúng ta khai báo 1 biến gọi là `name` và sau đó dùng nó trong JSX bằng cách bao nó bằng ngoạc nhọn

``` sh
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
Bạn có thể đặt bất kì biểu thức JS hợp lệ nào bên trong dấu ngoặc nhọn JSX. Ví dụ, `2 + 2`, `user.lastName`, hoặc `formatName(user)`
tất cả các biểu thức hợp lệ

Trong ví dụ dưới đây, chúng ta nhúng kết quả của việc gọi 1 hàm JS `formatName(user)`, trong 1 thẻ h1

``` sh
    function formatName(user) {
        return user.firstName + ' ' + user.lastName;
    }

    const user = {
        firstName: 'Harper',
        lastName: 'Perez'
    };

    const element = (
        <h1>
            Hello, {formatName(user)}!
        </h1>
    );

    ReactDOM.render(
        element,
        document.getElementById('root')
    );
```
Chúng ta chia JSX làm nhiều dòng để đọc cho dễ. Trong khi nó không bắt buộc, khi làm cái này chúng tôi khuyên bạn nên bao nó trong ngoạc đơn để tránh bẫy của [automatic semicolon insertion.](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi).

## Specifying Attributes with JSX

Bạn có thể dùng trích dẫn xác định chuỗi kí tự 

`const element = <div tabindex="0"></div>;`

Bạn có thể dùng ngoặc nhọn nhúng 1 biểu thức JS vào trong thuộc tính

`const element = <div><img src={user.avatarUrl}></div>;`

Đừng đặt quotes bao quanh ngoặc nhọn. Bạn có thể dùng cả 2 quotes(cho các giá trị chuỗi) or ngoặc nhọn cho các biểu thức, nhưng không dùng cả 2 thằng trong cùng 1 thuộc tính.

> **Warning**: Vì JSX giống JS hơn HTML, React DOM uses quy ước đặt tên thuộc tính theo `camelCase` thay vì đặt tên thuộc tính HTML. For example, `class` tở thành `className` trong JSX, và `tabindex` thành `tabIndex`

## Specifying Children with JSX

Nếu thẻ là rỗng, bạn có thể đóng ngay nó với />, giống XML

`const element = <img src={user.avatarUrl}  />;`

JSX có thể chứa Children

`const element = (
    <div>
        <h1>Hello</h1>
        <h2>Good morning sir</h2>
    </div>
);`

## JSX Prevents Injection Attacks

Nó là an toàn cho việc nhúng khi người dùng nhập vào trong JSX

```sh
    const title = response.potentiallyMaliciousInput;
    // This is safe:
    const element = <h1>{title} </h1>;
```

Bởi mặc định, React DOM [thoát](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-on-html) mọi giá trị đã được nhúng vào trong JSX trước khi rendering chúng ra. Vì vậy 
nó đảm bảo bạn không bao giờ bị tiêm thứ gì đó không viết rõ ràng vào ứng dụng của bạn

Mọi thứ được chuyển sang chuỗi trước khi bắt đầu rendered. Cái này giúp ngăn ngừa [XSS tấn công](https://en.wikipedia.org/wiki/Cross-site_scripting)

## JSX Represents Objects(Tương ứng là Objects)

Babel biên dịch JSX dưới lời gọi hàm `React.createElement`

Có 2 ví dụ giống nhau:

```sh
    const element = (
        <h1 className="greeting">
            Hello, world!
        </h1>
    );
```
```sh
    const element = React.createElement (
        'h1',
        {className: 'greeting'},
        'Hello World!'
    );
```

`React.createElement` thực hiện 1 vài kiểm tra giúp bạn viết bug-free code nhưng về cơ bản nó tạo 1 object giống:

```sh
    // Note: This structure is simplifed
    const element = {
        type: 'h1',
        props: {
            className: 'greeting',
            children: 'Hello World!'
        }
    };
```

Những objects này đã gọi "React elements". Bạn có thể nghĩ rằng chúng như mô tả cái bạn muốn hiển thị trên màn hình. React đọc được những objects này và dùng chúng để xây dựng DOM và giữ nó cho đến nay. 

Chúng ta sẽ tìm hiểu rendering React element to the DOM trong phần tiếp theo

> **Tip:** Chúng tôi khuyên bạn dùng `[Babel language definition](http://babeljs.io/docs/en/editors/)` cho editor của bạn vì ES6 và JSX
được đánh dấu đúng cách. Đây là website dùng `[Oceanic Next](https://labs.voronianski.com/oceanic-next-color-scheme/)` bảng phối màu tương thích với nó


