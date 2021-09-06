---
title: "minimal-mistakes에 utterances 적용하기" 
excerpt: "minimal-mistakes 테마를 적용한 블로그의 댓글 시스템으로 utterances를 적용하는 방법을 설명합니다.  "
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#333"
  actions:
    - label: "More Info"
      url: "https://utteranc.es/"

categories: 
- github 
tags: 
- utterances
- comment
- minimal-mistakes
- jekyll
---

## minimal-mistakes에 utterances 적용하기

기본적으로 jekyll에는 댓글을 달기 위한 시스템이 존재하지 않는다. 따라서 댓글을 달기 위해서는 외부 댓글 시스템을 이용해야 하는데, 연동 가능한 댓글 시스템으로는 [disqus](https://disqus.com/), [discourse](https://www.discourse.org/), [facebook](https://developers.facebook.com/docs/plugins/comments/#configurator), [Staticman](https://staticman.net/), [utterances](https://utteranc.es/) 등이 있다. 여기서는 그 중에서 utterances를 적용하기 위한 방법을 설명한다.

### utterances의 장점

utterances의 장점으로는,

- 가볍다
- 광고가 없다
- github 계정 로그인을 통해 댓글을 달 수 있다
- 댓글이 달리면 repository의 issue에 저장되며, 메일로 알림을 받을 수 있다
- 댓글에 markdown을 적용할 수 있다

### utterances 적용 방법

#### 1. repository 생성

댓글이 저장될 repository를 생성한다. 이름은 임의로 정해도 관계없다.

#### 2. utterances 설치

<https://github.com/apps/utterances>을 클릭하면 아래 그림과 같이 utterances 앱을 설치할 수 있는 화면이 나온다. 현재 이미 설치되어 있어 **configure**라고 되어 있지만, 신규 설치 시에는 **install**이라고 나오니 해당 버튼을 클릭하여 설치를 진행한다. 이후 나오는 화면에서 댓글을 저장하기 위한 repository를 선택한다.

<p align="left"><img src="{{ site.url }}/assets/img/utterances1.jpg"></p>

#### 3. utterances 설정

utterances 설정을 위해서 `_config.yml`을 연 후, 댓글 관련 설정을 아래와 같이 수행한다.

```yaml
comments:
  provider: "utterances"
  utterances:
    theme: "github-light"
    issue_term: "pathname"
```

여기서, `theme` 및 `issue_term`은 [utterances 설정 페이지](https://utteranc.es/?installation_id=19298349&setup_action=install)의 **Theme** 부분과 **Blog Post ↔ Issue Mapping** 부분을 참조하여 값을 입력한다.

<p align="left"><img src="{{ site.url }}/assets/img/utterances2.jpg"></p>

<p align="left"><img src="{{ site.url }}/assets/img/utterances3.jpg"></p>

만약 minimal-mistakes를 사용하지 않는다면 설정 페이지 하단에 생성된 스크립트를 복사하여 적절한 위치에 삽입하면 된다.

<p align="left"><img src="{{ site.url }}/assets/img/utterances4.jpg"></p>