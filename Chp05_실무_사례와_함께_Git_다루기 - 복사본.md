<div style="text-align:center">
<span style=";font-weight:bold;font-size:2em">팀 개발을 위한 Git, GitHub 시작하기</span>
</div>








# :book: Chp04. 실무 사례와 함께 Git 다루기





## :bow_and_arrow: ​TODO



| TODO LIST                                                   |
| ----------------------------------------------------------- |
| :dart: 마지막 커밋 수정하기(amend)                          |
| :dart: 원하는 커밋만 떼서 현재 브랜치에 붙인다(cherry-pick) |
| :dart: ​옛날 커밋으로 브랜치를 되돌린다(reset)               |
| :dart: ​커밋의 변경사항을 명시적으로 되돌린다(revert)        |
| :dart: ​변경사항을 잠시 따로 저장해둔다(stash)               |



더 다양한 명령어를 익혀봅시다.



고양이: 너굴님, 커밋이 잘못 푸시되었네요. 두 커밋 이전 상태로 되돌려주세요.

문어: 너굴님, [latest] 브랜치에서 빨리 고쳐야 하는 버그가 보이네요. [master] 브랜치에서 [hotfix] 브랜치를 따서 개발하고 나중에 [latest] 브랜치에 체리픽 주세요. 



---









## :cherry_blossom: 실습을 위한 사전 준비



### :seedling: GitHub 에서 새로운 원격저장소 만들기



깃과 깃허브로 관리하는 프로젝트를 시작하는 데엔 크게 2가지 방식이 있습니다.

1. **GitHub 에서 원격저장소를 만들고 이를 내 컴퓨터에 클론**한다
2. 내 컴퓨터에서 **먼저 로컬저장소를 만들고 GitHub에 원격저장소를 만들어 로컬저장소에 원격 저장소 주소를 remote add** 한다.

==> 1번 방식을 하겠습니다.



01\.  고양이로 로그인 후 **새로운 원격저장소**를 만듭니다.

<img src="Chp05_img\chrome_y4Y4DwKRfM.png" style="zoom:70%;border:2px solid;float:left;" />





02\.  README 를 생성해서 초기 커밋이 자동으로 되었네요. (initial commit 이 보이죠)
원격저장소 주소를 복사하고, 소스트리의 디폴트 계정을 고양이로 바꿉니다.

그리고 복사한 주소로 clone을 진행합니다.

<img src="Chp05_img\chrome_7hjN3RwXfm.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_3COsrpRT1U.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_eftj5sVwEu.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_8eiUeV0rH8.png" style="zoom:70%;border:2px solid;float:left;" />



이제 실습할 준비가 완료되었네요.







---









## :cherry_blossom: amend: 방금 만든 커밋에 내용 추가하기



### :seedling: amend로 마지막 커밋 수정하기

<span style="font-size:0.8em">커밋을 실수로 하면 꼭 하는 행동이 깃으로 또 한번 커밋을 날리는데 메시지를 "*커밋에 내용 추가"라는 식으로 보냅니다</span>

<span style="font-size:0.8em">그닥... 보기 좋지 않네요. 이제 방금 했던 커밋을 수정하는 법을 알아보죠</span>



01\. [git-playground] 폴더에서 amend.md 파일을 생성하고 내용에 '**어멘드 실습하기**' 라고 적고 저장합니다.

<img src="Chp05_img\Code_eAYAb5FVu7.png" style="zoom:70%;border:2px solid;float:left;" />







02\. 이후에는 소스트리에서 커밋을 합니다. 푸시는 하지마세요!

<img src="Chp05_img\SourceTree_UoJf6RELrl.png" style="zoom:70%;border:2px solid;float:left;" />







03\. amend.md 에 "어맨드"가 아니라 "amend" 라고 적어야하는 걸 뒤늦게 알아차린다고 가정하겠습니다.

수정 및 저장하고, 소스트리에서 커밋화면에서 **커밋 옵션**을 부가적으로 해줍니다.

