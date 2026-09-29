# C++ 编码规范

## 1. 文档目的

本规范用于统一 C++ 项目的代码风格、命名规则、文件组织、接口设计和编程习惯，提高代码的：

* 可读性
* 可维护性
* 一致性
* 可扩展性
* 可测试性

本规范以 Google C++ Style Guide 为主要参考依据，并结合通用 C++ 工程实践进行约束。

---

# 2. 适用范围

本规范适用于项目中的：

* C++ 源代码
* C++ 头文件
* 测试代码
* 示例代码
* 工具程序
* 静态库
* 动态库

第三方代码不强制修改为本规范风格，但与第三方代码交互的项目代码应遵循本规范。

---

# 3. 基本原则

## 3.1 可读性优先

代码首先应该让其他开发人员容易理解。

优先：

```cpp
if (condition) {
  DoSomething();
}
```

而不是通过复杂的表达式、宏或技巧压缩代码。

---

## 3.2 简单优先

避免没有实际收益的：

* 复杂继承
* 过度模板化
* 过度封装
* 不必要的设计模式
* 不必要的宏
* 不必要的抽象层

---

## 3.3 明确优先

代码的意图应该尽可能明确。

优先：

```cpp
const int timeout_ms = 1000;
```

而不是：

```cpp
const int value = 1000;
```

---

## 3.4 一致性优先

同一个项目中，相同类型的问题应该采用相同的解决方式。

例如：

* 命名方式统一
* 错误处理方式统一
* 文件组织方式统一
* 日志方式统一
* 智能指针使用方式统一

---

# 4. 文件规范

## 4.1 文件命名

文件名使用小写字母和下划线。

推荐：

```text
foo.h
foo.cc
foo_test.cc
bar_manager.h
bar_manager.cc
```

禁止：

```text
Foo.h
Foo.cpp
fooManager.cpp
foo-manager.cpp
```

---

## 4.2 文件扩展名

推荐：

```text
.h    C++ 头文件
.cc   C++ 源文件
```

项目如果统一使用其他扩展名，应保持整个项目一致。

---

## 4.3 头文件保护

优先使用 `#pragma once`：

```cpp
#pragma once
```

如果项目要求传统 include guard，则使用：

```cpp
#ifndef PROJECT_FOO_H_
#define PROJECT_FOO_H_

...

#endif  // PROJECT_FOO_H_
```

同一个项目不得混乱使用多种方式。

---

# 5. Include 规范

Include 顺序：

1. 当前源文件对应的头文件
2. C 标准库
3. C++ 标准库
4. 第三方库
5. 项目内部头文件

例如：

```cpp
#include "project/foo.h"

#include <cmath>
#include <memory>
#include <string>

#include <third_party/foo.h>

#include "project/bar.h"
```

不得依赖其他头文件的间接包含。

使用什么类型就显式包含对应头文件。

例如使用：

```cpp
std::vector
```

必须包含：

```cpp
#include <vector>
```

禁止：

```cpp
#include <bits/stdc++.h>
```

---

# 6. 命名规范

## 6.1 命名原则

命名必须：

* 有明确含义
* 避免歧义
* 避免过度缩写
* 避免无意义名称

推荐：

```cpp
file_path
user_name
connection_timeout
```

不推荐：

```cpp
fp
un
ct
```

除非缩写是行业内广泛认可的术语。

---

# 7. 命名空间

命名空间使用小写字母和下划线。

```cpp
namespace project_name {
}
```

子命名空间：

```cpp
namespace project_name::module {
}
```

禁止：

```cpp
namespace ProjectName {
}

namespace PROJECT_NAME {
}
```

不使用：

```cpp
using namespace std;
```

特别是在头文件中禁止使用 `using namespace`。

---

# 8. 类和结构体命名

类名和结构体名使用 `PascalCase`。

```cpp
class FileManager;
class NetworkConnection;
struct UserInfo;
```

禁止：

```cpp
class file_manager;
class fileManager;
class FILE_MANAGER;
```

---

# 9. 函数命名

函数名使用 `PascalCase`。

```cpp
void Initialize();
void Start();
void Stop();
bool IsValid();
std::string GetName();
```

Getter：

```cpp
std::string GetName() const;
```

