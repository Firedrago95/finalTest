- 리스트 중복검사
```java
private static void validateDuplicates(List<Integer>numbers) throws IllegalArgumentException {
  if (numbers.stream().distinct().count() != size) {
    throw new IllegalArgumentException(MESSAGE);
  }
}
```

- 문자열 Map 변환
```java
public static Map<String, Integer> readOrder() throws IllegalArgumentException {
        System.out.println(ConsoleMessage.REQUEST_ORDER.message);
        String input = Console.readLine().trim();
        InputValidator.validateOrder(input);
        try { // 반드시 예외처리 해야한다. (중복된 키값 예외발생 처리)
            return Arrays.stream(input.split(","))
                .map(menu -> menu.split("-"))
                .collect(Collectors.toMap(menuInfo -> menuInfo[0],
                    menuInfo -> Integer.parseInt(menuInfo[1])));
        } catch (IllegalStateException e) { //IllegalStateException 발생
            throw new IllegalArgumentException(ExceptionMessage.INVALID_ORDER.getMessage());
        }
    }
```
- enum 이름 포함 찾기
```java
private boolean isContain(String menuName) {
  return Arrays.stream(values())
      .anyMatch(menu -> menu.equals(menuName);
}
```
