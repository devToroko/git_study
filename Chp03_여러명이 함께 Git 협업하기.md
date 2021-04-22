<div style="text-align:center">
<span style=";font-weight:bold;font-size:2em">팀 개발을 위한 Git, GitHub 시작하기</span>
</div>






# :book: Chp03. 여러명이 함께 Git 협업하기





## :page_with_curl: TODO LIST



| 구분 | 내용                                                         |
| ---- | ------------------------------------------------------------ |
| 1절  | Git이 커밋을 관리하는 방식 :heavy_check_mark:                |
| 2절  | 브랜치를 만든다(branch), 이동한다(checkout) :heavy_check_mark: |
| 3절  | 브랜치를 병합한다(merge) :heavy_check_mark:                  |
| 4절  | 충돌을 해결한다 :heavy_check_mark:                           |
| 5절  | 풀 리퀘스트(Pull Request) ​                                   |
| 6절  | 릴리즈(release)                                              |



고양이: 이제는 분업할 때가 됐어. 나는 상세 설명 기능을 만들어서 커밋할게, 너는 장바구니 기능을 커밋해 줘.

문어: 좋아. 그런데 만약 동시에 커밋을 올리게되면 어떻게 돼? 꼬일수도 있지 않아?

고양이: 걱정 마, 우리 둘다 원격저장소에 커밋을 올릴 것이지만,
 			**원격저장소 안의 서로 다른 가지(브랜치)에 커밋을 올릴거야**. 
			그런 후에 나중에 각 브랜치에 있는 커밋을 합칠 수 있어.

문어: 아하, 그렇구나.일단은 고양이 브랜치, 문어 브랜치 하나씩 만들어야겠구나.



----





## :fountain_pen: 원격저장소에서 협업하기: 브랜치(Branch)





### :writing_hand: Git이 커밋을 관리하는 방식 : 줄줄이 기차



Git에서는 **병렬 버전 관리**를 어떻게 할까요?



Chp02 에서 변경사항을 묶어서 하나의 덩어리를 만들었는데, 이것이 커밋이죠. 

(좀더 상세히 말하자면 , 커밋을 하면 "커밋 객체"가 만들어지는 겁니다)

그리고 그 커밋들은 아래와 같이 줄줄이 연결되어있습니다.

(커밋 객체는 이전 커밋 객체에 대한 포인터값을 갖고 있다는 뜻입니다)

<img src="Chp03_img\POWERPNT_5KI6JEMkFv.png" style="zoom:80%;border:2px solid;float:left" />

한명이 작업한다면 위 그림처럼 되겠죠. 하지만 두 명 이상이 한다면 어떻게 될까요?

분명 한줄로는 커밋을 이어나가진 못할겁니다.

그러면 자연스럽게 두 갈래로 나뉘게 될거라는 것이 떠오를겁니다. 





맞습니다, 특정 기준이 되는 줄기에서 두 갈래로 커밋이 나뉘어지게 되는 것이죠. 아래 그림처럼요!

<img src="Chp03_img\POWERPNT_yNb1ISIMCE.png" style="zoom:80%;border:2px solid;float:left" />

(다른 커밋 객체 2개가 만들어지고, 각각 같은 포인터값을 갖게되는 것이죠)



**이렇게 특정 기준에서 줄기를 나누어 작업할 수 있는 기능을 "브랜치(Branch)" 라고 합니다**.

새로운 가지로 커밋을 하려면 반드시 브랜치를 먼저 만들어야 합니다.



(참고: https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html )

<img src="Chp03_img\chrome_NgHkZgX3Lu.png" style="zoom:80%;border:2px solid;float:left" />







### :writing_hand: 브랜치의 정체

Chp02의  master 와 origin/master 라는 꼬리표를 sourceTree 에서 본적 있죠?

이 master 라는 것은 Git이 기본으로 제공하는  브랜치입니다.



첫 번째 커밋을 하면 자동으로 'master' 라는 이름의 브랜치가 커밋을 가리키게 만들죠,

여기서 정말 중요한 점은  "master"라는 브랜치는 사실 커밋 객체를 가르키는 포인터라는 것입니다.

그리고 새로 커밋을 할때마다 "master" 브랜치(포인터)는 가장 최신 커밋을 가리킵니다.



그렇다면 이런 포인터를 1개 더 생성했다고 가정해보죠. 아래와 같이 말이죠.

