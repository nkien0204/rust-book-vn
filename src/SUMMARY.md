# Ngôn ngữ lập trình Rust (Rust Programming Language)
[Về rustvn.com](rustvn.com.md)
[Ngôn ngữ lập trình Rust](title-page.md)
[Lời tựa](foreword.md)
[Giới thiệu](ch00-00-introduction.md)

## Hành trình với Rust

- [Bắt đầu](ch01-00-getting-started.md)
    - [Cài đặt](ch01-01-installation.md)
    - [Chương trình đầu tiên 'Hello, World!'](ch01-02-hello-world.md)
    - [Cargo](ch01-03-hello-cargo.md)

- [Lập trình một trò chơi đoán chữ](ch02-00-guessing-game-tutorial.md)

- [Nguyên lý chung của của ngôn ngữ](ch03-00-common-programming-concepts.md)
    - [Biến và Sự Biến đổi (Mutability)](ch03-01-variables-and-mutability.md)
    - [Kiểu dữ liệu](ch03-02-data-types.md)
    - [Hàm](ch03-03-how-functions-work.md)
    - [Chú thích](ch03-04-comments.md)
    - [Luồng điều khiển](ch03-05-control-flow.md)

- [Nguyên lý quyền sở hữu (ownership)](ch04-00-understanding-ownership.md)
    - [Quyền sở hữu là gì?](ch04-01-what-is-ownership.md)
    - [Tham chiếu và nguyên lý borrow](ch04-02-references-and-borrowing.md)
    - [Kiểu dữ liệu slice](ch04-03-slices.md)

- [Kiểu Struct và lưu trữ dữ liệu](ch05-00-structs.md)
    - [Định nghĩa và khởi tạo Struct](ch05-01-defining-structs.md)
    - [Một ví dụ sử dụng Struct](ch05-02-example-structs.md)
    - [Phương thức](ch05-03-method-syntax.md)

- [Kiểu Enums and Cú pháp Matching trong Rust](ch06-00-enums.md)
    - [Định nghĩa kiểu Enum](ch06-01-defining-an-enum.md)
    - [Từ khoá `match`](ch06-02-match.md)
    - [Luồng điều khiển với `if let`](ch06-03-if-let.md)

## Rust Cơ bản

