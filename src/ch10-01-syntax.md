## Generic Data Types

Chúng ta có thể sử dụng generics để định nghĩa các hàm, struct hay một số kiểu dữ liệu khác. Cùng xem một vài ví dụ sau.

### Định nghĩa hàm

Khi định nghĩa một hàm, ta sẽ đặt generics vào trong phần signature của hàm đó. Lúc đó hàm này sẽ flexible hơn mà đáp ứng được nhiều kiểu dữ liệu hơn, qua đó tránh tình trạng lặp code.

Quay trở lại với hàm `largest`, Listing 10-4 ta có 2 hàm riêng biệt để tìm phần tử lớn nhất trong mảng lần lượt với kiểu `i32` và `char`.

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-04/src/main.rs:here}}
```

<span class="caption">Listing 10-4: Không sử dụng generics để định nghĩa hàm</span>

Có thể dễ dàng nhận thấy 2 hàm trên đều có cùng logic, chỉ khác nhau về kiểu dữ liệu dẫn đến code bị trùng lặp. Bây giờ hãy sử dụng generics để giải quyết vấn đề đó.

```rust,ignore
fn largest<T>(list: &[T]) -> T {
```

Trong hàm này, `T` sẽ là kiểu tổng quát (generics) của hàm. Tham số truyền vào là `list` với kiểu `T`, cuối cùng trả về một tham chiếu kiểu `T` 

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-05/src/main.rs}}
```

<span class="caption">Listing 10-5: Hàm `largest` sử dụng generic</span>

Tuy nhiên nếu biên dịch chương trình, ta sẽ gặp lỗi sau:

```console
{{#include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-05/output.txt}}
```

Đoạn lỗi trả ra có đề cập đến *trait* `std::cmp::PartialOrd`. Ta sẽ đi sau về nó ở những bài sau. Còn bây giờ, chỉ cần quan tâm là kiểu `T` sẽ áp dụng cho mọi kiểu dữ liệu, mà không phải kiểu nào cũng có thể so sánh lớn hơn, nhỏ hơn được. Vì vậy Rust gợi ý rằng ta nên sử dụng kiểu dữ liệu có thể so sánh, hay nói cách khác là kiểu dữ liệu này phải implement trait `PartialOrd`.

### Định nghĩa Struct

Ta hoàn toàn có thể định nghĩa structs có sử dụng generics như sau:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-06/src/main.rs}}
```

<span class="caption">Listing 10-6: Struct `Point<T>` sử dụng generics kiểu T cho 2 biến `x` và `y`</span>

Chú ý rằng `x` và `y` dùng có kiểu `T` nên khi sử dụng ta phải cho 2 biến này có cùng kiểu dữ liệu.
Đoạn code ở Listing 10-7 sẽ không thể biên dịch.

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-07/src/main.rs}}
```

<span class="caption">Listing 10-7: `x` và `y` cần cùng kiểu dữ liệu.</span>

Listing 10-7: The fields `x` and `y` must be the same type because both have
the same generic data type `T`.

```console
{{#include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-07/output.txt}}
```

Để `x` và `y` có kiểu khác nhau, ta có thể thêm một generic khác, giả sử có tên `U`.

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-08/src/main.rs}}
```

<span class="caption">Listing 10-8: Generic struct có kiểu dữ liệu khác nhau.</span>

Giờ đây có thể truyền bất cứ kiểu nào mà mình muốn. Tuy nhiên việc sử dụng quá nhiều generics có thể làm cho code rờm rà, khó đọc.

### Định nghĩa Enum

Generic enum khá giống với generic struct. Cùng nhìn vào một enum được sử dụng khá nhiều là `Option<T>`

```rust
enum Option<T> {
    Some(T),
    None,
}
```

Enum cũng có thể có nhiều generics, ví dụ điển hình là `Result<T, E>`

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Nếu `Result` trả về `Ok`, giá trị bên trong nó sẽ có kiểu `T`. Nếu trả về `Err`, giá trị sẽ có kiểu `E`.

### Định nghĩa method

Method được implement cho struct hoặc enum sau đó thêm generics như đoạn code dưới đấy

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-09/src/main.rs}}
```

<span class="caption">Listing 10-9: Implementing method có tên `x` kết hợp với generic `T`</span>

Ta còn có thể tạo ra các methods cho riêng một kiểu dữ liệu nào đó, ví dụ:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-10/src/main.rs:here}}
```

<span class="caption">Listing 10-10: Method `distance_from_origin` chỉ được sử dụng nếu kiểu dữ liệu là `f32`</span>

Điều này có nghĩa là bất kì `Point<T>` với `T` khác `f32` đều không thể sử dụng method `distance_from_origin`.

Generic type định nghĩa ở struct không nhất thiết phải giống với generic type định nghĩa cho method. Ví dụ:
<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch10-generic-types-traits-and-lifetimes/listing-10-11/src/main.rs}}
```

<span class="caption">Listing 10-11: Method có generic type khác với generic type của struct</span>

Ở đây mặc dù struct Point có generic type là `X1` và `Y1`, nhưng method `mixup` lại sử dụng generic type là `X2` và `Y2`

### Hiệu năng khi chạy code sử dụng Generic

Có thể bạn sẽ thắc mắc rằng liệu code có chậm hơn ở runtime nếu sử dụng generic. Câu trả lời là không hề.

Rust làm được điều đó là vì sử dụng cơ chế *monomorphization* tại compile time. *Monomorphization* là cơ chế chuyển đổi generic code về kiểu dữ liệu biết trước ở compile time. Ví dụ với `Option<T>` enum:

```rust
let integer = Some(5);
let float = Some(5.0);
```

Khi compile, Rust sẽ đọc biến truyền vào enum `Option<T>` và biết được kiểu dữ liệu mà nó sẽ phải dùng lần lượt là `i32` và `f64`, do đó thay thế nó cho generic ngay tại compile time.

Có thể mô phỏng *monomorphization* bằng đoạn code dưới đây:

<span class="filename">Filename: src/main.rs</span>

```rust
enum Option_i32 {
    Some(i32),
    None,
}

enum Option_f64 {
    Some(f64),
    None,
}

fn main() {
    let integer = Option_i32::Some(5);
    let float = Option_f64::Some(5.0);
}
```

Enum `Option<T>` được thay thế bằng kiểu dữ liệu cụ thể khi compile, do đó chương trình sẽ biên dịch chậm hơn nhưng khi runtime sẽ không có sự khác biệt về tốc độ

[traits-as-parameters]: ch10-02-traits.html#traits-as-parameters
[fixing]: ch10-02-traits.html#fixing-the-largest-function-with-trait-bounds
