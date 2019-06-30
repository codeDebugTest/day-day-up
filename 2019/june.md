# 六月

## 01
* [单点登录](https://yq.aliyun.com/articles/636281)
* [单点登录实现](https://www.cnblogs.com/ZenoLiang/p/8334614.html)

## 30
### svg 处理
#### raw-loader 
提取svg文件内容，并注入到javascript 或 css 中   

eg. 在javacript 中：
``` javascript
    import svgContent from './icons/alert.svg';
```
raw-loader 处理后的代码：
``` javascript
    module.exports = "<svg xmlns=\"http://www.w3.org/2000/svg\"... </svg>"
```
即 svgContent 的内容等于字符串形式的svg。由于svg 本身就是html 元素，在获取到svg内容后，通过以下代码可以直接插入到html 中去：
``` javascript
    window.document.getElementById('app').innerHTML = svgContent;
```
> 由于 raw-loader 会直接返回 SVG 的文本内容，并且无法通过 CSS 去展示 SVG 的文本内容，因此采用本方法后无法在 CSS 中导入 SVG。 也就是说在 CSS 中不可以出现 background-image: url(./svgs/activity.svg) 这样的代码，因为 background-image: url(<svg>...</svg>) 是不合法的。

#### svg-inline-loader 
svg-inline-loader 与上述 raw-loader 相似，不同在于svg-inline-loader 会分析svg文件内容，去除不必要的代码，以减少svg文件体积。也就是说 svg-inline-loader 增加了对 SVG 的压缩功能。

#### svgo-loader
将 <svg> 中一些无用的信息过滤去除，精简结构.例如：删除掉path 标签内的注释信息。