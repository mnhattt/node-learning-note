# câu hỏi

1. ## vì sao setTimeout\( \(\), 0\) hay setImmediate\(\) vẫn chạy sau ham

```
setImmediate(function () {
    console.log('first iteration');
})
console.log('second iteration'); // chay truc tiep tu call stack

// kq
second iteration // chay truc tiep tu call stack
first iteration  // duoc day vao node roi day qua callback queue truoc khi thuc thi o call stack
```

## 2. `process.nextTick()`

```
function cb() {
    console.log('Processed in nextTick');
}

setImmediate(function () {
    console.log('Processed immediate');
})

console.log('Processed in the call stack');

process.nextTick(cb);

//kq
Processed in the call stack
Processed in nextTick
Processed immediate
```

## 3. `setImmediate()` vs `setTimeout()` vs `process.nextTick()`

nếu chỉ thuần `setImmediate()`vs `setTimeout()` thì kết quả là ko xác định được\(non-deterministic\).

setImmediate\(\) được xác định để chạy đoạn mã ngay khi poll phare hoàn thành  
Trong khi setTimeout\(\) thì xác định đoạn mã sẽ được chạy sau ÍT NHẤT bao lâu. Nếu setTimeout = 0 thì nó không có nghĩa là chạy ngay mà nó có nghĩa là đoạn mã đó sẽ được đẩy vào callback queue ngay tức khác, và nó phải chờ các hàng đợi phía trước trống mới được thực thi\(đẩy vào call stack\)

trong khi đó `process.nextTick()` có khả năng đẩy hàm callback vào vị trí đầu tiên trong hàng đợi.

# \# event loop

Là cơ chế quan trọng thực thi lập trình bất đồng bộ, nằm trong module libuv

Event loop sẽ liên tục kiểm tra call stack, nếu call stack trống sẽ kiểm tra callback queue. Nếu có hàm trong callback queue, thì  đẩy qua call stack  của V8 để thực thi.

```
   ┌───────────────────────┐
┌─>│        timers         │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     I/O callbacks     │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     idle, prepare     │
│  └──────────┬────────────┘      ┌───────────────┐
│  ┌──────────┴────────────┐      │   incoming:   │
│  │         poll          │<─────┤  connections, │
│  └──────────┬────────────┘      │   data, etc.  │
│  ┌──────────┴────────────┐      └───────────────┘
│  │        check          │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└──┤    close callbacks    │
   └───────────────────────┘
```

Quá trình thực hiện của code sẽ là code được đưa vào call stack để thực thi, nếu có callback thì sẽ được đẩy sang node  
-&gt; khi hàm callback được gọi sẽ đẩy qua event queue  
-&gt; lúc này event loop sẽ xem call stack có trống không để đẩy hàm từ queue qua loop

# \# quan hệ giữa event-loop, V8, Node

![](/assets/event-loop-2.png)

