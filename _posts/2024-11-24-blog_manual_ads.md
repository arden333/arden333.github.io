---
layout: single
title: "[blog] github 블로그에 자동광고과 수동광고 게재하기"
categories: "blog"
tags: ["자동광고", "수동광고", "blog"]

toc: true
toc_sticky: true
---

## 사용하고 있는 블로그 테마
github 블로그에 자동광고와 수동광고를 게재하는 방법에 대해 이야기 하기 전에, 이 블로그의 테마에 대해 간단히 설명하려고 한다. 
테마에 따라 html파일이 존재하는 경로나 기존에 존재하는 코드는 다를 수 있다.

<br/>
현재 이 블로그는 Jekyll 테마 중 하나인 Minimal mistake 테마를 적용 중이다. 
여러 블로그의 내용을 찾아보며 자동광고와 수동광고를 게재하려는 시도를 해보았는데, 
광고와 본문이 겹치거나 광고가 게시물을 읽는데 방해될 정도로 도배되는 문제점들을 발견하고 그것을 해결해나간 과정을 기록하였다.   

<br/>
결과적으로 자동광고와 수동광고를 섞어서 게재하기로 했다. 
자동광고의 전면광고와 앵커광고가 매력적이었고, 광고가 도배되는 문제는 '제외할 영역' 기능을 이용해 통제했다.
자동광고 게재 미리보기를 한 결과 포스팅 화면에서는 본문 중간에 배치되는 인아티클 광고는 잘 삽입되지 않았다.
따라서, 수동광고는 포스팅 내에서 사이드바 광고와 본문 내에 삽입하는 인아티클 광고, 상단광고를 게재하기 위해 설정했다.

<br/>
필자가 원하던 광고 배치화면은 다음과 같다.
<br/>
<img src="https://github.com/user-attachments/assets/85c10df1-4555-4688-b7d4-d5e012929638" alt='블로그-메인-광고'>
<br>
<img src="https://github.com/user-attachments/assets/0049d816-0143-40ac-bbd0-4b2d25e33d37" alt='블로그-포스팅화면-광고'>

<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-3082151336412907"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-3082151336412907"
     data-ad-slot="3525353674"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

## 애드센스 광고 게재 방법
### 1. ad.txt 파일 만들기
구글 애드센스 승인을 받았다면 ads.txt를 찾을 수 없다는 경고 메시지를 먼저 보게될 것이다. 
그리고 '지금 해결하기' 버튼을 누르면 `google.com, pub-0000000000000000, DIRECT, f08c47fec0942fa0`이라는 코드가 보일 것이다.
이 코드를 그대로 복사해서 root에 `ads.txt` 파일을 만들어준 후 붙여넣기 한다. ads.txt 파일 경로는 `깃허브id.gitgub.io/ads.txt`가 될 것이다.
그리고 잠시 기다리면 확인 되었다는 메시지를 볼 수 있다.


### 2. 자동광고 게재하기
구글 애드센스에 로그인한 후 <b>[광고 - 사이트 기준]</b>에 들어가면 '코드 가져오기' 링크가 있다.
이 링크를 누르면 나의 게시자 id를 포함한 스크립트 코드를 복사할 수 있는데, 이 코드를 <head></head> 사이에 넣어줘야 한다.
<br/>
<br/>
<img width="1383" alt="애드센스-광고코드" src="https://github.com/user-attachments/assets/5ec0a62b-32c5-4f71-88ff-684d07054d63">
<br/>
<br/>
Minimal mistake 테마의 경우 head가 별도의 파일로 만들어져 있기 때문에 이 파일에 붙여 넣으면 된다. 
경로는 `_includes/head/custom.html`이며, 이 `custom.html`파일에 복사한 코드를 붙여넣기하면 자동광고가 게재된다.  
<br/>
<br/>
주의할 점이 있다면, 자동광고를 게재할 때, 자동광고가 표시되는 영역을 미리 살펴보고 불필요한 부분을 제외해주는 것이 좋다.
자동광고 게재 미리보기는 <b>[광고 - 사이트 기준 - 블로그 주소 옆 연필모양(수정)]</b> 아이콘을 클릭하면 볼 수 있다.

<br/>
이 블로그에서 자동광고가 게재되는 부분은 상단과 하단 각각 다음과 같다.
<br/>
<img width="1023" alt="상단-자동광고-영역" src="https://github.com/user-attachments/assets/2a398fd9-ea1c-410c-a3f8-99a6b855322e">
<center>[자동광고 상단 영역]</center>
<br/>
<img width="1038" alt="하단-자동광고-영역" src="https://github.com/user-attachments/assets/43ab04d3-d725-49a5-a02b-afc471e014fb">
<center>[자동광고 하단 영역]</center>
<br/>
하단을 보면 5개가 넘는 영역에 자동광고가 게재될 수 있다. 이대로 광고를 게재하니 광고가 도배된 것 같이 보여서 보기가 좋지 않았다.
광고영역을 일부 제한하여 1개의 하단 광고만 노출될 수 있도록 설정하였다. 광고가 너무 많은 사이트는 사용자의 이탈이 빠를 수 있으니 주의는 것이 좋다.

