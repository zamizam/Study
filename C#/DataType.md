# 자료형 확인 방법 (DataType)

## GetType() 
자료형을 확인하는 메소드

## typeof
자료형을 확인하는 연산자

## is
결과의 런타임 형식이 지정된 형식과 호환되는지 확인하는 연산자

```csharp
 object b = new Base();
if ( b is Base ) // true
if ( b is Derived) // false

object d = new Derived();
if ( b is Derived) // true

```


## as
