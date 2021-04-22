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

<img src="Chp04_img\chrome_65X84OiYry.png" style="zoom: 33%;" />





### :tumbler_glass: 브랜치와 포크



기본적으로 원본저장소(고양이의 원격저장소)에 커밋을 직접 푸시할 수 있는 사람은 원본저장소를 만든 본인들 뿐입니다. 지금은 고양이겠네요. 저희가 처음 원격저장소를 만들 때 고양이 계정으로 만들었으니까 말이죠.

그러면 문어는 어떻게 된걸까요? 여태까지 문어도 원격에 커밋을 했는데 말이죠.

이건 지금 저희가 실습을 위해서 따로 문어 계정을 만들지 않았기 때문이에요. 
만약 FM대로 해서 문어 계정을 만들었다면, **고양이 계정에서 문어를 협력자로 등록**해야합니다.



#### 참고) 협력자 등록하기

어떻게 하냐구요? 아래 그림을 보면 압니다.

<img src="Chp04_img\chrome_4trd8COMDa.png" style="zoom:80%;border:2px solid;float:left" />



<img src="Chp04_img\chrome_WDlBdIhtKZ.png" style="zoom:80%;border:2px solid;float:left" />



... 간단하죠? 이렇게 등록된 협력자는 원격저장소에 바로 커밋을 할 권한이 있습니다. 물론 그래도 풀 리퀘스트를 하는게 좋겠죠?



그런데 말입니다, 이렇게 협력자가 늘어나는 건 소유자 입장에서 꼭 반가운 건 아니에요.

아무래도 커밋(버전)과 관련된 관리가 어렵겠죠? 하지만 그렇다고 다른 사람의 도움을 안 받자니 그건 그것대로 힘들고 말이죠...



그래서! 나온 것이 바로 [ Fork ==> Pull Request ] 작업이죠.



Fork를 통해서 자기의 원격저장소에 저장 후, 다 완성이 되면 원본저장소(고양이의 원격저장소) 에 풀 리퀘스트를 하는 거죠.



포크는 clone 과 비슷하게 커밋 이력까지 싹다 복사해옵니다.





...



그러면 지금까지 배운걸 생각해보면 **협업을 하는 방식은 크게 2가지**겠네요.

1. **협력자로 등록하거나**
2. **상대가 Fork를 한 후 풀 리퀘스트를 날리면 그걸 수락하거나**

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

<img src="Chp04_img\chrome_lTmmnr5m82.png" style="zoom:60%;border:2px solid;float:left" />

GitHub 로그인 후 왼쪽 상단에서 고양이의 원격저장소를 검색합니다.





<img src="Chp04_img\chrome_DHRfa5uQDc.png" style="zoom:60%;border:2px solid;float:left" />

devToroko/iTshirt 클릭





<img src="Chp04_img\chrome_j5xWwoIulw.png" style="zoom:60%;border:2px solid;float:left" />

화면 상단의 우측에 있는 Fork 버튼을 클릭!





<img src="Chp04_img\chrome_P6WvW70k18.png" style="zoom:60%;border:2px solid;float:left" />

그러면 잠시 포크가 진행되는 화면이 나옵니다.



<img src="Chp04_img\chrome_OCOJl9EGqU.png" style="zoom:60%;border:2px solid;float:left" />

농심 너구리의 원격저장소에 무사히 복사가 완료되었네요.





#### 2\. Fork 한 원격 저장소를 로컬로 복사하기

이제 원격저장소의 데이터들을 로컬로 끌고 와서 소스트리에서 작업을 하도록 하죠.



<img src="Chp04_img\SourceTree_lQ9jCd9UiS.png" style="border:2px solid;float:left;" />

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

그리고 추가적으로 해당 계정을 **소스트리의 기본계정**으로 하면 끝입니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_lq7oWJ3MDg.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_ZMbNjYFnQI.png" style="zoom:80%;border:2px solid;float:left;" />



