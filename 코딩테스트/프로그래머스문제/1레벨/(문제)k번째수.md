### 날짜  2022-04-26 20:09
### 주제: #코딩테스트  #정렬 #copyOfRange 
---
### 메모
> 1.  for문을 이용해 반복 하면서 주어진 배열에 copyOfRange를 사용해 내가 사용할 배열을 새로 잘라서 사용한다. 
### 출처(참고문헌)
- https://programmers.co.kr/learn/courses/30/lessons/42748
### 연결문서


![[Pasted image 20220426201527.png]]

```java
public int[] solution(int[] array, int[][] commands) {
	int[] res = new int[commands.length];
	for(int i = 0; i < commands.length; i++){
		int[] answer = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
		Arrays.sort(answer);
		res[i] = answer[commands[i][2] - 1];
	}
	return res;
}
```