<img src="Chp03_img\POWERPNT_f62nr4Tu5M.png" style="zoom:80%;border:2px solid;float:left" />





이 상태에서 고양이 브랜치가 하나의 커밋을 더하고나서 master도 따로 커밋을 또 하면 다음과 같은 그림이 나옵니다.



\- 고양이 브랜치를 선택(checkout)하여서 커밋을 합니다.

<img src="Chp03_img\POWERPNT_XHlMPrXsRs.png" style="zoom:80%;border:2px solid;float:left" />



\- master 브랜치를 선택(checkout)하여서 커밋을 합니다. 그러면 아래와 같이 두개의 커밋이 하나의 커밋을 동시에 가리키는 것을 확인할 수 있습니다. 이렇게 되면 각자의 브랜치에서 각자의 커밋을 이어서 만들어 나갈 수 있겠죠? 

<img src="Chp03_img\POWERPNT_hXIQIqiV4N.png" style="zoom:80%;border:2px solid;float:left" />





그런데 말이죠...위에서 **checkout**을 통해서 브랜치를 바꾸는게 어떻게 가능할까요?

이것은 **\[HEAD] 라는 특수한 포인터** 덕분입니다.

이 포인터 덕분에 저희는 여러 브랜치들을 오고갈 수 있는 것이죠.

<img src="Chp03_img\POWERPNT_ivdiwgITR1.png" style="zoom:80%;border:2px solid;float:left" />

그런데 이렇게 checkout 명령어를 써서 HEAD를 옮기면 우리의 폴더 내부의 파일들 상태는 어떨까요?

지금 위 그림 같은 상황이면 우리가 마지막 커밋을 했을 때의 상황과 일치하는 파일 상태입니다.

그러면 HEAD가 고양이 브랜치를 가르키게 하면 어떻게 될까요? 

"커밋5" 최종적으로  commit했던 파일들이 보여줄겁니다.



checkout으로 꼭 특정 브랜치를 가르킬 필요는 없답니다. 
아래처럼 특정 커밋을 직접적으로 가리키게 할 수도 있죠. 
이런 HEAD의 상태를  "**분리된 HEAD ( Detached HEAD)**" 라고 합니다.

<img src="Chp03_img\POWERPNT_0hfQLxF55J.png" style="zoom:80%;border:2px solid;float:left" />









## :fountain_pen: 브랜치 실습 기본 : 만들고, 이동한다





### :writing_hand: 새 브랜치 만들기



이제 본격적으로 위에서 말했던 흐름대로 브랜치를 만들고, 브랜치를 checkout으로 이동해보죠.
잠시 여태까지 했던 커밋들을 돌아볼까요?

<img src="Chp03_img\SourceTree_0HhDARGwfG.png" style="zoom:80%;border:2px solid;float:left" />



현재 \[master] 브랜치의 최신 커밋을 기준으로 고양이가 상세 설명 개발에 사용할 **'detail-page' 라는 이름의 브랜치**를 만들어 보죠.



보통 **하나의 브랜치 당 한 사람**이 작업하는게 바람직합니다. 그래야 버전이 꼬이지 않겠죠? 
그러다보니 여러사람이 작업하는 **원격저장소에는 미리 브랜치 규칙을 정하는게 일반적**입니다.



지금 우리 같은 경우는 아래와 같은 규칙을 정했습니다.

- \[master] 브랜치에는직접 커밋을 올리지 않는다
- 기능 개발을 하기 전에 \[master] 브랜치를 기준으로 새로운 브랜치를 만든다
- 이 브랜치 이름은 \[feature/기능이름] 형식으로 하고 한 명만 커밋을 올린다
- \[feature/기능이름] 브랜치에서 기능 개발이 끝나면 \[master] 브랜치에 이를 합친다





지금부터 **고양이**의 입장에서 작업을 진행해보겠습니다. 
TODO에서 고양이와 문어가 대화할 때, 고양이는 기능 상세 설명을 작성한다고 했던거 기억하시죠 ?



1\. 다음 그림을 따라해보세요. 

<img src="Chp03_img\SourceTree_ixjc7BaqU6.png" style="zoom:80%;" />

현재 최신 커밋에 새로운 브랜치(커밋 객체를 가르키는 포인터)를 만듭니다. 

참고로 \[새 브랜치 체크아웃] 은 새 브랜치를 만듦과 동시에 \[HEAD\] 포인터도 그 브랜치를 가르키게 합니다.



