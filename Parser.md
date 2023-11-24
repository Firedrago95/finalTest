- 문자열 -> int

```java
private static int convertStringToInt(String input) throws IllegalArgumentException {
    validateNullOrEmpty(input);
    validateNumber(input);
    return Integer.parseInt(input);
}

private static void validateNullOrEmpty(String input) throws IllegalArgumentException {
    if (string == null || input.equals("")) {
        throw new IllegalArgumentException("[ERROR] 값을 입력해주세요");
    }
}

private static void validateNumber(String input) throws IllegalArgumentException {
    if (!input.matches("\\d+")) {
        throw new IllegalArgumentException("[ERROR] 숫자를 입력해주세요");
    }
}
```

- 문자열 -> Map<String,Integer>

```java
private static Map<String, Integer> convertStringToMap(String input)throws IllegalArgumentException {
    try{
        return Arrays.stream(input.split(","))
            .map(menu->menu.split("-"))
            .collect(Collectors.toMap(
            menuInfo->menuInfo[0],
            menuInfo->Integer.parseInt(menuInfo[1])
            ));
    } catch(NumberFormatException|ArrayIndexOutOfBoundsException e){
        throw new IllegalArgumentException(INVALID_FORM_MESSAGE,e);
    }
}
```

- 문자열 -> List

```java

```
