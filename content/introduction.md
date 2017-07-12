## docbox系统使用说明

### 下载运行项目
```html
git clone https://github.com/tomapto/docbox
npm install
npm start
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
左侧导航最小识别 三级标题 
更低级标题也会显示但是与三级标题显示无差别

不同语言 使用markdown的 三个反引号 后面加语言类型即可按照语言显示代码

如:
    ```javascript


