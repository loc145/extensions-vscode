Trong Vue.js, khi sử dụng directive `v-for` để render một danh sách, thêm `:key` vào mỗi phần tử trong danh sách là cần thiết vì nó giúp Vue xác định các phần tử riêng biệt trong danh sách và quản lý sự thay đổi của chúng một cách hiệu quả. Dưới đây là một ví dụ để chứng minh sự cần thiết của `:key` trong list rendering:

Giả sử bạn có một mảng `users` chứa các đối tượng người dùng:

```javascript
data() {
  return {
    users: [
      { id: 1, name: 'John' },
      { id: 2, name: 'Jane' },
      { id: 3, name: 'Bob' }
    ]
  };
}
```

Và bạn muốn hiển thị tên của từng người dùng trong danh sách:

```html
<ul>
  <li v-for="user in users">{{ user.name }}</li>
</ul>
```

Trong trường hợp này, Vue sẽ sử dụng chỉ mục của mỗi phần tử trong mảng làm key mặc định. Tuy nhiên, sử dụng chỉ mục làm key có thể gây ra một số vấn đề khi danh sách thay đổi. Ví dụ, nếu bạn xóa một phần tử ở vị trí thứ hai của mảng `users`:

```javascript
this.users.splice(1, 1);
```

Khi đó, Vue sẽ không thể nhận ra rằng phần tử bị xóa là phần tử thứ hai trong danh sách, mà chỉ biết rằng một phần tử đã bị xóa. Điều này có thể gây ra lỗi hiển thị không chính xác và các vấn đề liên quan khác.

Để giải quyết vấn đề này, chúng ta cần cung cấp một key duy nhất cho mỗi phần tử trong danh sách. Trong trường hợp này, chúng ta có thể sử dụng thuộc tính `id` của mỗi đối tượng người dùng làm key:

```html
<ul>
  <li v-for="user in users" :key="user.id">{{ user.name }}</li>
</ul>
```

Bằng cách thêm `:key="user.id"`, Vue sẽ theo dõi và cập nhật danh sách một cách chính xác khi có sự thay đổi. Khi một phần tử bị xóa, Vue sẽ xác định phần tử cần xóa dựa trên key và cập nhật giao diện người dùng tương ứng.

Tóm lại, việc thêm `:key` vào list rendering `v-for` là cần thiết để đảm bảo rằng Vue có thể xác định và quản lý các phần tử riêng biệt trong danh sách một cách chính xác, đồng thời đảm bảo hiệu suất và tính nhất quán của ứng dụng Vue.js.
