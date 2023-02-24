---
title: AJAX笔记
tags:
  - 笔记
categories:
  - 学习笔记
date: 2022-05-27 18:13:41
updated: 2022-05-27 18:13:41
---
## fetch
>网站中可使用，nodejs需要安装第三方库

### 参数
res包含的一些内置函数：
- `res.text()`：返回 URL 的文本内容。如果是网站，则返回 HTML。
- `res.json()`：返回格式化的 JSON 数据。
- `res.blob()`: 返回 blob 数据。
- `res.arrayBuffer()`：返回数组缓冲区数据
- `res.formData()`：返回 formData 数据。
<!-- more -->
### 基本使用
```js
fetch('url')
    .then(res => res.json())
    .then((data) => {
      console.log(data);
    });
```
### 搭配async/await
```js
async function func() {
    let data = await fetch('url').then(res => res.json());
    // 或者：let data = await (await fetch('url')).json()
    return data
}
```

## axios
> axios的请求是异步的，使用时要注意。

### 基本使用
```js
axios.get('url')
      .then(({ data }) => {
        console.log(data);
      })
      .catch((error) => {
        console.log(error);
      });
```
### 搭配async/await
```js
async function func() {
  let { data } = await axios.get(url)
  return data
},
```

## 原生js封装ajax
```js
var Ajax = {
    get: function(url, fn) {
        // XMLHttpRequest对象用于在后台与服务器交换数据   
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onreadystatechange = function() {
            // readyState == 4说明请求已完成
            if (xhr.readyState == 4 && xhr.status == 200 || xhr.status == 304) {
                // 从服务器获得数据 
                fn.call(this, xhr.responseText);
            }
        };
        xhr.send();
    }
}
// 使用Ajax
Ajax.get('url', (e) => {})
```
