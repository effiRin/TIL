# [Java] equals() 에 대하여

- String은 객체 자료형이라서 equals()로 비교해야 한다.
하지만 equals()도 내부적으로 ==연산자를 사용해 주소를 비교하는 것과 다름이 없다.

- equals()는 최상위 클래스인 Object에 포함되어있어 모든 하위 클래스에서 재정의해서 사용이 가능하다. Object 클래스의 equals()는 주소값을 비교한다.

- 그리고 String클래스의 equals()는 '문자열'을 비교하도록 재정의 되어 만들어졌다. 따라서 주소값을 먼저 비교하고, 주소값이 다르다면 char 타입으로 문자열 비교를 한다. 비교하여 같으면 true, 같지 않으면 false를 반환한다.

- 추가적 이야기  
'== 연산자'는 int, boolean과 같은 primitive type에 대해서 값을 비교하고, reference type에 대해서는 주소값을 비교한다. equals() 연산은 primitive type에서 존재하지 않기에, primitive type은 '==연산자'를 이용.

- 나중에 더 알아볼 것  
✅ StringBuffer에서는 equals가 먹히지 않는 이유


> 출처 : https://go-coding.tistory.com/35