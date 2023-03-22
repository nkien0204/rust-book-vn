# Generic, Traits và Lifetimes

Hầu hết các ngôn ngữ lập trình hiện nay đều có các công cụ để giảm thiểu việc trùng lặp code. Đối với Rust, ta có *generics*: có thể coi là một kiểu dữ liệu dạng tổng quát thay thế cho các kiểu dữ liệu thông thường.

Các tham số truyền vào trong hàm hoàn toàn có thể là các *generic*, khi đó ta sẽ không cần phải suy nghĩ quá nhiều về kiểu dữ liệu của tham số nữa (vd: `i32` hay `String`). Nếu bạn để ý, `Option<T>` trong chương 6, `Vec<T>` và `HashMap<K,V>` ở chương 8 hay `Result<T,E>` ở chương 9 đều sử dụng *generic*.

Trong chương này, ta sẽ học cách định nghĩa kiểu dữ liệu, hàm và phương thức sử dụng *generic*!

Đầu tiên, ta sẽ tìm hiểu cách giảm trùng lặp code khi sử dụng generic function cho các hàm chỉ có sự khác biệt về kiểu dữ liệu truyền vào. Đồng thời tìm hiểu thêm về generic trong struct và enum.

Tiếp theo, *traits* sẽ là công cụ giúp tạo ra các phương thức tổng quát và trừu tượng (rất giống *interface* trong Java). 

Trong Rust, generic type là một kiểu dữ liệu có thể chấp nhận nhiều kiểu dữ liệu khác nhau. Ví dụ, một generic type như `Vec<T>` có thể chứa bất kỳ kiểu dữ liệu nào, từ số nguyên đến chuỗi hay các struct. Tuy nhiên, đôi khi chúng ta muốn giới hạn kiểu dữ liệu được chấp nhận bởi generic type này để chỉ chấp nhận những kiểu dữ liệu có hành vi cụ thể.

Điều này có thể được đạt được bằng cách kết hợp traits và generic types. Trong Rust, traits là một cách để mô tả các hành vi của một kiểu dữ liệu. Bằng cách kết hợp một trait với một generic type, chúng ta có thể giới hạn generic type đó chỉ chấp nhận các kiểu dữ liệu có hành vi tương ứng với trait đó.

Ví dụ, nếu chúng ta muốn tạo một generic type chỉ chấp nhận các kiểu dữ liệu có thể sắp xếp được, chúng ta có thể sử dụng trait Ord của Rust để giới hạn kiểu dữ liệu được chấp nhận bởi generic type này. Bằng cách này, chúng ta sẽ không thể sử dụng generic type này với các kiểu dữ liệu không thể sắp xếp được như chuỗi hay struct không hỗ trợ tính năng sắp xếp.

Cuối cùng, ta sẽ bàn về *lifetimes*: Lifetime trong Rust là một khái niệm được sử dụng để quản lý việc sử dụng bộ nhớ động trong khi lập trình. Khi một biến được tạo ra, nó được lưu trữ trong bộ nhớ động của máy tính. Tuy nhiên, khi biến đó không còn được sử dụng, bộ nhớ đó cần được giải phóng để sử dụng cho các mục đích khác.

Trong Rust, các biến và các giá trị của chúng có thể có các lifetime khác nhau. Lifetime đại diện cho thời gian mà một giá trị được lưu trữ trong bộ nhớ. Khi một biến được tạo ra, nó được gắn kèm với một lifetime, được biểu thị bằng ký tự `'a` (với `'a` có thể được thay bằng bất kỳ ký tự nào khác).

Lifetime cho phép Rust xác định thời điểm mà một biến cần được giải phóng khỏi bộ nhớ động. Điều này giúp tránh các lỗi liên quan đến việc sử dụng bộ nhớ không hợp lý, chẳng hạn như truy cập đến vùng bộ nhớ đã được giải phóng hoặc truy cập đến vùng bộ nhớ không hợp lý. 

## Sử dụng hàm để tránh lặp code
Cùng bắt đầu với đoạn code sau:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-01/src/main.rs:here}}
```

<span class="caption">Listing 10-1: Tìm số lớn nhất trong chuỗi số</span>

Mảng các số được lưu bởi biến `number_list` và gán phần tử đầu tiên vào biến `largest`. Sau đó duyệt qua toàn bộ mảng, nếu số hiện tại lớn hơn số được lưu ở `largest`, tiến hành cập nhật giá trị lớn hơn đó vào `largest`. Trong bài này kết quả nhận được sẽ là 100.

Giả sử có thêm một chuỗi số thứ 2, nhiệm vụ bây giờ là tìm số lớn nhất trong chuối số thứ 2 này. Vì vậy, ta có thể copy đoạn logic vừa làm phía trên xuống để áp dụng cho chuỗi thứ 2.
<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-02/src/main.rs}}
```

<span class="caption">Listing 10-2: Tìm số lớn nhất trong từng chuỗi số</span>

Mặc dù nó hoạt động ổn, nhưng đây là một cách viết code tồi khi đoạn logic trên bị lặp lại, ta sẽ cần đưa chúng vào trong một hàm.

Tạo một hàm có tên `largest`. Gọi hàm này mỗi khi cần tìm số lơn nhất của chuỗi số.
<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-03/src/main.rs:here}}
```

<span class="caption">Listing 10-3: Sử dụng hàm để tránh lặp code</span>

Cách làm trên giúp giảm thiểu việc lặp code, tuy nhiên nó chỉ tốt khi các chuỗi mà ta làm việc có kiểu `i32`. Khi kiểu dữ liệu khác đi, (giả sử `char` hoặc `float`) hàm này sẽ không thể sử dụng, lúc này *generic* sẽ phát huy hiệu quả.

[ch18]: ch18-00-patterns.html