## Lưu trữ UTF-8 Encoded Text (Chữ định dạng UTF-8) với kiểu Strings

Chúng ta đã nói về `string` trong chương 4, nhưng chúng sẽ xem xét kỹ lưỡng chúng bây giờ.
Một Rustaceans mới thường gặp rắc rối với string khi kết hợp 3 thứ sau: Biểu thị lỗi trong string, 
string là cấu trúc dữ liệu phức tạp và thứ 3: UT8. 
Ba nhân tố này kết hợp thành thứ mà dường như khó khi bạn đến từ một ngôn ngữ khác.

Chúng ta thảo luận string trong ngữ cảnh collections bởi vì strings được coi như một tập hợp của các bytes, vài phương 
thức thêm vào cung cấp chức năng hữu dụng khi bytes của nó được coi như là text. Trong chương này, chúng ta sẽ nói về 
những điều khiển trong `String` (kiểu dữ liệu) mà mọi kiểu collection có, giống như việc tạo, cập nhật, và đọc. Chúng ta cũng sẽ bàn về các cách nơi
`String` là khác với các kiểu collection khác, cách indexing thành một `String` là phức tạp bởi sự khác nhau giữa cách người và máy tính giải thích kiểu 
`String`;


### String là gì?

Đầu tiên, Chúng ta sẽ định nghĩa thuật ngữ *string*. Rust chỉ có một kiểu string trong ngôn ngữ, nơi nó là dạng `slice` `str` mà thường 
được coi biểu thị trong `&str` (mượn). Trong chương 4, chúng ta đã nói về *string slices*, mà là tham chiếu tới dữ liệu text định dạng UTF-8. String, bản chất
ví dụ, là được lưu trữ trong tệp nhị phân và do đó là `string slices`

Kiểu `String`, nơi được cung cấp bởi thư viện chuẩn của Rust hơn là được lập trình thành ngôn ngữ core, là một kiểu chuỗi (string) có thể mở rộng, thay đổi, owned,
định dạng UTF8. Khi lập trình viên Rust (Rustaceans) tham chiếu "string" trong Rust, họ có thể đang tham chiếu tới kiểu `String` hoặc kiểu `&str`, hoặc không phải một 
trong 2 kiểu trên. Mặc dù chương này mục đích chính là về `String`, cả 2 kiểu là được sử dụng nhiều trong thư viện chuẩn Rust, và cả `String` 
và `slices` là dưới dạng UTF8-encoded

Thư viện chuẩn Rust cũng bao gồm một số kiểu string khác, giống như `OsString`, `OsStr`, `CString`, và `CStr`. Những thư viện craté có thể cung cấp cả nhiều lựa chọn
cho việc lưu trữ dữ liệu dạng string. Nhìn cách kiểu kia đều kết thức với `String` hoặc `Str`?. Chúng tahm chiếu tới biến hoặc sở hữu hoặc mượn, cũng giống `String` và
`str` bạn đã nhìn thầy trước đó. Các kiểu string này có thể lưu trữ text trong định dạng mã hoá khác nhau hoặc được thể hiện trong bộ nhớ theo một cách nào đó. Ví dụ, Chúng
ta sẽ không thảo luận các kiểu dữ liệu này trong chương này; xem tài liệu của chúng nhiều hơn hoặc cách sử dụng để biết cách khi nào sử dụng chúng một cách thích hợp.

### Tạo một String 

Nhiều thao tác với `Vec<T>` cũng được sử dụng với `String`, ví dụ hàm `new` để tạo một string, xem Listing 8-11

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-11/src/main.rs:here}}
```

<span class="caption">Listing 8-11: Tạo mới một `String` rỗng </span>

Dòng này tạo một mới một string rỗng và gán tới `s`. Thông thường, chúng ta sẽ khởi tạo với một giá trị mà chúng ta muốn
Để làm điều này, chúng ta có thể sử dụng phương thức `to_string`, mà nó có trong tất cả các kiểu mà thực hiện trait `Display`, và string cũng thế. Listing 8-12 xem xét 2 ví dụ


```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-12/src/main.rs:here}}
```

<span class="caption">Listing 8-12: Using the `to_string` method to create a
`String` from a string literal</span>

This code creates a string containing `initial contents`.

We can also use the function `String::from` to create a `String` from a string
literal. The code in Listing 8-13 is equivalent to the code from Listing 8-12
that uses `to_string`.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-13/src/main.rs:here}}
```