Setter：

```cpp
void SetName(const std::string& name);
```

布尔函数推荐使用：

```text
Is...
Has...
Can...
Should...
```

例如：

```cpp
bool IsValid() const;
bool HasValue() const;
bool CanStart() const;
```

---

# 10. 变量命名

普通变量使用 `snake_case`。

```cpp
int item_count = 0;
std::string file_path;
bool is_valid = false;
```

禁止：

```cpp
int itemCount;
int ItemCount;
int ITEM_COUNT;
```

循环变量：

```cpp
for (int i = 0; i < count; ++i) {
}
```

如果循环变量具有明确语义，应使用具有意义的名称。

---

# 11. 成员变量

成员变量使用 `snake_case_`。

```cpp
class Example {
 private:
  int count_;
  std::string name_;
};
```

禁止：

```cpp
int count;
int m_count;
int mCount;
int _count;
```

---

# 12. 常量

常量使用 `kPascalCase`。

```cpp
constexpr int kMaxSize = 100;
constexpr int kDefaultTimeout = 1000;
```

命名空间级常量：

```cpp
namespace project {

constexpr int kMaxSize = 100;

}  // namespace project
```

---

# 13. 枚举

优先使用 `enum class`。

```cpp
enum class Status {
  kUnknown,
  kRunning,
  kStopped,
};
```

枚举类型使用 `PascalCase`。

枚举值使用 `kPascalCase`。

禁止使用容易产生全局名称污染的普通 `enum`，除非存在明确兼容性需求。

---

# 14. 宏

尽量避免使用宏。

如果必须使用，宏名称使用大写字母和下划线：

```cpp
#define PROJECT_VERSION_MAJOR 1
```

不得使用宏实现普通函数。

不推荐：

```cpp
#define MAX(a, b) ((a) > (b) ? (a) : (b))
```

优先使用：

```cpp
template <typename T>
const T& Max(const T& a, const T& b);
```

或者：

```cpp
std::max(a, b);
```

---

# 15. 类型规范

优先使用标准 C++ 类型。

推荐：

```cpp
std::int32_t
std::uint32_t
std::size_t
std::string
std::vector<T>
```

避免：

```cpp
int32
uint32
DWORD
WORD
```

除非这些类型来自必须兼容的外部 API。

---

# 16. 指针和引用

使用：

```cpp
Type* pointer;
Type& reference;
```

禁止：

```cpp
Type *pointer;
Type &reference;
```

指针为空时使用：

```cpp
nullptr
```

禁止：

```cpp
NULL
0
```

---

# 17. const 规范

不修改的变量应使用 `const`。

```cpp
const int value = 10;
```

不修改对象时使用：

```cpp
void Process(const Data& data);
```

不修改成员变量的成员函数必须声明：

```cpp
std::string GetName() const;
```

---

# 18. auto 规范

当类型明显时可以使用 `auto`：

```cpp
auto value = GetValue();
auto iterator = container.begin();
```

当类型不明显且影响代码理解时，应明确写出类型：

```cpp
std::string value = GetValue();
```

不得为了减少字符数量而滥用 `auto`。

---

# 19. 智能指针

默认使用智能指针管理动态资源。

独占所有权：

```cpp
std::unique_ptr<T>
```

共享所有权：

```cpp
std::shared_ptr<T>
```

弱引用：

```cpp
std::weak_ptr<T>
```

优先：

```cpp
auto object = std::make_unique<Object>();
```

而不是：

```cpp
Object* object = new Object();
```

禁止裸指针表达资源所有权。

---

# 20. RAII

资源管理应遵循 RAII 原则。

资源包括：

* 动态内存
* 文件
* 锁
* socket
* 系统句柄
* 第三方库资源

优先让资源生命周期与对象生命周期绑定。

避免：

```cpp
Resource* resource = AcquireResource();

...

ReleaseResource(resource);
```

优先设计为：

```cpp
ResourceGuard resource;
```

---

# 21. new 和 delete

业务代码中禁止直接使用：

```cpp
new
delete
```

优先使用：

```cpp
std::make_unique
std::make_shared
```

只有在特殊底层场景下才允许直接调用 `new/delete`，并应保证生命周期明确。

---

