---
title: "YAML front matter 예제" 
excerpt: "github.io에서 YAML front matter 직성시 참고용 예제" 

# toc: true # toc on/off
# toc_sticky: true # toc를 우측으로 이동 고정
# toc_label: "Page Index"
# toc_icon: "cog"
# classes: wide # 와이드 페이지 설정

header:
  overlay_image: /assets/img/0003_header.jpg # image를 상단 고정 후 제목과 overlay
  overlay_filter: 0.5
  # overlay_filter: rgba(255, 0, 0, 0.5)
  # overlay_filter: linear-gradient(rgba(255, 0, 0, 0.5), rgba(0, 255, 255, 0.5))
  # overlay_color: "#333"
  caption: "Image credit: [**jekyllrb.com**](/https://jekyllrb.com/docs/front-matter/)"
  actions:
    - label: "More Info"
      url: "https://jekyllrb.com/docs/front-matter/"

categories: 
- markdown
tags: 
- YAML front matter
- sample
---

YAML front matter
```
---
title: "제목" 
excerpt: "간단한 요약문"
show_date: true # 발행일자 표시여부
read_time: true # 읽는데 소요되는 시간 표시여부

toc: true # toc on/off
toc_sticky: true # toc를 우측으로 이동 고정
toc_label: "Page Index"
# toc_icon: "cog"

# classes: wide # 와이드 페이지 설정

header:
  overlay_image: /assets/img/header.jpg # image를 상단 고정 후 제목과 overlay
  # show_overlay_excerpt: true
  overlay_filter: 0.5
  # overlay_filter: rgba(255, 0, 0, 0.5)
  # overlay_filter: linear-gradient(rgba(255, 0, 0, 0.5), rgba(0, 255, 255, 0.5))
  # overlay_color: "#333"
  caption: "Photo credit: [**Connieklubephoto**](/www.connieklubephoto.com)"
  actions:
    - label: "More Info"
      url: "https://unsplash.com"

categories: 
- 일반 
tags: 
- markdown
- 예제
---
```
