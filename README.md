# node-wget

A download tool, now supporting http/https resource and http/https proxy, written in nodejs.
Forked from https://github.com/wuchengwei/node-wget - Only one change : when a file is downloaded, if a file with the same name already existed, it will be overwritten and not appened.

# Installing
```
npm install git+https://github.com/Pixcell/node-wget.git
```

# Usage

<a name="download" />
## download(src, output, options)

```js
var wget = require('wget');
var src = 'https://raw.github.com/Fyrd/caniuse/master/data.json';
var output = '/tmp/data.json';
var options = {
    proxy: 'http://host:port'
};
var download = wget.download(src, output, options);
download.on('error', function(err) {
    console.log(err);
});
download.on('end', function(output) {
    console.log(output);
});
download.on('progress', function(progress) {
    // code to show progress bar
});
```

<a name="request" />
## request(options, callback)

```js
var wget = require('wget');
var options = {
    protocol: 'https',
    host: 'raw.github.com',
    path: '/Fyrd/caniuse/master/data.json',
    proxy: 'http://host:port',
    method: 'GET'
};
var req = wget.request(options, function(res) {
    var content = '';
    if (res.statusCode === 200) {
        res.on('error', function(err) {
            console.log(err);
        });
        res.on('data', function(chunk) {
            content += chunk;
        });
        res.on('end', function() {
            console.log(content);
        });
    } else {
        console.log('Server respond ' + res.statusCode);
    }
});

req.end();
req.on('error', function(err) {
    console.log(err);
});
```
