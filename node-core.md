# ![](/assets/node-core.png)

# cụ thể hơn

# ![](/assets/node-core-2.png)

# Core module

* C++ core
* JS core

---

# V8 Engine

V8 là một javascrpit engine dùng để biên dịch ra mã thực thi trên vi xử lý. Do được viết bằng C++ nên nó có thể được dùng độc lập hoặc được [nhúng](https://github.com/v8/v8/wiki/Getting-Started-with-Embedding) vào các chương trình viết bằng C++ khác.

Mã nguồn của V8 được dùng trong node có thể xem trong thư mục [deps/v8](https://github.com/nodejs/node/tree/master/deps/v8)

Có thể thử biên dịch một ví dụ về [js shell ](https://github.com/v8/v8/tree/master/samples)

dùng lệnh `shell --print_code` để xem code được biên dịch ra mã thực thi

thử thêm một chức năng\(lệnh\) greeting vào shell

### chú ý là dòng `#include <include/v8.h>`

# 

Ở trên đã thấy cách dùng V8, thì việc thực thi code js giống như ta nhập vào shell, nó sẽ được biên dịch ra mã máy và chạy. Tuy nhiên không phải thư viện nào cũng cần binding JS với C++ mà chỉ  thuần túy chứa các hàm.

### chú ý dòng  `const binding = process.binding('');`

---

# libuv



# 



