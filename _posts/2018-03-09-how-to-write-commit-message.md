---
layout: post
title:  "Git Commit"
date:   2018-03-09 13:24:00 +0800
categories: Github
tags: github commit-msg
---

## 一个良好的commit格式：

```
<type><(scope)>: <subject><(#issueId)>
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

### scope: 
 
 can be empty (eg. if the change is a global or difficult to assign to a single component)

### subject: 

start with verb (such as 'change'), 50-character line

### body:
  
 72-character wrapped. This should answer:
 * Why was this change necessary?
 * How does it address the problem?
 * Are there any side effects?

### footer: 
 - Include a link to the ticket, if any.
 - BREAKING CHANGE


## 参考项目

- [Angular](https://github.com/angular/angular/commits/master)
- [NG-ZORRO](https://github.com/NG-ZORRO/ng-zorro-antd/commits/master)