<span class="caption">Listing 8-13: Sử dụng hàm  `String::from` để tạo `String` từ một string gốc(lietrary)</span>
Bởi vì chuỗi được sử dụng cho nhiều thứ, chúng ta có thể sử dụng generic khác nhau cho string, đưa đến cho 
chúng ta nhiều lựa chọn. Một trong số đó dường như hơi thừa thãi, nhưng không sao cả. Trong trường hợp này, `String::from` và `to_string` cùng hành động giống nhau, do đó bạn có thể chọn phương thức nào cũng được phụ thuộc vào bạn.
Nhớ rằng strings là có định dạng mã hoá UTF-8, do dó chúng có bao gồm bất kỳ dữ liệu mã hoá trong đó, Listing 8-14 là ví dụ


```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-14/src/main.rs:here}}
```

<span class="caption">Listing 8-14: Lưu trữ câu lời chào trong các ngôn ngữ khác nhau</span>

Tất cả chúng là giá trị `String` hợp lệ


### Cập nhật một String 

A `String` can grow in size and its contents can change, just like the contents
of a `Vec<T>`, if you push more data into it. In addition, you can conveniently
use the `+` operator or the `format!` macro to concatenate `String` values.

#### Appending to a String with `push_str` and `push`

We can grow a `String` by using the `push_str` method to append a string slice,
as shown in Listing 8-15.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-15/src/main.rs:here}}
```

<span class="caption">Listing 8-15: Appending a string slice to a `String`
using the `push_str` method</span>

After these two lines, `s` will contain `foobar`. The `push_str` method takes a
string slice because we don’t necessarily want to take ownership of the
parameter. For example, in the code in Listing 8-16, we want to able to use
`s2` after appending its contents to `s1`.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-16/src/main.rs:here}}
```

<span class="caption">Listing 8-16: Using a string slice after appending its
contents to a `String`</span>

If the `push_str` method took ownership of `s2`, we wouldn’t be able to print
its value on the last line. However, this code works as we’d expect!

The `push` method takes a single character as a parameter and adds it to the
`String`. Listing 8-17 adds the letter “l” to a `String` using the `push`
method.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-17/src/main.rs:here}}
```

<span class="caption">Listing 8-17: Adding one character to a `String` value
using `push`</span>

As a result, `s` will contain `lol`.

#### Concatenation with the `+` Operator or the `format!` Macro

Often, you’ll want to combine two existing strings. One way to do so is to use
the `+` operator, as shown in Listing 8-18.

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-18/src/main.rs:here}}
```

<span class="caption">Listing 8-18: Using the `+` operator to combine two
`String` values into a new `String` value</span>

The string `s3` will contain `Hello, world!`. The reason `s1` is no longer
valid after the addition, and the reason we used a reference to `s2`, has to do
with the signature of the method that’s called when we use the `+` operator.
The `+` operator uses the `add` method, whose signature looks something like
this:

```rust,ignore
fn add(self, s: &str) -> String {
```

In the standard library, you’ll see `add` defined using generics. Here, we’ve
substituted in concrete types for the generic ones, which is what happens when
we call this method with `String` values. We’ll discuss generics in Chapter 10.
This signature gives us the clues we need to understand the tricky bits of the
`+` operator.

First, `s2` has an `&`, meaning that we’re adding a *reference* of the second
string to the first string. This is because of the `s` parameter in the `add`
function: we can only add a `&str` to a `String`; we can’t add two `String`
values together. But wait—the type of `&s2` is `&String`, not `&str`, as
specified in the second parameter to `add`. So why does Listing 8-18 compile?

