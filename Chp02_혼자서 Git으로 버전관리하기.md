<div style="text-align:center">
<span style=";font-weight:bold;font-size:2em">팀 개발을 위한 Git,GitHub 시작하기</span>
</div>






# :zap: Chp02. 혼자서 Git으로 버전관리하기



## :page_with_curl: TODO LIST

| 구분 | 내용                             |
| ---- | -------------------------------- |
| 1절  | 로컬저장소를 소스트리에 불러오기 |
| 2절  | 소스트리로 커밋 만들고 푸시하기  |
| 3절  | 그림으로 Git 뜯어보기            |









## :pencil2: 로컬저장소를 소스트리에 불러오기



### :writing_hand: 불러오기



1\. 소스트리 실행후 다음과 같은 순서로 클릭

<img src="Chp02_img\SourceTree_LjuZcjjaqR.png" style="border: 2px solid; float: left; zoom: 80%;" />





<img src="Chp02_img\SourceTree_jFA1FNgmrN.png" style="zoom:80%;border:2px solid;float:left" />





2\. history를 통해서 현재까지 커밋한 것 "그래프"로 보입니다.

<img src="Chp02_img\SourceTree_ROpSqgfyAT.png" style="zoom:80%;border:2px solid;float:left" />







### :writing_hand: ​로컬저장소의 정체는 \[.git] 폴더

그런데 여태한 커밋들이 그래프로 보이니 신기하죠? 이는 \[iTshirt-cat] 폴더에 있는 \[.git] 폴더에 저장된 정보 덕분입니다. 바로 이 폴더가 **로컬저장소**입니다.  ( **\[.git] 폴더** === **로컬저장소** )







## :pencil2: 소스트리로 커밋 만들고 푸시하기



### :writing_hand: ​사전작업

1\. visual studio code 로 \[iTshirt-cat] 폴더를 열고 새 파일 (tshirt-list.md) 를 생성하고 내용을 다음과 같이 입력합니다.

<img src="Chp02_img\Code_rfFFAMN4aY.png" style="zoom:80%;" />





2\.  같은 방법으로 feature-list.md 파일을 생성하고 내용을 다음과 같이 합니다.

<img src="Chp02_img\Code_HJ6A4cImii.png" style="zoom:80%;" />







### :writing_hand: ​소스트리에서 파일을 선택(add) 하고 커밋(commit)으로 만들기



소스트리에 돌아가면 커밋하지 않은 변경사항 이라는 문구가 보입니다.

<img src="Chp02_img\SourceTree_ewUQ68erHo.png" style="zoom:80%;border:2px solid; float:left" />

이는 기존 커밋과 내용이 달라졌기 때문입니다.



1\. 커밋 만들기

<img src="Chp02_img\SourceTree_Bj7j0ffGZ5.png" style="zoom:80%;border:2px solid; float:left" />

( 이미 스테이지 뷰 나누기가 체크된 상태면 클릭 안해도 됩니다 )



\[+] 버튼 클릭 후의 모습

<img src="Chp02_img\SourceTree_PY6WI6hQNC.png" style="zoom:80%;border:2px solid; float:left" />



여기서 말하는 스테이지는 "커밋의 구성요소"가 되는 것을 의미합니다.





2\. 커밋하기

<img src="Chp02_img\SourceTree_raYWuvnPp0.png" style="zoom:80%;border:2px solid; float:left" />



\[커밋] 버튼 클릭 후

<img src="Chp02_img\SourceTree_kcnyQWT3Ws.png" style="zoom:80%;border:2px solid; float:left" />





3\. 다시 \[History] 탭을 눌러서 그래프를 보면, 아까 한 커밋의 내용이 반영된 것을 볼 수 있습니다.

<img src="Chp02_img\SourceTree_lYv742WeCf.png" style="zoom:80%;border:2px solid; float:left" />







### :writing_hand: ​커밋을 원격저장소에 푸시하기



1\.

<img src="Chp02_img\SourceTree_1ZIrdPnt31.png" style="zoom:80%;border:2px solid;float:left" />



위 그래프를 자세히 살펴보면 최신 커밋인 "티셔츠, 기능 리스트 추가"에는 "master"
"개발자 목록 추가" 에는 "origin/master" 가 붙어있는 것을 볼 수 있습니다.

이것은 원격과 로컬저장소 각각이 현재의 커밋 상태를 보여줍니다.
현재 원격은 하나 뒤떨어진 커밋을 갖고 있네요.



**origin** ?

origin은 우리가 연결한 <span style="color:red;font-weight:bold">GitHub 원격저장소의 "닉네임"</span>입니다.

Chp00 에서 "git remote add  <span style="color:red;font-weight:bold">origin</span> [원격저장소 주소]" 라는 명령어를 사용했는데요.

이때 우리는 이미 원격저장소의 닉네임을 정한 것이죠.



**master** ?

master 는 우리가 계속해서 커밋을 올리는 "줄기(브랜치)" 라는 것입니다.

master 브랜치는 우리가 따로 만들지 않아도 Git이 기본으로 제공하는 브랜치이지요.





2\.

이제 로컬에서 새로 만든 커밋을 원격에도 업로드하죠. 푸시를 해야겠죠?

![](Chp02_img\SourceTree_nSSamV3cEq.png)

위 과정은 **git push origin master** 와 동일합니다.



이러고 나서 그래프는 다음과 같이 변하죠.

<img src="Chp02_img\SourceTree_Lud2orlcGk.png" style="zoom:80%;border:2px solid;float:left" />









## :pencil2: 그림으로 Git 뜯어보기(생략 - 책으로 보기)





### :writing_hand: 커밋은 Delta(차이점)가 아니라 Snapshot(스냅사진)

내용 생략~



### :writing_hand: Git 으로 관리하는 파일의 4가지 상태

- 추적 안됨 ( untracked )
- tracked ( 스테이지에 한번이라도 올라와서 커밋되면 "추적됨" 상태 중 하나가 된다)
  - 수정없음
  - 수정함
  - 스테이지됨