2\. 다시 History 에 가면...

<img src="Chp03_img\SourceTree_ymld0ivlJe.png" style="zoom:80%;border:2px solid;float:left" />

왼쪽의 사이드바에 폴더 목록 처럼 나뉘는 것은 sourceTree의 편의 기능입니다. "/" 로 브랜치 이름을 정해주면

알아서 디렉토리 구조처럼 보여주는 것이지요.





3\. 이제 \[iTshirt-cat] 폴더에서 **새 파일**(detail-page.md)을 만들고, 내용 작성 및 저장 후, 커밋을 하겠습니다.

<img src="Chp03_img\Code_8rjSaM10dS.png" style="zoom:80%;border:2px solid;float:left" />



<img src="Chp03_img\SourceTree_kKMVNchtY6.png" style="zoom:80%;border:2px solid;float:left" />



커밋하면 그래프가 다음과 같이 나옵니다. 현재 브랜치(feature/detail)가 최신 커밋을 잘 가르키고 있네요.

<img src="Chp03_img\SourceTree_beLylXSGhJ.png" style="zoom:80%;border:2px solid;float:left" />





4\. feature/detail 브랜치에서 커밋을 하나 더 추가해보죠. 예전에 작성한 feature-list.md 파일에 내용을 
    추가합니다.

<img src="Chp03_img\Code_8jRZY63e6V.png" style="zoom:80%;border:2px solid;float:left" />





5\. 소스트리에 돌아가서 커밋을 진행해봅니다.

<img src="Chp03_img\SourceTree_jscwxT5Fhf.png" style="border:2px solid;float:left" />

\[-에 바뀐 내용 즉시 푸시] 체크박스를 선택하고 \[ 커밋 ] 버튼을 눌러주세요. 그러면 \[feature/detail-page]에 푸시까지 한 번에 됩니다.





6\. History에 \[**origin**/feature/detail-page\] 이 보입니다. 
    원격 저장소에도 현재 브랜치의 커밋이 잘 올라갔다는 뜻입니다.

<img src="Chp03_img\SourceTree_84i1wt72oC.png" style="zoom:80%;border:2px solid;float:left" />



7\. 원격저장소에 가보니 브랜치가 하나 더 생긴것을 확인 할 수 있습니다.

<img src="Chp03_img\chrome_l8dwShrdbQ.png" style="zoom:60%;border:2px solid;float:left" />







### :writing_hand: 브랜치 이동하기 : 체크아웃(checkout)

이번에는 고양이가 아니라 **문어의 입장**에서 브랜치를 만들고 버전관리를 해보죠.
(문어는 장바구니 기능을 만들기로 했던거 기억하시죠?)

master 브랜치로 돌아가서(checkout 사용) 새로운 브랜치를 만들면서 차차 해보죠.



1\. 소스트리 좌측 탭에서 **체크아웃**하려는 브랜치에서 마우스 오른쪽 클릭 \> 체크아웃 *... 를 클릭합니다.
    귀찮으면 그냥 더블 클릭해도 됩니다.

<img src="Chp03_img\SourceTree_mnDmJh6mpU.png" style="zoom:80%;border:2px solid;float:left" />



2\. **브랜치를 생성**합니다.

<img src="Chp03_img\SourceTree_ZPsqjpjAEh.png" style="zoom:80%;border:2px solid;float:left" />



3\. 이렇게 **생성된 브랜치**에서 **feature-list.md 파일의 내용을 살짝 변경**해보겠습니다. 문어는 고양이가 현재 이 
     파일을 건든지는 모르는 상태라고 가정하고 변경하는겁니다. (이런 일은 실제로도 비일비재할 겁니다)

<img src="Chp03_img\Code_PWb7ai7yif.png" style="zoom:80%;float:left" />



여기에 덧붙여 cart.md 파일을 생성하겠습니다.

<img src="Chp03_img\akQHQAAOJg.png" style="zoom:80%;float:left" />





4\. 커밋과 푸시를 진행합니다.

<img src="Chp03_img\SourceTree_nQlBZ0SGf1.png" style="zoom:80%;border:2px solid;float:left" />



<img src="Chp03_img\SourceTree_7RNTqJDkVq.png" style="zoom:80%;border:2px solid;float:left" />





---





## :fountain_pen: 브랜치와 브랜치를 합치기 : 병합(merge, 머지)



### :writing_hand: 병합은 무엇인가?