---

참고로! 해당 계정을 기본 계정으로 하면, --global user.name 이 바뀝니다. 

그러면 Chp00 에서 제가 push를 할 때 났던 에러가 날 수도 있습니다.  
원격저장소의 소유자가 아닌 다른 사용자의 이름으로 push를 함부로 하려니까 당연히 막히는 거지요.

조심하세요.

----





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



푸시까지하면 아래와 같이 너구리의 포크한 원격저장소에 커밋이 반영됩니다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_vGqYxGKabL.png" style="zoom:80%;border:2px solid;float:left;" />





---





## 🍴  원본저장소에 풀 리퀘스트

<span style="font-size:0.8em">이제 너구리의 작업은 끝났습니다. 원본 저장소의 주인인 고양이에게 확인을 받고 원본 저장소에 반영을 할 시간입니다!</span> 





### :tumbler_glass: 포크한 저장소를 원본 저장소로 풀 리퀘스트 보내기

<span style="font-size:0.8em">이제 풀리퀘스트를 원본 저장소에 보냅시다!</span>







<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_ohcwUG1LeT.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_IAItFbPjmP.png" style="zoom:80%;border:2px solid;float:left;" />

1~2번을 확인하고 나서, 3번(풀 리퀘스트)을 클릭해줍니다.





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





 ] 

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_VqfreeAdHE.png" style="zoom:80%;border:2px solid;float:left;" />

풀 리퀘스트의 변경사항을 File changed 를 통해서 볼 수 있으며, [ Review changes ] 버튼을 클릭해서 이것에 대해서 3가지 결정을 내릴수 있습니다. 

변화에 대한 댓글만 달고 싶으면 (Comment),
승인을 하고 싶으면 (Approve),
수정을 요청하고 싶다면 (Request changes) 를 하면 됩니다.

만족스러운 고양이 씨는 위와 같이 쓰고 Approve 선택 후 Submit review를 했습니다.





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

<span style="font-size:0.8em">컨트리뷰터가 된 너구리는 이 기세를 몰아 '티셔츠 찜하기' 기능을 코딩했습니다. 그리고 풀 리퀘스트를 보냈는데, 코드 충돌이 났네요!!!</span> 

<span style="font-size:0.8em">하지만 그 과정에서 내가 추가한 코드 외에도 충돌을 해결하느라 생긴 병합 커밋이 생길 것입니다(솔직히 이거 뭔소린지 모르겠음). 이를 피하고 깔끔하게 변경한 부분만 풀 리퀘스트를 보낼 방법 없을까요?</span>



### :beer: 원본저장소에 새로운 커밋이 있는데, 포크한 내 원격저장소에 안보여요

<span style="font-size:0.8em">먼저 고양이&문어의 원본 저장소와 너구리의 원격저장소가 서로 같은 코드를 고쳐서 병합할 때 충돌이 나는 상황을 만들어 보죠</span>



#### 1\. [ iTshirt-raccoon ]  내용 변경하기(feat. like.md)



like.md 파일을 수정해보죠.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_I0IBKWAF1R.png" style="zoom:80%;border:2px solid;float:left;" />



그러고 나서 다음과 같이 작성 후 커밋!

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_CQB9EC3b1J.png" style="zoom:80%;border:2px solid;float:left;" />



"찜하기 기능 추가" 커밋이 원격저장소에도 잘 반영되었습니다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_EobUNnbdUD.png" style="zoom:80%;border:2px solid;float:left;" />







#### 2\. [ iTshirt-cat ] 로컬 저장소 최신화



소스트리의 iTshirt-cat  탭에서 보면 ![](C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_I8MZVsJcPi.png)이 보이네요. 

좋아요 기능 추가, Merge pull request 가 원격에는 반영되어있지만, 로컬에는 반영이 안되었다는 뜻입니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_toT7aHYiAD.png" style="zoom:80%;border:2px solid;float:left;" />



