# 자동차 경주

초간단 자동차 경주 게임을 구현한다.

## 과제 진행 요구사항

- 구현할 기능을 `READMD.md`에 정리한다.
- Git 커밋 단위는 기능 목록 단위로 한다.
    - Git 커밋은 [AngularJS Git Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)을
      기반으로 한다.

## 프로그래밍 요구 사항

### 요구 사항 1

- `Kotlin 1.9.24` 버전에서 실행 가능해야 한다.
- Kotlin 코드만을 사용해서 구현해야 한다.
- 프로그램의 실행 시작점은 `Application`의 `main()`이다.
- `build.gradle.kts` 파일은 변경할 수 없다. 제공된 라이브러리 이외의 외부 라이브러리는 사용하지 않아야 한다.
- 프로그램 종료 시 `System.exit()` 혹은 `exitProcess()`를 호출하지 않아야 한다.
- 프로그래밍 요구 사항에서 달리 명시하지 않는 한 `파일`, `패키지` 등의 이름을 바꾸거나 이동하지 않는다.
- [Kotlin Style Guide](https://kotlinlang.org/docs/coding-conventions.html)

### 요구 사항 2

- `indent depth`를 3이 넘지 않도록 한다. (2까지 가능)
- 메서드는 한 가지 일만 하도록 하여 최대한 작게 만든다.
- `JUnit 5`와 `AssertJ`를 이용하여 정리한 기능 목록이 정상적으로 작동하는지 테스트 코드를 작성하여 확인한다.

#### 라이브러리

- `camp.nextstep.edu.missionutils`에서 제공하는 `Randoms` 및 `Console` API를 사용하여 구현해야 한다.
    - Random 값 추출은 `camp.nextstep.edu.missionutils.Randoms`의 `pickNumberInRange()`를 사용한다.
    - 사용자가 입력하는 값은 `camp.nextstep.edu.missionutils.Console`의 `readLine()`을 활용한다.

## 구현할 기능 목록 및 요구 사항

#### 자동차 (Car)

자동차는 아래의 기능을 포함합니다.

- [데이터] 자동차 이름
    - 객체가 생성될 때 자동차 이름을 설정한다.
    - 자동차 이름은 5글자 이하여야 한다. 만약 이를 초과할 때 `IllegalArgumentException` 예외를 발생시킨다.
- [데이터] 자동차가 이동 한 거리
    - 기본값으로 0을 가진다.
- [함수] 거리를 1 늘린다.
    - 만약 오버플로우가 발생하면 사용자가 너무 큰 값을 입력하였음을 알리며 `IllegalArgumentException` 예외를 발생시킨다.

#### 게임 (RacingGame)

- [데이터] 리스트 형식의 자동차 객체들
    - 참여하는 자동차는 객체가 생성될 때 추가한다.
    - 이를 위해 생성자로 리스트 형식의 `자동차 이름들`을 받는다.
    - `getter`에 대해서만 허용하여 자동차 객체에 접근할 수 있습니다.
- [함수] 경기 1라운드를 진행
    - 자동차 별로 전진 여부를 결정한다.
    - `0 ~ 9` 중 랜덤한 값을 구하고, `4` 이상일 경우 전진한다.
- [함수] 현재 라운드를 기준으로 1등을 반환
    - 1등에 해당하는 자동차 객체들을 반환한다.

#### 입출력 (View)

- [함수] 사용자로부터 경주할 자동차 이름 요청, 입력 내용 반환
    - 안내 문구는 `경주할 자동차 이름을 입력하세요.(이름은 쉼표(,) 기준으로 구분)`이다.
    - 사용자의 입력을 `,`을 기준으로 구분하여 리스트 형식으로 반환한다.
- [함수] 사용자로부터 시도할 횟수 요청, 입력 내용 반환
    - 안내 문구는 `시도할 횟수는 몇 회인가요?`이다.
- [함수] `실행 결과` 문자열을 출력하는 메서드
- [함수] 라운드별 자동차가 전진한 거리를 출력
    - 자동차 이름과 거리가 모두 나타나야 한다.
    - 이동한 거리는 거리 1 거리당 `-`으로 출력한다.
    - `${자동차 이름} : ${이동한 거리}` 형식으로 출력한다.
- [함수] 최종 우승한 자동차의 이름 출력
    - 최종 우승한 자동차를 리스트로 받는다.
    - 자동차의 이름을 출력한다.
    - 우승자가 여러 명일 경우 `,`를 통해 구분한다.
    - `최종 우승자 : ${이름}` 또는 `최종 우승자 : ${이름}, ${이름}` 형식을 따른다.

#### 게임 로직 실행 (Application)

- [함수] 순차적으로 게임 진행
    - 사용자에게 자동차 이름을 요청한다.
    - `RacingGame` 객체를 생성한다.
    - 진행할 게임 횟수를 요청한다.
    - 게임 횟수만큼 라운드를 진행하고, 이동 거리를 출력한다.
    - 게임 결과를 출력한다.

## 실행 결과 예시

```
경주할 자동차 이름을 입력하세요.(이름은 쉼표(,) 기준으로 구분)
pobi,woni,jun
시도할 횟수는 몇 회인가요?
5

실행 결과
pobi : -
woni : 
jun : -

pobi : --
woni : -
jun : --

pobi : ---
woni : --
jun : ---

pobi : ----
woni : ---
jun : ----

pobi : -----
woni : ----
jun : -----

최종 우승자 : pobi, jun
```

## 순서도 다이어그램

![2주차 미션 순서도](image/Flowchart%20for%20Week%202.png)