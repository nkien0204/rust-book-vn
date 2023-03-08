## Lưu trữ danh sách các giá trị với Vectors 

Cho tới nay chúng ta đã nhìn thấy kiểu danh sách là `Vec<T>` - đọc là vector. xwVector cho phép chúng ta lưu trữ  
nhiều các giá trị cùng kiểu bằng cách đặt chúng cạnh nhau trong bộ nhớ. Vector chỉ cho phép lưu trữ các giá trị
cùng kiểu dữ liệu. Eg: Cùng kiểu i32, i64, str, u8... Chúng hưu dụng khi chúng ta có danh sách các đối tượng, giống 
như mỗi dòng text trong một file hoặc giá của các items trong một giỏ hàng. 

### Cách tạo một vector

Để tạo một vector mới và rỗng, chúng ta gọi hàm `Vec::new`, xem ví dụ Listing 8-1

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-01/src/main.rs:here}}
```

<span class="caption">Listing 8-1: Tạo một vector mới, rỗng, kiểu dữ liệu `i32`</span>

Chú ý rằng, chúng thêm ký hiệu ở đây. Bởi vì, chúng ta đã không chèn bất kỳ giá trị nào vào vector này, Rust
sẽ không biết kiểu dữ liệu nào chúng ta định lưu trữ. Điều này khá là quan trọng. Bởi vì Vector đã 
thực hiện sử dụng kiểu dữ liệu tổng quát (generics). Chúng ta sẽ xem xét cách để sử dụng 
generics với kiểu dữ liệu mà bạn muốn trong Chương 10. Hiện tại, Kiểu `Vec<T>` được cung cấp
bởi thư viện chuẩn và có thể lưu trữ bất kỳ giá tị nào. Khi chúng tạo một vector để lưu trữ một kiểu cụ thể,
chúng ta có thể chi tiết kiểu trong dấu <>. Trong 9-1, chúng ta đã nói rằng `Vec<T>` trong đó v sẽ giữ thành phần với kiểu dữ liệu `i32`

Thường xuyên hơn, bạn sẽ tạo một `Vec<T>` với giá trị khởi tạo và Rust sẽ tự ngầm hiểu(infer)) kiểu mà bạn muốn 
lưu trữ, do đó hiếm bạn cần ký hiệu cho kiểu dữ liệu. Rust cũng cấp một macro `vec!` mà sẽ tạo 
một vector mới mà sẽ giữ các giá trị mà bạn truyền vào. Listing 8-2 tạo một `Vec<i32` và dữ giá tị
`1`,`2`, và `3`. Kiểu số nguyên là `i32` bởi vì nó là kiểu số nguyên mặc định (4 bytes). Điều này chúng ta 
đã thảo luận trong [“Data types”][data-types]<!-- ignore -->  Chương 3

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-02/src/main.rs:here}}
```

<span class="caption">Listing 8-2: Tạo một vectỏ mới bao gồm các giá trị </span>
Bởi vì chúng ta khởi tạo các giá trị `i32`, Rust có thể ngầm hiểu kiểu của `v` là `Vec<i32>`, và ký hiệu 
cho kiểu là không cần thiết. Tiêp theo, chúng ta sẽ xem xét cách để thay đổi một vector


### Cập nhật một Vector 
Để tạo một vector và sau đó thêm các thành phần tới chúng, chúng ta sử dụng phương thức `push` như được chỉ ra 
trong Listing 8-3

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-03/src/main.rs:here}}
```

<span class="caption">Listing 8-3: Sử dụng phương thức `push` để thêm các giá trị tới một
vector</span>
Bởi vì với bất kỳ biến nào, nếu bạn muôn có thể thay đổi giá trị của chúng, bạn cũng sẽ cần làm cho nó `mutable` (có thể thay đổi được) bằng cách sử dụng từ khoá `mut`, như đã nói đến trong Chương 3. Số chúng đặt trong vector là kiểu `i32`, và Rust 
ngầm hiểu từ dữ liệu, do đó chúng ta không thực sự cần ký hiệu `Vec<i32>`

### Huỷ thành phần trong một vector 

Giống như bất kỳ kiếu `struct` nào, một vector được giải phóng khi nó ra ngoài phạm vi của nó xem Listing 8-4.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-04/src/main.rs:here}}
```

<span class="caption">Listing 8-4: Nơi vector và các giá trị của nó bị huỷ</span>

Khi vector bị huỷ, tất cả nội dung trong nó sẽ bị huỷ, nghĩa rằng tất cả số nguyên nó giữ sẽ bị xoá sạch.
Điều này có vẻ dường như đơn giản nhưng nếu như chúng ta bắt đầu học về `tham chiếu` (`reference`) tới các thành phần
của một vector, chắc chắn nó không còn dễ hiểu như vậy nữa



### Đọc thành phần (elements) trong Vector

Có 2 cách để tham chiếu  một giá trị lưu trong một vector: thông qua index (chỉ số) hoặc sử dụng phương thức `get`.
Trong ví dụ dưới đây, chúng ta ký hiệu kiểu của các giá trị mà được trở về từ các hàm trên cho mục địch phân làm rõ hơn.



