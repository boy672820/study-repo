# 1. 깃 구조
## 1.1. Working copy, Index, Repository

### 1.1.1. About

여러개의 파일을 그룹으로 묶거나, 별개로 파일을 나누어 버전을 만들기 위한 구조
* **_Working copy_**
* **_Index_** or **_Staging area_**
* **_Repository_**

---

### 1.1.2. Example

예를들어, 새로운 파일 index.html 파일과 README.md 파일을 만들었다고 치자.

새로 생성된 두 파일은 Git의 Working copy 영역에 저장 된다.

> git add index.html README.md

add 명령어로 index.html 과 README.md 파일은 Index(or Staging area)로 저장 된다.

> git commit "First commit"

commit 명령어로 index 영역에 있는 파일들은 Repository의 "First commit" 이라는 코멘트의 버전으로 저장 된다.

---

### 1.1.3. Point
예시와 같이 두 파일을 그룹으로 묶어 Index 영역에 저장 시킨 후 commit 명령어를 통해 Repository 버전으로 만들거나,   

index.html 또는 README.md 파일을 별개로 Index 영역에 저장시켜 버전을 만들 수 있게 하기 위한 git의 구조이다.