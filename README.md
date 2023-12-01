## 먼저

> 1. 깃허브: **Fork**하기 => **Clone**하기 (깃허브 desktop) => **Firedrago95 브랜치** 만들기 => **_initial commit 하고 확인_** 꼭!!! (PullRequest 보내지는지도!!)
> - Application, ApplicationTest 둘 다 돌아가는지 부터 확인
> 2. 설계에 공들이자, 계속 고치는 대공사보다 설계에 공들이는게 더 빠르다
> 3. 라이브러리는 알려준 고대로 쓰자! List<String>을 shuffle하라 했으면 그모양 그대로

## 순서

### START

### 기능 목록을 작성할 때

- 복잡한 문제라면 **플로우차트**를 그린다
- 어떤 클래스가 어떤 데이터를 담아야 하는지 **코드 짜기 _전에_ 생각한다!!!**
- 가능하면 출력해야 하는 내용을 **`view`에 복붙**하면서 작성하자

#### 패키지 나누기

- `controller` `model` `util` `view` 패키지 생성
- `util` 패키지 안에 `validator` 패키지 생성
- `util` 패키지 안에 `ExceptionMessage` enum 클래스 생성
- `InputValidator` 와 `도메인Validator` 클래스 생성
```java
public class InputValidator {
    private static final Pattern dateRegex = Pattern.compile(/*정규식*/);

    public static void validate/*도메인*/(String input) throws IllegalArgumentException {
        validateNullOrEmpty(input);
        validateDateForm(input);
    }

    private static void validate/*도메인*/Form(String input) throws IllegalArgumentException {
        if (!orderRegex.matcher(input).matches()) {
            throw new IllegalArgumentException(ExceptionMessage.에러메시지.getMessage());
        }
    }

    private static void validateNullOrEmpty(String input) throws IllegalArgumentException {
        if (input == null || input.equals("")) {
            throw new IllegalArgumentException(ExceptionMessage.NULL_OR_EMPTY.getMessage());
        }
    }
```
```java
public enum ExceptionMessage {
    /*예외 메세지 추가*/
    NULL_OR_EMPTY("[ERROR] 값을 입력해주세요");

    private final String message;

    ExceptionMessage(String message) {this.message = message;}

    public String getMessage() {
        return message;
    }
}

```

