git diff
===

그림으로 깃 보기
http://marklodato.github.io/visual-git-guide/index-ko.html

1. 로컬의 Branch간 비교
~~~
git diff <branch명> <다른 branch명> 
~~~
2.  로컬과 리모트의 내용 비교
~~~
git diff <branch명> origin/<branch명> 
~~~

3. Commit 간 비교 
~~~
git diff <hash> < hash>
~~~

4. pull request 내용과 비교
checkout remote branch 이름을 먼저 확인한 뒤
~~~
git diff <현재 브랜치> <checkout remote branch> 
~~~
5. 특정 커밋과 pull request 비교
checkout remote branch 이름을 먼저 확인한 뒤
~~~
git diff <commit hash> <checkout remote branch>
~~~
6. 마지막 커밋과 그 이전 커밋 비교
~~~
git diff HEAD HEAD^ 
~~~

7. 마지막 커밋과 현재 수정사항 확인
아래 stage된 것과 아닌 것을 모두 확인하는 법이다. 주의 할 점은 untracking 파일은 비교에서 제외된다는 것이다.
~~~
git diff HEAD
~~~
8. 현재 staged 된 수정사항 만 따로 확인
~~~
git diff --cached 또는 git diff --staged
~~~

9. 현재 unstaged 된 수정사항만 확인
~~~
git diff
~~~