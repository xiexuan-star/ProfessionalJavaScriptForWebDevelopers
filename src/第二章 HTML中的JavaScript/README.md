# 第二章 HTML中的JavaScript

## 2.1 \<script\>元素

8个属性:

async: 立即下载脚本, 但不阻止其他页面动作

脚本不一定按照声明顺序执行, 且不一定在DOMContentLoaded事件后执行

charset(abandoned): 代码字符集

crossorigin: 配置相关请求的CORS设置

defer: 脚本立即下载,但延迟到文档被完全解析和显示之后再执行,只对外部脚本有效

同时, 脚本会按照声明的顺序执行

integrity: SRI, 比对资源于制定的加密签名以验证子资源完整性

language(abandoned): 废弃

src: 外部文件, 会忽略行内代码. 同时, 初次请求不会受CORS的影响

type: 一般都为"text/javascript"

### 2.1.1 标签位置

### 2.1.2 推迟执行脚本

### 2.1.3 异步执行脚本

### 2.1.4 动态加载脚本

通过创建script标签来动态插入脚本

### 2.1.5 XHTML中的变化

### 2.1.6 废弃的语法

## 2.2 行内代码与外部文件


