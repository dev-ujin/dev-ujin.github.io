---
layout: post
title: "[IDE]Eclipse::Server Locations 활성화"
date: 2020-10-19 15:45:00 0800
categories: IDE
tags: eclipse server
comments: 1
---

> 

# 문제 상황
Servers 탭에서 Server명 더블클릭 > Server Locations에서 옵션을 선택하고 싶은데 gray처리되어 선택이 안됨

# 해결 방법
## 1) Switch Location으로 해결
1. Servers탭에서 `Server명 우클릭 > Properties > General`
2. **Switch Location** 클릭해 workspace metadata에서 다른 위치로 변경
3. 재시도

> 하지만 위의 방법이 먹히지 않았다... 또다시 삽질하다가 아래의 방법을 찾았고 문제 해결에 성공하였다!

## 2) Add and Remove로 해결
1. Servers탭에서 `Server명 우클릭 > Add and Remove > Remove all` 클릭
2. 재시도


### 출처
[https://stackoverflow.com/questions/4919846/why-tomcat-server-location-property-is-greyed-in-eclipse/4919907](https://stackoverflow.com/questions/4919846/why-tomcat-server-location-property-is-greyed-in-eclipse/4919907)