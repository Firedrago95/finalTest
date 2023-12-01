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
        validate/*도메인*/Form(input);
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
}

/* 테스트 코드 */
public class InputValidatorTest {

    @ParameterizedTest
    @ValueSource(strings = {"" /*, "a", "pasta-1", "제로콜라-하나"*/})
    @NullSource
    void 주문_예외발생_테스트(String input) {
        assertThatThrownBy(() -> InputValidator.validateOrder(input))
            .isInstanceOf(IllegalArgumentException.class);
    }

    @ParameterizedTest
    @ValueSource(strings = {/*"해산물파스타-1,제로콜라-1", "티본스테이크-2,제로콜라-1,해산물파스타-2"*/})
    void 주문_정상입력_테스트(String input) {
        assertDoesNotThrow(() -> InputValidator.validateOrder(input));
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

#### InputView 작성

- `ConsoleMessage` private enum 으로 출력메세지 관리
1. 입력메세지출력
2. 문자열 받아오기
3. 입력 유효성검사 (InputValidator)
4. 자료형 변환 후 리턴
```java
public class InputView {

    private enum ConsoleMessage {
        REQUEST_ORDER(/*출력 메세지는 문제에서 복붙하자*/);

        private final String message;

        ConsoleMessage(String message) {
            this.message = message;
        }
    }

    public static Map<String, Integer> readOrder() throws IllegalArgumentException {
        System.out.println(ConsoleMessage.REQUEST_ORDER.message);
        String input = Console.readLine().trim();
        InputValidator.validateOrder(input);
        return convertStringToMap(input);
    }
    // 문자열 -> Map<String, Integer> 형변환 (예외발생 주의)
    private static Map<String, Integer> convertStringToMap(String input) {
        try {
            return Arrays.stream(input.split(","))
                .map(menu -> menu.split("-"))
                .collect(Collectors.toMap(menuInfo -> menuInfo[0],
                    menuInfo -> Integer.parseInt(menuInfo[1])));
        } catch (IllegalStateException e) {
            throw new IllegalArgumentException(ExceptionMessage.INVALID_ORDER.getMessage());
        }
    }
```
