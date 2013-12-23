###변수 선언###
```
[const] 타입 변수명 [초기식]
```
const 키워드로 상수를 정의할 수 있으며 그 때는 초기값을 대입해야 한다.
```
char a
const int b = 1
```

###함수 선언###
```
[반환타입] 함수명(인자목록) [gen 타입목록]:
	함수몸체
```
함수명은 고유하지 않으며, 인자의 형과 갯수에 따라 구분할 수 있다.
인자 없는 함수는 호출시에 Ruby 처럼 괄호를 생략할 수 있다.
함수 첫 인자의 이름으로 self 키워드를 사용하면, self.function 과 같은 식으로 호출할 수 있다.
이 표현식을 사용할 경우 가상함수 테이블을 참조한다.

예로 아래와 같은 함수 정의가 있다면. `-10.abs()` 혹은 `-10.abs` 와 같이 호출할 수 있다.
```
int abs(int self):
	if self < 0:
		ret -self
	else:
		ret self
```
함수명을 연산자로 한다면 연산자 오버라이딩을 구현할 수 있다.
```
T list +(T list self, T list other) gen T:
	ret T list.join(self, other)
```

###타입 선언###
```
type 타입명 [ext 타입목록] [gen 타입목록]:
	타입몸체
```
타입의 몸체는 멤버의 선언으로 정의한다. 멤버의 정의는 바깥에 위치하도록 한다.
```
type Person:
	int age
	char list name
```

###타입 축약###
```
type 타입명 [gen 타입목록] = 타입
```
타입 정의에 다른 타입을 대입하여 긴 타입명을 짧게 바꿀 수 있다.
```
type string = char list
type id_list gen T = int T Pair list
```

###상속###

```
type Programmer ext Person, Nerd:
	int coffee

init (Programmer self, int age, char list name):
	init(self as Person, age, name)	# 가상함수를 사용하지 않는다
	init(self as Nerd)
	self.coffee = int.maximum
```

###제네릭 타입 선언###

제네릭 타입은 타입을 인자로 받는 타입이다.
제네릭 타입의 선언은 아래와 같이 한다.
```
type Pair gen FT, ST:
	FT first
	ST second
```

###생성자###
```
init (타입명 self, [인자목록]):
	함수몸체
```
init 키워드로 정의된 함수는 생성자라고 하며 타입명으로 호출할 수 있다.
객체를 생성하려면 타입에 해당하는 init 함수가 적어도 하나 이상 있어야 한다.
```
init (Person self, int age, char list name="John"):
	self.age = age
	self.name = name

Person person = Person(3) 	# Person person(3) 으로 축약할 수 있다.
stdout < person.age 		# 3
stdout < person.name 		# John
```

###상수 선언###

상수는 const 키워드를 이용하여 선언할 수 있다.
클래스 안에 const 키워드를 사용한다면, 이 상수는 클래스 명을 통해 접근할 수 있다.
```
type A:
	const int a = 10
stdout < A.a	# 10
```
혹은 인자명으로 type 키워드를 사용하여 타입의 정적 함수처럼 사용할 수 있다.
```
int b(A type):
	ret 20
stdout < A.b	# 20
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

###모듈###
```
module [네임스페이스]:
	모듈몸체
```
이름공간을 다루기 위해 module 키워드를 사용한다.

모듈 안에서는 using 키워드로 다른 이름공간의 객체들을 불러와서 사용할 수 있다.
```
module a.b.c:
	using std.out as stdout
	using folder.file
	stdout < file.member
```