<br/>
자동광고 영역을 제외하는 것은 <b>[광고 - 사이트 기준 - 블로그 주소 옆 연필모양(수정)]</b> 아이콘을 클릭한 후 오른쪽 메뉴의 '제외된 영역'을 선택한다.
그리고 제외하고 싶은 영역을 클릭한 후 '적용' 버튼을 누르면 된다.

### 3. 수동광고 게재하기
#### 광고코드 파일 생성
수동광고를 게재하기 위해서 임의로 광고단위를 만들어줘야한다. 구글 애드센스에 로그인한 뒤 <b>[광고 - 광고 단위 기준]</b>을 클릭한다. 그러면 만들 수 있는 4가지 광고가 보인다.

<br/>
<img width="897" alt="수동광고-종류" src="https://github.com/user-attachments/assets/a6fc2053-8164-4c6d-99d9-55c4cdc75d57">
<br/>
이 중에서는 디스플레이 광고를 추천한다. 설명글에도 나와있듯이 용도와 위치에 관계없는 무난한 광고들이 노출된다.

<br/>
`인피드 광고`는 글 목록 사이에 마치 내가 작성한 글 제목인 것처럼 중간에 광고가 삽입되는 것이다. 
`인아티클 광고`는 글 중간에 넣기 적절한 광고로 이미지와 텍스트로 구성되어 있다.  
`멀티플렉스 광고`는 이미지로 구성된 여러 개의 광고가 표의 형태로 만들어진 광고인데, 개인적으로는 현란하고 산만해서 잘 사용하지 않는다. 만약 사용한다면 블로그의 하단 영역에 넣기 좋을 듯하다.

<br/>
디스플레이 광고를 생성하면 스크립트 코드가 보일 것이다. 구글 애드센스에서는 `<body></body>` 사이에 이 코드를 삽입하라고 한다. 

<br/>
사실 하나의 광고를 생성한 후 같은 코드를 여러 영역에 넣어도 된다. 하지만 필자는 어느 영역에서 광고 수익이 더 많이 나오는지 통계를 확인하고 싶어서 영역에 따라 디스플레이 광고를 별도로 만들었다. 포스팅 상단에 들어갈 광고단위 1개, 사이드바에 들어갈 광고단위 1개, 총 2개를 만들었다.

<br/>
이제 원하는 영역에 광고코드를 편하게 넣을 수 있도록 사전작업을 하고자 한다. `_includes/advertisement.html` 파일을 생성한 후 광고 코드를 복사, 붙여넣기 한다. 

<br/>
<img src='https://github.com/user-attachments/assets/96989528-120c-43ee-963a-ccc5b17ccfb1' alt='광고코드-생성화면'>
<br/>

#### 포스팅 화면 내 상단광고 게재
필자는 블로그의 메인화면이 아닌, 메인화면에서 글 제목을 눌렀을 때 보이는 포스팅 화면에서 상단광고를 노출시키고 싶었다. 포스팅의 layout이 'single'이기 때문에 `single.html`에 광고코드를 넣어주었다. 경로는 `_layouts/single.html`이다.

<br/>
제목이 포함되는 header가 끝나는 부분과 본문인 page_content 섹션 사이에 수동광고 코드를 아래와 같이 넣어주었다. 
<br/>
<img width="1024" alt="상단광고-코드" src="https://github.com/user-attachments/assets/c6f7df58-627d-4876-b901-1787fe63b933">
<br/> 
이렇게 했을 때 포스팅의 상단에 광고는 성공적으로 잘 노출이 된다. 그러나 본문이 광고와 겹쳐 보이는 이슈가 있었다. 광고 단위를 만들 때 세로 높이를 조절해서 다시 광고단위를 만드는 것도 한 가지 방법일 것이다. 그러나 본문을 작성할 때 처음부터 바로 h태그를 사용하니 글자와 광고가 겹쳐보이는 문제가 해결되었다. 

#### 포스팅 화면 내 사이드바 광고 게재
사이드바 광고 게재는 특히 많은 시행착오를 겪었는데 [이 블로그](https://devinlife.com/howto%20github%20pages/adsense/)의 도움을 많이 받았다.

<br/>
필자는 메인 페이지가 아닌 포스팅 화면에서만 사이드바 광고를 노출시키고 싶었다. 그래서 상단 광고와 마찬가지로 `single.html`에서 작업해주었다. 포스팅에서 사이드에 있는 목차를 방해하지 않으면서 함께 움직여야 한다. 따라서 콘텐츠 섹션의 코드를 다음과 같이 수정해주었다.

<br/>
<img width="1020" alt="사이드바-광고-코드" src="https://github.com/user-attachments/assets/f97a526e-97f7-429e-987a-77e9545f2d7f">
<br/>
그리고 `_config.yml`의 default에 `toc_ads`와 'toc_sticky'를 추가해주면 된다.
<br/>
```yaml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      toc_ads: true
      toc_sticky: true
```
