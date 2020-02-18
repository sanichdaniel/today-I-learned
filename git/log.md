Git Log
===

한줄로 커밋들 보기

~~~
git log --oneline
~~~

그래프로 커밋들 보기
~~~
git log --graph
~~~


최근 n개 커밋

~~~
git log -n
~~~


기한
~~~
git log --after="2014-7-1" --before="2014-7-4"

// today, yesterday 도 가능
~~~

A 브랜치, 커밋에는 없고 B 브랜치, 커밋에만 있는것
~~~ 
git log master..feature
~~~