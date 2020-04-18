<div style="text-align:center">
<span style=";font-weight:bold;font-size:2em">팀 개발을 위한 Git, GitHub 시작하기</span>
</div>







# :book: Chp04. 둘 이상의 원격저장소로 협업하기





## :page_with_curl: TODO LIST



| 구분 | 내용                                                         |
| ---- | ------------------------------------------------------------ |
| 1절  | 원본저장소를 복사해서 원격저장소를 만든다(fork)              |
| 1절  | 원격저장소를 소스트리를 통해서 로컬저장소로 가져온다(clone)  |
| 2절  | 원격저장소에서 원본저장소로 풀 리퀘스트를 보낸다(pull request) |
| 2절  | 풀 리퀘스트를 승인하고, 병합한다(merge)                      |
| 3절  | 묵은 커밋을 새 커밋으로 이력을 조작한다(rebase)              |



고양이와 문어가 오픈소스를 만들어 GitHub에 공개한 서비스가 흥행했다고 가정하죠.

지나가던 개발자 너구리가  이 프로젝트에 "좋아요" 기능을 본인이 직접 코딩한게 있는데, 한번 현재 프로젝트에 껴보는게 어떻냐고 고양이와 문어에게 물어보네요.



너구리 : 가능?

고양이 : 일단은 가능한데요, 원본저장소에 바로 **커밋하는 권한**을 주는 건 쪼~금 어려울 거 같아요. 
			   대신 기능을 추가한 소스 코드를 보내주면 **확인하고 반영해볼지 결정할게요**.

너구리 : 알겠어요.

문어     :  권한을 못주는 점 죄송합니다. 하지만 만약 반영하게 되면 **프로젝트 리스트에 이름**을 올려드릴게요.





---





## 🍴  Fork  - 원격저장소 복사해오기

<span style="font-size:0.8em">현재 너구리는 원격 저장소에 직접 커밋할 권한이 없습니다. 그러면 어떡해 해야할까요?</span> 

<span style="font-size:0.8em">본인의 새로운 GitHub 원격 저장소를 생성후 , 그 곳에 너구리의 원격저장소를 복사한  후  일단 작업을 하고, 그걸 허락을 받으면 됩니다.</span>



<span style="font-size:0.8em">그러면 일단 너구리의 원격 저장소에 복사를 해야겠네요! 이걸 우리는</span>

<span style="color:red;font-weight:bold;font-size:1.2em">Fork</span> 라고합니다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_65X84OiYry.png" style="zoom: 33%;" />





### :tumbler_glass: 브랜치와 포크

