**병합은 두 버전의 "합집합"을 구하는 과정입니다**.

1. 병합커밋(Merge Commit)
2. 빨리감기(Fast-forward)
3. 충돌(Conflict)

![](Chp03_img\POWERPNT_KJtay9jUNl.png)







### :writing_hand: 두 브랜치를 합치는 과정



Git에서 **브랜치와 브랜치를 합치는 명령어는 머지**입니다. 고양이와 문어의 브랜치를 \[master] 브랜치로 합쳐야합니다. 그 과정을 도식하면 아래 그림과 같습니다.



1\. master 브랜치에 feature/detail-page 브랜치를 합치기 전, 즉 현재의 상태입니다.

<img src="Chp03_img\POWERPNT_2J180uOkVn.png" style="zoom:80%;border:2px solid;float:left" />



2\. 합치는 과정

우선 master branch를 feature/detail-page 브랜치와 병합을 시도합니다. 그러면 빨리 감기를 통한 병합이 되고

아래 그림과 같은 상태가 됩니다.

<img src="Chp03_img\POWERPNT_mWcNEn3h1S.png" style="zoom:80%;border:2px solid;float:left" />



그 이후에는 필요없게 된 feature/detail-page 브랜치는 지워도 됩니다.

<img src="Chp03_img\POWERPNT_MY3NQmyjVE.png" style="zoom:80%;border:2px solid;float:left" />





이제는 master 브랜치와 feature/cart 브랜치를 병합할 차례입니다. 이 병합은 충돌이 나지 않으면 병합 커밋이 생성될 겁니다. 그런데 새로운 병합 커밋이 생기면 그 커밋은 두 브랜치 중 어떤 것이 가르키게 될까요?

이것은 본인의 선택입니다. 현재는 master 브랜치에 feature/cart 브랜치를 합치는 상황이니까 
master 브랜치가 최종적인 병합 커밋을 가르키도록 하겠습니다. 그리고 이렇게 되면 남은 feature/cart 브랜치는 여전히 커밋5 를 가르키고 있을 겁니다.

<img src="Chp03_img\POWERPNT_aEth6KKBOm.png" style="zoom:80%;border:2px solid;float:left" />







### :writing_hand: 브랜치 합치기 실습 : 빨리 감기 병합



1\. 소스트리 좌측에서 **master 브랜치를 체크아웃** 하고, 그 상태에서 **feature/detail-page 와 병합**을 합니다. 
    방법은 아래와 같습니다.

<img src="Chp03_img\SourceTree_qQpf6tXCWb.png" style="border: 2px solid; float: left; zoom: 80%;" />

<img src="Chp03_img\SourceTree_pUn40d59Aa.png" style="zoom:80%;float:left" />





2\. 두 브랜치가 합쳐지면 그래프의 모양은 다음과 같이 변합니다.

<img src="Chp03_img\SourceTree_EABUXmFUtv.png" style="zoom:80%;border: 2px solid; float: left; " />

그런데 위 그림에서 master 에 숫자"2" 가 붙어있습니다. 이것은 2개의 커밋이 로컬 저장소에만 이루어졌고,

원격 저장소(origin)에는 올라가지 않았다는 뜻입니다.



그래프만 봐도 현재 origin/master 브랜치가 master 브랜치보다 2개의 커밋이 뒤쳐진 걸 알수 있죠.





3\. 반영되지 않은 2개의 **커밋을 원격에 푸시**합니다.

<img src="Chp03_img\SourceTree_675Kppoevr.png" style="zoom:80%;border: 2px solid; float: left;" />



<img src="Chp03_img\SourceTree_K2eSaCkYht.png" style="zoom:80%;border: 2px solid; float: left;" />









## :fountain_pen: 앗! 둘이 똑같은 코드를 고쳤어요 : 충돌(conflict) 해결하기



### :writing_hand: 브랜치 합치기 실습 : 병합 커밋 및 충돌 해결

앞에서는 master 브랜치를 기준으로 병합했다면, 이번에는 feature 브랜치 기준으로 병합해보죠.
아래 도식을 보면서 이해해보죠.



<img src="Chp03_img\ZRQtibcjBp.png" style="zoom:80%;border: 2px solid; float: left;" />

위 그림을 보면 알겠지만 feature 브랜치 기준으로 병합을 했습니다. 왜 그랬을까요?

<span style="color:red;font-weight:bold">병합 커밋을 만들어내는 과정에는 얼마든지 충돌이 날 수 있습니다</span>. 

