### map 출력로직
- map에따라 다른 출력메세지일 경우, String으로 받는다.
- if문으로 분기 만든다.
```java
public static void printCount(Map<BallCount, Integer> count) {
  String result = getResult(count);
  System.out.println(result);
}

private static String getResult(Map<BallCount, Integer> count) {
  int strike = count.get(BallCount.STRIKE);
  int ball = count.get(BallCount.BALL);
  if (strike == 0 && ball == 0) {
      return ConsoleMessage.NOTHING.message;
  }
  if (strike == 0) {
      return ball + "볼";
  }
  if (ball == 0) {
      return strike + "스트라이크";
  }
  return ball + "볼 " + strike + "스트라이크";
}
```
- 0인 값을 빼고 싶을때
```java
private static void printDiscountList(Map<String, Integer> appliedDiscount) {
  for (Map.Entry<String, Integer> discount : appliedDiscount.entrySet()) {
    if (discount.getValue() != ZERO) {
      System.out.println(
        discount.getKey() + ": " + "-" + convertFormatted(discount.getValue())+ CURRENCY);
    }
  }
}
```
