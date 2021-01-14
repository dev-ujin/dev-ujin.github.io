---
layout: post
title: "[Git] Commit Template 만드는 방법"
date: 2021-01-14 18:11:00 0100
categories: Git
tags:
comments: 1
---
> 

# 🤦‍♀️ Commit Message 어떻게 적기로 했더라...
커밋 메시지를 작성할 때 가장 중요한 건 **일관성**이라고 생각한다. 팀 프로젝트에서는 말할 것도 없고, 개인 프로젝트에서도 빠른 트래킹을 위해서 커밋 메시지의 일관성을 유지해야한다. 커밋 메시지를 누르면 상세하게 어느 부분에서 변경이 일어났는지 Git이 친절하게 알려주기 때문에 결국 커밋 메시지란 코드에서 무엇을, 왜, 어떻게 변경했는지 간략하게 적어두고 나중에 찾아보기 쉽도록 하는 것이다. 이렇게 적었다가, 저렇게 적었다가, 다시 또 이렇게 적고... 뒤죽박죽 적다 보면 나중에 커밋의 정확한 의도를 파악하기가 힘들어지고 결국엔 커밋을 눌러서 코드 변경 내역을 보고 커밋 메시지를 이해하게 되는 주객전도 현상이 일어난다...~~는 내 얘기~~

# 🎨 Commit Template
Git은 `Commit Template`을 제공하는데 Template을 한 번 만들어두면 Commit시에 양식을 자동으로 띄울 수 있는 기능이다. Repository마다 다르게 설정할 수 있어서 굳굳👍

# 👩‍🎨 Commit Template 만드는 방법
## 1. Commit Template 파일 생성하기
모든 Repository에서 공통으로 사용할 Template인지 현재 Repository에서만 사용할 Template인지에 따라 파일 생성 위치가 달라진다.
```
// 모든 Repository에 공통으로 사용할 경우
vi ~/.gitmessage

// 현재 Repository에만 별도로 사용할 경우
vi .git/gitmessage
```

## 2. Commit Template 채우기
다른 개발자 분들의 글을 참고해서 템플릿 틀을 잡고 기존에 Commit에 사용하던 Emoji도 같이 첨부하였다.
```
# [<type>] <subject>
| =========== Subject 50 Characters ============ |
# Example : [feat] Implement login


# (Optional) Body
| ======================== Body 72 Characters ======================== |

# (Optional) <Resource> <Issue/Ticket> <Number>
# Example : Github Issue #114

# ========== Type ========== 
# feat       sparkles           New feature
# fix        beetle             Bug fix
# refactor   hammer             Code refactor (code change)
# style      art                Format/Structure improvement (no code change)
# doc        pencil             Everything related to documentation
# test       white_check_mark   Everything related to test
# chore      moyai              Etc (no production code change)
#
# ========== Remember to ==========
# * Capitalize the subject line
# * Use the imperative form in the subject line
# * Do not end the subject line with a period
# * Separate subject from body with a blank line
# * Use the body to explain what and why rather than how
# * Can use multiple lines with "-" or "*" for bullet points in body
```

### 3. Git 기본 설정에 Commit Template 등록
파일의 생성 위치가 다르기 때문에 1번 과정에서와 마찬가지로 두가지 경우로 나뉜다. 
```
// 모든 Repository에 공통으로 사용할 경우
git config --global commit.template ~/.gitmessage

// 현재 Repository에서만 별도로 사용할 경우
git config commit.template <Repository경로>/.git/gitmessage
```

# 👩‍🎨 Commit Template 사용 방법
```
git commit
```
템플릿을 채우고 `ZZ`(vi편집기 : 저장 후 종료) 혹은 `:wq!`(vi편집기 : 강제 저장 후 종료)로 저장한다.

# 📚 참고
- [https://gist.github.com/zakkak/7e06725ebd1336bfebebe254de3de825](https://gist.github.com/zakkak/7e06725ebd1336bfebebe254de3de825)
- [https://ujuc.github.io/2020/02/02/git-commit-message-template-man-deul-gi/](https://ujuc.github.io/2020/02/02/git-commit-message-template-man-deul-gi/)