- [Quản lý Dự Án Lớn với packages (gói), crates (nhóm các packages) và modules (mức module)](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)
    - [Packages và Crates](ch07-01-packages-and-crates.md)
    - [Định nghĩa module với chính sách riêng tư (privacy)](ch07-02-defining-modules-to-control-scope-and-privacy.md)
    - [Truy xuất tới item trong module (Module Tree)](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
    - [Định nghĩa phạm vi sử dụng cho đường dẫn với từ khoá `use`](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
    - [Chia module thành nhiều file khác nhau](ch07-05-separating-modules-into-different-files.md)

- [Kiểu dữ liệu Collections Phổ biến](ch08-00-common-collections.md)
    - [Lưu trữ danh sách giá trị với Vector](ch08-01-vectors.md)
    - [Lưu trữ UTF-8 Encoded Text với kiểu Strings](ch08-02-strings.md)
    - [Lưu trữ cặp keys/value sử dụng Hash Maps](ch08-03-hash-maps.md)

- [Xử lý lỗi](ch09-00-error-handling.md)
    - [Lỗi không thể phục với `panic`](ch09-01-unrecoverable-errors-with-panic.md)
    - [Lỗi có thể khôi phục với `Result`](ch09-02-recoverable-errors-with-result.md)
    - [Khi nào `panic!` và khi nào không nên `panic!`](ch09-03-to-panic-or-not-to-panic.md)

- [Kiểu tổng quát (Generic Types), Traits, và  Lifetimes (Vòng đời)](ch10-00-generics.md)
    - [Kiểu dữ liệu Generic](ch10-01-syntax.md)
    - [Traits: Định nghĩa đặc tính chung (shared behavior)](ch10-02-traits.md)
    - [Xác thực tham chiếu sử dụng Lifetimes](ch10-03-lifetime-syntax.md)

- [Viết một test case](ch11-00-testing.md)
    - [Cách để viết một test](ch11-01-writing-tests.md)
    - [Điều khiển cách hoạt động của một Test](ch11-02-running-tests.md)
    - [Chiến thuật Test (Test Organization)](ch11-03-test-organization.md)

- [Dự án I/O: Xây dựng một chương trình dòng lệnh (Command Line)](ch12-00-an-io-project.md)
    - [Chấp nhận tham số dòng lệnh](ch12-01-accepting-command-line-arguments.md)
    - [Đọc một file](ch12-02-reading-a-file.md)
    - [Sửa đổi code để cái thiện tính module hoá và xử lý lỗi](ch12-03-improving-error-handling-and-modularity.md)
    - [Phát triển tính năng của thư viện với hướng phát triển thử nghiệm](ch12-04-testing-the-librarys-functionality.md)
    - [Làm việc với biến môi trường](ch12-05-working-with-environment-variables.md)
    - [Viết thông điệp lỗi và chuyển tiếp tới đầu ra chuẩn của lỗi (Standard Error Output)](ch12-06-writing-to-stderr-instead-of-stdout.md)

##  Thinking in Rust

- [ Tính năng ngôn ngữ lập trình Hàm: Iterators và Closures](ch13-00-functional-features.md)
    - [Closures: Hàm vô danh và có thể lấy thông tin ngữ cảnh](ch13-01-closures.md)
    - [Xử lý chuỗi đối tượng nhờ Iterators (Đối tượng Lặp)](ch13-02-iterators.md)
    - [Cải thiện Dự án I/O](ch13-03-improving-our-io-project.md)
    - [So sánh hiệu năng: Vòng lặp theo chỉ số với lặp dạng Iterators](ch13-04-performance.md)

- [Nhiều hơn về Cargo and trang Crates.io](ch14-00-more-about-cargo.md)
    - [Cấu hình tuỳ biến build với tham số cho release](ch14-01-release-profiles.md)
    - [Đưa một crate lên trang Crates.io](ch14-02-publishing-to-crates-io.md)
    - [Dự án với Cargo (Cargo Workspaces)](ch14-03-cargo-workspaces.md)
    - [Cài đặt chương trình từ  Crates.io với `cargo install`](ch14-04-installing-binaries.md)
    - [Mở rộng Cargo với nhiều lệnh tuỳ biến](ch14-05-extending-cargo.md)

- [Con trỏ thông mình (Smart Pointers)](ch15-00-smart-pointers.md)
    - [ Sử dụng `Box<T>`](ch15-01-box.md)
    - [ Con trỏ thông minh như tham chiếu + Deref Trait](ch15-02-deref.md)
    - [ Chạy chương trình với `Drop` Trait như bộ dọn rác (cleanup)](ch15-03-drop.md)
    - [`Rc<T>`, Con trỏ thông minh với bộ đếm số lượng tham chiếu (Reference Counted)](ch15-04-rc.md)
    - [`RefCell<T>` và Thiết kế Interior Mutability Pattern(1)](ch15-05-interior-mutability.md)
    - [Vòng đời của tham chiếu có thể rò rỉ bộ nhớ](ch15-06-reference-cycles.md)

- [Lập trình song song](ch16-00-concurrency.md)
    - [Sử dụng Threads(luồng) cho lập trình đa luồng](ch16-01-threads.md)
    - [Trao đổi dữ liệu giữa các threads](ch16-02-message-passing.md)
    - [Chia sẻ trạng thái](ch16-03-shared-state.md)
    - [Mở rộng với Đặc tính `Sync` và `Send` ](ch16-04-extensible-concurrency-sync-and-send.md)

- [Lập trình hướng đối tượng trong Rust ](ch17-00-oop.md)
    - [Đặc tính của ngôn ngữ hướng đối tượng ](ch17-01-what-is-oo.md)
    - [Sử dụng Đối tượng Trait (Objects Traits)](ch17-02-trait-objects.md)
    - [Thực hiện design pattern hướng đối tượng ](ch17-03-oo-design-patterns.md)

## Chủ đề nâng cao

- [Patterns và Matching](ch18-00-patterns.md)
    - [Các nơi có thể áp dụng mẫu `match`](ch18-01-all-the-places-for-patterns.md)
    - [Refutability: Phần Refutability trong `match`](ch18-02-refutability.md)
    - [Cú pháp `match`](ch18-03-pattern-syntax.md)

- [Tính năng nâng cao](ch19-00-advanced-features.md)
    - [Unsafe Rust](ch19-01-unsafe-rust.md)
    - [Advanced Traits](ch19-03-advanced-traits.md)
    - [Advanced Types](ch19-04-advanced-types.md)
    - [Advanced Functions và  Closures](ch19-05-advanced-functions-and-closures.md)
    - [Macros](ch19-06-macros.md)

- [Final Project: Building a Multithreaded Web Server](ch20-00-final-project-a-web-server.md)
    - [Building a Single-Threaded Web Server](ch20-01-single-threaded.md)
    - [Turning Our Single-Threaded Server into a Multithreaded Server](ch20-02-multithreaded.md)
    - [Graceful Shutdown and Cleanup](ch20-03-graceful-shutdown-and-cleanup.md)

- [Phụ Lục](appendix-00.md)
    - [A - Từ khoá](appendix-01-keywords.md)
    - [B - Toán tử và Ký Hiệu](appendix-02-operators.md)
    - [C - Traits Có thể kế thừa(Derivable Traits)](appendix-03-derivable-traits.md)
    - [D - Công cụ phát triển hữu dụng](appendix-04-useful-development-tools.md)
    - [E - Phiên bản Rust](appendix-05-editions.md)
    - [F - Dịch sách Translations of the Book](appendix-06-translation.md)
    - [G - Cách Rust được tạo và “Nightly Rust” là gì?](appendix-07-nightly-rust.md)
