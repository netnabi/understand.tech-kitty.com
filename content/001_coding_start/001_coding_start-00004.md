---
title: "함수/메소드 Function/Method"
date: 2021-12-12T11:16:32+09:00
description: "함수의 정의, Definition of Function."
tags: [함수, 메소드, Function, Method, 스코프, Scope, 호출자, Executor, Trigger]
draft: false
---

###### 이전에 알아야 읽어두어야 할 글
[변수 Variable](/001_coding_start/001_coding_start-00003)

---

### 이 글을 읽기 위한 배경

- 앞서 설명한 변수의 이해
- 단순화(추상화) 하는 능력

### 얻게 되는 내용

- 함수의 이해와 사용

---

### 개요

앞서 배웠던 "계란후라이 요리 프로그램"을 다시 한번 꺼내 봅시다.  
아래와 같이 나타낼 수 있을 거 같아요.  

```r
음식 계란후라이 = 요리프로그램(계란)
```
종류는 "음식" 이고 요리프로그램(기계)를 계란(재료)를 넣어서 실행해보니, 뭔가 음식 비스므리한게 나왔는데 그걸 "계란후라이"라고 이름으로 가리킵니다.

이전에 만들어 놨던걸 더 작성하기 쉽게 간략화 시킵니다.
빠른 설명을 위해 짧은 프로그램으로 변화 시켜 봅시다.

---

### 함수라는 형태의 탄생

**[ 계란 후라이 요리 프로그램 : 짧은 버전 ]**

&nbsp;&nbsp;&nbsp;&nbsp;과정 - 1. 요리를 시작합니다.  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 2. 프라이팬을 가스렌지로 데웁니다.  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 3. 식용유를 프라이팬에 두릅니다.  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 4. 달걀을 깨서 프라이팬에 넣습니다.  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 5. 요리 완료.  

요리를 시작과 종료는 프로그램의 시작과 종료를 뜻 합니다. 간단한 기호로 바꿉시다.  
- 프로그램의 시작 : {
- 프로그램의 종료 : }

그리고 나머지 과정들을 바라보는 시야를 바꿔봅니다.  
"프라이팬을 가스렌지로 데우는" 과정은 간단해 보이지만 이 또한 많은 세부 과정들을 내포합니다.  

**[ 세부과정 : 프라이팬을 가스렌지로 데우기 ]**

&nbsp;&nbsp;&nbsp;&nbsp;과정 - 1. { (세부과정의 시작)  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 2. 가스렌지를 켭니다  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 3. 가스렌지를 약으로 조정합니다.  
&nbsp;&nbsp;&nbsp;&nbsp;과정 - 4. } (세부과정의 종료)  

결국 이것도 작은 프로그램이고, 작은 프로그램들이 모여서 "계란 후라이 프로그램"을 완성하는 것이죠.
이렇게 표현될 수 있습니다.  

**[ 계란후라이 소스코드 ]**  
```r
{  
    가스렌지로 데워라(프라이팬)  
    프라이팬에 넣어라(식용유)  
    프라이팬에 넣어라(달걀)  
}  
```

점점 간단해지는 거 같습니다.  
아쉽게도 소스코드는 영어로 작성하셔야 합니다.  

**[ 계란후라이 소스코드 ]**  
```r
{  
    boilByGas(fri-pan)  
    putIntoFriPan(oil)  
    putIntoFriPan(egg)  
}  
```

소스코드는 강력한 변수의 기능이 있습니다. 필수요건이죠.  
그렇다면 이 프로그램에도 이름을 지어서 가리킬 수 있을 거 같아요.  

**[ 계란후라이 소스코드 : 이름 짓기 : CookingFriEgg ]**  
```r
Program CookingFriEgg <- {  
    boilByGas(fri-pan)  
    putIntoFriPan(oil)  
    putIntoFriPan(egg)  
}
```
여기서 프로그램(Program) 은 과정들의 묶음이고 각 과정도 어찌보면 미니 프로그램이라고 볼 수 있습니다. 즉 과정 = 프로그램 = 미니 프로그램 은 하나의 프로그램 종류(type) 이군요.  