<img src="Chp05_img\Code_6ZxSpbuHVl.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\Typora_9xS0k3kCY7.png" style="zoom:70%;border:2px solid;float:left;" />



확인창이 아래와 같이 뜨면 OK 해줍니다.

<img src="Chp05_img\GufNmkmQFW.png" style="zoom:70%;border:2px solid;float:left;" />



그러면 아래와 같이 커밋 메시지에 바로 전의 커밋 메시지가 뜹니다. 이 커밋 메시지도 수정하고 싶으면 수정하셔도 됩니다.

<img src="Chp05_img\SourceTree_d9S0rBoZb8.png" style="zoom:70%;border:2px solid;float:left;" />







04\.  커밋이 잘 바뀐걸 확인할 수 있습니다.

<img src="Chp05_img\SourceTree_1Sd6kBs2c0.png" style="zoom:70%;border:2px solid;float:left;" />







### :seedling: amend로 마지막 커밋 메시지를 수정하고 원격 브랜치에 강제 푸시하기



01\. 방금 만든 커밋을 push 해보죠.

<img src="Chp05_img\SourceTree_1rL81VmPjH.png" style="zoom:70%;border:2px solid;float:left;" />









02\. 이번엔 코드 수정 없이 커밋 메시지만 수정해보겠습니다.

커밋 옵션에서 마지막 커밋 정정을 체크 후 커밋 메시지에 '커밋 메시지 수정' 이라는 텍스트를 추가합니다.

수정 완료 후 커밋을 누릅니다.

<img src="Chp05_img\Typora_drv6LuuvF8.png" style="zoom:70%;border:2px solid;float:left;" />



그러면 아래와 같은 독특한 그래프가 그려지네요. 한번 푸시를 하고 나서 커밋을 해서 그렇습니다.

<img src="Chp05_img\SourceTree_Wdo709o1GW.png" style="zoom:70%;border:2px solid;float:left;" />









03\. 이제 강제 푸시를 할 건데, 이 강제 푸시를 하려는 브랜치는 만드시 혼자만 쓰고 있어야 합니다.

[ 도구 > 옵션 > Git 탭 ]

<img src="Chp05_img\SourceTree_kuVIPP7vM8.png" style="zoom:70%;border:2px solid;float:left;" />



04\. 세팅이 끝나면 푸시를 클릭합니다. 그리고 팝업창에 [강제 푸시] 옵션을 체크하고 푸시합니다.

<img src="Chp05_img\SourceTree_POt2ejZW3E.png" style="zoom:70%;border:2px solid;float:left;" />



그러면 아래와 같이 깔끔하게 수정이 된것을 확인할 수 있습니다.

<img src="Chp05_img\SourceTree_Wv1Viy6YDR.png" style="zoom:70%;border:2px solid;float:left;" />





---





## :cherry_blossom: cherry-pick: 커밋 떼 와서 브랜치에 붙이기

<div style="font-size:0.8em"></div>

너구리 회사의 브랜치 전략을 살펴보죠



개발자들은 master 브랜치에서 각자 \[ feat/ 기능이름 ] 으로 브랜치를 따서 개발하고, 
개발을 완료한 후에 \[ master] 브랜치에 병합시킵니다. 

이 \[master] 브랜치의 코드는 자동으로 test.itshirt.com에 배포되어 항상 최신 개발 버전을 볼 수 있습니다.
그리고 \[master] 에서 굵직한 개발이 끝나면 이 코드를  \[latest] 브랜치에 병합시키고 이를 실제 서버인 \[latest] 
브랜치에 병합시키고 이를 실제 서버인 itshirt.com에 배포합니다.



위의 설명을 그림으로 보면 아래와 같다.



<img src="Chp05_img\POWERPNT_V0GbJpIps7.png" style="zoom:70%;border:2px solid;float:left;">





그런데 어제 출시한 코드가 담긴 latest 브랜치에 당장 고쳐야하는 버그가 있다는 것을 뒤늦게 깨닫고, 
문어는 급하게 master 브랜치에서 \[fixt/text-bug] 브랜치를 따서 고치고 이를 마스터 브랜치에 병합했습니다.

이제 latest 브랜치에 반영해야 하는데, master 브랜치에 있는 다른 변경사항 말고 딱 그 버그를 고친 커밋만 반영하려고 합니다 아직 다른 기능들은 출시할 시점이 아니거든요...



이럴 때!   **체리픽** 기능을 쓰면 됩니다.



---



### :seedling: cherry-pick: 다른 브랜치의 커밋 하나만 내 브랜치에 반영하기



이번 실습에서는 feat/a , feat/b 브랜치를 만들고 feat/a 브랜치의 커밋 하나를 feat/b 브랜치에 반영하겠습니다.





#### 01.  feat/a 브랜치 생성 및 커밋 연달아 생성



\- **베이스 생성**

<img src="Chp05_img\SourceTree_w1ieiuEW3r.png" style="zoom:70%;border:2px solid;float:left;" />



\- **커밋 생성 (1)**

<img src="Chp05_img\Code_1hgbiaIW9q.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_6BhXxXkubO.png" style="zoom:70%;border:2px solid;float:left;" />





\- **커밋 생성(2)**

<img src="Chp05_img\Code_0SnZpBsj0j.png" style="zoom:70%;border:2px solid;float:left;" />

<img src="Chp05_img\SourceTree_DAAJGMQi3f.png" style="zoom:70%;border:2px solid;float:left;" />





\- **커밋 생성(3)**

<img src="Chp05_img\Code_gN22NQdWey.png" style="zoom:70%;border:2px solid;float:left;" />





\- **결과: 그래프 모습**

<img src="Chp05_img\SourceTree_O0xSc6iTiy.png" style="zoom:70%;border:2px solid;float:left;" />





#### 02. feat/b 브랜치 생성 후 한 개의 커밋 생성



\- 브랜치 생성 (master로 체크아웃 후 생성)

<img src="Chp05_img\q7MsvCHKm5.png" style="zoom:70%;border:2px solid;float:left;" />

<img src="Chp05_img\SourceTree_ryUIO0dP2p.png" style="zoom:70%;border:2px solid;float:left;" />



\- 커밋 생성

<img src="Chp05_img\Code_TBBSpaWhEe.png" style="zoom:70%;border:2px solid;float:left;" />

<img src="Chp05_img\SourceTree_rS3Hbu0Far.png" style="zoom:70%;border:2px solid;float:left;" />



\- 결과: 그래프 모습

<img src="Chp05_img\SourceTree_AdUT1EpyxB.png" style="zoom:70%;border:2px solid;float:left;" />



위의 그래프를 보고 현재까지의 상황을 정리하면,  고양이가 feat/a 브랜치를 ,   문어가 feat/b 브랜치를  작업하고
있습니다. 그런데, 문어는 고양이의 커밋 중 '두 번째 커밋 - 탐나는 커밋' 만을 가져와서 feat/b 브랜치에 반영하고 싶습니다.

가져오고 싶은 것은 두 번째 커밋인데 feat/a 브랜치와 병합하면 '첫 번째 커밋'과 '세번째 커밋'이 
feat/b 브랜치에 반영되니 이 상황은 피하고 싶네요.

이때! 체리픽을 사용하는 기능이 체리픽입니다.







#### 03. 체리픽으로 원하는 커밋 가져오기



\- feat/b 브랜치에 있는 상태에서 복제하길 원하는 커밋인  feat/a 의 '두 번째 커밋 - 탐나는 커밋' 위에서
  오른쪽 버튼 클릭 후, \[체리 픽]을 클릭합니다. 

<img src="Chp05_img\SourceTree_0N4i2rjKFf.png" style="zoom:70%;border:2px solid;float:left;" />

==> 이게 성공하면, '두 번째 커밋 - 탐나는 커밋'이 \[feat/b] 브랜치에 반영됩니다. 이 커밋의 변경사항은 cherrypick.md 파일 추가였죠? 따라서 \[ feat/b ] 브랜치에는 cherrypick.md 파일이 추가됩니다.





\- 메시지 확인 클릭

<img src="Chp05_img\SourceTree_B32OeOC5UN.png" style="zoom:70%;border:2px solid;float:left;" />





\- 결과: 그래프 확인

<img src="Chp05_img\SourceTree_8OKt8STY9L.png" style="zoom:70%;border:2px solid;float:left;" />



위에보면 원하던 커밋을 [ feat/b ] 브랜치에 성공적으로 붙였습니다. 

여기서 중요한 것은 비록 "복사한" 커밋이지만,  **두 커밋의 ID 값이 다르다는 것**을 알 수 있습니다.

**즉 서로 같은 커밋이 아니라는 것이죠**..





----







## :cherry_blossom: reset: 옛날 커밋으로 브랜치를 되돌리기



고양이는 '좋아요' 및 '싫어요' 리액션 버튼을 만들었습니다. 그런데 개발팀에 전달된 요청사항이 '싫어요' 버튼
빼고 '좋아요' 버튼만 만들어 달라고 바뀌었습니다. 이미 '싫어요' 버튼까지 개발이 끝났는데 어쩌죠?

다행히 중간중간 커밋을 자주 만들어놔서 옜날 커밋으로 간단히 상태만 돌리면 끝날 문제입니다.

이럴 때 쓰는 명령이 reset(되돌리기) 입니다.





### :seedling: Soft/Mixed reset: 모든 기억을 남기면서 브랜치를 되돌리기



바로 전에 만들었던 [ feat/b ] 브랜치에서 이어서 실습하겠습니다.



일단 본격적으로 시작하기 앞서 로컬에서 일어났던 변경사항들을 원격에 푸시하겠습니다.

<img src="Chp05_img\SourceTree_fmajddthSV.png" style="zoom:70%;border:2px solid;float:left;" />







#### 01.  reset 하기



\- [ feat/b ] 브랜치는 현재 '두번째 커밋 - 탐나는 커밋' 에 있습니다. 이 브랜치의 최신 상태를 하나 전인 
  'featb 기능 추가' 커밋으로 되돌려 보겠습니다. 'featb 기능 추가'에 오른쪽 마우스 클릭 후,
  \[ 이 커밋까지 현재 브랜치를 초기화 ] 를 클릭합니다.



<img src="Chp05_img\4ZCWu8VGyk.png" style="zoom:70%;border:2px solid;float:left;" />





#### 02.  Soft, Mixed, Hard  모드



그런데  \[ 이 커밋까지 현재 브랜치를 초기화 ]  클릭 후, 헷갈리는 옵션이 아래와 같이 나옵니다.

<img src="Chp05_img\SourceTree_jy3RYDJAci.png" style="zoom:70%;border:2px solid;float:left;" />



우리가 보통 생각하는 리셋, **지금 작업 공간이 더럽든, 깨끗하든, 혹은 커밋 다음에 100개의 커밋이 추가했든 그냥 깔끔하게 히스토리를 돌리는 그런 리셋** , 은   **\[Hard]**  를 선택하면 됩니다.



반명 \[ Soft ], \[ Mixed ] 모드는 원하는 커밋으로 이력을 되돌리긴 하지만, 이 다음에 추가했던 모든 변경사항을 작업 공간으로 뽑아 줍니다.



변경사항을 작업 공간으로 뽑아 준다는 게 뭔지 모르겠죠? 실습으로 알아보죠.







\- 기본 옵션인 **\[ Mixed ] 모드**를 선택하고 확인 클릭합니다.

<img src="Chp05_img\SourceTree_nBrV2m57Sb.png" style="zoom:70%;border:2px solid;float:left;" />



그런데 클릭 후에 그래프에 "커밋하지 않은 변경사항"이 생깁니다. 아래와 같이 말이죠.

<img src="Chp05_img\SourceTree_FvTtTORB35.png" style="zoom:70%;border:2px solid;float:left;" />



해당 커밋의 내용을 확인하면 '두번째 커밋 - 탐나는 커밋' 에서 추가했던 \[ cherrypick.md ] 변경사항이 스테이지 아래로 튕겨나온 걸 볼 수 있습니다.

**시간은 성공적으로 되돌렸지만 변경사항은  '두번째 커밋 - 탐나는 커밋'을 커밋하기 전 상태로 남겨둔 것입니다.**



커밋이 없던 걸로 되돌렸지만, cherrypick.md를 만들었던 기록이 스테이지 아래에 살아났으니 이제 이걸 마음대로 변경도 가능하다는 겁니다!





\- 참고: Soft 모드 vs Hard 모드 (눈으로만 보기)

- Mixed 모드는 변경사항을 스테이지 아래로 둬서 다시 무엇을 스테이지 위로 Add 할지 고민할 수 있습니다.

- Soft 모드는 변경사항을 스테이지 위로 둬서 다시 당장 커밋할 수 있습니다.







### :seedling: Hard reset: 모든 기억을 지우며 브랜치를 되돌리기



#### 01. 다시 미래로 가기  

앞서 설명했듯, Hard 모드는 내가 어디에 있든지, 커밋하지 않은 변경사항이 얼마나 있는지와 상관 없이 어드로든 갈끔하게 이동할 수 있습니다.

자아, 그러면 미래로 돌아가보죠.  



\- 원격 브랜치인 [ origin/feat/b ] 에 있는 '두번재 커밋 - 탐나는 커밋'에서 우측 버튼을 클릭한 뒤 
  \[ 이 커밋까지 현재 브랜치를 초기화 ] 를 클릭하고 브랜치를 되돌리겠습니다.



<img src="Chp05_img\SourceTree_2ppPnZd9ON.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_w2eHgdLahY.png" style="zoom:70%;border:2px solid;float:left;" />



아래와 같이 확인창이 나오면 \[ 예 ] 를 클릭하세요. 

<img src="Chp05_img\sbV784eMWD.png" style="zoom:70%;border:2px solid;float:left;" />



\- 결과: 그래프 확인

<img src="Chp05_img\SourceTree_fpRjKkxuQh.png" style="zoom:70%;border:2px solid;float:left;" />



미래로 무사히 왔네요.





#### 02. 더 과거로 가기

더 과거로 가겠습니다. 'featb 기능 추가' 과거로 돌아가겠습니다. 이번엔 \[Hard] 리셋을 해서 이력을 깔끔하게 과거로 돌아갈 것입니다. 아래와 같이 실습해보세요.

<img src="Chp05_img\kcW8kqTgnG.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_KwSClXq0tr.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_x5WMRpuXVj.png" style="zoom:70%;border:2px solid;float:left;" />







#### 03. (강제)푸시까지 하기



아 그런데 아직 원격에는 반영이 안됐네요. 푸시를 아직 안했으니 당연한 거죠.

다만,  **히스토리를 수정하는 푸시이기 때문에 [강제 푸시] 옵션으로 해야합니다**.

(강제 푸시는 나만 쓰는 브랜치에서만 해야하는 거... 기억하죠?)



\- 강제 푸시하기

<img src="Chp05_img\SourceTree_gHrsT5Wbrq.png" style="zoom:70%;border:2px solid;float:left;" />



\- 결과: 그래프 확인

<img src="Chp05_img\SourceTree_kjerjodt3N.png" style="zoom:70%;border:2px solid;float:left;" />





----







## :cherry_blossom: revert: 이 커밋 변경사항을 되돌리고 싶어요

앞 절에서 reset 명령어로 커밋을 마치 없었던 일처럼 되돌리는 방법을 배웠습니다.

**하지만 모두가 함께 쓰는 브랜치라 이력 관리가 중요하다면 이렇게 쥐도 새도 모르게 없었던 일처럼 만드는 것은**
**올바르지 않습니다.**

이러는 것보다는 **변경사항을 되돌리는 새로운 커밋을 만드는 것**이 더 좋습니다.

이를 위한 게 바로 **revert(되돌리기)** 입니다.



### :seedling: revert: 커밋의 변경사항을 되도리는 새로운 커밋 만들기



#### 01. 이상한 커밋 생성



\- README.md 파일을 열어서 '#git-playground' 를 삭제합니다.

<img src="Chp05_img\Code_kDFsgEinmU.png" style="zoom:70%;border:2px solid;float:left;" />



\- 커밋합니다.

<img src="Chp05_img\SourceTree_sQyDnybQHU.png" style="zoom:70%;border:2px solid;float:left;" />







#### 02. revert 하기

이제 이 이상한 커밋을 되돌려보죠. 히스토리 패널로 돌아와서 되돌리고 싶은 커밋인 '사이트 제목 삭제'에서
마우스 오른쪽 버튼을 클릭하고 \[커밋 되돌리기] 를 선택합니다.



<img src="Chp05_img\hcuEtNRuhg.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\G4GX7XToIS.png" style="zoom:70%;border:2px solid;float:left;" />



결과: 

<img src="Chp05_img\SourceTree_VhZrIbeqTl.png" style="zoom:70%;border:2px solid;float:left;" />



'Revert "사이트 제목 삭제" ' 커밋이 만들어진 것을 확인합니다. revert 커밋은 꼭 방금 커밋이 아니더라도, 이전에 한 커밋도 얼마든지 되돌릴 수 있습니다!







----







## :cherry_blossom: stash: 변경사항 잠시 보류, 커밋은 안 만듦



너구리가 열심히 [ feat/b ] 브랜치에서 개발을 하고 있었는데 급하게 고쳐야하는 버그가 생겼습니다.

다른 브랜치로 이동하려는데 현재 브랜치에 아직 커밋하지 않은 변경사항 파일이 10개가 있습니다.

하지만 아직 커밋으로 만들기에는 애매한 파일들입니다. 

이 변경사항을 잠깐 보류하고, 이따가 다시 꺼내쓰는 방법이 스태시(Stash - 넣어 두다) 입니다.





### :seedling: stash: 커밋하지 않은 변경 사항을 보류하기



#### 01. 여러 변경사항 생성 후, 스태시 하기



<img src="Chp05_img\Code_vYMcFh6Lor.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_rkFcVZVgtA.png" style="zoom:70%;border:2px solid;float:left;" />



결과:

<img src="Chp05_img\SourceTree_apKfVAAuBi.png" style="zoom:70%;border:2px solid;float:left;" />

작업 공간이 깔끔해졌습니다! 이제 변경된 파일에 신경쓰지 않고 자유롭게 Pull 이나 브랜치 이동이 가능합니다.



참고로 stash는 tracked 상태(추적중 - 한번이라도 Git에 올렸던 상태)인 파일들만 들어갑니다.

새로 만든 파일은 untracked 상태니까 들어가지 않겠죠?





#### 02. 보류했던 변경사항 다시 꺼내기



<img src="Chp05_img\SourceTree_yDxortJ7Nv.png" style="zoom:70%;border:2px solid;float:left;" />



<img src="Chp05_img\SourceTree_GfApJhnSjc.png" style="zoom:70%;border:2px solid;float:left;" />



결과: 

<img src="Chp05_img\SourceTree_8ZEBmXZo0t.png" style="zoom:70%;border:2px solid;float:left;" />





---





이것으로 GUI로 깃을 다루는 법은 익혔습니다.

이제 대망의 CLI 로 깃을 다루는 법을 다음 챕터부터 배워보죠!