# 22. 移动语义

需要转移资源所有权时使用移动语义。

```cpp
Object(Object&& other) noexcept;
Object& operator=(Object&& other) noexcept;
```

不应无意义地使用 `std::move`。

例如返回局部对象时：

```cpp
std::string CreateName() {
  std::string name = "example";
  return name;
}
```

不需要：

```cpp
return std::move(name);
```

---

# 23. 拷贝控制

如果类型不允许复制，应显式删除：

```cpp
class Object {
 public:
  Object(const Object&) = delete;
  Object& operator=(const Object&) = delete;
};
```

如果类型支持移动：

```cpp
Object(Object&&) noexcept = default;
Object& operator=(Object&&) noexcept = default;
```

资源管理类必须明确其：

* Copy
* Move
* Destructor

行为。

---

# 24. 构造函数

单参数构造函数默认使用 `explicit`。

```cpp
explicit Object(int value);
```

避免产生意外的隐式类型转换。

---

# 25. 虚函数

重写基类虚函数必须使用：

```cpp
override
```

例如：

```cpp
void Execute() override;
```

如果类不允许继续继承，可以使用：

```cpp
class Example final {
};
```

---

# 26. 类成员顺序

推荐顺序：

```cpp
class Example {
 public:
  // 构造函数和析构函数

  // 公共接口

  // Getter / Setter

 protected:
  // protected 接口

 private:
  // 私有函数

  // 成员变量
};
```

访问权限顺序：

```text
public
protected
private
```

---

# 27. 函数设计

函数应该：

* 单一职责
* 参数数量合理
* 副作用明确
* 返回值明确

避免一个函数同时负责：

```text
读取文件
解析数据
处理数据
保存文件
打印日志
```

应该拆分成多个职责明确的函数。

---

# 28. 函数参数

避免不必要的值拷贝。

不修改对象：

```cpp
void Process(const Object& object);
```

需要修改对象：

```cpp
void Process(Object& object);
```

需要取得所有权：

```cpp
void Process(std::unique_ptr<Object> object);
```

小型基础类型直接值传递：

```cpp
void SetSize(int size);
void SetEnabled(bool enabled);
```

---

# 29. 返回值

优先通过返回值表达结果。

```cpp
bool Initialize();
Result Load();
std::string GetName();
```

避免使用输出参数：

```cpp
bool GetName(std::string* name);
```

除非存在明确的性能、兼容性或 API 设计原因。

---

# 30. 布尔表达式

保持条件表达式简单。

推荐：

```cpp
if (value == nullptr) {
  return false;
}
```

复杂条件应拆分：

```cpp
const bool valid_input = input != nullptr;
const bool valid_size = size > 0;

if (!valid_input || !valid_size) {
  return false;
}
```

避免过深的嵌套。

---

# 31. Early Return

错误条件可以使用 early return。

推荐：

```cpp
if (!IsValid()) {
  return false;
}

if (!Initialize()) {
  return false;
}

return true;
```

避免：

```cpp
if (IsValid()) {
  if (Initialize()) {
    return true;
  }
}

return false;
```

---

# 32. switch

`switch` 必须明确处理所有可能情况。

```cpp
switch (status) {
  case Status::kRunning:
    Run();
    break;

  case Status::kStopped:
    Stop();
    break;

  default:
    HandleUnknownStatus();
    break;
}
```

禁止无意的 fall-through。

如果确实需要 fall-through，应明确标识。

---

# 33. 大括号

统一使用大括号。

```cpp
if (condition) {
  DoSomething();
}
```

即使只有一条语句，也不省略：

```cpp
if (condition) {
  return;
}
```

禁止：

```cpp
if (condition)
  return;
```

---

# 34. 缩进

使用 **2 个空格**。

禁止使用 Tab 进行代码缩进。

例如：

```cpp
if (condition) {
  DoSomething();

  if (condition2) {
    DoSomethingElse();
  }
}
```

---

# 35. 行长度

普通代码行原则上不超过 **80 个字符**。

如果强制换行会严重降低可读性，可以适当超过。

函数调用：

```cpp
const auto result = Process(
    input,
    options,
    callback);
```

---

# 36. 空格

运算符两侧使用空格：

