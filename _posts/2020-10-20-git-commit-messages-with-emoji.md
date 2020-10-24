---
layout: post
title:  "Github::Emoji로 Commit Message 분류하기"
date:   2020-10-20 00:23:00 0800
categories: Git/Github
tags: Git
comments: 1
---

> Github을 돌아다니던 중 Emoji가 들어간 귀여운 Commit Message를 발견하였다! 탐난다!
> [Atom](https://github.com/atom/atom/blob/master/CONTRIBUTING.md#git-commit-messages)에서 권장하는 몇가지 사항이 있는데 내 상황에 맞게 조금 변경해보려 한다!

## 문제 발생...&#x1F644;
![git-commit-messages-with-emoji-01](https://dev-ujin.github.io/assets/res/../../../../../_site/assets/res/git-commit-messages-with-emoji-01.png)
본문 왼쪽에 Margin이 생기고 폰트가 모두 흰색으로 바뀌는 현상이 발생했다. 디자인 에러인가 싶어서 css파일을 열심히 봤지만 다른 포스트에서는 문제가 발생하지 않았고 구글링을 해본 결과

![git-commit-messages-with-emoji-02](https://dev-ujin.github.io/assets/res/../../../../../_site/assets/res/git-commit-messages-with-emoji-02.png)
[Markdown Guide](https://www.markdownguide.org/tools/jekyll/)에서 Jekyll Markdown에서 복붙 Emoji는 지원하지만 Shortcode Emoji는 지원하지 않는다는 것을 알아냈다. Shortcode를 사용하려면 [jemoji](https://github.com/jekyll/jemoji)를 플러그인해서 사용해야한다.


## My Commit Emoji &#x1F995;

|Emoji|Syntax for Github|Syntax for Post|DESCRIPTION|
|---|---|---|---|
|&#x1F389;|`tada`|`&#x1F389;`|Initial commit|
|&#x1F4C4;|`page_facing_up`|`&#x1F4C4;`|Add code/files|
|&#x1F4A5;|`boom`|`&#x1F4A5;`|Remove code/files|
|&#x1F6A9;|`triangular_flag_on_post`|`&#x1F6A9;`|Update code/files|
|&#x1F18E;|`ab`|`&#x1F18E;`|Fix typo|
|&#x1F6A7;|`contruction`|`&#x1F6A7;`|Work in progress|
|&#x1F527;|`wrench`|`&#x1F527;`|Configuration files|
|&#x1F69A;|`truck`|`&#x1F69A;`|Move/Rename repository|
|&#x1F484;|`lipstick`|`&#x1F484;`|Improve UI/Style|
|&#x1F4A1;|`bulb`|`&#x1F4A1;`|Documentize code|
|&#x1F40E;|`racehorse`|`&#x1F40E;`|Improve performance|
|&#x1F41E;|`beetle`|`&#x1F41E;`|Fix a bug|
|&#x2728;|`sparkles`|`&#x2728;`|New Features|
|&#x1F516;|`bookmark`|`&#x1F516;`|Version tag|
|&#x2705;|`white_check_mark`|`&#x2705;`|Add/Update a test|
|&#x2795;|`heavy_plus_sign`|`&#x2795;`|Add dependencies|
|&#x2796;|`heavy_minus_sign`|`&#x2796;`|Remove dependencies|
|&#x1F427;|`penguin`|`&#x1F427;`|Linux|
|&#x1F34E;|`apple`|`&#x1F34E;`|MacOs|
|&#x1F3C1;|`chekckered_flag`|`&#x1F3C1;`|Windows|
|&#x1F42C;|`dolphin`|`&#x1F42C;`|MySQL|
|&#x1F418;|`elephant`|`&#x1F418;`|PostgreSQL|
|&#x1F343;|`leaves`|`&#x1F343;`|MongoDB|
|&#x1F433;|`whale`|`&#x1F433;`|Docker|


## Reference
아래 두 사이트를 참고하면 모든 Emoji를 표현할 수 있다!
- [https://unicode.org/emoji/charts/full-emoji-list.html](https://unicode.org/emoji/charts/full-emoji-list.html)
- [https://emojipedia.org/](https://emojipedia.org/)







