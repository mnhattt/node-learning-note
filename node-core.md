# Core module

các moudule chức năng như fs, http, ... viết bằng JS

# Node api

Một số module chạy với C++ addon được binding bằng V8 engine

http://latentflip.com/loupe/

# V8 engine

Giả sử Node xử lý IO xong sẽ gọi hàm callback, các hàm callback sẽ được pass vào event queue cho V8 xử lý, xử lý xong sẽ pass về node lại

# libuv

quản lý async IO

thread pool

![](http://docs.libuv.org/en/v1.x/_images/architecture.png)

