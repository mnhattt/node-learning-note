```
console.log('script start')

const interval = setInterval(() => {
    console.log('setInterval')
}, 0)

setTimeout(() => {
    console.log('setTimeout 1 ')
    Promise.resolve().then(() => {
        console.log('promise 3')
    }).then(() => {
        console.log('promise 4')
    }).then(() => { // chèn setInterval 
        setTimeout(() => {
            console.log('setTimeout 2')
            Promise.resolve().then(() => {
                console.log('promise 5')
            }).then(() => {
                console.log('promise 6')
            }).then(() => {
                clearInterval(interval)
            })
        }, 0)
    })
}, 0)

Promise.resolve().then(() => {
    console.log('promise 1')
}).then(() => {
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

khi stack rống, event-loop quét task queue để chọn task đẩy vào stack.

1. mirco-task sẽ được duyệt trước marco-task\(??\). Thứ tự ưu tiên là

* process.nextTick

* promise

   Ở trường hợp trên thì promise 1 và promise 2 sẽ thực thi trước

2. Sau đó tới lượt marco-task setInterval\(\) và setTimeout\(\)

setInterval\(\) ưu tiên chạy trước setTimeout\(\) \(??\) =&gt; setInterval =&gt; setTimeout 1  + promise 3 =&gt; promise 4  
3. Sau khi setTimeout\(\) chạy xôi



![](/assets/micro-marco.png)

