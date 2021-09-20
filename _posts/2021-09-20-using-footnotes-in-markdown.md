---
title: "Markdown에서 각주를 사용하는 방법" 
excerpt: "Markdown에서 각주를 사용하는 두가지 방법을 설명합니다."
show_date: true
read_time: true

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#CD5C5C"

categories: 
- markdown
tags: 
- markdown
- footnotes
- github
---

Markdown에서 각주를 사용하는 법은 두가지 정도로 정리할 수 있습니다.

### 첫번째 방법
[Markdown Extended Syntax](https://www.markdownguide.org/extended-syntax/)의 Footnotes 기능을 사용하는 방법입니다(typora, joplin 등). 이 방법은 Markdown Extended Syntax가 적용되지 않는 곳에서는 적용되지 않습니다. 이 방법을 사용할 경우 자동으로 각주가 문서 제일 뒷편에 표시됩니다.

```
이것은 각주[^1]에 대한 것입니다.

[^1]: 각주에 대한 설명
```
예제) 이것은 각주[^1]에 대한 것입니다.

[^1]: 각주에 대한 설명(첫번째 방법)

### 두번째 방법
html을 사용하여 각주를 구현하는 방법입니다. 이 방법을 사용할 경우 수동으로 문서 제일 뒷편에 각주를 옮겨야 합니다.

```
이것은 각주<sup>[1](#footnote_1)</sup>에 대한 것입니다.

<!-- 글 뒷 부분에 -->
<a name="footnote_1">1</a>: 각주에 대한 설명
```
예제) 이것은 각주<sup>[1](#footnote_1)</sup>에 대한 것입니다.

<a name="footnote_1">1</a>: 각주에 대한 설명(두번째 방법)