그럼 이제 로컬에도 최신 상태를 반영하도록 pull하겠습니다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\1RD2y7Aqrq.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_aHB4NY3gGR.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_cuxXsVM3ih.png" style="zoom:80%;border:2px solid;float:left;" />







#### 3\. 충돌상황 만들기



충돌 상황을 만들기 위해서 일단 고양이 계정을 기본 계정으로 변경후 2개의 커밋을 추가해보겠습니다.





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_wy8BjpCDx8.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_2urwg06f9k.png" style="zoom:80%;border:2px solid;float:left;" />





그 이후에 [ iTshirt-cat ] 폴더를 열고 "like.md" 에 텍스트를 추가합니다. 충돌을 내기 위해서 말이죠!

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_NtxH7UXue9.png" style="zoom:80%;border:2px solid;float:left;" />





그러고 나서 커밋 + 푸시!

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_hC2K1ZZj6Y.png" style="zoom:80%;border:2px solid;float:left;" />





그리고 추가적으로 README.txt에서 너구리를 추가합니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_1XDKrxmMuX.png" style="zoom:80%;border:2px solid;float:left;" />

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_Ki2qyK6lYD.png" style="zoom:80%;border:2px solid;float:left;" />

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_PhlH1dyrG4.png" style="zoom:80%;border:2px solid;float:left;" />





#### 4\. 다시 너구리의 입장으로...

이제 너구리로 돌아와서 , 풀 리퀘스트를 보내려는 상황입니다. 그런데! 너구리 입장에서는 현재

고양이가 커밋 + 푸시한 것에 대한 상황을 전혀 모릅니다! 



실습을 하면서 어떻게 되는지 봅시다.



너구리 계정으로 Github 로그인 후 [NongSimNeoGuri/iTshirt] 원격 저장소에서 [ New pull request ] 를 클릭합니다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_x05hATEmDI.png" style="zoom:80%;border:2px solid;float:left;" />



충돌이 났네요. 에구...

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_7tqRcHMP4q.png" style="zoom:80%;border:2px solid;float:left;" />







### :beer: 여러 원격저장소 히스토리를 한눈에 보기: 리모트 추가(Add remote)

<span style="font-size:0.8em">지금 같은 상황은 너구리가 고양이의 원본 저장소의 현재 상태를 몰라서 일어난 겁니다. 그럼 알면 되겠네요!</span> 



1\. 다시 너구리의 입장으로 돌아가보죠

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_nsJ4aaVvad.png" style="zoom:80%;border:2px solid;float:left;" />





**[ iTshirt-raccoon ] 탭을 선택 후**  

왼쪽에서 원격을 클릭하면 하단에 [NongSimNeoGuri/iTshirt] 원격 저장소만 origin이라는 이름으로 바라보고 있습니다. 하지만 고양이의 원격 저장소인 [devToroko/iTshirt] 원격저장소는 보지 않고 있죠.

그러면 추가해보죠.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_1rvaWX1uSk.png" style="zoom:80%;border:2px solid;float:left;" />





<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_UH5XpkNGSO.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_loZTVkcFpr.png" style="zoom:80%;border:2px solid;float:left;" />

upstream 은 원본저장소를 지칭하는 관용적 닉네임입니다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_WLYr7kas8F.png" style="zoom:80%;border:2px solid;float:left;" />





이제 upstream , 즉 원본저장소에 있는 **커밋 히스토리를 받아오겠습니다**. 이것을 **패치(fetch) 라고 합니다.**

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_sdSbbJXqyN.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_AeHr7WtMfd.png" style="zoom:80%;border:2px solid;float:left;" />



#### 패치는 간단히 말하면 "새로고침"입니다. 

패치를 하면 원본저장소 **이력을 업데이트**합니다. 이력만 가져오는 거니까 **내 코드에는 아무 영향이 없습니다**.

