# Python-Coding-Guidelines

## Table of Contents

1. [Các quy chuẩn thủ công](#quy-chuan-thu-cong)
   
    1.1. [Naming Convention](#name-convention)
   
    1.2. [Comment](#comment)
   
    1.3. [Comment](#comment)

    1.4. [Type Hinting](#type-hinting)




## Các quy chuẩn thủ công <a name="quy-chuan-thu-cong"></a>
### Naming Convention <a name="name-convention"></a>

Sau đây là một vài cách đặt tên biến quy chuẩn:

| Name                      | Convention | Code Example                                         |
|---------------------------|------------|------------------------------------------------------|
| single variable name      | snake_case | `age: int = 100`                                     |
| compound variable name    | snake_case | `first_name: str = "Akira"`                          |
| constant name             | CONST      | `CPU: number = 8`                                    |
| compound constant name    | CONST      | `MAX_NUMBER: number = 100`                           |
| enum name                 | PascalCase | `class Color(Enum): RED = 1 GREEN = 2`               |
| function name             | snake_case | `def main()`                                         |
| function with parameters  | snake_case | `def calculate(n1: int, n2: int)`                    |
| function with return type | snake_case | `def calculate(n1: int, n2: int) -> int:`            |
| compound function name    | snake_case | `def add_two_numbers(n1: int, n2: int) -> int:`      |
| class name                | PascalCase | `class Base`                                         |
| compound class name       | PascalCase | `class MyClass`                                      |
| interfaces                | PascalCase | `class IUser(ABC)`                                   |
| casting                   | default    | `age: int = int(100)`                                |
| list                      | camelCase  | `myList: list[int] = [1,2,3]`                        |
| tuple                     | camelCase  | `myTuple: tuple[int] = (1,2,3)`                      |
| set                       | snake_case | `my_set: set[int] = {1,2,3}`                         |
| dictionary                | snake_case | `my_dictionary: dict = {"name": "John", "age": 100}` |
| multiple type hinting     | snake_case | `var_a: Union[int, str]`                             |

Ngoài ra, chúng ta có thể sử dụng thư viện [pep8-naming](https://github.com/PyCQA/pep8-naming) để có thể kiểm soát cách đặt tên cho các biến trong python project của mình.

### Comment <a name="comment"></a>
Comment được viết với một số mục đích, bao gồm:

* Sử dụng comment để thiết kế và phác thảo trước đoạn code đó:
  ```
  # Step 1:
  # Step 2:
  # Step 3:
  ...
  ```
* Mô tả thuật toán.
* Sử dụng như một tag. VD các tag `BUG`, `FIXME`, `TODO` nên được sử dụng để đánh dấu những chỗ cần cải thiện hoặc sửa lỗi..

Comment cũng được giới hạn bởi số ký tự tối đa giống như code thông thường


### Docstring <a name="docstring"></a>
* Vị trí docstring: Đặt ngay sau định nghĩa của function, class, hoặc module.
* Có 2 dạng docstring, docstring 1 dòng và docstring nhiều dòng. Trong docstring 1 dòng, chúng ta có thể chú thích giống với comment. Với docstring nhiều dòng, dòng đầu tiên sẽ mô tả ngắn gọn mục đích của function (mô tả chỉ nên viết trên 1 dòng duy nhất), sau đó những hàm sau sẽ mô tả các tham số, và các giá trị trả về.
* Có thể dùng Google style, NumPy style hoặc reStructuredText style để viết docstring. Chọn một phong cách và tuân theo nó trong suốt dự án.
* Tương tự như code và comment, docstring cũng tuân thủ số lượng ký tự tối đa trong 1 dòng.
* Có một số extention trong các IDE để có thể gen cho chúng ta template docstring. Ngoài ra, chúng ta có thể lấy template đó và nhờ các chatbot LLM viết hộ cho chúng ta docstring.
* Điểm khác biệt với comment là chúng ta hoàn toàn có thể đọc lại các docstring cho các hàm tương ứng thông qua hàm `help()`, hoặc qua các IDE.

### Type Hinting <a name="type-hinting"></a>

Type hinting là cách dùng để xác định trước kiểu dữ liệu của một giá trị.

Ví dụ:
```
def addBinary(a: int, b: int)-> int:
...
```
Tuy nhiên, Python là một untyped language, do đó, nếu ta truyền một biến dạng `str` vào biến `a` ở ví dụ trên thì code vẫn sẽ chạy. Và dù đã có docstring rồi, nhưng với type hinting, chúng ta có thể sử dụng các tool để thực hiện Static Type Checking, cũng như là giúp các IDE cung cấp intellisense.

Để Static Type Checking, chúng ta có thể sử dụng thư viện `mypy`.

### Logging <a name="logging"></a>
Logging cũng là một trong những vấn đề cần quan tâm khi chúng ta phát triển product. Sau đây là một vài lưu ý:
#### Tránh sử dụng root logger:
Nếu sử dụng root logger, chúng ta sẽ gặp một số vấn đề
* Kiểm soát hạn chế: Root logger cung cấp ít khả năng kiểm soát cách xử lý log, dễ dẫn đến các thông điệp log sai hoặc gửi đến đích không mong muốn.
* Quản lý phức tạp: Khó quản lý nhiều logger trong ứng dụng lớn, dẫn đến trùng lặp hoặc cấu hình sai.
* Không tách biệt dữ liệu log: Root logger dùng chung cho tất cả module, gây khó khăn trong việc tách log theo module.
* Rủi ro bảo mật: Root logger có thể bị sửa đổi bởi bất kỳ module nào, tiềm ẩn nguy cơ bảo mật.
  
<em>Giải pháp:</em> Tạo logger riêng cho từng module bằng cách sử dụng `logging.getLogger()`. Điều này giúp quản lý log độc lập và dễ dàng phân tích. Nên tắt tính năng truyền tin (`propagate = False`) để tránh trùng lặp thông điệp log.

#### Tách riêng một module để config logging
Khi phát triển một product phức tạp, thì việc quản lý và cấu hình logging cũng trở nên khó khăn hơn. Nếu ta không tách riêng thành một module riêng, chúng ta sẽ gặp khó khăn trong việc in và quản lý log trên từng môi trường test, dev, hay các log sẽ bị chồng chéo nhau.

#### Sử dụng log chính xác
Sử dụng đúng các loại log:
* CRITICAL: Thể hiện các lỗi rất nghiêm trọng cần được chú ý ngay lập tức, nếu không ứng dụng có thể không tiếp tục hoạt động. Ví dụ, nếu xảy ra lỗi khi kết nối đến cơ sở dữ liệu, có thể ghi lại lỗi với mức độ critical.
* ERROR: Thể hiện lỗi khi thực hiện một tác vụ nào đó. Ví dụ, ghi lại lỗi khi xử lý yêu cầu HTTP hoặc lỗi cơ sở dữ liệu.
* WARNING: Thể hiện thông tin cảnh báo về các tình huống có thể xảy ra lỗi trong tương lai, ví dụ như "dung lượng ổ đĩa thấp".
* INFO: Thể hiện thông tin chung về hoạt động của ứng dụng, giúp đảm bảo rằng ứng dụng đang chạy như mong đợi.
* DEBUG: Cung cấp thông tin chi tiết, thường được sử dụng để khi ta debug.

#### Những trường hợp không nên in log
* Thông tin không quan trọng: Tránh log những thông tin không cần thiết hoặc không liên quan đến việc gỡ lỗi hoặc phân tích, vì nó có thể làm tăng kích thước tệp log và khiến việc tìm kiếm thông tin hữu ích trở nên khó khăn.
* Thông tin nhạy cảm: Không bao giờ ghi lại thông tin nhạy cảm như mật khẩu, thông tin thẻ tín dụng, hoặc dữ liệu cá nhân của người dùng. Điều này có thể gây rủi ro bảo mật.
* Tránh log trong các khối mã thực thi lặp lại nhiều lần hoặc có yêu cầu hiệu suất cao (ví dụ: vòng lặp lồng nhau) vì nó có thể ảnh hưởng đến hiệu suất.

## Các quy chuẩn tự động

### Quy chuẩn chung

Chúng ta hoàn toàn có tự động hóa bằng `pre-commit` với các công cụ và thư viện như flake8, pylint, black, isort. Bên cạnh các quy chuẩn ở trên, các tool này còn có thể hỗ trợ trong việc xử lý:
* Code dài dòng: giới hạn mỗi dòng có một số ký tự nhất định.
* Thụt lề: Kiểm tra indentations
* Dấu cách: Kiểm tra việc sử dụng khoảng trắng đúng cách xung quanh các toán tử, sau dấu phẩy, hoặc sau các hàm định nghĩa.
* Dòng trống: Đảm bảo rằng có ít nhất 2 dòng trống giữa các class hoặc định nghĩa function, và 1 dòng trống giữa các phương thức trong một class.
* Kết thúc tệp: Đảm bảo có một dòng trống ở cuối mỗi tệp.
* Import không sử dụng: Kiểm tra các import không được sử dụng.
* Biến không sử dụng: Phát hiện các biến được khai báo nhưng không sử dụng.
* Độ phức tạp của hàm.

Ngoài ra, trong `pylint` còn hỗ trợ:
* Cấu trúc chương trình: Kiểm tra hàm không có return, hàm quá dài, class không có docstring.
* Naming convention
* Thừa nhận diện: Báo lỗi nếu một biến, hàm, hoặc lớp bị thừa mà không sử dụng.

### Quy chuẩn bảo mật
Để không bị lộ lọt ra ngoài các secret key (ví dụ như API keys, token, mật khẩu) trong source code khi ta quản lý trên Git, chúng ta có những cách sau:
* Đưa các file `.env` hoặc các file config chứa các secret key vào `.gitignore`.
* Sử dụng các Environment Variables để không đưa trực tiếp key vào trong code.
  ```
  api_key = os.getenv('API_KEY')
  ```
* Sử dụng một số tool để có thể phát hiện các secret key hoặc dữ liệu nhạy cảm có trong code: ví dụ như sử dụng Detect-secrets (by Yelp) trong pre-commits.

  