```cpp
int value = a + b;
```

逗号后使用空格：

```cpp
Function(a, b, c);
```

函数调用括号前不加空格：

```cpp
Function();
```

控制语句括号前加空格：

```cpp
if (condition) {
}
```

---

# 37. 空行

使用空行区分不同逻辑。

推荐：

```cpp
Initialize();

LoadData();

ProcessData();

SaveData();
```

不应大量连续空行。

---

# 38. 注释

注释应该解释：

* 为什么这样做
* 特殊约束
* 非显而易见的设计
* 算法原理
* 外部接口限制

不要简单重复代码：

```cpp
// Increment i by 1.
++i;
```

这种注释没有价值。

---

# 39. TODO

暂时无法完成的工作使用：

```cpp
// TODO(username): Description.
```

例如：

```cpp
// TODO(user): Add validation for malformed input.
```

TODO 应尽可能描述：

* 谁负责
* 要做什么

---

# 40. 公共 API 注释

公共 API 应提供必要的文档说明。

例如：

```cpp
// Returns the current configuration.
//
// Returns:
//   The current configuration object.
Config GetConfig() const;
```

公共接口的注释应重点说明：

* 功能
* 参数
* 返回值
* 异常
* 生命周期要求
* 线程安全要求

---

# 41. Magic Number

避免直接使用没有语义的数字。

不推荐：

```cpp
if (size > 1024) {
}
```

推荐：

```cpp
constexpr int kMaxSize = 1024;

if (size > kMaxSize) {
}
```

但是对于明显的数学表达式，可以保留：

```cpp
const double area = width * height / 2.0;
```

---

# 42. 字符串

普通字符串使用：

```cpp
std::string
```

只读字符串视图可以使用：

```cpp
std::string_view
```

不要使用：

```cpp
const char* 
```

作为普通字符串的默认表示。

与 C API 交互时除外。

---

# 43. 时间

涉及时间时使用标准时间类型：

```cpp
std::chrono
```

例如：

```cpp
std::chrono::milliseconds
std::chrono::seconds
```

避免直接使用没有单位含义的整数：

```cpp
int timeout = 1000;
```

优先：

```cpp
std::chrono::milliseconds timeout{1000};
```

---

# 44. 类型转换

优先使用 C++ 显式转换：

```cpp
static_cast<int>(value);
const_cast<T*>(value);
reinterpret_cast<T*>(value);
dynamic_cast<T*>(value);
```

禁止使用 C 风格转换：

```cpp
(int)value;
```

转换必须明确其目的。

---

# 45. C 风格数组

优先使用：

```cpp
std::array
std::vector
std::string
```

避免：

```cpp
int values[10];
```

对于固定大小且需要栈上数组的场景可以使用：

```cpp
std::array<int, 10> values;
```

---

# 46. 容器选择

根据语义选择容器：

```text
std::vector      连续动态数组
std::array       固定大小数组
std::deque       双端队列
std::list        双向链表
std::map         有序键值结构
std::unordered_map  哈希键值结构
std::set         有序集合
std::unordered_set 哈希集合
```

默认优先考虑：

```cpp
std::vector
```

不要仅因为“可能需要”就选择复杂容器。

---

# 47. 范围 for

遍历容器时优先使用范围 for。

```cpp
for (const auto& item : items) {
  Process(item);
}
```

需要修改：

```cpp
for (auto& item : items) {
  Update(item);
}
```

不需要索引时不要使用传统下标循环。

---

# 48. 头文件设计

头文件应该尽量轻量。

优先使用前向声明减少依赖：

```cpp
class Manager;
```

而不是不必要地：

```cpp
#include "manager.h"
```

但是对于标准库类型，应根据实际情况直接包含所需头文件。

不要为了减少 include 而牺牲代码正确性。

---

# 49. 头文件中的实现

普通类成员函数优先放在 `.cc` 文件中。

头文件主要包含：

* 类型声明
* 类声明
* 函数声明
* 必要的模板实现
* 必要的 inline 实现

模板代码如果必须放在头文件中，可以直接实现。

---

# 50. 全局变量

禁止使用可修改的全局变量。

不推荐：

```cpp
int g_count = 0;
```

优先：

```cpp
class Manager {
 private:
  int count_ = 0;
};
```

