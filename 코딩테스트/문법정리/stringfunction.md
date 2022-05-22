# endsWith(String)

- 문자열에서 특정 문자열로 끝나는지를 확인할 수 있으며, 그 결과를 true 혹은 false 로 반환한다.

# String.valueOf(int i)

- 파라미터가 null이면 문자열 "null"을 만들어서 반환한다.
- toString() 대상 값이 null 이면 Null Point Exception을 발생시키고 Object에 담긴 값이 String이 아니어도 출력한다.

#  문자열 -> char[] , char[] -> 문자열

- 문자열 -> char[]: char[] answer = s.toCharArray()
- char[] -> 문자열: String.valueOf(answer)

# String.split("")

- 문자 단위로 끊어서 공백도 포함해서 String[]로 생성된다.

# String.join()

- join("추가할 문자", "대상 list")
- join("추가할 문자", "대상 Array")



# 대소문자 변환 시 %26을 이용하면 좋은듯하다.
- 시저암호 풀이에서 사용
```java
sChar = (char)((sChar + n - 'A') % 26 + 'A');
```
# String 값에 char 값 누적으로 더하기 할 수 있다.
- 시저암호 풀이에서 사용
```java
String answer = "";
Char ch = 'A';

answer += ch;
```

# String.replaceAll(기존 문자열, 바꿀 문자열)