# Chapter 11. 예외 처리

# 11.1 예외와 예외 클래스

- 자바는 예외가 발생하면 예외 클래스로부터 객체를 생성한다.
- 자바의 모든 에러와 예외 클래스는 Throwable을 상속받아 만들어진다.
- 예외 클래스는 java.lang.Exception 클래스를 상속받는다.
- Throwable → Exception → 모든 예외 클래스
    
    ex) 실행예외인 RuntimeException은 Exception의 자식 클래스
    

# 11.2 예외 처리 코드

### try catch finally

```java
try{

} catch(예외클래스 e) {

} finally {

}
```

- 정상 실행 시 : try → finally
- 예외 발생 시 : catch → finally
- finally는 항상 실행된다. (finally는 생략 가능하다.)

# 11.3 예외 종류에 따른 처리

- try 블록에서는 다양한 예외가 발생한다. 이 경우에는 다중 catch를 통해 발생하는 예외에 따라 예외 처리 코드를 다르게 작성할 수 있다.

```java
try{
	
} catch(ArrayIndexOutOfBoundsException e) {

} catch(NumberFormatException e) {

}
```

- 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 예외의 catch 블록으로 바로 이동한다.
- 단, 처리할 예외 클래스들이 상속 관계에 있을 때는 하위 클래스 catch 블록을 먼저 작성해야 한다.

```java
try{
	// 1. NumberFormatException 발생
} catch(Exception e) {
	// 2. 해당 catch문으로 이동
} catch(NumberFormatException e) {

}
```

- 두개 이상의 예외를 하나의 catch 블록으로 처리하고 싶을때는 기호 | 로 연결한다.

```java
try{

} catch (NumberFormatException | ArrayIndexOutOfBoundsException e) {

}
```

# 11.4 리소스 자동 닫기

- try 괄호에 리소스를 여는 코드를 작성하면 try 블록이 정상적으로 실행완료되었거나 예외가 발생하면 자동으로 리소스의 close() 메소드가 호출된다.

```java
try(FileInputStream fis = new FileInputStream("file.txt")){

} catch(예외클래스 e) {

}
```

# 11.5 예외 떠넘기기

- 메소드 내부에서 예외가 발생할 때 throws를 통해 메소드를 호출한 곳으로 예외를 떠넘길 수 있다.

```java
try{
	method1();
} catch(Exception e) {
	//method1에서 오류가 발생하면 여기에서 처리
}

public void method1() throws Exception{
	...
}
```

- 나열할 예외 클래스가 많으면 throws Exception이나 throws Throwable만으로 모든 예외를 떠넘길 수 있다.
- main 메소드에서 예외를 떠넘기면 결국 JVM이 최종적으로 예외처리를 하게된다.

# 11.6 사용자 정의 예외

- 컴파일러가 체크하는 일반예외로 선언하거나 체크하지 않는 실행 예외로 선언한다.
- 일반예외 : Exception의 자식 클래스로 선언
- 실행예외 : RuntimeException의 자식 클래스로 선언

```java
public class CustomException extends Exception {
	public CustomException(String message){
		super(message);
	}
}
```

- 클래스 선언 후 해당 예외를 발생시키고 싶을 때는 throw를 통해 발생시킨다.

```java
if(errorOccured){
	throw new CustomException("에러발생!!");
}
...
```