Listing 8-5 chỉ ra cả 2 phương thức truy xuất một giá trị trong một vector, một sử dụng chỉ số, một sử dụng phương thức `get`

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-05/src/main.rs:here}}
```

<span class="caption">Listing 8-5: Sử dụng cú pháp chỉ số hoặc phương thức `get` để truy xuất một đối tượng trong một vector</span>

Chú ý có 2 chi tiết ở đây. Đầu tiên, chúng ta sử dụng giá trị chỉ số `2` để lấy phần tử thứ 3 bởi vì vector được 
đánh chỉ số bắt đầu từ 0. Thứ hai, chúng ta lấy phần tử thứ 3 bởi sử dụng `&` hoặc `[]`, mà đưa chúng ta 
một tham chiếu hoặc sử dụng phương thức `get` với chỉ số truyền vào như tham số, kết quả là `Option<&T>`

Lý do Rust cung cấp 2 cách để tham chiếu một thành phần là bạn có thể chọn cách chương trình hành xử (behaves) khi bạn
cố gắng để sử dụng một giá trị ngoài dãy các thành phần xác định. Ví dụ, xem xét chuyện gì xảy ra khi chúng ta có một
vector với chỉ 5 thành phần và bạn lại luốn truy xuất tới thành phần có index 100. Xem xét Listing 8-6.


```rust,should_panic,panics
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-06/src/main.rs:here}}
```

<span class="caption">Listing 8-6: Attempting to access the element at index
100 in a vector containing five elements</span>

Khi bạn chạy đoạn code này, phương thức đầu tiên `[]` sẽ gây chương trình `panic`(ngắt) bởi vì 
nó tham chiếu tới một thành phần không tồn tại. Điều này là tốt khi bạn muốn chương trình `crash` nếu 
như bạn không muốn có sự truy xuất tới thành phần ngoài vector (Ví dụ như 1 số chương trình cố gắn truy nhập ô nhớ sau vector đề biết nhiều thông tin hơn chẳng hạn)

Khi phương thức `get` được sử dụng với chỉ số nằm ngoài một vector, nó trở về `None` ngoài trừ panicking (`ngắt`). 
Bạn sẽ sử dụng phương thức này nếu truy xuất một thành phần vược ra ngoài khoảng của vector có thể xảy ra thường xuyên 
trong một số trường hợp. Code của bạn sẽ có logic để xử lý hoặc là `Some(&element)` hoặc `None` như đã thảo luận trong chương 6.Ví dụ, chỉ số có thể đến từ một người nhập vào một số. Nếu họ vô tình nhập một số mà quá lớn, chương trình
sẽ có giá trị `None`, bạn có thể nói người dùng bao nhiều items trong vector hiện tại, và đưa cho họ một cơ hội khác với
giá trị nhập vào hợp lý hơn. Điều này là nhiều thân thiện hơn là ngắt chương trình chỉ vì một lỗi nhập số ngớ ngẩn.

Khi chương trình có một tham chiếu hợp lệ, chương trình `borrow checker` (bộ kiểm tra nguyên lý mượn) thực thi luật
quyền sở hữu (ownership) và nguyên lý borrowing (đã nói trong chương 4) để đảm bảo các tham chiếu và bất kỳ tham chiếu
khác tới nội dung của vector còn lại hợp lệ. Nhắc lại luật này, bạn không thể có cùng lúc tham chiếu mutable và immutable trong cùng phạm vi (scope - Ví dụ cùng 1 hàm). Luật này áp dụng trong Listing 8-7, nơi chúng ta giữ một tham chiếu immutable(không thay đổi được) tới thành phần đầu tiên của vector và cố gắn thêm một thành phần tới cuối cùng. Chương trình này sẽ 
không chạy nếu chúng ta cố gắng tham chiếu tới thành phần đó trong hàm.


```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-07/src/main.rs:here}}
```

<span class="caption">Listing 8-7: Cố gắng thêm một thành phần tới một vector trong 
khi giữ một tham chiếu tới một thành phần</span>

Biên dịch code này sẽ lỗi:

```console
{{#include ../listings/ch08-common-collections/listing-08-07/output.txt}}
```

Code trong Listing 8-7 thoạt nhìn không có gì sai: Tại sao một tham chiếu tới thành phần đầu tiên
quan tâm tới sự thay đổi tại thành phần cuối của một vector? Lỗi này là bởi vì cách vector hoạt động: bởi vì 
vectors đặt các giá trị cạnh trong trong bộ nhớ, thêm một thanh phần mới vào cuối của vector có thể yêu cầu cấp phát
bộ nhớ và copy các thành phần của tới không gian mới này, nếu không đủ bộ nhớ để đặt tất cả các thành phần cạnh nhau nơi
vector được lưu trữ hiện tại. Trong trường hợp này, tham chiếu tới thành phần đầu tiên trỏ tới bộ nhớ được thu hồi (deallocated memory). Luật borrowing ngăn chặn chương trình rơi vào tình huống này.


> Chú ý: Cho nhiều thông tin chi tiết thực hiện kiểu `Vec<T>` , xem cuốn [“The
> Rustonomicon”][nomicon].

### Duyệt qua các giá trị trong một Vector 
Để truy xuất mỗi thành phàn trong một vector lần lượt, chúng ta có thể duyệt qua (iterate) tất các thành phần
hhown là sử dụng chỉ thị để truy xuất mỗi thành phần. Listing 8-8 chỉ cách để sử dụng `for` lặp để có tham chiếu immutable tới mỗi thành phần trong một Vector `i32` và in chúng 
```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-08/src/main.rs:here}}
```

<span class="caption">Listing 8-8: In mỗi thành phần trong một Vector bởi duyệt qua các thành phần sử dụng vòng lặp `for`</span>

Chúng ta cũng có thể duyệt qua tham chiếu mutable tới mỗi thành phần trong một vector mutable lần lượt để thay đổi tất cả thành phần.
Vòng lặp `for` trong Listing 8-9 sẽ cộng thêm `50` tới mỗi thành phần

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-09/src/main.rs:here}}
```

