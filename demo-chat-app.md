

Tạo 1 TCP server và lắng nghe các kết nối tới



```js
var server = require('net').createServer()

let counter = 0
let sockets = {} // gan cho moi socket.id:{socket}

server.on('connection', socket => {
    socket.id = counter++
        sockets[socket.id] = socket

    console.log(`${socket.id} connected`)
    socket.write(`Welcome ${socket.id}!\n`)

    socket.on('data', data => {
        // Object.entries(sockets)[0][1].write('emit from socket 1')
        // Object.entries(sockets).forEach(element => {
        //     element[1].write('bla bla')
        // });
        Object.entries(sockets).forEach(([, _socket]) => {
            if (_socket.id != socket.id)
                _socket.write(`${socket.id} say: ${data}`)
        });
    })

    socket.on('end', () => {
        delete sockets[socket.id]
        console.log('client is disconnect');
    })
})

server.listen(8000, () => {
    console.log('tcp server is running');
})

// bi loi chua fix duoc
process.on('uncaughtException', function (err) {
    console.log('error', 'UNCAUGHT EXCEPTION - keeping process alive:', err);
});
```



## DEMO

![](/assets/demo-chat-app.png)