**최신 코드를 내 코드에 반영하는 풀(Pull)과는 다르죠**.



아무튼 이제는 upstream/master 브랜치와 현재 master 브랜치에서 충돌되는 게 있는 거라고 짐작을 할 수 있게 되었습니다.



너구리 기능은 잘 만들었지만, 너무 예전 코드를 기점으로 새 코드를 추가했습니다. 이렇게 하면 원본저장소의 최신 코드와 충돌이 날 가능성이 높죠. 이제 충돌을 해결해보죠.









### :beer: 묵은 커밋을 방금 한 커밋처럼 : 리베이스(Rebase)



자... 여기까지 작업을 했으면 병합하는 방법은 2가지입니다.

첫번째는 저희가 익숙한 병합 커밋을 하나 만들고, 그 커밋을 현재의 master 브랜치에 올리고, 문제가 없으면

upstream/master 브랜치에 풀 리퀘스트를 날리는 겁니다.

하지만 현재의 master 브랜치는 변경점이 1개뿐인데, 이것때문에 병합 커밋 한개를 생성하는게 좀 언짢지 않나요?



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\POWERPNT_XZ8raJCOhI.png" style="zoom:80%;border:2px solid;float:left;" />





이러지 말고 아래 처럼하면 어떨까요?

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\POWERPNT_iGQdOmH8MM.png" style="zoom:80%;border:2px solid;float:left;" />

빨간 네모 박스 친부분을 똑 떼어내서...



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\POWERPNT_UXYPp5UY0k.png" style="zoom:80%;border:2px solid;float:left;" />

요렇게 붙여주는 겁니다!!





실습해보죠!



1\.  [ iTshirt-raccoon ] 탭의 그래프를 다시보죠.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_AeHr7WtMfd.png" style="zoom:80%;border:2px solid;float:left;" />

"찜하기 기능 추가" 커밋을 똑 떼어내서 "개발자 목록에 너구리 추가" 커밋 뒤에 이어 붙이면 되겠네요!



소스트리에서 아래와 같이 해줍시다.

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\UxkYWNrC7a.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\sxNmfioCrm.png" style="zoom:80%;border:2px solid;float:left;" />

위 경고창은 현재 리베이스를 하려는 변경사항이 사용되지 않고 있는 상태인지를 묻는 것입니다.

리베이스는 히스토리를 강제로 조작하기 때문에 다른 사람이 이 히스토리를 보고 있으면 완전히 꼬입니다.



**그렇기 때문에 리베이스는 반드시 혼자만 쓰는 브랜치에서 수행해야합니다.**



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_Fbs0ppJTMG.png" style="zoom:80%;border:2px solid;float:left;" />

그리고 충돌이 났네요! 당연하죠, 너구리와 고양이가 똑같은 코드를 고쳤으니까요. 

충돌을 해결합시다.



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_hrPpD3t4Lv.png" style="zoom:80%;border:2px solid;float:left;" />

<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\Code_tX8YnFkBLG.png" style="zoom:80%;border:2px solid;float:left;" />



<img src="C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_88cJWkMkSB.png" style="zoom:80%;border:2px solid;float:left;" />







C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_bfFdEdtt3a.png





C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_0gNjnvkXsT.png





C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_H1DaKf3wZS.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\SourceTree_Q5iFKTCbq8.png





C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_icitjAxxQp.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_9jNXwch09m.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_4lBmd5kBQB.png





다시 고양이로 github를 로그인하고 다음과정을 거쳐서 최종적으로 merge 해줍니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_2RmPy6JOCh.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_OclgRpNyAe.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp04_img\chrome_e6IvoDWk9v.png





TheUnlikelyCandidates Novocaine

Alexander Stewart Backwards

## 귀찮은 거 미리 :anger:

<img src="" style="zoom:80%;border:2px solid;float:left;" />

<span style="font-size:0.8em"></span>