그래서 **모두가 사용하는 master 브랜치**에 바로 병합하지 않고, 

혼자서만 사용하는 feature/cart 브랜치 기준으로 먼저 병합해서 문제가 없는지 확인합니다.



<img src="Chp03_img\POWERPNT_pjLQmUMjDy.png" style="zoom:80%;border: 2px solid; float:left;" />

병합커밋이 무사히 생긴것을 feature/cart 브랜치로 확인했으면, 이것을 master 브랜치에 반영합니다.



이제 소스트리로 직접 해보죠.



1\. feature/cart 브랜치 기준으로 병합을 시도합니다. 먼저  **feature/cart 에 체크아웃**을 하고
    **병합하려는 커밋인 master 브랜치**의 최신 커밋에 오른쪽 마우스 클릭 후 \[병합] 을 클릭합니다.

<img src="Chp03_img\SourceTree_mjy7hfn9ZK.png" style="zoom:80%;border: 2px solid; float:left;" />

<img src="Chp03_img\SourceTree_EtajyrWiqa.png" style="zoom:80%;border: 2px solid; float:left;" />





2\. 앗! 충돌이 났군요... 일단 경고창의 닫기 버튼을 눌러줍니다.

<img src="Chp03_img\SourceTree_X8UdvbUOE7.png" style="zoom:80%;border: 2px solid; float:left;" />





3\. 커밋하지 않은 변경사항을 선택하면 feature-list.md  파일이 스테이지 아래에 있는 것을 확인할 수 있습니다.

<img src="Chp03_img\SourceTree_nRGGEMb34o.png" style="zoom:80%;border: 2px solid; float:left;" />





4\. VS Code 로 해당 파일을 열어보죠. 

<img src="Chp03_img\Code_xuU6iAq8HA.png" style="zoom:80%;" />

'=======' 를 기준으로 위는 베이스 브랜치인 \[feature/cart] 브랜치의 코드가, 아래는 병합 대상인 \[master] 브랜치의 코드가 보입니다.



5\. 충돌을 해결해봅시다. 방버은 간단합니다. `<<<HEAD` , `=======`, `>>>master` 를 수동으로 지우고 적절하게 텍스트를 수정하고 저장하면 됩니다. 아래와 같이 말이죠.

<img src="Chp03_img\Code_BI32suWjji.png" style="zoom:80%;" />



6\. 다시 소스트리로 돌아가서 스테이지 아래의 feature-list.md 파일을 선택하고 오른쪽 미리보기 창에서 충돌이 모두 해결되었는지 봅니다 `<<<`, `===` 등의 특수문자가 없고 바뀐 텍스트가 보이면, 충돌은 해결된 겁니다.

"스테이지에 올라가지 않은 파일"에서  \[+] 버튼을 클릭하여 스테이지 위로 Add 합니다. 

<img src="Chp03_img\SourceTree_jaGgbNV23I.png" style="zoom:80%;border: 2px solid; float:left;" />





7\. 병합합니다.

<img src="Chp03_img\SourceTree_yNrdtssdmg.png" style="zoom:80%;border: 2px solid; float:left;" />

충돌이 난 것에 대한 커밋 메시지가 적혀있네요. 그대로 두고 커밋하겠습니다.



<img src="Chp03_img\SourceTree_9pp1Rf3iZa.png" style="zoom:80%;border: 2px solid; float:left;" />

이로써 충돌이 해결되었습니다!





8\. 이제 push를 합시다.

<img src="Chp03_img\SourceTree_gTI83duGvq.png" style="zoom:80%;border: 2px solid; float:left;" />

<img src="Chp03_img\SourceTree_BAlICNvk34.png" style="zoom:80%;border: 2px solid; float:left;" />







9\. 이제 병합된 커밋에는 문제가 없습니다. 그러니 master 브랜치에도 이를 반영할 차례이죠.

master 브랜치로 다시 checkout을 하고 \[feature/cart] 브랜치의 최신 커밋에 병합을 시도합니다.



<img src="Chp03_img\1ekvRD67Y8.png" style="zoom:80%;border: 2px solid; float:left;" />

<img src="Chp03_img\a9Uv8JokSu.png" style="zoom:80%;border: 2px solid; float:left;" />







10\. 이어서 바로 Push 도 하겠습니다.



<img src="Chp03_img\SourceTree_nGXBFvlwGi.png" style="zoom:80%;border: 2px solid; float:left;" />

