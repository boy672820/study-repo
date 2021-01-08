# error: src refspec master does not match any

<pre>
error: src refspec master does not match any   
error: failed to push some refs to 'https://github.com/boy672820/study-repo'
</pre>

번역하면   
"src refspec 마스터가 일치하지 않습니다."

src refspec 이 뭔지 몰라서 검색해보니   
로컬 저장소에 원격 저장소의 branch를 매핑하는 것을 git은 refspec이라 하고,
이를 통해 push, fetch 등 명령어를 사용하고 관리한다.

> refspec은 _.git/config_ 파일에   
"+ _원격 저장소 Refs 패턴_ : _로컬 저장소 Refs 패턴_" 형식으로 저장되어 있음.

자세한 내용은   
Attlassian Tutorial: https://www.atlassian.com/git/tutorials/refs-and-the-reflog#refspecs   
Git SCM: https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EB%82%B4%EB%B6%80-Refspec


## 즉, 로컬 저장소와 원격 저장소의 branch가 맞지 않다는 것

> $ git pull

나는 원격 저장소와 로컬 저장소를 merge 시키셔서 문제를 해결했다.

---

<pre>
From https://github.com/boy672820/study-repo
* branch    main    -> FETCH_HEAD
fatal: refusing to merge unrelated histories
</pre>

---
---

# fatal: unable to access '...': The requested URL returned error: 403

요청한 원격 저장소에 접근 권한이 없을 때 발생하는 에러

말 그대로 권한 문제이기 때문에 로그인을 다시하거나 원격 저장소 주소 또는 현재 사용하는 유저 정보(username, email)를 확인해 보는게 좋을 것 같다.

나의 경우 github 측에서 비밀번호 변경 요청으로 이런 에러가 나왔다.
비밀번호 변경한 후 다시 로그인하여 문제 해결