이걸 우리는 이제 함수(Function) 또는 메쏘드(Method)라 부르기로 합니다.

> Method  
> 1. [명사] 방법 (→direct method)
> 2. [명사] 체계성

 [출처: [메소드; 네이버사전](https://dict.naver.com/search.dict?dicQuery=%EB%A9%94%EC%86%8C%EB%93%9C&query=%EB%A9%94%EC%86%8C%EB%93%9C&target=dic&ie=utf8&query_utf=&isOnlyViewEE=)]

> Function  
> 1. [명사] (사람사물의) 기능
> 2. [명사] 행사, 의식
> 3. [동사] (제대로) 기능하다[작용하다] (=operate)

 [출처: [function; 네이버사전](https://dict.naver.com/search.dict?dicQuery=function&query=function&target=dic&ie=utf8&query_utf=&isOnlyViewEE=)]

바꿔봅시다.

```r
function CookingFriEgg <- {  
    boilByGas(fri-pan)
    ...
}
```

어차피 저 function 의 시작({ 표시)과 끝(} 표시)는 CookingFriEgg 의 이름과 동일시 되는 것처럼 보입니다. 그냥 합쳐주면 어떨까요?

```r
function CookingFriEgg {  
    boilByGas(fri-pan)
    ...
}
```

흠.. 여기서 우리가 빠진게 있습니다.  
처음 요리 프로그램의 요소 중 "준비물" 이 빠져 있네요.  
그리고 준비물의 자리는 맨 끝이었습니다. 그러니까 끝에 넣어봅시다.  

```r
# 준비물이 빠져있다 괄호 "(~)" 를 넣자.
음식 계란후라이 = 요리프로그램(계란)

# 준비물이 들어간 함수의 형태
function CookingFriEgg {  
    boilByGas(fri-pan)
    ...
}(egg)
```

아 뭔가 아쉽습니다. 함수의 작업이 많아져서 줄(세부작업..등)이 길어지면,
준비물이 안 보일 거 같습니다. 그리고 준비물이란건 프로그램(함수)을 시작하기 전에 준비되어야 하니까 느낌상 앞에 있어야 할거 같아요. 또 원래 함수이름 뒤에 있었으니 뒤쪽에 넣으면 예쁠거 같습니다.

```r
# 준비물이 들어간 함수의 형태, 예쁘게
function CookingFriEgg (egg) {  
    boilByGas(fri-pan)
    ...
}
```

이 정도면 매우 훌륭해 보입니다. ^^  
준비물도 결국에는 변수입니다. 이름을 지은 것 뿐이죠.  
그리고 이름은 우리 마음대로 지을 수 있으니, 새로운 이름도 지을 수 있습니다.  
거기에 어떤 종류인지도 궁금합니다. 종류도 넣어보죠

```r
# 준비물도 결국에는 우리 마음대로 이름을 지을 수 있어요.
function CookingFriEgg (달걀 prettyEgg ) {  
    boilByGas(fri-pan)
    ...
}
```

이제 그럴듯한 완성을 해봅시다. 빠진 준비물도 있었구요.  
혼란스러울까봐 한글로 먼저 다 적어봅시다.  
몇가지 좀 수정하구요.

**[ 계란후라이 소스코드 : 완성 ]**  
```r
# 한글판 
함수 계란후라이요리 (식재료 날달걀, 요리도구 프라이팬, 식재료 식용유){  
    가스랜지로 데워라(프라이팬)  
    프라이팬에 넣어라(식용유)  
    프라이팬에 넣어라(날달걀)  
}
# 영문판 
function CookingFriEgg ( Material pureEgg, CookingTool friPan, Material oil ){
    boilByGas(friPan)  
    putIntoFriPan(oil)  
    putIntoFriPan(pureEgg)  
}
```

우와, 이렇게 결국에는 우리가 흔히 보는 프로그래밍 언어의 함수의 모습입니다.  
물론 완벽하지는 않지만요.  

계란후라이프로그램(이하 : 후라이함수)은 여러 세부 과정들로 이루어져 있고  
세부 과정도 하나의 과정이니까 함수라고 부를 수 있습니다.
그럼 세부 과정이 어떻게 되는지 알려줘야 우리 파더기(컴퓨터, 갑작스런 등장!)가 알아듣지 않을까요?  
알아서 하는 법이 없으니까요.

후라이 요리하는 법은 알겠는데, 세부과정 boilByGas<가스렌지로 데워라>는 어떻게 하는지 모를테니까요.

**[ 계란후라이 소스코드 : 세부과정도 얘기해줘 ]** 
```r
# 후라이 함수
function CookingFriEgg ( Material pureEgg, CookingTool friPan, Material oil ){
    boilByGas(friPan)  
    putIntoFriPan(oil)  
    putIntoFriPan(pureEgg)  
}

# 세부과정 boilByGas <가스렌지로 데워라>
function boilByGas ( CookingTool myFriPan ){
    turnOnGas(); # 준비물이 없다고 하죠, 아 귀찮네요.
    tuneGas("weak"); # 강,중,약 중 약 으로 합시다.
}

# 세부과정 putIntoFriPan <프라이팬에 넣어라>
function putIntoFriPan ( Material something ){
    pureIntoPan(something); # 그 정체모를 식재료를 프라이팬에 붓습니다.
}
```

재료들의 이름이 계속 달라지는게 보이나요?  
왜 그럴까요? 각 함수(과정)에서는 정해진대로 자기 할일만 하면 됩니다.  
준비물이 A,B,C,... 가 들어오면 그걸 가지고 정해진 수순대로 진행하기만 하면 되죠.  
그 내용물(어떠한 존재?)이 뭔지는 "아 모르겠고~" 그걸 가지고 "어떻게 해"라는 것만 적혀 있으니 자연스러운 거라고도 볼 수 있습니다.

어렵나요? 다시 한번 설명해보죠.

1. function CookingFriEgg( ..., Material pureEgg ) : 이 프로그램 바깥에서 준비물이 왔습니다. 그걸 우리는 pureEgg 라고 부르기로 했어요. 그리고 그걸 가지고 무엇을 하든 함수 내부에서 정해진대로 움직이기만 하면 됩니다.

2. putIntoFriPan(pureEgg) : 우리가 pureEgg 라고 이름지은 존재를 putIntoFriPan 함수에다가 집어넣어 버립니다. 안에서 어떻게 할지는 잘 모르겠지만, 이름으로 봐서는 프라이팬에다가 집어넣을 거 같아요.

3. function putIntoFriPan( Material something ) : 이 프로그램 바깥에서 뭔가 준비물이 왔는데요. 우리는 매우 귀찮으니 "무엇" 이라고 이름을 짓습니다. 이 '무엇'을 가지고 어떻게 하든 내부에 정해진대로만 할거에요. 하필이면 이때는 "무엇"이 "바깥에서는 pureEgg" 라고 불렀을 뿐이에요. 하지만 바깥 사정까지 신경쓰고 싶지 않아요.

이 정도면 함수의 형태를 만들어봤고 아주 조금은 감이 오기 시작할거에요.  
하지만 우리는 "계란 후라이"를 만들지는 못했어요.  
왜냐구요? 계획만 세웠으니까요. (새해 계획은 세웠으나 실행해본 적은 없는 것처럼요.)

---

### 함수의 실행 (Execute, Call)

여기서 우리는 "계란 후라이"를 실제로 얻기 위해 이 함수를 작동시켜야 합니다.  
이것을 우리는 함수를 "실행(Execute)" 한다 또는 호출(Call) 한다라고 합니다.  

```r

# 후라이 함수 < 하지만 이건 계획일 뿐 >
function CookingFriEgg ( Material pureEgg, CookingTool friPan, Material oil ){
    ....
}

# 함수를 실행해서 "후라이"를 얻자. 이름이 없는 프로그램의 시작이다.
call {
    # 마켓에서 "egg"라고 글자가 적혀 있는걸 사옵니다. 그걸 "pEgg" 라고 이름으로 가리킵니다.
    Material pEgg <- buyFromMarket("egg")  
    # 친구한테 "테팔"이라고 글자가 프라이팬을 뺏어옵니다. 그걸 "fPan" 이름으로 합시다.
    CookingTool fPan <- getFromFriend("테팔")
    # 창고에서 "식용유"라고 적혀있는거 가져와서 "oil" 이라고 이름을 지읍시다.  
    Material oil <- getFromStorage("식용유") 

    # 우리가 작성해 놓은 계획(함수)에 준비물을 넣어서 실행(또는 호출) 합니다.
    # 그럼 실행하고 나면, "계란 후라이"를 얻게 되는데 그걸 우리는 "friedEgg" 라고 부르기로 합시다.
    Food friedEgg <- call CookingFriEgg( pEgg, fPan, oil )
}
```

"call {" 프로그램의 시작이 눈에 띕니다.  
계획은 세웠지만 언제 실행할지 모르잖아요. 그럼 이 "계란 후라이 함수를 실행하라"라는 계획은 도대체 언제 "실행" 하는 걸까요?
결국 이 계획을 "이 부분에서 지금 당장해" 라는 것도 필요합니다. 그걸 표현하기 위해 call (이름이 없어 하지만 이것도 계획){ ... } 를 호출해 버린 겁니다.  

그래야 "게란 후라이"를 얻으낼 수 있죠.
그 언젠가는 계획(함수)를 실행해야만 결과를 얻는다는 뜻입니다.  

아 글자가 너무 많아 귀찮아졌어요. 줄일 수 있으면 좋겠습니다.

```r

# 후라이 함수 < 하지만 이건 계획일 뿐 >
function CookingFriEgg ( Material pureEgg, CookingTool friPan, Material oil ){
    ....
}

# call 하고 {, } 이 없어져도 되지 않을까요? 
# 어차피 시작(앞의 함수와 구분이 되니)과 끝(이 계획을 작성한 종이의 끝)이 보이는데 말이지요.

....
# 이걸 줄이면...
Food friedEgg <- call CookingFriEgg( pEgg, fPan, oil )
# 좀 더 간단하게...
Food friedEgg <- CookingFriEgg( pEgg, fPan, oil )

# 이 계획(문서, 종이)의 끝 부분, 더 이상 작성할 공간이 없다.
```

실행이나 호출은 함수의 이름만 언급하고, 준비물만 넣어주면 땡. 이라고 생각할 수 있고,  
다른 함수들은 { 로 시작해서 } 끝나도록 다 작성해 놨으니,  
어디서부터 어디까지가 "계획(함수)"고 어디서 부터가 "함수"가 아닌 곳을 구분이 됩니다.  
그러니 다른 함수의 영역만 간섭하지 않는다면 "실행"의 영역이라 봐도 좋은 것입니다.

```r

function 초록색공_함수(){ # 초록색공_함수의 시작
    # 이 함수는 초록색 공을 만들어 줄 것이다.
    ...
} # 초록색공_함수의 끝

# 실행의 영역 : 여기부터 ----------------------------
# function 으로 시작하지 않으니 함수는 아니다. 구분 가능.

# 초록색공_함수 실행 전.
Ball greenBall <- 초록색공_함수()
# 초록색공_함수 실행 후. 무언가를 얻었고 그걸 우린 "greenBall" 이라고 이름짓자.

# 이 쯤에는 ----------------------------
# "greenBall" 만 얻은 상태다, "muJiGae" 라는 이름이 아래에 보이지만 
# 우리는 "위"에서"아래"로 진행하니 아직 이 아래쪽의 일은 "모른다"

# 실행의 영역 : 여기까지 ----------------------------

# 다시 function 단어가 보이니 함수의 영역이 시작되었다.
function 무지개_함수(){ # 무지개_함수의 시작
    # 무지개 생산.
} # 무지개_함수의 끝

# 무지개_함수 실행 전.
Light muJiGae <- 무지개_함수()
# 무지개_함수 실행 후. 무언가를 얻었고 그걸 우린 "muJiGae" 이라고 이름짓자.

# 이 쯤에는 ----------------------------
# "greenBall" 과 "muJiGae" 를 얻은 상태다!

```

그럼 이런 경우는 어떻게 될까요?

```r

function 초록색공_함수(){ ... }

Ball greenBall <- 초록색공_함수()
Light muJiGae <- 무지개_함수() # 이래도 될까요?

function 무지개_함수(){ ... }
```

우리 파더기(컴퓨터)는 단순합니다. <u>위에서 아래</u>로 밖에 읽지 못하고, <u>읽은 것만 기억</u>할 수 있어요.  
"무지개_함수" 가 알려주지 못한 상태에서 호출을 시도한다면 <u>알지 못하거나 처음 본</u> 함수이기 때문에 "아 몰라." 라고 말하면서 하던 일을 중단할 수 밖에 없어요.

--- 

#### 중간 정리

프로그램은 결국 함수나 메쏘드로 부를 수도 있고, 세부 작업도 결국 함수라고 부를 수 있습니다.  
그리고 함수를 작성한다는 건 "계획"을 만든 것이고 이 "계획"을 실행하는 것 또한 그 함수를 작성하고 나서야 가능하다는 것입니다.

**[ 가능한 시나리오 1 ]**
1. A 라는 계획을 만듬.
2. B 라는 계획을 만듬.
3. A 라는 계획을 실행 또는 호출해.
4. B 라는 계획을 실행 또는 호출해.

**[ 가능한 시나리오 2 ]**
1. A 라는 계획을 만듬.
2. A 라는 계획을 실행 또는 호출해.
3. B 라는 계획을 만듬.
4. B 라는 계획을 실행 또는 호출해.

**[ 불가능한 시나리오 : 계획을 실행하다가 중단된다 ]**
1. A 라는 계획을 만듬.
2. B 라는 계획을 실행 또는 호출해. < <u>B 계획은 아직 본적이 없는걸?</u> >, **아 몰라 중단!!**
3. B 라는 계획을 만듬.
4. A 라는 계획을 실행 또는 호출해. < A 계획은 위(1번)에 있었으니까 할 수 있어. >

여기서 우리는 의문을 또 하나 가지게 됩니다.  
그럼 이 "최종" 계획은 누가, 언제 하는 거지? 라는 의문입니다.

---

#### 스코프; Scope

여담으로 스코프라는 단어를 볼때가 있는데, 아직은(?) 별게 아닙니다.  
"시작과 끝"이라는 이 긴 단어를 간결하게 표현하고 싶을 때 이 단어를 쓰게 됩니다.  
함수의 스코프는 function 함수이름(){ <-- 여기부터 ... 여기까지 --> } 가 되겠죠.
나중에 이에 관해 이야기를 할 때가 올 것입니다.

> Scope  
> 1. [명사] [U] (지력·연구·활동 등의) 범위, 영역; (정신적) 시야
> 2. [명사] 여지(space), 기회, 배출구 ((for))
> 3. [명사] (공간의) 넓이, 길이; 지역, 지구

 [출처: [Scope; 네이버사전](https://dict.naver.com/search.dict?dicQuery=scope&query=scope&target=dic&ie=utf8&query_utf=&isOnlyViewEE=)]

---

#### 함수의 중단? 종료; return

함수란건 결국 뭔가를 순차적으로 실행하는 역할을 합니다.  
그럼 중간에 하기 싫거나 하지 말아야 할 경우가 있을 겁니다.  
예를 들어,  
계란 후라이 요리를 하는 중에 프라이팬까지 다 데웠습니다.  

"아 이런... 계란이 상했습니다."  

그럼 여러분은 요리를 계속 해야 할까요? 아니면 중단해야 할까요?
계획을 진행하다 중단한다는 의미는  
<u>중단하는 과정 이후의 다음 과정들은 진행하지 않는다!</u> 라는 걸 의미할 겁니다.

즉 특정 상황(조건)이 된다면, 계획을 중단해! 라는 <b>"중단 계획"</b>도 세워야 한다는 거죠.
그 문장은 각 언어마다 여러가지로 쓰일 수 있습니다.  

- Return
- Exit
- Stop

```r
function CookingFriEgg ( Material pureEgg, CookingTool friPan, Material oil ){
    boilByGas(friPan)  
    putIntoFriPan(oil)  
    # 이 쯤에서 계란을 넣기전에 확인을 해 볼겁니다.
    if( pureEgg 가 상했니? ){
        # 응 상했다면 이 영역(스코프) if {...} 을 진행시킵니다.
        # 상하지 않았다면 이 영역은 무시하고 실행하지 않습니다.
        return; # 이 함수는 더 이상 실행하면 안돼. 이 밑에 계획있던건 하지 마!
    }
    putIntoFriPan(pureEgg)  # 계란이 상했는지 윗줄에서 판단 후에 상했다면 이 계획은 무시.
    waitUntil()             # 계란이 상했는지 윗줄에서 판단 후에 상했다면 이 계획은 무시.
    ... # 이 아래로 주~욱 전부 무시.
}
```


--- 

#### 호출자; Executor 의 존재

우리는 프로그래머로서 열심히 계획을 다 작성했어요.  
근데 풀리지 않는 의문은 도대체 이 장대하고 거대한 "계란 후라이 요리" 함수는 누가 실행해주는 걸까요?  

프로그래머가 실행할까요? 그럴거면 계획 작성하지 말고 직접 해먹으면 되겠지요.  
그저 우리는 계획을 만들었으니 그 <b>누군가</b>가 계란후라이를 가져다주길 기다려야 하는 것입니다.
언제요? 우리가 원하는 시점에요.

**[프로그램을 실행하는데 필요한 조건]**
1. 프로그래머가 작성한 소스코드 (계획)
2. 계획을 실행시켜줘야 할 그 무엇 (호출자, Executor)
3. 호출자에게 명령을 내리는 때(시점, 계획 진행시켜)

![호출을 명령](/images/001_coding_start/001_coding_start-000004/executor.jpeg)
###### [호출자에게 명령을] 계획이 나이스 하군. 진행시켜.

> Executor  
> 1. [명사][전문 용어] 유언 집행자

 [출처: [Executor; 네이버사전](https://dict.naver.com/search.dict?dicQuery=Executor&query=Executor&target=dic&ie=utf8&query_utf=&isOnlyViewEE=)]

말 그대로 호출자(Caller) 또는 실행자 (Executor)는 어떤 명령이나 계획을 집행하는 사람이라는 뜻이에요.  
그러니까 프로그래머가 직접 실행하는게 아니라는 말씀.  

프로그래머는 실행자에게 "나의 장대한 계획"을 진행시켜라 라고 명령을 내리는 존재입니다.  
언제요? 계란 후라이 먹고 싶을 때요.

Executor 는 컴퓨터 세계에 존재하고, 그는 우리가 시킬때까지 "대기"하고 있다고만 생각하면 됩니다. 그리고 프로그래머는 그 Executor 에게 소스코드를 전달하면서 이걸 진행시켜 라고 얘기하고 나서 그 함수(계획)가 완료될때가지 기다리고 나면, 우리는 결과("계란후라이")를 얻을 수 있습니다.

**[ 프로그램이 작동하는 과정 ]**
1. 프로그래머가 소스코드를 작성 : 계획 작성
2. 프로그래머가 실행자에게 소스코드를 전달 : 계획 전달
3. 프로그래머가 실행자에게 "진행시켜" 라고 명령 전달 : 계획 진행 시작
4. 프로그래머는 기다린다. : 계획 진행 중.
5. 프로그래머는 기다린다. : 실행자가 계획이 완료되었다고 얘기하기 전까지.
6. 프로그래머는 결과를 얻는다 : 실행자가 다 되었다며 결과를 프로그래머에게 준다.

여기서 새롭게 등장 "트리거(Trigger)" 가 등장합니다. 3번 단계를 얘기하는 데요.

> Trigger  
> 1. [명사] (총의) 방아쇠
> 2. [명사] (반응사건을 유발한) 계기[도화선]
> 3. [동사] 촉발시키다 (=set off)
> 4. [동사] (장치를) 작동시키다 (=set off)

 [출처: [trigger; 네이버사전](https://dict.naver.com/search.dict?dicQuery=trigger&query=trigger&target=dic&ie=utf8&query_utf=&isOnlyViewEE=)]

말 그대로 계획을 "진행시켜!"라고 하는 행위나 할 수 있는 사람, 물건 아니면 또 다른 함수를 트리거라고 부릅니다.
가끔씩 보게 되는 언어이니 짤막하게 언급하고 지나갑니다.

각 언어의 호출자에게 "트리거"를 하는 코드를 보고 갑시다.
```r
## Java : "java" 라는 실행자에게 우리 프로그램 "CookingFriEggProgram" 을 전달하면서 트리거를 합니다.
java -jar CookingFriEggProgram.jar
## Python : "python" 이라는 실행자에게 마찬가지로요.
python CookingFriEggProgram.py
## Go-Lang : 운영체제(Window 나 MacOS) 에 호출자가 숨어 있어요. 굳이 언급안해도 됩니다.
CookingFriEggProgram.exe
```

그럼 우리 일상생활에서 트리거는 어떤게 있을까요?

**[일상 생활에서의 트리거]**
- 스마트폰에서 카카오톡 앱 아이콘을 "터치" 한다.
- 윈도우 PC 에서 카카오톡 앱 아이콘을 마우스로 "더블 클릭" 한다.
- 스마트폰을 켜고 싶을 때, 전원버튼을 "꾹 누른다".
- 말 잘 안듣는 아이가 있을 때, 잔소리를 "시작"한다.

---

#### Executor 는 어떻게 함수를 시작할까?

여기서 소스코드를 조금이라도 작성해 본 사람은 궁금증을 가질 수 있습니다.  
나의 소스코드를 실행하라고 요청했는데 Executor 는 도대체 내 계획이 어디서부터 시작되는지를 알까? 입니다.  

이건 각 언어를 만들어낸 사람의 약속으로 정해져 있다라고 얘기할 수 있습니다.
여러분이 작성한 소스코드가 수십개의 파일이고, 수천개의 함수로 가득차 있다고 합시다.  

당연히 우리 Executor 도 멍텅구리입니다. 하나부터 열까지 다 알려줘야 해요.  
프로그래머와 언어를 만들어내신 분이 힘을 합쳐 Executor 에게 "여기가 시작"점이야 라고 알려주기만 하면 됩니다.

**[ Executor 가 소스코드를 실행하는 과정 ]**
1. 프로그래머가 소스코드 작성완료
2. 실행자에게 소스코드 실행 명령 내림. <트리거>
3. 프로그래밍 언어 마다 <U>정해진</U> 시작점이 소스코드에 있는지 찾음.
4. 찾으면 그곳 부터 진행시킴
5. 못 찾으면 "못 찾겠다 꾀고리"를 시전 후, 실행하지 않고 하던일을 그만둠.

**[ JAVA : "정해진 시작점", 여러분이 찾아보세요. ]**
```java
public class CookingFriEggProgram 
{ 
    // 어라? 위치가 위인데, 괜찮을까? 왜 괜찮은지 여러분이 판단 해보세요.
    static void CookingFriEgg( Material pureEgg, CookingTool friPan, Material oil ){
        boilByGas(friPan);      // 이 함수는 다른 곳 어딘가에 또 있다고 하자.
        putIntoFriPan(oil); 
        putIntoFriPan(pureEgg);  
    }

    // 함수들은 준비되었다.
    static void buyFromMarket(...){
        // ...
    }

    public static void main(String[] args) { 
        // 마켓에서 "egg"라고 글자가 적혀 있는걸 사옵니다. 그걸 "pEgg" 라고 이름으로 가리킵니다.
        Material pEgg = buyFromMarket("egg");
        // 친구한테 "테팔"이라고 글자가 프라이팬을 뺏어옵니다. 그걸 "fPan" 이름으로 합시다.
        CookingTool fPan = getFromFriend("테팔");
        // 창고에서 "식용유"라고 적혀있는거 가져와서 "oil" 이라고 이름을 지읍시다.  
        Material oil = getFromStorage("식용유");

        // 우리가 작성해 놓은 계획(함수)에 준비물을 넣어서 실행(또는 호출) 합니다.
        // 그럼 실행하고 나면, "계란 후라이"를 얻게 되는데 그걸 우리는 "friedEgg" 라고 부르기로 합시다.
        Food friedEgg = CookingFriEgg( pEgg, fPan, oil );
    }

    // 어라? 위치가 아래인데, 괜찮을까? 왜 괜찮은지 여러분이 판단 해보세요.
    static void getFromFriend(...){
        // ...
    }

    static void getFromStorage(...){
        // ...
    }

}
```

**[ C : "정해진 시작점", 여러분이 찾아보세요. 문법은 약간 틀릴 수 있어요 ]**
```c
#include <stdio.h>
int main (int argc, char *argv[]) {
    int friedEgg = CookingFriEgg(...);
    return 0;
}
void buyFromMarket(...){
    // ...
}
void getFromFriend(...){
    // ...
}
void getFromStorage(...){
    // ...
}
int CookingFriEgg( char* pureEgg, char* friPan, char* oil ){
    ...  
}
```

**[ Python : "정해진 시작점", 여러분이 찾아보세요. 문법은 약간 틀릴 수 있어요 ]**
```python

def CookingFriEgg(...):
	# ...
    # ...

def buyFromMarket(...):
	# ...

def getFromFriend(...):
	# ...

def getFromStorage(...):
	# ...
    # ...

friedEgg = CookingFriEgg(...);

```

---

#### 호출,호출,호출; Call,Call,Call

여기서 잠깐 우리 함수의 호출하는 법까지 알아봤는데 이런 모양도 생각해 볼 수 있어요.
```r
function returnApple(감 gam){
    # 감을 주면 사과를 내보내주마.
}
function returnGam(호두 hodu){
    # hodu를 주면 감을 내보내주마.
}
function returnHoney(사과 sagwa)){
    # sagwa를 주면 꿀을 내보내주마.
}
function returnTea(꿀 ggul)){
    # ggul을 주면 차를 내보내주마.
}

# 우리가 배운 함수 이용법
호두 h <- "호두라면 호두인것이다"
감 g <- returnGam(h)
사과 a <- returnApple(g)
차 c <- returnTea(a)

# "호두라면 호두인것이다" 에서 사과가지 한 줄로 표현할 수 있을까요?
차 c <- returnTea(returnApple(returnGam("호두라면 호두인것이다")))

# 이상한가요? 한번 생각해 보세요. 맞는지 틀리는지...
```

---

## 정리

우리는 함수의 모습을 만들어 보았고, 실제 프로그래밍 언어가 사용하는 함수의 모습에 근접할 수 있었어요. 
함수는 결국 계획의 다른 이름이었고, 계획은 세부 계획을 가지고 있듯이 함수는 다른 함수를 실행할 계획으로 구성된다는 것을 추측할 수 있었습니다.  

그리고 그 거대한 함수는 호출자(Executor) 에게 맡겨서 프로그래머가 트리거를 하고, 함수의 실행이 완료가 되고 나면 우리는 결과를 얻어낼 수 있습니다.

다음 과정에서는 "조건" 이라는 것과 "분기"라는 것에 대해 살펴봅시다.  
우리는 이 조건을 위해 함수를 공부했는지도 모릅니다.

###### 다음 주제로 이어지는 글

- [예정] IF,ELSE 조건, 분기의 서막

---