# event loop

Là cơ chế quan trọng thực thi lập trình bất đồng bộ, nằm trong module libuv

Event loop sẽ liên  tục quét rồi lấy ra các hàm trong callback queue, sau đó đẩy qua call stack  của V8 để thực thi.

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



Lý do vì sao setTimeout\(0\) luôn thực thi sau setImmediate ???

process.nextTick thì làm gì ???

