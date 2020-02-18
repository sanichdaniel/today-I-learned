브랜치를 통합하는 방법
===

Merge
---
2개의 브랜치를 통합해주며 변경 내용의 이력이 모두 그대로 남아 있다

> 현재 내가 합치려고 하는 브랜치가 master 브랜치라 가정한다

 ## 1) Fast-forward

브랸치 분기후, master 브랜치가 **변경되지 않았을때** 

master 브랜치의 팁을 분기한 브랜치의 팁으로 옯긴다.

 ## 2) 3-way merge

브랜치 분기후 'master' 브랜치에 **변경 되었을때**

1. 내 브랜치 커밋
2. 남의 브랜치 커밋
3. 두 브랜치의 공통 조상이 되는 커밋

3개의 커밋을 비교

git은 각 브랜치의 tip의 커밋의 공통 부모 커밋을 찾는다. 그리고 이 2개의 브랜치의 커밋들을 합친 'merge 'commit'을 만든다

Rebase
---

 base가 되는 커밋을 새로 잡아주고, 새로운 base에서 커밋들을 연결시켜준다. 그래서 fast-forward merge를 하게 해주어 불필요한 머지 커밋을 안남긴다. 

interactive mode로 **과거의 히스토리**까지 **조작가능**


![unowned](/git/img/rebase.png)  

분기한 브랜치의 base를 마스터 브랜치의 tip으로 만들어준다.

그 후에 master 브랜치에서 머지하면 fast-forward merge가 된다

~~~
gco dev
git rebase master
gco master
git merge dev
~~~


-i interactive option
---

로컬의 히스토리 조작가능

pick, drop, squash, edit 등등