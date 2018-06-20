# Components and Props

>### Components cho phép bạn chia nhỏ UI độc lập, mục đích để quản lý và tái sử dụng nó. Trang này giới thiệu về khái niệm components. Bạn có thể tìm ở [detailed component API reference here.](https://reactjs.org/docs/react-component.html).

Khái niệm, components giống như JS function. Họ cho phép đầu vào tùy ý(gọi là "props") và trả về React elements hiển thị trên màn hình.


### Functional and Class Components

Cách đơn giản nhất để định nghĩa 1 component là viết 1 JS function:

```sh
function Welcom(props) {
    return <h1>Hello, {props.name}</h1>
}
```

Hàm này là 1 Reac component hợp lệ bởi vì nó thừa nhận 1 đối số props đơn (viết tắt của thuộc tính) với dữ liệu và trả về 1 element React.
Chúng ta gọi như component "functional" bởi vì chúng theo nghĩa đen là JS functions

Bạn có thể dùng 1 [ES6 class](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) để định nghĩa 1 component

```sh
class Welcome extends React.Component {
    render (
        return <h1>Hello, {this.props.name}</h1>;
    )
}
```

Trên đây là 2 components tương đương từ quan điểm của React

Classe có vài chức năng được thêm chúng ta sẽ thảo luận trong chương tiếp theo. Sau đó, chúng ta sẽ dùng functional components
cho sự đồng nhất của chúng.
