# spwan

```text
var cp = require('child_process')

var cat = cp.spawn('cat', ['big-text.txt'])
var grep = cp.spawn('grep', ['-c', 'word'])


cat.stdout.pipe(grep.stdin)
grep.stdout.pipe(process.stdout)
```



