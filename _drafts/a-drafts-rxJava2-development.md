# Observable

소개
<hr/>
이 페이지는 rxJava 2 버전을기반으로 설명하며, Observable를 공부하기 위해 정리했습니다. 
<br/>
<br/>
<br/>

사용 설명
<hr/>


<strong>just</strong> - 단일


| rxjava 1.x | rxjava 2.x|    | 종류 | 리스트 | 
|:--------|:-------:|:-------:|:-------:|:-------:|
| Observable  | Observable  | | 기본 | just(),subscribe(),dispose(),create() | 
|----
|  x  | Maybe  |              | FromXXX() | fromArray, fromIterable, fromCallable,<br/> fromFuture, fromPublisher
 | 
|----
|  x  | Flowable  |           | ㅊlass| Single, Maybe, Subject, ConnectableObservable| 
|----
{: rules="groups"}

###### rxjava 1.x 과 rxjava 2.x 클래스 비교
<hr/>
<br/