The reason we’re able to use `&s2` in the call to `add` is that the compiler
can *coerce* the `&String` argument into a `&str`. When we call the `add`
method, Rust uses a *deref coercion*, which here turns `&s2` into `&s2[..]`.
We’ll discuss deref coercion in more depth in Chapter 15. Because `add` does
not take ownership of the `s` parameter, `s2` will still be a valid `String`
after this operation.

Second, we can see in the signature that `add` takes ownership of `self`,
because `self` does *not* have an `&`. This means `s1` in Listing 8-18 will be
moved into the `add` call and will no longer be valid after that. So although
`let s3 = s1 + &s2;` looks like it will copy both strings and create a new one,
this statement actually takes ownership of `s1`, appends a copy of the contents
of `s2`, and then returns ownership of the result. In other words, it looks
like it’s making a lot of copies but isn’t; the implementation is more
efficient than copying.

If we need to concatenate multiple strings, the behavior of the `+` operator
gets unwieldy:

```rust
{{#rustdoc_include ../listings/ch08-common-collections/no-listing-01-concat-multiple-strings/src/main.rs:here}}
```

At this point, `s` will be `tic-tac-toe`. With all of the `+` and `"`
characters, it’s difficult to see what’s going on. For more complicated string
combining, we can instead use the `format!` macro:

```rust
{{#rustdoc_include ../listings/ch08-common-collections/no-listing-02-format/src/main.rs:here}}
```

This code also sets `s` to `tic-tac-toe`. The `format!` macro works like
`println!`, but instead of printing the output to the screen, it returns a
`String` with the contents. The version of the code using `format!` is much
easier to read, and the code generated by the `format!` macro uses references
so that this call doesn’t take ownership of any of its parameters.

### Indexing into Strings

