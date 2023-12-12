- 리스트 중복검사
```java
private static void validateDuplicates(List<Integer>numbers) throws IllegalArgumentException {
  if (numbers.stream().distinct().count() != size) {
    throw new IllegalArgumentException(MESSAGE);
  }
}
```

- 문자열 Map 변환 (IllegalStateException 처리 주의)
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
- list 와 list 같은 위치에 같은 값 찾기
```java
private int countStrike(List<Integer> computer, List<Integer>user) {
  return (int) IntStream.rangeClosed(0,2)
    .filter(index -> computer.get(index) == user.get(index))
    .count();
}
```
- list와 list 같은 숫자 포함되는 갯수 찾기
```java
private int countSameNumber(List<Integer> computer, List<Integer> user) {
  return (int) user.stream()
    .filter(numer -> computer.contains(number))
    .count();
}
```
