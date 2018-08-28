---
layout: archive
title:  "Google Ai-TTS[Text To Speech] 사용 방법"
date:   2018-07-23 12:00:10
author: ks J
categories: GoogleServices
tags: GoogleServices,Ai,TextToSpeech
---

소개
<hr/>
모바일 개발 내에서 Voice를 이용한 검색을 하기 위해 Dialogflow를 분석중입니다. 

## DialogFlow란?
사용자가 말하는것에서 데이터를 추출해서 특정 키에 맞게 Response룰 돌려 주는 서비스 입니다. 
흔히 TTS라도 명칭하고, 자연어를 분리작업 하는 부분이 정말 잘 되어있습니다. 

<hr/>


<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_genral.png"  style="width: auto;"/>
① 설정 > General > Beta Features 에서 Client access token을 사용하여 Client작업을 실행하면 됩니다.<br/><br/>
①-① Client access totken   : Client개발시 Config에 적는 AccessToken Key Query를 전달 할때 사용한다.<br/><br/>
①-② Developer access token : Entity와 Intent를 관리하는데 사용한다.<br/><br/>


<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_entity_create.png"  style="width: auto;"/>
<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_entity_complete.png"  style="width: auto;"/>
② Entities > CREATE ENTITY 를 사용해서 KEY를 만들면 됩니다. <br/><br/>
②-① Entity Name 설정 <br/><br/>
- 이름 설정 : 엔티티 이름은 문자로 시작해야하며 A-Z, a-z, 0-9, _ (밑줄), - (대시) 만 포함 할 수 있습니다.<br/><br/>
- Define synonyms   동의어 정의 <br/>
- Allow automated expansion 자동 확장 허용<br/><br/>
②-② Entity Value - AOA를 적을때는 AOA(에이오에이) 한글 버전도 같이 적어줘야 한다.<br/><br/>

<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_entity_switch_raw_mode.png"  style="width: auto;"/>
②-③ ②-② 의 값을 분할해서 입력 하거나 [AOA, 에이오에이]라고 입력하면 된다. <br/>
그외 Switch to raw mode에 들어가서 JSON 또는 CSV 형식으로 입력하면 많은 양의 데이터를 삽입하기 편하다.<br/><br/>

사용자가 말하거나 입력한 데이터의 값을 ②-③에서 매칭후, ②-②키값을 response로 돌려준다고 생각하시면 됩니다. 

<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_intent_creating.png"  style="width: auto;"/>
③ Intents > CREATE INTENT <br/>
③-① Intent Name 설정<br/>
③-② Entities에서 만든 ENTITY KEY를 넣어주면 됩니다. 포커스를 두고  ↓ 키보드를 클릭하면 만들어둔 ENTITY KEY를 볼수 있습니다.<br/><br/>

<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_intent_training.png"  style="width: auto;"/>
③-③ Training phrases는 Intent의 학습을 올려주는 셋팅으로, 처음 Intent생성시 무조건 한개정도는 적고 테스트해봐야 적용 됩니다. <br/><br/>


<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_training_menu.png"  style="width: auto;"/>
④ Training <br/>
지금까지 Client에서 검색한 내용에 대해서 AI가 학습하는 이라고 생각하면 <br/>
좋을것 같다<br/><br/>


<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_history_matching.png"  style="width: auto;"/>
<img src="{{ site.baseurl }}/assets/dialogflw_resource/ppt_history_not_matching.png"  style="width: auto;"/>
⑤ History<br/>
Matching 또는 No Matching 된 내용을 확인해볼수 있다. <br/><br/>

~~~java

"Voice No Matching"
> "User phrase was not matched by any intent. Add the phrase to new / 
existing intent or create fallback intent to respond to unrecognized input."

~~~

#### 샘플
Android SDK [Sample](https://github.com/dialogflow/dialogflow-android-client)

__Github__{: style="color: #e26716"}
<img src="{{ site.baseurl }}/assets/dialogflw_resource/github_dialogflow_base.png"  style="width: auto;"/>

__Base/build.gradle__{: style="color: #e26716"}
<img src="{{ site.baseurl }}/assets/dialogflw_resource/github_dialogflow_build.png"  style="width: auto;"/>

~~~java
dependencies {
        classpath 'com.android.tools.build:gradle:2.3.3'
}
//gradle version: 2.3.3 으로 셋팅해야 한다. 
//자신의 Android Studio Gradle Version으로 읽어 들여지기 때문에, 수정하도록한다.
~~~

__apiAiSampleApp__{: style="color: #e26716"}
<img src="{{ site.baseurl }}/assets/dialogflw_resource/github_dialogflow_config.png"  style="width: auto;"/>

~~~java
    public static final String ACCESS_TOKEN = "{YOUR CLIENT ACCESS TOKEN}";
~~~
<hr/>
<hr/>
