---
title: "Jekyll Minimal Mistakes 테마의 일반 텍스트 크기 변경하는 방법"
categories:
  - Blog
tags:
  - Blog
  - Jekyll
  - Minimal Mistakes
  - minimal-mistakes
---

**Github Page**로 블로그를 만드는 사람들의 거의 대다수는 **Jekyll**를 사용하는 것 같고 그 중 매우 많은 스타 수를 기록하고 있는 **minimal-mistakes** 테마는 커스터마이징도 쉽고 문서들도 잘 만들어져 있어 쓰기 매우 좋은 테마 중에 하나다.

나 또한 이 테마를 사용하기로 결정하였고 해당 테마를 쓰면서의 경험이라는 이름의 삽질을 공유하려고 한다.

---

처음 글을 딱 쓰고 글을 보니 글씨 크기가 너무 큰데.... 라는 생각이 들어 글씨 크기를 조정하기 위해 일단 공식 [문서](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/#customizing)를 보았고 해당 문서에서는 project/assets/css/main.scss를 수정하면 된다고 나와있었다!

오 이제 하면 되겠다라고 생각해서 글씨의 크기를 지정하는 스타일 시트가 무엇인지 찾아다녔고 [\_variables.scss](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/minimal-mistakes/_variables.scss#L36) 파일에 글씨 크기와 관련된 변수들이 있어 해당 변수들을 이용하는 줄 알고 가져와 수정하였다.

- 그런데 안됬다. 😭

chrome 개발자 도구를 이용해 찍어보니 [\_page.scss](https://github.com/mmistakes/minimal-mistakes/blob/8a67ce8e41ec850f2d7c373aa47739b2abfee6f1/_sass/minimal-mistakes/_page.scss#L116C20-L116C20)에서 일반 p, li, dl 태그를 1em으로 하드코딩해서 지정하고 있었고 이걸 재정의하면 블로그 글의 글씨만 크기를 줄일 수 있었다!

따라서 다음의 코드를 assets/css/main.scss 파일을 만들어 넣어주었다.

```scss
@charset "utf-8";

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials

.page__content {
  p,
  li,
  dl {
    font-size: 0.9em;
  }
}
```

또한 [\_reset.scss](https://github.com/mmistakes/minimal-mistakes/blob/8a67ce8e41ec850f2d7c373aa47739b2abfee6f1/_sass/minimal-mistakes/_reset.scss#L7)에서 font-size em 크기의 기준을 지정하고 있으며 해당 구문을 오버라이드하여 블로그 전체의 글씨 크기를 줄일 수 있다.

```scss
@charset "utf-8";

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials

html {
  font-size: 16px;

  @include breakpoint($medium) {
    font-size: 18px;
  }

  @include breakpoint($large) {
    font-size: 20px;
  }

  @include breakpoint($x-large) {
    font-size: 22px;
  }
}
```

해당 글의 중심 출처: [https://github.com/mmistakes/minimal-mistakes/discussions/1219#discussioncomment-172827](https://github.com/mmistakes/minimal-mistakes/discussions/1219#discussioncomment-172827)