In many other programming languages, accessing individual characters in a
string by referencing them by index is a valid and common operation. However,
if you try to access parts of a `String` using indexing syntax in Rust, you’ll
get an error. Consider the invalid code in Listing 8-19.

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-19/src/main.rs:here}}
```

<span class="caption">Listing 8-19: Attempting to use indexing syntax with a
String</span>

This code will result in the following error:

```console
{{#include ../listings/ch08-common-collections/listing-08-19/output.txt}}
```

The error and the note tell the story: Rust strings don’t support indexing. But
why not? To answer that question, we need to discuss how Rust stores strings in
memory.

#### Internal Representation

A `String` is a wrapper over a `Vec<u8>`. Let’s look at some of our properly
encoded UTF-8 example strings from Listing 8-14. First, this one:

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-14/src/main.rs:spanish}}
```

In this case, `len` will be 4, which means the vector storing the string “Hola”
is 4 bytes long. Each of these letters takes 1 byte when encoded in UTF-8. The
following line, however, may surprise you. (Note that this string begins with
the capital Cyrillic letter Ze, not the Arabic number 3.)

```rust
{{#rustdoc_include ../listings/ch08-common-collections/listing-08-14/src/main.rs:russian}}
```

Asked how long the string is, you might say 12. In fact, Rust’s answer is 24:
that’s the number of bytes it takes to encode “Здравствуйте” in UTF-8, because
each Unicode scalar value in that string takes 2 bytes of storage. Therefore,
an index into the string’s bytes will not always correlate to a valid Unicode
scalar value. To demonstrate, consider this invalid Rust code:

```rust,ignore,does_not_compile
let hello = "Здравствуйте";
let answer = &hello[0];
```

You already know that `answer` will not be `З`, the first letter. When encoded
in UTF-8, the first byte of `З` is `208` and the second is `151`, so it would
seem that `answer` should in fact be `208`, but `208` is not a valid character
on its own. Returning `208` is likely not what a user would want if they asked
for the first letter of this string; however, that’s the only data that Rust
has at byte index 0. Users generally don’t want the byte value returned, even
if the string contains only Latin letters: if `&"hello"[0]` were valid code
that returned the byte value, it would return `104`, not `h`.

The answer, then, is that to avoid returning an unexpected value and causing
bugs that might not be discovered immediately, Rust doesn’t compile this code
at all and prevents misunderstandings early in the development process.

#### Bytes and Scalar Values and Grapheme Clusters! Oh My!

Another point about UTF-8 is that there are actually three relevant ways to
look at strings from Rust’s perspective: as bytes, scalar values, and grapheme
clusters (the closest thing to what we would call *letters*).

If we look at the Hindi word “नमस्ते” written in the Devanagari script, it is
stored as a vector of `u8` values that looks like this:

```text
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164,
224, 165, 135]
```

That’s 18 bytes and is how computers ultimately store this data. If we look at
them as Unicode scalar values, which are what Rust’s `char` type is, those
bytes look like this:

```text
['न', 'म', 'स', '्', 'त', 'े']
```

There are six `char` values here, but the fourth and sixth are not letters:
they’re diacritics that don’t make sense on their own. Finally, if we look at
them as grapheme clusters, we’d get what a person would call the four letters
that make up the Hindi word:

```text
["न", "म", "स्", "ते"]
```

Rust provides different ways of interpreting the raw string data that computers
store so that each program can choose the interpretation it needs, no matter
what human language the data is in.

A final reason Rust doesn’t allow us to index into a `String` to get a
character is that indexing operations are expected to always take constant time
(O(1)). But it isn’t possible to guarantee that performance with a `String`,
because Rust would have to walk through the contents from the beginning to the
index to determine how many valid characters there were.

### Slicing Strings

Indexing into a string is often a bad idea because it’s not clear what the
return type of the string-indexing operation should be: a byte value, a
character, a grapheme cluster, or a string slice. If you really need to use
indices to create string slices, therefore, Rust asks you to be more specific.

Rather than indexing using `[]` with a single number, you can use `[]` with a
range to create a string slice containing particular bytes:

```rust
let hello = "Здравствуйте";

let s = &hello[0..4];
```

Here, `s` will be a `&str` that contains the first 4 bytes of the string.
Earlier, we mentioned that each of these characters was 2 bytes, which means
`s` will be `Зд`.

If we were to try to slice only part of a character’s bytes with something like
`&hello[0..1]`, Rust would panic at runtime in the same way as if an invalid
index were accessed in a vector:

```console
{{#include ../listings/ch08-common-collections/output-only-01-not-char-boundary/output.txt}}
```

You should use ranges to create string slices with caution, because doing so
can crash your program.

### Methods for Iterating Over Strings

The best way to operate on pieces of strings is to be explicit about whether
you want characters or bytes. For individual Unicode scalar values, use the
`chars` method. Calling `chars` on “नमस्ते” separates out and returns six values
of type `char`, and you can iterate over the result to access each element:

```rust
for c in "नमस्ते".chars() {
    println!("{}", c);
}
```

This code will print the following:

```text
न
म
स
्
त
े
```

Alternatively, the `bytes` method returns each raw byte, which might be
appropriate for your domain:

```rust
for b in "नमस्ते".bytes() {
    println!("{}", b);
}
```

This code will print the 18 bytes that make up this `String`:

```text
224
164
// --snip--
165
135
```

But be sure to remember that valid Unicode scalar values may be made up of more
than 1 byte.

Getting grapheme clusters from strings is complex, so this functionality is not
provided by the standard library. Crates are available on
[crates.io](https://crates.io/)<!-- ignore --> if this is the functionality you
need.

### Strings Are Not So Simple

To summarize, strings are complicated. Different programming languages make
different choices about how to present this complexity to the programmer. Rust
has chosen to make the correct handling of `String` data the default behavior
for all Rust programs, which means programmers have to put more thought into
handling UTF-8 data upfront. This trade-off exposes more of the complexity of
strings than is apparent in other programming languages, but it prevents you
from having to handle errors involving non-ASCII characters later in your
development life cycle.

Let’s switch to something a bit less complex: hash maps!
