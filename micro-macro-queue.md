```js
const interval = setInterval(() => {
    console.log('setInterval')
}, 0)

setTimeout(() => {
    console.log('setTimeout 1 ')
    Promise.resolve()
        .then(() => {
            console.log('promise 3')
        })
        .then(() => {
            console.log('promise 4')
        })
        .then(() => {
            setTimeout(() => {
                console.log('setTimeout 2')
                Promise.resolve()
                    .then(() => {
                        console.log('promise 5')
                    })
                    .then(() => {
                        console.log('promise 6')
                    })
                    .then(() => {
                        clearInterval(interval)
                    })
            }, 0)
        })
}, 0)



Promise.resolve()
    .then(() => {
        console.log('promise 1')
    })
    .then(() => {
        console.log('promise 2')
    })

// kq
script start
promise 1
promise 2
setInterval
setTimeout 1 
promise 3
promise 4
setInterval // chèn
setTimeout 2
promise 5
promise 6
```

## giải thích kết quả thực hiện

1. khi stack rống, event-loop quét task queue để chọn task đẩy vào stack.
   mirco-task sẽ được duyệt trước marco-task\(??\). Thứ tự ưu tiên là

   * process.nextTick

   * promise

   Kết quả: promise 1 và promise 2 sẽ thực thi trước

2. Sau đó tới lượt marco-task setInterval\(\) và setTimeout\(\) được thực thi, một lệnh setInterval\(\) tiếp theo sẽ được đẩy ngay sau setTimeout\(\) vì time = 0.
   Kết quả:  setInterval =&gt; setTimeout 1

3. Sau khi thực thi setTimeout\(\), promise 3 và promise 4 được đẩy vào micro-task và thực thi ngay sau đó.
4. 234
5. 




1. 
setInterval\(\) ưu tiên chạy trước setTimeout\(\) \(??\) =&gt; setInterval =&gt; setTimeout 1  + promise 3 =&gt; promise 4  
3. Sau khi setTimeout\(\) chạy xong

![](/assets/micro-marco.png)