如果确实需要全局常量：

```cpp
constexpr int kMaxCount = 100;
```

---

# 51. static

`static` 应根据实际语义使用。

文件内部私有函数可以使用匿名命名空间：

```cpp
namespace {

void Helper() {
}

}  // namespace
```

不推荐在 `.cc` 文件中大量使用：

```cpp
static void Helper();
```

对于 C++ 项目，优先使用匿名命名空间表达内部链接。

---

# 52. 匿名命名空间

只供当前 `.cc` 文件使用的函数、变量、类型，可以放入匿名命名空间：

```cpp
namespace {

constexpr int kDefaultValue = 10;

void Helper() {
}

}  // namespace
```

不要将内部实现暴露到公共命名空间。

---

# 53. 线程安全

线程安全必须明确。

如果一个类不是线程安全的，不要求为了“看起来安全”而增加无意义的锁。

公共 API 如果要求线程安全，应在文档中明确说明。

例如：

```cpp
// Thread-safe.
void SetValue(int value);
```

或者：

```cpp
// Not thread-safe. Calls must be externally synchronized.
void SetValue(int value);
```

---

# 54. 并发代码

优先使用标准 C++ 并发设施：

```cpp
std::mutex
std::lock_guard
std::unique_lock
std::condition_variable
std::thread
std::atomic
```

锁的生命周期必须使用 RAII。

推荐：

```cpp
std::lock_guard<std::mutex> lock(mutex_);
```

避免手动：

```cpp
mutex_.lock();

...

mutex_.unlock();
```

---

# 55. 错误处理

错误处理方式必须保持一致。

错误可以通过：

* 返回值
* `std::optional`
* `std::expected`
* 异常

表达。

项目应选择统一策略，不允许不同模块随意采用不同方式。

错误信息应包含足够上下文。

例如：

```text
Failed to open configuration file: xxx
```

而不是：

```text
Failed.
```

---

# 56. 异常

异常应该用于真正的异常情况，而不是普通控制流程。

禁止：

```cpp
try {
  ...
} catch (...) {
  ...
}
```

然后静默忽略错误。

捕获异常后必须：

* 处理
* 转换
* 记录
* 重新抛出

至少完成其中一种有意义的操作。

---

# 57. 测试代码

测试代码也必须遵循本规范。

测试名称应表达测试行为。

推荐：

```cpp
TEST(FooTest, ReturnsFalseWhenInputIsInvalid) {
}
```

避免：

```cpp
TEST(Test1) {
}
```

测试应该：

* 独立
* 可重复
* 不依赖执行顺序
* 失败时提供明确上下文

---

# 58. 性能

性能优化必须基于实际测量。

禁止仅凭主观判断进行优化。

优化之前：

```text
Measure → Identify bottleneck → Optimize → Measure again
```

不要为了避免一次拷贝而引入明显复杂的代码，除非性能数据证明该拷贝确实是瓶颈。

---

# 59. 未定义行为

禁止依赖未定义行为。

特别注意：

* 越界访问
* 悬空引用
* 悬空指针
* use-after-free
* double free
* 未初始化变量
* 有符号整数溢出
* 错误的类型转换

---

# 60. 生命周期

对象生命周期必须明确。

尤其关注：

* 引用
* 指针
* callback
* lambda 捕获
* 异步任务
* 线程
* 全局对象

避免返回局部变量的引用：

```cpp
const std::string& GetName() {
  std::string name;
  return name;
}
```

这是错误的。

---

# 61. Lambda

Lambda 捕获列表必须明确。

优先：

```cpp
[&value]() {
  Process(value);
}
```

而不是无理由：

```cpp
[&]() {
  Process(value);
}
```

特别是在异步代码中，应避免无意识捕获局部变量引用。

---

# 62. C++ 标准

项目应明确指定 C++ 标准版本。

例如：

```text
C++17
```

或者：

```text
C++20
```

不得在同一个项目中随意混用不同语言标准。

代码只能使用项目声明的 C++ 标准所支持的语言特性。

---

# 63. 编译器警告

项目应开启合理的编译器警告。

警告原则：

> 警告不是错误，但重要警告不应被忽略。

禁止通过大量：

