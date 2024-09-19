# Python-Coding-Guidelines

## Table of Contents
3. [Proposed Convention](#proposed-convention)


## Proposed Convention <a name="proposed-convention"></a>

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
