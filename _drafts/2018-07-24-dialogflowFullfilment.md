---
layout: archive
title:  "DialogFlow 검색하는 방법"
date:   2018-07-24 12:00:10
author: ks J
categories: GoogleServices
tags: Dialogflow TTS Ai
---
소개
<hr/>
모바일 개발 내에서 Voice를 이용한 검색을 하기 위해 Dialogflow를 분석중입니다. 
Fullfilment와Webhook 사용법에 대해서 적었습니다.
<br/>

### SQLite + Dialogflow
~~~java
//Required 
@ ALBUM_ENT     - "앨범"        :"바람이 불었으면 좋겠어"
@ ARTIST_ENT    - "아티스트"    :"길구봉구"
@ GENRE_ENT     - "장르"        :"Ballad"
@ YEAR_ENT      - "년도"        :"2014" //2014.01.03
@ WRITER_ENT    - "작사"        :"이현승, 길구봉구"
@ COMPOSER_ENT  - "작곡"        :"이현승, 길구봉구"
@ SONG_ENT      - "타이틀-곡"   :"바람이 불었으면 좋겠어"
@ MONTH_ENT     - "월"          :"1월" //2014.01.03

//Option
@ NEGATIVE_ENT  - "OP1"         :"아닌, 하지않은, 하지않았던, 않은, 않았던"
@ IN_ENT        - "OP2"         :"속한, 참여한, 참가"

//Garbage
@ ACTION_ENT    - "빈값"        :"찾아줘, 해줘"
@ GARBAGE_ENT   - "빈값"        :"에, 중가"
@ KEYWORD_ENT   - "빈값"        :"노래"

~~~
<br>

### Dialogflow Web과 Android Sample Client의 Response는 왜 다를까??
<hr/>

~~~java
{
  "responseId": "-RANKEY-",
  "queryResult": {
    "queryText": "최신노래중에 길구봉구가 작사하지 않은 노래 찿아줘",
    "parameters": {
      "number": "",
      "WRITER_GROUP_ENT": {
        "WRITER_KEY_NAME_ENT": "작사",
        "ARTIST_ENT": "길구봉구"
      },
      "ARTIST_ENT1": "",
      "YEAR_ENT": "",
      "SONG_ENT": "",
      "ARTIST_ENT2": "이하이",
      "ARTIST_ENT": "",
      "MONTH_ENT": "",
      "ALBUM_ENT": "",
      "SING_CONTRACT1": "",
      "ACTION_ENT": "",
      "GARBAGE_ENT": [
        "중에"
      ],
      "NEGATIVE_ENT": "부정",
      "COMPOSER_GROUP_ENT": "",
      "KEYWORD_ENT": "최신곡",
      "SING_CONTRACT": "",
      "KEYWORD_ENT1": "노래",
      "GENRE_ENT": ""
    },
    "allRequiredParamsPresent": true,
    "fulfillmentText": "노래 찾았습니다.",
    "fulfillmentMessages": [
      {
        "text": {
          "text": [
            "노래 찾았습니다."
          ]
        }
      }
    ],
    "intent": {
      "name": "-RANKEY-",
      "displayName": "노래검색"
    },
    "intentDetectionConfidence": 1,
    "languageCode": "ko"
  }
}
---
JAVA RESPONSE

I: Resolved query: 최신노래중에 길구봉구가 작사한 노래 찾아줘
I: Action: Speech: 노래 찾았습니다. Intent id: 00000000-29b4-463f-9732-95ada2fbe98a Intent name: 노래검색
I: Parameters: {GARBAGE_ENT=["중에"], KEYWORD_ENT1="노래", KEYWORD_ENT="최신곡", ACTION_ENT="SEARCH"}
I: Index[: 0] GARBAGE_ENT: ["중에"]
I: Index[: 1] KEYWORD_ENT1: "노래"
I: Index[: 2] KEYWORD_ENT: "최신곡"
I: Index[: 3] ACTION_ENT: "SEARCH"

~~~
현재 안드로이드 샘플은 V1 api를 가져오고 있고, Dialogflow에선 V2beta api기반으로 화면에 노출됩니다. 
아직 많은 테스트를 해보지 못해서, 정확히 쓸수는 없지만 v1, v2의 버전사이에 Entity Option [Define synonyms(동의어 정의), Allow automated expansion(자동 확장 허용)]없는 기능에 대해서 결과값이 다른것 같습니다. 

현재로써는 nodeJS-v2버전으로 코딩을 하면 위 Json 형식의 결과값을 받아 볼수 있고, 차후에 더 재미난 
구현을 하기 위해선, 서버를 구축해서 해야하나 라는 고민을 하고 있습니다. 



