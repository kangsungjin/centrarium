# Observable

소개
<hr/>
이 페이지는 rxJava 2 버전을기반으로 설명하며, Observable를 공부하기 위해 정리했습니다. 
<br/>
<br/>
<br/>

사용 설명
<hr/>

__기본__{: style="color: #1b557a"} <br >

_just_{: style="color: #e26716"} - 단일
_subscribe_{: style="color: #e26716"}
_dispose_{: style="color: #e26716"}
_create_{: style="color: #e26716"}

__FromXXXX__{: style="color: #1b557a"} <br >
_fromArray_{: style="color: #e26716"}
_fromIterable_{: style="color: #e26716"}
_fromCallable_{: style="color: #e26716"}
_fromFuture_{: style="color: #e26716"}
_fromPublisher_{: style="color: #e26716"}

__Class__{: style="color: #1b557a"} <br >
_Single_{: style="color: #e26716"}
_Maybe_{: style="color: #e26716"}
_Subject_{: style="color: #e26716"}
_ConnectableObservable_{: style="color: #e26716"}



| rxjava 1.x | rxjava 2.x|    | 종류 | 리스트 | 
|:--------|:-------:|:-------:|:-------:|:-------:|
| Observable  | Observable  | | 기본 | just(),subscribe(),dispose(),create() | 
|----
|  x  | Maybe  |              | FromXXX() | fromArray, fromIterable, fromCallable,<br/> fromFuture, fromPublisher
 | 
|----
|  x  | Flowable  |           | class| Single, Maybe, Subject, ConnectableObservable| 
|----
{: rules="groups"}

###### rxjava 1.x 과 rxjava 2.x 클래스 비교

<hr/>

구독자에게 전달 할때 사용하는 세가지 함수<br/>
_onNext_{: style="color: #e26716"} : 데이터 발행을 할때 사용<br/>
_onComplete_{: style="color: #e26716"} : 모든 데이터의 발행을 완료 했을때 발생하고, 이곳에서 dispose()가 실행됩니다. <br/>
_onError_{: style="color: #e26716"} : 에러가 생겼을때 호출되며, 에러가 생겼을경우는 onNext,onComplete를 호출하지 않기때문에 dispose()처를를 따로 해주어야합니다. 메모리누수를 방지하기 위해서 입니다.<br/>


<br/>