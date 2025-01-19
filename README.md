# 2D Nest-Hesit 둥지강탈
## 📖 목차
1. [프로젝트 소개](#프로젝트-소개)
2. [주요기능](#주요기능)
3. [개발기간](#개발기간)
4. [와이어프레임](#와이어프레임)
5. [프로젝트 파일 구조](#프로젝트-파일-구조)
6. [Trouble Shooting](#trouble-shooting)
7. [시연연상](#시연연상)
    
## 👨‍🏫 프로젝트 소개
- 게임 컨셉

**`몬스터를 모으는 수집형 요소`** + **`성장시킨 몬스터를 통해 던전 탐험`**

- 아트 컨셉

**`SD캐릭터`** : 2등신의 플레이어블 캐릭터

`초록,파랑` : 메인 몬스터인 파란색, 초록색 몬스터의 색을 전반적으로 사용

- 조작 컨셉

**`Top-Down`**: 위에서 아래를 바라보는 View로 2D게임의 경험을 느낄 수 있도록 함

**`던전` :** 인게임 던전에서 여러 몬스터들을 상대하고 알을 탈취하고 탈출구를 향해서 향하는 경험을 할 수 있다.

## 💜 주요기능
- 몬스터 시스템
  - FSM을 사용하여 몬스터의 상태를 관리
  - NavMesh를 이용하여 몬스터의 AI 시스템 구현 (공격, 추격, 플레이어를 따라오는 행동 등)
  - CSV에서 데이터를 불러와 스텟 데이터 적용하는 시스템
  - 몬스터의 공격모드 방어모드를 선택할 수 있는 시스템
  - 
- PoolManager
  - 이펙트, 스폰되는 몬스터들을 Pooling하여 재사용
  - 사운드 클립 오브젝트도 여러 소리가 동시에 발생하기 때문에 풀링해놓고 클립을 사용

- 보스 시스템
  - Behaviour Tree를 사용해 보스의 체력별로 다양한 패턴을 수행하고 랜덤하게 패턴을 사용하도록 구현

- FireBaseCrashHandler
  - FireBase를 붙혀 안드로이드를 타겟으로 빌드를하고 배포를하면서 Crash가 발생하는 곳을 분석 및 수정
  - 에디터의 StackTrace를 추적하면서 UnityCrash와 비교하기위해서 RealTimeDataBase에 ErrorStackTrace를 발송해 비교분석해보는 작업 수행


## ⏲️ 개발기간
- 2024.06.28 ~ 2024.07.28

## 개발하면서 고민을 많이 했던 부분
- BaseMonster 상속관련  
  PartnerMonster와 EnemyMonster는 대부분 같은 기능(컴포넌트)을 공유하지만 AI행동양식과 StateMachine의 상태전이가 다른 부분이 존재  
  (적은 추적이 끝나면 제자리로 돌아가지만, 아군 몬스터는 추적이 끝나면 플레이어를 따라다님)
  BaseMonster를 두 클래스 모두 상속받지만 AIHandler와 StateMachine은 공통된 부분은 Base를 통해 처리하고
  차이가 있는 부분은 Base를 상속받아 메서드 오버라이딩으로 동작을 다르게 구현
- 객체지향을 위한 설계  
  ICondition 인터페이스를 만들어 데이터(체력, 스태미나, 마나 등)가 변화할 때 실행되는 Modify()메서드와 OnModifyEvent Action을 구현
  ICondition을 상속받은 BaseCondition을 구현한 뒤, Player, Monster, Boss 등 Modify 메서드 오버라이딩을 통해 구현

  여러 Handler(컴포넌트)를 만들어 붙혀주는 방식으로 수정해야할 부분이 생긴다면 해당 클래스만 변경하고 나머지 클래스들에게 영향이 많이 가지 않게 설계
  
  
  

## 와이어프레임





## 프로젝트 파일 구조
 



## Trouble Shooting

## 최적화를 위해 노력했던 부분
- 컴포넌트 캐싱  
  GetGomponent()메서드는 비용이 많기 때문에 런타임중에 자주 실행되면 성능상 좋지 않다.
  Start Awake Init같은 초기화 할 때 미리 변수에 캐싱해놓고 최대한 재사용하면서 런타임에서 GetComponent를 자주 호출 하지 않도록 함
- 오브젝트 풀링  
  이펙트, 사운드, 몬스터 스폰 등 한번에 여러 오브젝트들이 나타나고 사라져야하는 구간에서 풀링을 사용하지 않으면 해당 프레임이 튀는 현상을 발견
- 쉐이더 문제기능](#주요기능)
3. [개발기간](#개발기간)
4. [와이어프레임](#와이어프레임)
5. [프로젝트 파일 구조](#프로젝트-파일-구조)
6. [Trouble Shooting](#trouble-shooting)
7. [시연연상](#시연연상)
    
## 👨‍🏫 프로젝트 소개
- 게임 컨셉

**`몬스터를 모으는 수집형 요소`** + **`성장시킨 몬스터를 통해 던전 탐험`**

- 아트 컨셉

**`SD캐릭터`** : 2등신의 플레이어블 캐릭터

`초록,파랑` : 메인 몬스터인 파란색, 초록색 몬스터의 색을 전반적으로 사용

- 조작 컨셉

**`Top-Down`**: 위에서 아래를 바라보는 View로 2D게임의 경험을 느낄 수 있도록 함

**`던전` :** 인게임 던전에서 여러 몬스터들을 상대하고 알을 탈취하고 탈출구를 향해서 향하는 경험을 할 수 있다.

## 💜 주요기능
- 몬스터 시스템
  - FSM을 사용하여 몬스터의 상태를 관리
  - NavMesh를 이용하여 몬스터의 AI 시스템 구현 (공격, 추격, 플레이어를 따라오는 행동 등)
  - CSV에서 데이터를 불러와 스텟 데이터 적용하는 시스템
  - 몬스터의 공격모드 방어모드를 선택할 수 있는 시스템
  - 
- PoolManager
  - 이펙트, 스폰되는 몬스터들을 Pooling하여 재사용
  - 사운드 클립 오브젝트도 여러 소리가 동시에 발생하기 때문에 풀링해놓고 클립을 사용

- 보스 시스템
  - Behaviour Tree를 사용해 보스의 체력별로 다양한 패턴을 수행하고 랜덤하게 패턴을 사용하도록 구현

- FireBaseCrashHandler
  - FireBase를 붙혀 안드로이드를 타겟으로 빌드를하고 배포를하면서 Crash가 발생하는 곳을 분석 및 수정
  - 에디터의 StackTrace를 추적하면서 UnityCrash와 비교하기위해서 RealTimeDataBase에 ErrorStackTrace를 발송해 비교분석해보는 작업 수행


## ⏲️ 개발기간
- 2024.06.28 ~ 2024.07.28

## 개발하면서 고민을 많이 했던 부분
- BaseMonster 상속관련  
  PartnerMonster와 EnemyMonster는 대부분 같은 기능(컴포넌트)을 공유하지만 AI행동양식과 StateMachine의 상태전이가 다른 부분이 존재  
  (적은 추적이 끝나면 제자리로 돌아가지만, 아군 몬스터는 추적이 끝나면 플레이어를 따라다님)
  BaseMonster를 두 클래스 모두 상속받지만 AIHandler와 StateMachine은 공통된 부분은 Base를 통해 처리하고
  차이가 있는 부분은 Base를 상속받아 메서드 오버라이딩으로 동작을 다르게 구현
- 객체지향을 위한 설계  
  ICondition 인터페이스를 만들어 데이터(체력, 스태미나, 마나 등)가 변화할 때 실행되는 Modify()메서드와 OnModifyEvent Action을 구현
  ICondition을 상속받은 BaseCondition을 구현한 뒤, Player, Monster, Boss 등 Modify 메서드 오버라이딩을 통해 구현

  여러 Handler(컴포넌트)를 만들어 붙혀주는 방식으로 수정해야할 부분이 생긴다면 해당 클래스만 변경하고 나머지 클래스들에게 영향이 많이 가지 않게 설계
  
  
  

## 와이어프레임





## 프로젝트 파일 구조
 



## Trouble Shooting

## 최적화를 위해 노력했던 부분
- 컴포넌트 캐싱  
  GetGomponent()메서드는 비용이 많기 때문에 런타임중에 자주 실행되면 성능상 좋지 않다.
  Start Awake Init같은 초기화 할 때 미리 변수에 캐싱해놓고 최대한 재사용하면서 런타임에서 GetComponent를 자주 호출 하지 않도록 함
- 오브젝트 풀링  
  이펙트, 사운드, 몬스터 스폰 등 한번에 여러 오브젝트들이 나타나고 사라져야하는 구간에서 풀링을 사용하지 않으면 해당 프레임이 튀는 현상을 발견
- 쉐이더 문제
- Canvas
  캔버스에 그려져있는 오브젝트가 변화되면 해당 캔버스의 전체를 다시 그리기 때문에
  UI_Scene이나, UI_Popup 등 여러 캔버스를 통해 관리하여 자주 변화하는 Canvas와 그렇지 않은 Canvas를 최대한 분리하려고 함
  
  


## 시연연상