<hr/>
[ OAuth2 ](https://developers.google.com/identity/sign-in/web/devconsole-project)


#### "Try it now" >"curl copy"하기
~~~java

curl 
-H "Content-Type: application/json; charset=utf-8"  
-H "Authorization: Bearer 00000000pwUnL3ygis94VJW4bYcooKAschNXZQ-iyBmc-AFE74g-XWl7r8azQbgHQ-FRWrzlnJ9oHnOBZNkFf1wqPpoIik1tVUrx5GYiC9FpVanyiWOYc_Vd_WSnE"  
-d "{\"queryInput\":{\"text\":{\"text\":\"김건모가 작사하고 첸이 작곡한 아이유 노래 찾아줘\",\"languageCode\":\"ko\"}},\"queryParams\":{\"timeZone\":\"Asia/Seoul\"}}" "https://dialogflow.googleapis.com/v2beta1/projects/ninanospeechai/agent/sessions/00000000-23b9-ea23-d1ea-81c2e1ff33b8:detectIntent"
---

~~~

## Node셋팅

#### [A.구글 클라우드쉘 사용](https://console.cloud.google.com/cloudshell/editor?fromcloudshell)
#### B.로컬 서버 셋팅 방법

데비안 계열(우분투)에서 일반 사용자 계정인 경우,
1. sudo apt-get install curl

~~~java
> Error
패키지 목록이나 상태 파일을 파싱할수 없거나 열수 없습니다. 
/var/lib/apt/lists/kr.archive.ubuntu.com_ubuntu_dists_trusty_universe_i18n_Translation-en

> 해결
cd /var/lib/apt/lists/
sudo mv "kr....-en" backup_"kr...-en" // 이름변경을 하고 Update를 시도 한다. 

sudo apt-get update
~~~
___________


2. node install  use Curl

~~~java
sudo apt-get install -y nodejs
sudo apt-get install npm

node -v
> /usr/sbin/node: 그런 파일이나 디렉터리가 없습니다

> Command : whereis node
>> /usr/bin/node 
>> /usr/bin/X11/node 
>> /usr/include/node 
>> /usr/share/man/man1/node.1.gz

>> sbin/은 시스템 관리를 위한 명령어 (root)
>> bin/은 기본적인 명령어 (일반사용자)

sudo node -v
> v8.11.4

npm -v
> 5.6.0
~~~

sbin/은 시스템 관리를 위한 명령어 (root)
bin/은 기본적인 명령어 (일반사용자)

<hr/> 

3. Dialogflow Node V2 [Sample](https://github.com/dialogflow/dialogflow-nodejs-client-v2)
4. Node모듈 셋팅
~~~java
sudo npm install --save dialogflow
~~~ 

5. 퀵스타트Js 실행
~~~java
cd sample/

sudo node quickstart.js
ERROR: Error: 
Unexpected error while acquiring application default 
credentials: Could not load the default credentials. 
Browse to https://developers.google.com/accounts/docs/application-default-credentials 
for more information.
    at GoogleAuth.<anonymous> (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:248:31)

    at step (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:47:23)

    at Object.next (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:28:53)

    at fulfilled (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:19:58)

    at <anonymous>
    at process._tickCallback (internal/process/next_tick.js:188:7)


(node:5578) UnhandledPromiseRejectionWarning: Error: 
Unexpected error while acquiring application default 
credentials: Could not load the default credentials. 
Browse to https://developers.google.com/accounts/docs/application-default-credentials 
for more information.
    at GoogleAuth.<anonymous> (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:248:31)

    at step (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:47:23)

    at Object.next (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:28:53)

    at fulfilled (/var/www/webNode/dialogflow-nodejs-client-v2/
    samples/node_modules/google-auth-library/build/src/auth/googleauth.js:19:58)

    at <anonymous>
    at process._tickCallback (internal/process/next_tick.js:188:7)

(node:5578) UnhandledPromiseRejectionWarning: 
Unhandled promise rejection. This error originated either by throwing inside of an async 
function without a catch block, or by rejecting a promise which was not handled with .catch(). (rejection id: 3)

(node:5578) [DEP0018] DeprecationWarning: 
Unhandled promise rejections are deprecated. In the future, promise rejections that are 
not handled will terminate the Node.js process with a non-zero exit code.

> sudo chmod 766 quickstart.js // 읽기전용을 해제한다.

//위 에러는 인증이 맞지 않아 나는 오류입니다. 
> vi quickstart.js
const projectId = '{your_project_id}';

> node quickstart.js

ERROR: { Error: 7 PERMISSION_DENIED: Dialogflow API has not been used in project 563584335869 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/dialogflow.googleapis.com/overview?project=563584335869 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.
~~~

curl -H "Content-Type: application/json; charset=utf-8"  -H "Authorization: 
Bearer ya29.c.EloOBrxIiTZLyvbC1jEvqBffUCmwodHQqPYPQgbmxkRAmami779oGweedKBFLbQ5re6vLYsTZnfJlfdmleWycTwWazL9KSoVCYwAW4Ldc7jeR2YkInNiaxXGQ_M"  
Bearer ya29.c.EloNBrpwUnL3ygis94VJW4bYcooKAschNXZQ-iyBmc-AFE74g-XWl7r8azQbgHQ-FRWrzlnJ9oHnOBZNkFf1wqPpoIik1tVUrx5GYiC9FpVanyiWOYc_Vd_WSnE

-d "{\"queryInput\":{\"text\":{\"text\":\"김건모가 작사하고 첸이 작곡한 아이유 노래 찾아줘\",\"languageCode\":\"ko\"}},\"queryParams\":{\"timeZone\":\"Asia/Seoul\"}}" "https://dialogflow.googleapis.com/v2beta1/projects/ninanospeechai/agent/sessions/384e0a2e-23b9-ea23-d1ea-81c2e1ff33b8:detectIntent"






