---
layout: post
title:  "Eclipse::Servers 탭 활성화"
date:   2020-10-19 13:04:00 0800
categories: Error
tags: eclipse server
comments: 1
---

> 

# 문제 상황
Server 관련 설정을 위해 Show View에서 찾는데 보이지 않음

# 해결 방법
## Show View에서 찾기
`Window > Show View > Other... > Servers` 검색해서 찾음

## Show View에 없는 경우
1. `Help > Install New Software > Work with`에 **http://download.eclipse.org/releases/[eclipse-version]**을 입력
2. **Web, XML, Java EE and OSGi Enterprise Develpment** 선택
3. 필요한 항목에 체크
   - **JST Server Adapters**
   - **JST Server Adapters Extension**