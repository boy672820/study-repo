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

git

---

<pre>
From https://github.com/boy672820/study-repo
* branch    main    -> FETCH_HEAD
fatal: refusing to merge unrelated histories
</pre>

