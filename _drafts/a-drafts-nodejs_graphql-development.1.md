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

_just_{: style="color: #e26716"} - 데이터를 차례로 발행하는 함수, Observable을 생성하고, 한개의 값을 넣을 수 있고, 같은 타입의 인자로 최대 10개 까지 처리가능하다. 
<br />

~~~ java
//코드
Observable.just(1,2,3).subscribe(System.out::println);
~~~


~~~ java
//결과
1
2
3
~~~
<br />
_subscribe_{: style="color: #e26716"} - 동작시키기 위해 준비해둔 observable을 실행할때 사용.  <br >

~~~ java
//원형
Disposeable subscribe()
...
~~~
인자가 없는 subscribe() onNext, onComplete 이벤트를 무시하고 onError이벤트가 발생했을때만 throw를 던지기때문에 Observable 코드를 테스트하거나 디버깅 할때 용이.

_dispose_{: style="color: #e26716"} - 데이터 발생을 해지 할때 사용. Observable과 구독자 관계를 끊을때 사용합니다. onComplete가 발생할때 dispose를 호출하기 때문에 따로 dispose를 호출할 필요가 없습니다.
<br >

~~~ java
//코드
Observable<String> ob = Observable.just("k","s","j")
Disposable d = ob.subscribe(
    v -> System.out.println("onNext : "+ v),
    err -> System.out.println("onError"),
    () -> System.out.println("onComplete")
);
System.out.println("T/F : "+d.isDisposed);
~~~

~~~ java
//결과
onNext : k
onNext : s
onNext : j
onComplete
T/F : true
~~~

_create_{: style="color: #e26716"} -  onNext, onComplete, onError를 개발자가 직접 호출해야 한다. 
직접 호출해야 하기 때문에, onError 또는 dispose, back pressure등도 고려해야 한다는걸 명심하자.
<br >

~~~ java
//코드
Observable<String> ob = Observable.create(
    (ObservableEmitter<String> em) -> {
    em.onNext("k");
    em.onNext("s");
    em.onNext("j");
    em.onComplete();
});

ob.subscribe(System.out::println);
~~~

~~~ java
//결과
k
s
j
~~~


__FromXXXX__{: style="color: #1b557a"} <br >
_fromArray_{: style="color: #e26716"} <br >
_fromIterable_{: style="color: #e26716"} <br >
_fromCallable_{: style="color: #e26716"} <br >
_fromFuture_{: style="color: #e26716"} <br >
_fromPublisher_{: style="color: #e26716"} <br >

__Class__{: style="color: #1b557a"} <br >
_Single_{: style="color: #e26716"} <br >
_Maybe_{: style="color: #e26716"} <br >
_Subject_{: style="color: #e26716"} <br >
_ConnectableObservable_{: style="color: #e26716"} <br >



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