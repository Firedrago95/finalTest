- 리스트 중복검사
```java
private static void validateDuplicates(List<Integer>numbers) throws IllegalArgumentException {
  if (numbers.stream().distinct().count() != size) {
    throw new IllegalArgumentException(MESSAGE);
  }
}
```
