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



기본적으로 원본저장소(고양이의 원격저장소)에 커밋을 직접 푸시할 수 있는 사람은 원본저장소를 만든 본인들 뿐입니다. 지금은 고양이겠네요. 저희가 처음 원격저장소를 만들 때 고양이 계정으로 만들었으니까 말이죠.

그러면 문어는 어떻게 된걸까요? 여태까지 문어도 원격에 커밋을 했는데 말이죠.

이건 지금 저희가 실습을 위해서 따로 문어 계정을 만들지 않았기 때문이에요. 
만약 FM대로 해서 문어 계정을 만들었다면, **고양이 계정에서 문어를 협력자로 등록**해야합니다.



어떻게 하냐구요? 아래 그림을 보면 압니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_4trd8COMDa.png" style="zoom:80%;border:2px solid;float:left" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_WDlBdIhtKZ.png" style="zoom:80%;border:2px solid;float:left" />



... 간단하죠? 이렇게 등록된 협력자는 원격저장소에 바로 커밋을 할 권한이 있습니다. 물론 그래도 풀 리퀘스트를 하는게 좋겠죠?



그런데 말입니다, 이렇게 협력자가 늘어나는 건 소유자 입장에서 꼭 반가운 건 아니에요.

아무래도 커밋(버전)과 관련된 관리가 어렵겠죠? 하지만 그렇다고 다른 사람의 도움을 안 받자니 그건 그것대로 힘들고 말이죠...



그래서! 나온 것이 바로 [ Fork ==> Pull Request ] 작업이죠.



Fork를 통해서 자기의 원격저장소에 저장 후, 다 완성이 되면 원본저장소(고양이의 원격저장소) 에 풀 리퀘스트를 하는 거죠.



포크는 clone 과 비슷하게 커밋 이력까지 싹다 복사해옵니다.





...



그러면 지금까지 배운걸 생각해보면 협업을 하는 방식은 크게 2가지겠네요.

1. 협력자로 등록하거나
2. 상대가 Fork를 한 후 풀 리퀘스트를 날리거나

1은 같이 협업하는 사람이 많지 않을 때 좋구요. 2는 50명 정도로 다수의 인원이 할 때 좋습니다.







---





### :tumbler_glass: Fork로 콕 집기



일단 너구리 계정을 생성해야겠죠? 

저는 생성할 때 원래 갖고 있던 Gmail 계정을 사용했습니다.

Gmail에는 편리한 기능이 있는데요, 예를들어서 제가 qkrtkddjs12345@gmail.com 이라는 아이디가 이미 있으면,

거기에 +1 을 추가해서 깃허브에 등록이 가능해요. 아래와 같이 말이죠.

qkrtkddjs12345+1@gmail.com  / 닉네임 : NongSimNeoguri (농심 너구리 :laughing: ) 



아무튼 위와 같이 생성 후에 Sign in 후에 Fork 작업을 아래 그림과 같이 합니다.



#### 1\. Fork 하기

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_lTmmnr5m82.png" style="zoom:60%;border:2px solid;float:left" />

검색을 합니다.





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_DHRfa5uQDc.png" style="zoom:60%;border:2px solid;float:left" />

devToroko/iTshirt 클릭





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_j5xWwoIulw.png" style="zoom:60%;border:2px solid;float:left" />

화면 상단의 우측에 있는 Fork 버튼을 클릭!





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_P6WvW70k18.png" style="zoom:60%;border:2px solid;float:left" />

그러면 잠시 포크가 진행되는 화면이 나옵니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_OCOJl9EGqU.png" style="zoom:60%;border:2px solid;float:left" />

농심 너구리의 원격저장소에 무사히 복사가 완료되었네요.





#### 2\. Fork 한 원격 저장소를 로컬로 복사하기

이제 원격저장소의 데이터들을 로컬로 끌고 와서 소스트리에서 작업을 하도록 하죠.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_lQ9jCd9UiS.png" style="border:2px solid;float:left;" />

새 탭을 만들고 ==> clone ==> 너구리의 원격저장소 주소를 적어주고 ==> 로컬에 저장할 위치를 선정해주고 ==> 클론, 끝!



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_sPI1GZ2hrG.png" style="border:2px solid;float:left;" />

짠! 성공적으로 클론이 되었네요 :smile:



#### 3\. 소스트리에 계정 등록 및 기본계정 등록

이렇게 하고 나서 가장 먼저 할일은 **너구리 계저으로 다시 소스트리를 로그인**하는 겁니다. 너구리의 원격저장소에 푸시를 하려면 당연히 소유자인 너구리 계정이어야하겠죠? 

그럼 바꿔보죠!



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_ge7mI2NKqi.png" style="border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_Jwju1Sb2Zl.png" style="zoom:80%;border:2px solid;float:left;" />



클릭 한 후에는 Sourctree password request 라는 이름의 창이 뜨면 비밀번호를 입력하게 됩니다.

해주세요. 그러고 나서 호스팅 계정 편집 창에서 초록색 체크박스로 "인증성공" 이 뜨면 성공한겁니다.

그 이후로는 확인버튼을 누르면 끝입니다.



이렇게 하면 소스트리에 계정이 하나 추가된겁니다. 

