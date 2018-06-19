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
Chúng ta chia JSX làm nhiều dòng để đọc cho dễ. Trong khi nó không bắt buộc, khi làm cái này chúng tôi khuyên bạn nên bao nó trong ngoạc đơn để tránh bẫy của automatic semicolon insertion.
