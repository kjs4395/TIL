# java 자료형 int 와 long형 차이

* long 형이 더 큰 숫자를 표현 할 수 있지만 메모리를 많이 먹는다.

|  <center>/</center> |  <center>long</center> |  <center>int</center> |
|:--------|:--------:|--------:|
|**bit수** | <center> 64bit </center> | <center>32bit </center>|
|**최대값** | <center> 9223372036854775807 </center> |<center> 2147483647 </center>|
|**최소값** | <center> -9223372036854775808 </center> |<center> -2147483648 </center> |

# char 을 int 로 변환하는법
1. Java.lang.Character.getNumericValue() Method 사용
2. char (0부터 9까지의 숫자)를 char (0에서 9)로 간단히 빼면 int (0-9)로 변환 할 수 있다. (ASCII 코드 표에 의해!)