<img src="Chp03_img\SourceTree_doouCxSjqX.png" style="zoom:80%;border: 2px solid; float:left;" />





11\. 원격 저장소도 확인해보죠.

<img src="Chp03_img\chrome_4t5FiLKvsE.png" style="zoom:80%;border: 2px solid; float:left;" />





12\. 여태 생성한 Branch 들도 보이네요.



<img src="Chp03_img\chrome_QZNa7Elxxe.png" style="zoom:80%;border: 2px solid; float:left;" />









## :fountain_pen: 브랜치를 합치는 예의바른 방법 : 풀 리퀘스트

<span style="font-size:0.8em">그런데 충돌만 해결했다고 무작정 내 브랜치를 master 브랜치에 병합해도 될까요?</span>
<span style="font-size:0.8em">모두가 사용하는 것이니 모두의 허락을 받고 병합을 하는게 좋지 않을까요? 맞습니다. 지금부터 할 풀 리퀘스트가 바로 그것입니다.</span>





### :writing_hand: 풀 리퀘스트 만들기

지금부터 고양이는 댓글 기능을 위해서 feature/comment 브랜치를 만들 것입니다. 그리고 고양이와 문어는 지금부터 서로 \[master] 브랜치에 통합하기 이전에 풀 리퀘스트를 하기로 약속합니다.



1\. 먼저 댓글 기능 제작을 위해 \[feature/comment] 브랜치를 생성할 것입니다.

<img src="Chp03_img\SourceTree_Dc3SVWqMS6.png" style="zoom:80%;border: 2px solid; float:left;" />



<img src="Chp03_img\SourceTree_rTZcCqs6Sk.png" style="zoom:80%;border: 2px solid; float:left;" />







2\. 해당 브랜치에서 comment.md 파일을 새로 생성 후 , 내용을 작성하고, 저장한다.

<img src="Chp03_img\0EiUJVRNPE.png" style="zoom:80%;border: 2px solid; float:left;" />





<img src="Chp03_img\SourceTree_vLqLP9xncB.png" style="zoom:80%;border: 2px solid; float:left;" />





3\.  원격 저장소에 가면 아래와 같은 화면을 볼 수 있습니다.

<img src="Chp03_img\chrome_ZS2yjZ4ima.png" style="zoom:80%;border:2px solid;float:left" />

그러면 위에서 처럼 노란색 음영이 나타난 곳에 방금 푸시한 브랜치에 대한 알림이 보입니다.

그 옆에 있는 "Compare & pull request" 를 눌러서 풀 리퀘스트를 해보도록 하겠습니다.







4\. 풀 리퀘스트 작서을 해보죠



<img src="Chp03_img\chrome_UCWDaZX7hD.png" style="zoom:80%;border:2px solid;float:left" />

1. [ base : master  ]  : 병합된 커밋이 들어갈 브랜치를 정하는 선택박스
2. [ compare : feature/comment ] : 병합의 대상이 될, 즉 내가 만들어서 base브랜치에 반영시키고 싶은 브랜치 
3. [ compare : feature/comment ] : base 브랜치와 compare 브랜치가 충돌없이 병합될 수 있다는 뜻입니다.
   이것은  GitHub가 자동으로 계산해주는 것입니다. 만약 충돌이 나면  Conflict 라고 알려줍니다.
4. Reviewers : 저장소의 협력자가 여러명이라면 몇명을 콕 찝어서 이 풀 리퀘스트를 검토시킬 수 있습니다.
5. Assignees : 이 풀 리퀘스트를 담당하는 동료를 적어줍니다. 보통 자기자신입니다.
6. Labels : 이 풀 리퀘스트에  관한 라벨을 달아줍니다. 예를 들어 "버그","리뷰 필요","프런트엔드","백엔드"





5\. 이후에 문어로 원격저장소에 오면 아래와 같은 풀 리퀘스트가 온 것을 확인할 수 있죠.
     그러면 문어는 

<img src="Chp03_img\chrome_9d01gtIcdj.png" style="border:2px solid;float:left" />

문어는 이제 이 풀 리퀘스트를 수락(Accept) 할 건지, 수정을 요청할 것인지(Request Change) , 병합할 수도 있습니다(Merge pull request). 

문어는 이 풀 리퀘스트가 문제가 없다고 판단하여 Merge pull request 를 클릭했습니다.