그리고 추가적으로 해당 계정을 소스트리의 기본계정으로 하면 끝입니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_lq7oWJ3MDg.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_ZMbNjYFnQI.png" style="zoom:80%;border:2px solid;float:left;" />





#### 4\. 너구리의 로컬에서 작업하기

너구리의 로컬 폴더인 [ iTshirt-raccoon ] 를 열어서 VS Code 를 실행해줍니다.

그 이후에 파일을 생성하고, 커밋을 해주겠습니다. 물론 최종적으로 푸시도 하고요.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_PMtLvQSTpO.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_k9WCGcCxi0.png" style="zoom:80%;border:2px solid;float:left;" />

현재 커밋하려는  사람은 "농심 너구리" 입니다. 그러니 커밋 하려는 사람의 정보를 바꿔야 겠죠?

소스트리 커밋 페이지에서 devToroko 라는 닉네임 옆의 사람모양의 아이콘이 보이시죠? 그걸 클릭하면 

커밋하려는 사람의 정보를 바꿀 수가 있습니다. 위처럼 바꿔주고 커밋을 해주세요~



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_omyhcD98Yl.png" style="zoom:80%;border:2px solid;float:left;" />

위와 같이 작성하고 최종적으로 커밋을 눌러주세요!



푸시까지하면 아래와 같은 그래프가 나오겠죠?

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_vGqYxGKabL.png" style="zoom:80%;border:2px solid;float:left;" />





---





## 🍴  원본저장소에 풀 리퀘스트

<span style="font-size:0.8em">이제 너구리의 작업은 끝났습니다. 원본 저장소의 주인인 고양이에게 확인을 받고 원본 저장소에 반영을 할 시간입니다!</span> 





### :tumbler_glass: 포크한 저장소를 원본 저장소로 풀 리퀘스트 보내기

<span style="font-size:0.8em">이제 풀리퀘스트를 원본 저장소에 보냅시다!</span>







<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_ohcwUG1LeT.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_IAItFbPjmP.png" style="zoom:80%;border:2px solid;float:left;" />

1~2 를 확인하고 나서, 3(풀리퀘스트)을 해줍니다.





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_hY2SaDaaB4.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_sRlTY8dqyl.png" style="zoom:80%;border:2px solid;float:left;" />

자! 성공적으로 풀 리퀘스트를 했습니다. 이제는 고양이(원본저장소의 소유자)의 병합을 기다리면 됩니다.







### :tumbler_glass: 풀 리퀘스트를 승인+병합하기

<span style="font-size:0.8em">이제 고양이 계정으로 돌아가서 상황을 보죠</span>



고양이 계정으로 로그인 후 다음과 같은 작업들을 해봅시다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_O6MS11GaWH.png" style="zoom:80%;border:2px solid;float:left;" />

저 순서대로 클릭한 후에 너구리 씨가 포크했단 사실을 확인합니다.















<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_1MTh98CtxN.png" style="zoom:80%;border:2px solid;float:left;" />

[ Pull requests ] 를 클릭하여 풀 리퀘스트가 들어온 사실을 볼 수 있습니다.

밑에를 보니 방금 너구리씨가 보낸 풀 리퀘스트가 보이네요!  더 세부적으로 확인하기 위해 해당 리퀘스트를 클릭!







<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_VqfreeAdHE.png" style="zoom:80%;border:2px solid;float:left;" />

풀 리퀘스트의 변경사항을 File changed 를 통해서 볼 수 있으며

만약 해당 변화에 대한 댓글만 달고 싶으면 (Comment),
승인을 하고 싶으면 (Approve),
수정을 요청하고 싶다면 (Request changes) 를 하면 됩니다.

만족스러운 고양이 씨는 위와 같이 쓰고 Approve 선택후 Submit review를 했습니다.





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_D16RUCbkE0.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_HZkbEutf96.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_2FwAO9XM8y.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_eY8ivmyT97.png" style="zoom:80%;border:2px solid;float:left;" />

고양이 원본저장소에도 무사히 내용이 반영되었네요!





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_025uSpBf1J.png" style="zoom:80%;border:2px solid;float:left;" />

이제 너구리도 원본저장소의 컨트리뷰터에 포함된 것을 확인할 수 있습니다.





---





다시 너구리 계정으로 로그인해서, 너구리 본인의 업적(?)을 자랑해보죠!





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_2BtNAoXsfA.png" style="zoom:80%;border:2px solid;float:left;" />







<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_mtKCSLjxcB.png" style="zoom:80%;border:2px solid;float:left;" />

Customize your pins 를 클릭 후 , 방금 전에 풀리퀘스트를 보냈던 원본저장소 프로젝트를 체크하고 Save pins 를 하면 끝입니다!



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_tQPGpSvcIX.png" style="zoom:80%;border:2px solid;float:left;" />

(자랑 중)









## 🍴  묵은 커밋을 새 커밋으로 이력 조작하기(rebase)

<span style="font-size:0.8em"></span> 







<img src="" style="zoom:80%;border:2px solid;float:left;" />



## 귀찮은 거 미리 :anger:

<img src="" style="zoom:80%;border:2px solid;float:left;" />

<span style="font-size:0.8em"></span>

