- 문자열 -> Map<String,Integer>

```java
private static Map<String, Integer> convertStringToMap(String input) throws IllegalArgumentException {
    try {
        return Arrays.stream(input.split(","))
        .map(menu -> menu.split("-"))
        .collect(Collectors.toMap(
            menuInfo -> menuInfo[0],
            menuInfo -> Integer.parseInt(menuInfo[1])
        ));
    } catch (NumberFormatException | ArrayIndexOutOfBoundsException e) {
        throw new IllegalArgumentException(INVALID_FORM_MESSAGE, e);
    }
}
```

- 문자열 -> List

```java

```
