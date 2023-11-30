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
String input = "티본스테이크-1,초코케이크-2,제로콜라-2"
Arrays.stream(input.split(","))
  .map(order -> order.split("-")
  .collect(Collectors.toMap(menu -> menu[0],
    menu -> Integer.parseInt(menu[1]))); 
```
