- 빈 값 검사 

```java
private static void validateNullOrEmpty(String a) throws IllegalArgumentException {
    if (a == null || a.equals("")) {
        hrow new IllegalArgumentException(NULL_EMPTY_MESSAGE);
    }
}
```