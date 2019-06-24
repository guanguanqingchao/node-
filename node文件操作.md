### Buffer
JS支持字符串，对字符串的操作是只读。Buffer是二进制形式，可以转换为字符串，Buffer可以对二进制进行修改。
Buffer将JS的数据处理能力从字符串扩展到了任意二进制数据。


    fs.readFileSync(process.argv[1]).toString('utf-8')
### stream

### File System（文件系统）

NodeJS通过fs内置模块提供对文件的操作。fs模块提供的API基本上可以分为以下三类：

#### 文件属性读写。其中常用的有fs.stat、fs.chmod、fs.chown等等。

#### 文件内容读写。其中常用的有fs.readFile、fs.readdir、fs.writeFile、fs.mkdir等等。

#### 底层文件操作。其中常用的有fs.open、fs.read、fs.write、fs.close等等。

NodeJS最精华的异步IO模型在fs模块里有着充分的体现，例如上边提到的这些API都通过回调函数传递结果。以fs.readFile为例：

    fs.readFile(pathname, function (err, data) {
        if (err) {
            // Deal with error.
        } else {
            // Deal with data.
        }
    });
### path 文件路径

    __dirname /Users/didi/PersonalTest/node_modules
    __dirname /Users/didi/PersonalTest/CMS_SYS/node_modules
    // Users/didi/PersonalTest/CMS_SYS
    console.log('__dirname', path.join(__dirname, '../node_modules')) 
    console.log('__dirname', path.join(__dirname, './node_modules'))
  
  深度优先遍历获取目录路径

    function travel(dir, callback) {
        fs.readdirSync(dir).forEach(function (file) {
            var pathname = path.join(dir, file);

            if (fs.statSync(pathname).isDirectory()) {
                travel(pathname, callback);
            } else {
                callback(pathname);
            }
        });
    }

    console.log(fs.readdirSync('./home/user')) //获取user目录下的文件

    travel('./home/user', function (pathname) {
        console.log('pathname', pathname)
    })



