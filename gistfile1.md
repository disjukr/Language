스크립트 언어스러운 컴파일 언어 

###변수 선언###
```
[const]-타입-변수명-[초기식]
```
###함수 선언###
```
func-[타입]-함수명(인자,)-[제네릭명,]:
	표현식,
```
함수명은 고유하지 않으며, 인자의 형과 갯수에 따라 구분할 수 있다.
인자 없는 함수는 Ruby 처럼 괄호를 생략할 수 있다.
함수 첫 인자의 이름으로 self 키워드를 사용하면, self.function 과 같은 식으로 호출할 수 있다.

예로 아래와 같은 함수 정의가 있다면. `-10.abs()` 혹은 `-10.abs` 와 같이 호출할 수 있다.
```
func int abs(int self):
	if self < 0:
		ret -self
	else:
		ret self
```
함수명을 연산자로 한다면 연산자 오버라이딩을 구현할 수 있다.
```
func T list +(T list self, T list other) unknown T:
	ret T list.join(self, other)
```
###클래스 선언###
```
class-클래스명(타입,):
	변수선언,
```
클래스의 정의는 변수의 나열과 같아 매우 간결하고, 외부 메서드로 이를 확장한다.
함수 명으로 사용된 init 키워드는 생성자라고 하며 new 키워드로 호출할 수 있다.
객체를 생성하려면 클래스에 해댕하는 init 함수가 적어도 하나 이상 있어야 한다.
```
class Person:
	int age
	char list name

func init(Person self, int age, char list name=“John”):
	self.age = age
	self.name = name

Person person = Person.new(3) 	# Person person(3) 으로 축약할 수 있다.
stdout < person.age 			# 3
stdout < person.name 			# John
```
###상속###

선언시 상속할 클래스명을 콤마로 구분해 기입한다. 다중 상속을 지원한다.
```
class Programmer(Person):
	int coffee

func init(Programmer self, int age, char list name):
	self.Person.init(age, name)
	self.coffee = int.maximum
```
###상수 선언###

상수는 const 키워드를 이용하여 선언할 수 있다.
클래스 안에 const 키워드를 사용한다면, 이 상수는 클래스 명을 통해 접근할 수 있다.
```
class A:
	const int a = 10
stdout < A.a	# 10
```
혹은 인자명으로 class 키워드를 사용하여 클래스의 정적 함수처럼 사용할 수 있다.
```
func b(A class):	
	ret 20
stdout < A.b	# 20
```
###캐스팅###

캐스팅 함수는 타입명을 함수명으로 사용하면 성립된다. 부모 클래스 캐스트 함수는 자동으로 생성된다.
아래와 같은 식이라면, person.char list 혹은 char list(person) 두 가지 방식으로 호출할 수 있다.
```
func char list(Person self):
	ret self.name
```
###제네릭 클래스 선언###

제네릭 클래스는 타입을 인자로 받는 클래스이다.
제네릭 클래스의 선언은 아래와 같이 한다.
```
class FT ST Pair unknown FT, unknown ST:
	FT first
	ST second
```
###typedef###

typedef 키워드를 통해 길고 복잡한 타입명을 축약할 수 있다. 
typedef 에도 제네릭 적용이 가능하다.
```
typedef string: char list
typedef T id_list: int T Pair list
```
###lambda 와 delegate###

lambda 키워드를 통해 무명 함수를 만들 수 있다. 컴파일 타임에 확장된다.

delegate 키워드를 통해 동적으로 함수를 선택하여 호출할 수 있다.
```
delegate int square(int) = lambda x: x^2
stdout < square(3) 	# 9
```
###분기문###

if, elif, else 문은 Python 의 그것과 일치한다.

###반복문###

while 문은 Python 의 그것과 일치한다.

for 의 경우 T enumerable 클래스를 상속받아 구현해야 한다.
작동 방식은 Python 의 그것과 일치한다.