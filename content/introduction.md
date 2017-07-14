
# 文档格式说明

## docbox系统使用说明

###  下载运行项目
```html
$ git clone https://github.com/tomapto/docbox
$ npm install
$ npm start
```


### 附加md文件
修改 /src/custom/content.js文件

```javascript
module.exports =
    '# 结构\n' +
    // fs.readFileSync('./content/introduction.md', 'utf8') + '\n' +
    '# 使用帮助\n' +
    fs.readFileSync('./content/documentation.md', 'utf8') + '\n';
    //附加新的文件读取即可
```
### 说明
1. 左侧导航最小识别 ,三级标题 更低级标题也会显示但是与三级标题显示无差别

2. 不同语言 使用markdown的 三个反引号 后面加语言类型即可按照语言显示代码

3. 不同的语言类型会在不同的语言模式下隐藏显示 如果是都需要显示 可以将语言设置为 html


### 语言类型
如:
    ```javascript
支持语言

语言类型|说明|显示范围
|-:|-:|-:|
javascript||JavaScript
bash||CLI
curl||curl
python||Python
java||Java
objc||objective-c
swift||Swift
endpoint|URL请求 值包括 PUT,POST,GET,DELETE,PATCH|所有
html||所有
json||所有
http||所有


### 请求
    ```
    GET /wobbles/v1/{username} wobbles:read
    ```
```endpoint
GET /wobbles/v1/{username} wobbles:read
```

### 命令行代码
    ```curl
    $ curl https://wobble.biz/wobbles/v1/{username}
    ```


```curl
$ curl https://wobble.biz/wobbles/v1/{username}
```
