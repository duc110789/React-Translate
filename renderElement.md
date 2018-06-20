# Rendering Elements

>### Elements là các khối nhỏ nhất được xây dựng của React app 

1 Element diễn tả cái bạn muốn nhìn thấy trên màn hình

`const element = <h1>Hello, World!</h1>`;

Không giống DOM elements trên trình duyệt, React elements là các đối tượng đơn giản và rẻ để tạo ra.
React DOM chú ý cập nhật DOM để phù hợp với các React elements

> **Note**: Người ta thường nhầm lẫn elements với khái niệm rộng rãi hơn về components. Chúng tôi sẽ hướng dẫn component vào phần sau.
Elements là các components 'made of', và chúng tôi khuyên bạn đọc phần này trước khi nhảy về phía trước.

## Rendering an Element into the DOM(Rendering 1 element trong DOM)

Giả sử có 1 thẻ `<div>` trong HTML

`<div id="root"></div>`

Chúng ta gọi là 1 "root" DOM node bởi vì mọi thứ bên trong nó được quản lý bởi React DOM

Ứng dụng xây dựng với React thường có 1 single root DOM node. Nếu bạn tích hợp React bên trong ứng dụng hiện có, bạn có thể có nhiều
root DOM node như bạn thích 

Render 1 React element trong 1 root DOM node, chuyển cả 2 đến ReactDOM.render()

```sh
    const element = <h1>Hello, World!</h1>
    ReactDOM.render(
        element,
        document.getElementById('root')
    );
```

## Updating the rendered Element

React element là thay đổi. Mỗi lần bạn tạo 1 element, bạn không thể thay đổi its children hoặc thuộc tính.
1 element giống như khung hình duy nhất trong 1 bộ phim nó đại diện cho UI tại thời điểm nhất định.

Với kiến thức của chúng ta hiện tại, cách duy nhất để cập nhật UI là tạo 1 element, và chuyển nó đến ReactDOM.render()

Xem xét ticking clock ví dụ sau đây

```sh
    function tick() {
        const element = (
            <div>
                <h1>Hello, World !</h1>
                <h2>It is {new Date().toLocaleTimeString()}.</h2>
            </div>
        );
        ReactDOM.render(
            element,
            document.getElementById('root');
        );
    }
    setInterval(tick, 1000);
```

Nó gọi `ReactDOM.render()` mỗi giây từ gọi lại hàm setInterval()

> **Note:** Trong thực hành, hầu hết ứng dụng React chỉ gọi 1 lần hàm ReactDOM.render(). Trong phần tiếp theo chúng ta sẽ học cách
cách đóng gói trong stateful components như thế nào. Chúng tôi khuyên bạn không nên bỏ qua các chủ đề bởi vì chúng xây dựng quan hệ với nhau

### React Only Updates What’s Necessary(React chỉ updates những cái cần thiết)

React DOM so sánh element với its children tới 1 phần trước, và chỉ ứng dụng DOM updates cần thiết để đưa DOM tới trạng thái cần thiết.

Bạn có thể xác minh bằng inspecting ở ví dụ trước với tools trình duyệt

Even though(mặc dù) chúng ta tạo 1 element mô tả toàn bộ cây giao diện người dùng trên mọi tick, chỉ text node của nội dung có sự thay đổi được cập nhật bởi React DOM

Kinh nghiệm của tôi, nghĩ về cách có thể xem giao diện bất kì thời điểm cụ thể nào hơn là làm thế nào thay đổi thời gian, loại bỏ toàn bộ 1 class lỗi.
