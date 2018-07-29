---
layout: post
title:  "Jekyll 中尝试 mermaid"
description: ""
tags: 测试，博客，markdown
mermaid: true
comments: true
date: 2018/07/29 19:27:00
---

## GitHub 项目用例
{% mermaid %}
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
{% endmermaid %}

## 尝试其他 mermaid 语法

{% mermaid %}
sequenceDiagram;
participant 已暂存;
participant 已修改;
participant 已提交;
已暂存 ->> 已修改: 修改文件，比如在 bash 中使用 vim 命令;
已修改 ->> 已暂存: git add fileName;
已暂存 ->> 已提交: git commit;
已修改 ->> 已提交: git commit -a 可以跳过加入暂存区;
{% endmermaid %}
