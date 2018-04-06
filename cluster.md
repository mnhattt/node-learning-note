# Cluster

Dùng cluster để xử lý các request tới bởi các tiến trình khác nhau.  
\* Vấn đề: request tới cùng 1 route vẫn được xử lý bởi các process khác nhau nhưng thời gian xử lý rất lâu.  


```text
// index.js

const express = require('express')
var app = express()

function doWork(duration) {
    const start = Date.now()
    while (Date.now() - start < duration) {} // spin 
}

app.get('/', (req, res) => {
    doWork(5000)
    res.send('hello')
})

app.listen(4000)
```

Dùng cluster để fork ra nhiều process xử lý request

```text
const cluster = require('cluster')

if (cluster.isMaster) {
    console.log(`Master ${process.pid} is running`);
    cluster.fork()
    cluster.fork()
    cluster.fork()
} else {
    console.log(`Worker ${process.pid} started`);
    const express = require('express')
    var app = express()

    function doWork(duration) {
        const start = Date.now()
        while (Date.now() - start < duration) {} // spin 
    }

    app.get('/', (req, res) => {
        doWork(3000)
        res.send('hello, server by' + ` process ${process.pid}`)

    })
    app.get('/fast', (req, res) => {
        res.send('fast request, server by' + ` process ${process.pid}`)
    })

    app.listen(4000)
}
```



