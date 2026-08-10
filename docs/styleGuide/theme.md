# 테마 적용

<!-- synonyms: 스타일, 디자인, 테마, style, theme, 커스터마이징, 외관, 시트 스타일, default grace mint material krds gray simple, 테마 설정 -->

## 기본 테마 종류
현재 배포되고 있는 테마는 다음과 같습니다.

`기본`, `기본(이미지)`, `grace`, `material`, `mint`, `simple`, `gray`, `krds`

이 중 기본(이미지) 테마에서만 이미지를 png, gif파일로 제공합니다. 그 외의 테마는 base64로 인코딩된 svg파일로 이미지를 제공합니다.

테마명 옆의 ()안에는 테마의 Prefix명입니다.

`ibsheet.js`파일의 경로를 `/assets/ibsheet/`로 가정하고 설명하겠습니다.

기본 테마 (`IB`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/default/main.css"/>
```

![default theme](/assets/imgs/styleguide_css_default_theme.png "default theme")

기본(이미지) 테마 (`IB`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/default_img/main.css"/>
```

![default theme](/assets/imgs/styleguide_css_default_theme.png "default theme")

grace 테마 (`IBGR`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/grace/main.css"/>
```

![grace theme](/assets/imgs/styleguide_css_grace_theme.png "grace theme")

material 테마 (`IBMR`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/material/main.css"/>
```

![material theme](/assets/imgs/styleguide_css_material_theme.png "material theme")

mint 테마 (`IBMT`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/mint/main.css"/>
```

![mint theme](/assets/imgs/styleguide_css_mint_theme.png "mint theme")

simple 테마 (`IBSP`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/simple/main.css"/>
```

![simple theme](/assets/imgs/styleguide_css_simple_theme.png "simple theme")

gray 테마 (`IBGY`)
```html
<link rel="stylesheet" href="/assets/ibsheet/css/gray/main.css"/>
```

![gray theme](/assets/imgs/styleguide_css_gray_theme.png "gray theme")

krds 테마 (`IBKD`)
`krds.go.kr`(전자정부 디자인 시스템, egov) 권고를 반영한 테마입니다. 주요 특징은 다음과 같습니다.
- 불필요한 세로 구분선(Border)을 제거해 깔끔한 UI를 제공합니다.
- 세로 스크롤바를 기본은 슬림하게 표시하고, 마우스를 올리면(hover) 확대합니다.
- 편집 가능한 셀에 input 스타일 border를 적용해, 읽기 전용 셀과 구분되도록 강조합니다.
```html
<link rel="stylesheet" href="/assets/ibsheet/css/krds/main.css"/>
```

![krds theme](/assets/imgs/styleguide_css_krds_theme.png "krds theme")

* * *

## 테마 적용 방법
테마의 Prefix명은 [Style cfg](/docs/props/cfg/style)에서 설정하거나, [setTheme func](/docs/funcs/core/set-theme)에서 변경할 테마의 prefix파라미터에서 사용됩니다.

[Style cfg](/docs/props/cfg/style)로 사용하시는 경우, 앞서 사용하실 테마에 맞는 css파일을 먼저 호출하셔야 합니다.

[setTheme func](/docs/funcs/core/set-theme)로 테마를 적용하시는 경우, 테마의 prefix명과 테마의 css파일의 경로가 파라미터로 사용됩니다.