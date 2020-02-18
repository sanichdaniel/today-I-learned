Reset
===

1) 커밋 단위 -> 브랜치의 tip을 옮겨서 현재 브랜치의 커밋들을 지울 수 있다
2) 파일 단위 -> 파일을 unstage

옵션
---
* **--soft**: staged 스냅샷과, working directory는 그대로
* **--mixed**: staged 스냅샷은 커밋에 맞게 업데이트되지만 working directory는 그대로. 기본 옵션
* **--hard**:  stage된 스냅샷과, working directory까지 특정 커밋으로 초기화

Checkout
===

HEAD 포인트를 특정 커밋으로 옮기게

1) 커밋, 브랜치 단위의 체크아웃
2) 파일 단위의 체크아웃: 파일 컨텐트를 특정 커밋으로 (워킹디렉토리 변경된것 되돌림)

Detached Head State
===

> 브랜치에 연결된 상태가 아니다.

A-B-C-D-E-F-G 브랜치가 있을때

master 브랜치로 체크아웃하면 커밋 G에 올꺼고, 브랜치에 끝자락에 있으면 attached 연결된 상태다. 

만약 임의의 커밋으로 체크아웃한다면 브랜치에 연결된 상태가 아니고 detached 상태이다. 

커밋들 사이를 돌아다닐 수 있다. 

Ref
---
https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting