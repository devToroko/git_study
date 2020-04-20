<div style="text-align:center">
<span style=";font-weight:bold;font-size:2em">팀 개발을 위한 Git, GitHub 시작하기</span>
</div>








# :book: Chp04. 둘 이상의 원격저장소로 협업하기





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





## :cherry_blossom: 실습을 위한 사전 준비 : 새로운 원격저장소 만들기



### :seedling: GitHub 에서 새로운 원격저장소 만들기



깃과 깃허브로 관리하는 프로젝트를 시작하는 데엔 크게 2가지 방식이 있습니다.

1. GitHub 에서 원격저장소를 만들고 이를 내 컴퓨터에 클론한다
2. 내 컴퓨터에서 먼저 로컬저장소를 만들고 GitHub에 원격저장소를 만들어 로컬저장소에 원격 저장소 주소를 remote add 한다.

==> 1번 방식을 하겠습니다.



01\.  고양이로 로그인 후 새로운 원격저장소를 만듭니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\chrome_y4Y4DwKRfM.png





2\.  README 를 생성해서 초기 커밋이 자동으로 되었네요. (initial commit 이 보이죠)
원격저장소 주소를 복사하고, 소스트리의 디폴트 계정을 고양이로 바꿉니다.

그리고 복사한 주소로 clone을 진행합니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\chrome_7hjN3RwXfm.png

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_3COsrpRT1U.png



C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_eftj5sVwEu.png

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_8eiUeV0rH8.png



이제 실습할 준비가 완료되었네요.





## :cherry_blossom: amend: 방금 만든 커밋에 내용 추가하기



### :seedling: amend로 마지막 커밋 수정하기

<span style="font-size:0.8em">커밋을 실수로 하면 꼭 하는 행동이 깃으로 또 한번 커밋을 날리는데 메시지를 "*커밋에 내용 추가"라는 식으로 보냅니다</span>

<span style="font-size:0.8em">그닥... 보기 좋지 않네요. 이제 방금 했던 커밋을 수정하는 법을 알아보죠</span>



1\. [git-playground] 폴더에서 amend.md 파일을 생성하고 내용에 '어멘드 실습하기' 라고 적고 저장합니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\Code_eAYAb5FVu7.png







2\. 이후에는 소스트리에서 커밋을 합니다. 푸시는 하지마세요!

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_UoJf6RELrl.png







3\. amend.md 에 "어맨드"가 아니라 "amend" 라고 적어야하는 걸 뒤늦게 알아차린다고 가정하겠습니다.

수정 및 저장하고, 소스트리에서 커밋화면에서 **커밋 옵션**을 부가적으로 해줍니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\Code_6ZxSpbuHVl.png

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\Typora_9xS0k3kCY7.png



확인창이 아래와 같이 뜨면 OK 해줍니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\GufNmkmQFW.png



그러면 아래와 같이 커밋 메시지에 바로 전의 커밋 메시지가 뜹니다. 이 커밋 메시지도 수정하고 싶으면 수정하셔도 됩니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_d9S0rBoZb8.png







4\.  커밋이 잘 바뀐걸 확인할 수 있습니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_1Sd6kBs2c0.png







### :seedling: amend로 마지막 커밋 메시지를 수정하고 원격 브랜치에 강제 푸시하기



1\. 방금 만든 커밋을 push 해보죠.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_1rL81VmPjH.png









2\. 이번엔 코드 수정 없이 커밋 메시지만 수정해보겠습니다.

커밋 옵션에서 마지막 커밋 정정을 체크 후 커밋 메시지에 '커밋 메시지 수정' 이라는 텍스트를 추가합니다.

수정 완료 후 커밋을 누릅니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\Typora_drv6LuuvF8.png



그러면 아래와 같은 독특한 그래프가 그려지네요. 한번 푸시를 하고 나서 커밋을 해서 그렇습니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_Wdo709o1GW.png









3\. 이제 강제 푸시를 할 건데, 이 강제 푸시를 하려는 브랜치는 만드시 혼자만 쓰고 있어야 합니다.

[ 도구 > 옵션 > Git 탭 ]

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_kuVIPP7vM8.png



4\. 세팅이 끝나면 푸시를 클릭합니다. 그리고 팝업창에 [강제 푸시] 옵션을 체크하고 푸시합니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_POt2ejZW3E.png



그러면 아래와 같이 깔끔하게 수정이 된것을 확인할 수 있습니다.

C:\Users\parknote\Desktop\팀개발을위한Git_GitHub_시작하기\Chp05_img\SourceTree_Wv1Viy6YDR.png









## :cherry_blossom: cherry-pick: 커밋 하나만 떼 와서 지금 브랜치에 붙이기



### :seedling: cherry-pick: 다른 브랜치의 커밋 하나만 내 브랜치에 반영하기

<div style="font-size:0.8em"><p>
w    
</p></div>











## 귀찮은 거 미리 :anger:

<img src="" style="zoom:70%;border:2px solid;float:left;" />

<span style="font-size:0.8em"></span>