6\. Merge pull request 를 누르면 병합 커밋을 만들 수 있는 입력창이 보입니다. 
브랜치와 브랜치를 병합하는 것은 CLI나 GUI나 GitHub나 그게 그거입니다.

<img src="Chp03_img\chrome_TgQIHcxBFy.png" style="zoom:80%;border:2px solid;float:left" />





7\. 풀 리퀘스트가 성공적으로 병합된 후에는 닫혔다는 메시지가 나옵니다.

<img src="Chp03_img\chrome_UVeTOkS5Sb.png" style="zoom:80%;border:2px solid;float:left" />





이렇게 닫혀진 풀 리퀘스트는 Pull request > Closed 를 클릭하면 아까 닫힌 것을 확인할 수 있습니다.

<img src="Chp03_img\chrome_9AYbowZZT3.png" style="zoom:80%;border:2px solid;float:left" />



(참고로 지금은 고양이 계정으로만 계속 로그인해서 작업했지만, FM으로 하면 문어 계정을 만들고 계속 번갈아가면서 작업을 하는게 맞습니다. 책에서는 한 계정으로 위와 같이 했습니다.)



그런데 소스트리에서도 이런 병합이 잘 반영되었을까요?



<img src="Chp03_img\SourceTree_vp9YRTXX43.png" style="zoom:80%;border:2px solid;float:left" />

....?????

어떻게 된거죠 여전히 \[origin/master] 브랜치는 옛날 커밋을 가리키고 있습니다!
GitHub에서 분명 아까 병합커밋을 생성했는데 말이죠... 



이건 Git의 새로운 이력을 업데이트하는 명령어 \[ 패치 (Fetch) ] 를 안해서 그렇습니다.

<span style="color:red;font-weight:bold">풀(Pull) 이 실제 코드를 내려받는 데 비해 패치는 그래프만 업데이트합니다</span>.



<img src="Chp03_img\SourceTree_VQDPqHR4KK.png" style="zoom:80%;border:2px solid;float:left" />





이후에 그래프가 업데이트된 것을 확인합니다.

<img src="Chp03_img\SourceTree_Z4JlcmKtNv.png" style="zoom:80%;border:2px solid;float:left" />

(로컬에 있는 master 브랜치의 커밋이 2개 밀렸다는 표시가 보이네요)



8\.  이제 로컬 저장소의 master 브랜치에 새로운 커밋을 반영합시다.

<img src="Chp03_img\Typora_IP3ipId7q0.png" style="zoom:80%;border:2px solid;float:left" />



<img src="Chp03_img\SourceTree_39MUL7hM4V.png" style="zoom:67%;border:2px solid;float:left" />



<img src="Chp03_img\SourceTree_tT005W4D4v.png" style="zoom:67%;border:2px solid;float:left" />







## :fountain_pen: 개발이 완료되었습니다, 출시하죠! 릴리즈(release) !

<span style="font-size:0.8em">이제 고양이와 문어가 만든 프로젝트가 어느정도 완성되어 세상에 공개하려합니다. 버전 1.0.0 으로 공개할 예정인데, GitHub에서는 이를 어떻게 표시할까요?</span>



### :writing_hand: 특정 커밋에 포스트잇 붙이기 - 태그(tag)

현재 코드 상태를 버전 v1.0.0 으로 기록하려합니다. 이것은 태그를 통해서 간단하게 표시할 수 있는데요,

**태그는** 여태 저희가 썼던 브랜치와 같은 **포인터**입니다.



현재 저희의 최신 커밋은 [ Merge pull request # 1 ~~~] 커밋에 v1.0.0 태그를 달아보죠.



1\. \[master] 브랜치에 있는 상태에서 소스트리 상단의 \[태그] 아이콘을 클릭합니다.

<img src="Chp03_img\SourceTree_ky9aTPHGq5.png" style="zoom:67%;border:2px solid;float:left" />



<img src="Chp03_img\SourceTree_SfkpJuSFNO.png" style="zoom:67%;border:2px solid;float:left" />







2\. 태그도 푸시를 해줘야 원격저장소에서 볼 수 있습니다.

<img src="Chp03_img\SourceTree_QmwwQMmcRj.png" style="zoom:67%;border:2px solid;float:left" />





원격 저장소에 가면 태그가 등록된것을 확인할 수 있습니다.

<img src="Chp03_img\chrome_JBkQieiKsR.png" style="zoom:67%;border:2px solid;float:left" />