```cpp
#pragma warning(disable: ...)
```

掩盖实际问题。

如果必须关闭某个警告，应：

1. 明确原因
2. 尽可能缩小作用范围
3. 添加注释

---

# 64. 静态检查

项目建议使用：

* clang-format
* clang-tidy
* 编译器 warning
* AddressSanitizer
* UndefinedBehaviorSanitizer
* 静态分析工具

格式化工具用于统一格式。

静态分析工具用于发现潜在问题。

两者不能互相替代。

---

# 65. Git 提交

提交代码前必须确保：

* 编译通过
* 测试通过
* 无新增严重 warning
* 格式符合规范
* 不提交临时文件
* 不提交编译产物
* 不提交调试日志
* 不提交敏感信息

禁止提交：

```text
*.exe
*.dll
*.obj
*.pdb
build/
.vs/
.idea/
```

具体忽略规则由项目 `.gitignore` 统一管理。

---

# 66. Code Review

Code Review 至少检查以下内容：

### 命名

* [ ] 类名符合规范
* [ ] 函数名符合规范
* [ ] 变量名符合规范
* [ ] 成员变量符合规范
* [ ] 常量符合规范

### 设计

* [ ] 单一职责
* [ ] 生命周期明确
* [ ] 所有权明确
* [ ] 没有不必要的复杂设计

### 资源

* [ ] 没有资源泄漏
* [ ] 优先使用 RAII
* [ ] 正确使用智能指针

### 安全

* [ ] 没有明显越界
* [ ] 没有悬空引用
* [ ] 没有悬空指针
* [ ] 没有未初始化变量
* [ ] 没有未定义行为

### 可维护性

* [ ] 函数职责清晰
* [ ] 注释解释必要的设计原因
* [ ] 没有明显重复代码
* [ ] 没有无意义的抽象

---

# 67. 规范优先级

当不同规范发生冲突时，按照以下优先级处理：

1. C++ 语言标准
2. 编译器和工具链要求
3. 项目架构规范
4. 本编码规范
5. Google C++ Style Guide
6. 个人编码习惯

项目已有明确约定时，应优先遵循项目约定。

---

# 68. 例外处理

规范不是为了限制合理的工程设计。

如果确实需要违反某项规范，应满足：

1. 有明确技术原因
2. 影响范围尽可能小
3. 添加必要注释
4. Code Review 时说明原因

不允许以“个人习惯”为理由违反规范。

---

# 69. 推荐工具配置

建议项目统一配置：

```text
.clang-format
.clang-tidy
.editorconfig
.gitignore
```

其中：

| 文件              | 用途        |
| --------------- | --------- |
| `.clang-format` | 自动代码格式化   |
| `.clang-tidy`   | 静态代码检查    |
| `.editorconfig` | 编辑器基础格式统一 |
| `.gitignore`    | Git 文件过滤  |

---

# 70. 规范执行原则

本规范最终目标不是让代码“看起来统一”，而是降低长期维护成本。

因此：

* 格式问题交给工具解决
* 命名问题通过 Code Review 解决
* 架构问题通过设计评审解决
* 性能问题通过 Benchmark 解决
* 正确性问题通过测试和静态分析解决

开发人员不应花大量时间争论可以由自动化工具解决的问题。

---

# 71. 最低强制要求

所有提交到主分支的 C++ 代码至少必须满足：

1. 使用统一的文件命名规则
2. 使用统一的命名规则
3. 使用 `nullptr`
4. 不使用 C 风格类型转换
5. 不使用 `using namespace`
6. 优先使用 RAII
7. 优先使用智能指针管理所有权
8. 不允许明显的资源泄漏
9. 不允许明显的未定义行为
10. 不提交编译产物和临时文件
11. 代码能够通过项目规定的格式化工具
12. 代码能够通过项目规定的编译和测试
13. 不允许通过关闭警告掩盖代码问题
14. 公共 API 必须具有明确的接口语义
15. 违反规范必须有明确的技术理由

---

# 72. 参考规范

本规范主要参考：

* Google C++ Style Guide
* ISO C++ Standard
* C++ Core Guidelines
* LLVM Coding Standards

具体工具和项目配置应以项目自身的构建环境和工程规范为准。