<span class="caption">Listing 8-9: Duyệt qua các tham chiếu mutable trỏ tới các thành phần trong một vector</span>

Để thay đổi giá trị mà một tham chiếu mutable trỏ tới, chúng ta có thể sử toàn tử `*` (gọi là dereference operator) để lấy giá trị trong `i` trước khi chúng ta
có thể sử dụng toán tử `+=`. Chúng ta sẽ nói nhiều về toán tử derefence này 
[“Toán từ Dereference như một con trỏ tới một giá trị”][deref]<!-- ignore -->
trong chương 15

### Sử dụng Enum để lưu trữ nhiều kiểu dữ liệu
Vectors có thể chỉ lưu trữ các giá trị mà có cùng kiểu. Điều này có thể hơi bất tiện; rõ ràng có trường hợp cho cần dể lưu trữ một danh sách các phần tử của kiểu khác nhau
May mắn thay, biến thể của một enum định nghĩa dưới cùng kiểu enum, nên khi chúng ta cần 1 kiểu để  thể hiện các thành phần của kiểu khác nhau, chúng ta có thể sử dụng `enum`!
Ví dụ, chúng ta muốn lấy gái trị từ một dòng trong 1 spreadsheet (tài liệu) nơi một số cột trong hàng bao gồm số nguyên dượng, một vài sốt thực, và một số string.
Chúng ta có thể định nghĩa một enum mà các biến của nó sẽ giữ kiểu khác nhau, và tất các biến enum sẽ được xem là cùng một kiểu: kiểu enum. Sau đó chúng ta có thể tạo một vector
để lưu trữ enum và do đó không giới giạn lưu trữ kiểu dữ liệu khác nhau. Chúng ta sẽ trình bày điều này trong Listing 8-10

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-10/src/main.rs:here}}
```

<span class="caption">Listing 8-10: Định nghĩa `enum` để lưu trữ giá trị của kiểu khác nhau trong một vector </span>

Rust cần để biết kiểu dữ liệu nào sẽ trong một Vector tại lúc biên dịch do đó nó biết trình chính xác bao nhiều bộ nhớ trong vùng heap sẽ được cần để lưu trữ mỗi thành phần.
Chúng ta cũng phải chính xác về kiểu dữ liệu nào được cho phép trong vector này. Nếu Rust cho phép một vector để lưu trữ bất kỳ kiểu nào, sẽ có lúc rằng một hoặc nhiều kiểu
sẽ gây lỗi với điều khiển thực hiện trong thành phần của Vector. Sử dụng enum với `match` cú pháp nghĩa rằng Rust sẽ đảm bảo tại lúc biên dịch mõi trường hợp có thể xảy ra sẽ được 
xử lý, bởi như đã nói ở Chương 6.
Nếu bạn không biết tập hợp kiểu có thể của kiểu dữ liệu mà một chương trình tại lúc runtime (lúc chạy chương trình) lưu giữ trong một Vector, công nghệ enum sẽ áp dụng được. Thay vào 
đó, bạn có thể sử dụng trait object (đối tuợng trait), mà chúng ta sẽ học trong Chương 17 

Nào, chúng ta đã thảo luận một số cách thông thường để sử dụng Vector, xem lại [the API documentation][vec-api]<!-- ignore -->  để tất cả các phương thức hữu dụng định nghĩa trong
`Vec<T>` trong thư viện chuẩn. Ví dụ, trong hàm `push`, phương thức `pop` xoá và trả về giá trị cuối cùng. Tiếp theo, cùng xem xét kiểu collection `String`

[data-types]: ch03-02-data-types.html#data-types
[nomicon]: ../nomicon/vec/vec.html
[vec-api]: ../std/vec/struct.Vec.html
[deref]: ch15-02-deref.html#following-the-pointer-to-the-value-with-the-dereference-operator
