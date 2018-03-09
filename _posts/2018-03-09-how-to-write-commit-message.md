---
layout: post
title:  "Git Commit"
date:   2017-04-09 16:45:40 +0800
categories: Github
tags: github commit-msg
---

## 一个良好的commit格式：

```
<type>(module): <subject>(#issueId)
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```


### types：
- feat: 添加新特性
- fix: 修复bug
- docs: 仅仅修改了文档
- style: 仅仅修改了空格、格式缩进、都好等等，不改变代码逻辑
- refactor: 代码重构，没有加新功能或者修复bug
- perf: 增加代码进行性能测试
- test: 增加测试用例
- chore: 改变构建流程、或者增加依赖库、工具等



## 参考项目

- [Angular](https://github.com/angular/angular/commits/master)
- [NG-ZORRO](https://github.com/NG-ZORRO/ng-zorro-antd/commits/master)
