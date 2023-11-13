# Kotlin-Coding-Conventions

# Coding conventions
코딩 컨벤션을 사용하는 이유!!!!
모든 프로그래밍언어는 널리 알려져 있고 쉽게 따를 수 있는 코딩컨벤션이 필수적이다.
Kotlin을 사용하는 프로젝트의 코드 스타일과 코드 구성에 대한 가이드라인을 제공한다.
[공식문서로 이동하기](https://kotlinlang.org/docs/coding-conventions.html)

# Configure style in IDE 스타일 구성 IDE에서
Kotlin에서 가장 많이 사용되는 두 가지 IDE인 IntelliJ IDEA와 Android Studio는 코드 스타일 지정에 대한 강력한 지원을 제공한다. 지정된 코드 스타일에 따라 코드 서식을 자동으로 지정하도록 구성할 수 있다.

## Apply the style guide 스타일 가이드 적용
1. 여기로 가라 -> Settings/Preferences | Editor | Code Style | Kotlin.
2. 클릭해라 Set from....
3. 선택해라 Kotlin style guide.


## Verify that your code follows the style guide
1. 여기로 가라 -> Settings/Preferences | Editor | Inspections | General.
2. 켜라 Incorrect formatting inspection(잘못된 서식 검사). 스타일 가이드에 설명된 다른 문제(ex. 명명 규칙)를 확인하는 추가 검사는 기본적으로 활성화되어 있다.

---

# Source code organization 소스 코드 구성

## Directory structure 디렉토리 구조
순수 코틀린 프로젝트에서 권장되는 디렉토리 구조는 일반 루트 패키지를 생략한 패키지 구조를 따른다.

예를 들어, 프로젝트의 모든 코드가 `org.example.kotlin` 패키지와 그 하위 패키지에 있다면 `org.example.kotlin` 패키지에 있는 파일은 바로 소스 루트 아래에 배치한다.
```
파일 최상단에 패키지 선언이 없다.
```

`org.example.kotlin.network.socket` 패키지에 있는 파일은 `network/socket` 하위 디렉토리의 소스 루트에 배치해야 한다.
```
파일 최상단에 다음과 같이 작성하라는 것 같다.

package network.socket
```

## Source file names 소스 파일 이름
Kotlin 파일이 단일 클래스 또는 인터페이스인 경우, class의 이름과 파일명이 같고 `.kt`확장자를 추가해야한다. 모든 타입의 클래스와 인터페이스들에 적용된다.
한 파일에 여러개의 클래스가 있거나, top-level 선언만 포함하는 경우, 파일이 무엇을 담고 있는지 설명하는 이름을 지정해라.

Upper camelCase(PascalCase)를 사용해라
예시 -> `ProcessDeclarations.kt`

파일 이름은 파일내의 코드가 무엇을 하는지 설명해야 한다.
따라서, `Util`과 같은 의미 없는 단어의 파일 이름을 피해야한다. (뜨끔..)

## Source file organization 소스 파일 구성
파일이 수백줄이 넘지 않는 합리적인 수준이라면, 의미가 서로 밀접한 관계의 여러 선언(클래스들, 최상위 함수, 속성들)을 동일한 Kotlin 파일에 배치하는 것이 좋다.

특히, 클래스의 모든 클라이언트와 관련된 클래스의 확장 함수를 정의할 때는 클래스 자체와 같은 파일에 넣자.

특정 클라이언트에 대해서만 의미가 있는 확장 함수를 정의할 때는 해당 클라이언트의 코드 옆에 배치해라.

특정 클래스의 모든 확장 함수를 담기 위해 파일을 만들지 마라



## Class layout 클래스 레이아웃
클래스 내용은 다음의 순서로 구성되어야만 한다.

1. property 선언 및 초기화 blocks
2. 부 생성자 (secondary constructors)
3. Method 선언
4. Companion object

메서드 선언을 알파벳순이나 표시 여부에 따라 정렬하지 말고, 일반 메서드와 확장 메서드를 분리하지마라
클래스를 위에서 아래로 읽는 사람이 무슨 일이 일어나고 있는지 논리를 따라갈 수 있도록 관련 내용을 배치해라
순서를 정하고 (상위 수준 먼저 또는 그 반대로) 그 순서를 지켜라
중첩된 클래스는 해당 클래스를 사용하는 코드 옆에 배치해라. 만약 클래스가 외부에서 사용되어야 하고 클래스 내부에서 참조되지 않는 경우에는 companion object 뒤의 맨 마지막에 배치해라

## Interface implementation layout 인터페이스 구현 레이아웃
인터페이스를 구현할 때 구현 멤버를 인터페이스의 멤버와 동일한 순서로 유지해라
(필요한 경우 구현에 추가로 사용된 private methods와 산재시켜라)

## Overload layout 오버로드 레이아웃
항상 클래스 내에서 같은 이름의 메서드를 만들 때(오버로딩 할 때) 나란히(서로 인접하게) 배치해라

# Naming rules 이름 규칙
코틀린에서 package와 class 이름을 짓는 건 매우 간단하다.

패키지 이름은 `소문자`만 사용하고, `밑줄`을 사용하지 않는다.
ex) `org.example.project`
일반적으로 여러 단어 사용을 권장하지 않지만, 여러 단어를 사용하려면
camelCase를 사용하자. ex) org.example.myProject

`class`와 `object`이름은 PascalCase를 사용한다.
ex) class DeclarationProcessor { }

## Function names 함수 이름
함수, 프로퍼티, 로컬 변수의 이름은 camelCase를 사용한다.
ex) fun processDeclarations() { }
var declarationCount = 1

예외) 클래스의 인스턴스를 생성할 때 사용하는 factory 함수는
abstract return type과 동일한 이름을 가질 수 있다.
```
interface Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun Foo(): Foo { return FooImpl() }
```



## Names for test methods 테스트 메서드 이름
테스트에서는(테스트에서만!) 백틱안에서 공백이 있는 메서드 이름을 사용할 수 있다.
주의! 이러한 메서드 이름은 안드로이드 런타임에서 지원되지 않는다.
테스트 코드에서는 메서드 이름에 밑줄도 사용할 수 있다.
```
class MyTestCase {
     @Test fun `ensure everything works`() { /*...*/ }

     @Test fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

## Property names 프로퍼티 이름
상수의 이름은 대문자(uppercase)와 snake_case를 사용해야한다.
```
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```

행동이나 가변 데이터를 가진 top-level또는 object 속성의 이름들은 camelCase를 사용해야한다.
```
val mutableCollection: MutableSet<String> = HashSet()
```

싱글톤 객체에 대한 참조를 가지고 있는 속성들의 이름은 object 선언과 같은 네이밍 스타일을 사용할 수 있다.
```
val PersonComparator: Comparator<Person> = /*...*/
```
enum 상수의 경우, 대문자와 snake_case를 사용하거나 PascalCase를 사용한다. 사용에 따라 달라진다.

## Names for backing properties 백킹 속성의 이름

클래스가 개념적으로 동일한 두 개의 속성을 가지고 있다면, (하나는 공개 API의 일부이고 다른 하나는 구현 세부사항인) `private` 속성의 이름에 밑줄을 접두사로 사용해라

(비공식 설명 : `_elementList`는 private으로 클래스 내부에서만 사용되고, `elementList`는 public으로 외부에 공개되어 사용된다.)
```
class C {
    private val _elementList = mutableListOf<Element>()

    val elementList: List<Element>
         get() = _elementList
}
```

## Choose good names 좋은 이름 선택
`class`이름은 일반적으로 클래스가 무엇인지 설명하는 명사 또는 명사 구문으로 구성된다.
ex) List, PersonReader

`method`이름은 일반적으로 동사 또는 동사 구문으로 메서드가 수행하는 작업을 설명한다.
ex) close, readPersons
메서드가 객체를 변경하는지 아니면 새 객체를 반환하는지도 이름에서 알 수 있어야 한다.
ex) sort는 해당 컬렉션 자체를 정렬, sorted는 컬렉션의 정렬된 복제본

이름은 엔티티의 용도를 명확하게 나타내야한다. 이름에 의미 없는 단어를 사용하지 않는다.
ex) Manager, Wrapper

약어를 이름의 일부로 사용하는 경우 두 글자로 구성된 경우는 대문자로 표시하고, 더 긴 경우는 첫 글자만 대문자로 표시한다.
ex) IOStream / XmlFormatter, HttpInputStream


# Formatting

## Indentation 들여쓰기
들여쓰기는 4개의 `space`공백을 사용, `tab`사용 금지
중괄호 {}의 경우, 구문이 시작되는 줄 끝에 여는 중괄호({)를 놓고, 
닫는 중괄호(})는 구문이 시작되는 첫 글자와 수평으로 정렬된 줄에 놓는다.

```
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```

## Horizontal whitespace 수평 공백
- 이항 연산자(`a + b`) 주위에 공백을 넣어라 (예외: "range to" 연산자 주위에는 공백을 넣지 마라(`0..i`)
- 단항 연산자(`a++`) 주위엔 공백을 넣지마라
- 제어 흐름 키워드(`if`, `when`, `for`, `while`) 와 해당 여는 괄호(`(`) 사이에 공백을 넣어라
- 기본 생성자 선언, 메서드 선언 또는 메서드 호출에서는 여는 괄호(`(`) 앞에 공백을 넣지 마라

```
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```
- 절대 `(`,`[` 뒤 또는 `]`,`)` 앞에 공백을 넣지마라 
- `.`또는 `?.`주위에 공백을 넣지마라 (`foo.bar().filter { it > 2 }.joinToString()`,`foo?.bar()`)
- // 뒤에는 공백을 넣어라 (//는 주석이다.)
- 매개변수(파라미터)의 타입을 지정하는데 사용되는 꺽쇠괄호 주위에 공백을 넣지마라 (`class Map<K, V> { ... }`)
- ::: 주위에 공백을 넣지마라 (`Foo::class`, `String::length`)
- nullable 타입을 표시하는데 사용되는 `?`앞에 공백을 넣지마라 (`String?`)

일반적인 규칙으로 어떤 종류든 수평 정렬을 피해라.
식별자의 이름을 다른 길이의 이름으로 변경해도 선언이나 사용 방법의 포맷에 영향을 주지 않아야 한다.

## Colon 콜론 :
다음과 같은 경우에 : 앞에 공백을 넣어라
- type과 supertype을 분리하는데 사용되는 경우
- superclass 생성자 또는 같은 클래스의 다른 생성자에 위임할 때
- `object` 키워드 뒤에 사용되는 경우

선언과 type을 분리할 때는 : 앞에 공백을 넣지마라, 항상 : 뒤에 공백을 둬야한다.
```
abstract class Foo<out T : Any> : IFoo {
    abstract fun foo(a: Int): T
}

class FooImpl : Foo() {
    constructor(x: String) : this(x) { /*...*/ }

    val x = object : IFoo { /*...*/ }
}

```


## Class headers

## Modifiers order 수정자 순서
선언에 여러개의 modifier가 있으면 항상 다음 순서로 배치해라
```
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation / fun // as a modifier in `fun interface`
companion
inline / value
infix
operator
data
```

모든 어노테이션은 modifier 앞에 놓는다.
```
@Named("Foo")
private val foo: Foo
```

라이브러리에서 작업하는 것이 아니라면, 중복되는 수정자(ex. `public`)는 생략해라

## Annotations 어노테이션
어노테이션은 해당 선언 앞에 별도의 줄에 동일한 들여쓰기로 배치한다.
```
@Target(AnnotationTarget.PROPERTY)
annotation class JsonExclude
```

Argument가 없는 어노테이션들은 같은 줄에 배치할 수 있다.
```
@JsonExclude @JvmField
var x: Strinvar x: String
```

Argument가 없는 어노테이션은 해당 선언과 같은 줄에 배치할 수 있다.
```
@Test fun foo() { /*...*/ }
```

## File annotations 파일 어노테이션
파일 어노테이션이 있는 경우, `package` 선언 앞에 배치 되며, 빈줄(blank line)로 구분된다.
패키지가 아닌 파일을 대상으로 한다는 사실을 강조하기 위해 구분한다.
```
/** License, copyright and whatever */
@file:JvmName("FooBar")

package foo.bar
```

## Functions 함수
함수 시그니처가 한줄에 맞지 않다면, 아래와 같은 구문을 사용하자
```
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType,
): ReturnType {
    // body
}
```
함수 파라미터(매개변수)는 들여쓰기(스페이스바 4번)을 사용해라
이렇게 하면 생성자 파라미터(매개변수)와 일관성을 유지할 수 있다.

함수의 본문이 단일 표현식으로 구성된 경우, 표현식 본문을 사용을 선호한다.
```
fun foo(): Int {     // bad
    return 1
}

fun foo() = 1        // good
```

## Expression bodies 표현식 본문
만약, 함수가 같은 첫 줄에 선언하기 맞지 않는 표현식이 있는 경우
첫 줄에 `=`기호를 넣고 다음 줄에 본문을 4칸 들여쓰기 한다.
```
fun f(x: String, y: String, z: String) =
    veryLongFunctionCallWithManyWords(andLongParametersToo(), x, y, z)
```

## Properties 속성
매우 간단한 읽기 전용 속성인 경우, 한 줄 포맷을 고려해라
```
val isEmpty: Boolean get() = size == 0
```

좀 더 복잡한 속성인 경우, 항상 `get`과 `set` 키워드를 별도의 줄에 둔다.
```
val foo: String
    get() { /*...*/ }
```

초기화가 있는 속성의 경우, 초기화자가 길면 `=` 기회 뒤에 줄바꿈을 추가하고 4칸 들여서 초기화를쓴다.

```
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```


## Control flow statements

## Method calls 메소드 호출

인수(argument) 목록이 긴 경우, 여는 괄호 뒤에 줄을 바꿔라
인수를 4칸 들여쓰기 한다.
밀접하게 관련된 인수들은 같은 줄에 그룹화 한다.

```
drawSquare(
    x = 10, y = 10,
    width = 100, height = 100,
    fill = true
)
```
인수 이름과 값을 구분하는 `=` 기호 주의에 공백을 넣어라

## Wrap chained calls 연쇄 호출 묶기
연쇄 호출을 묶을 때는 다음 줄에 `.` 문자 또는 `?.` 연산자를 한 번 들여쓰기 해서 넣어라
```
val anchor = owner
    ?.firstChild!!
    .siblings(forward = true)
    .dropWhile { it is PsiComment || it is PsiWhiteSpace }
```
첫 번째 호출 앞에는 보통 줄바꿈이 들어가야 한다.
그러나, 코드가 더 이해하기 쉽게 만들어줄 수 있다면 생략해도 좋다.


## Lambdas 람다
람다 표현식에서 중괄호 주변과 매개변수와 본문을 구분하는 화살표 주변에 공백을 사용해야 한다.
호출이 하나의 람다를 사용하는 경우, 가능하면 괄호 밖에 람다를 전달해라
(비공식 해설 : `( )` <- 이 괄호를 쓰지 말라 라는 것 같다.)
```
list.filter { it > 10 }
```

람다에 레이블을 지정할 경우, 레이블과 중괄호 사이에 공백을 넣지 마라
```
fun foo() {
    ints.forEach lit@{
        // ...
    }
}
```

여러 줄의 람다에서 매개변수 이름을 선언할 때, 첫 번째 줄에 이름을 위치시키고, 그 뒤에 화살표와 줄바꿈을 추가해라

```
appendCommaSeparated(properties) { prop ->
    val propertyValue = prop.get(obj)  // ...
}
```

매개변수 목록이 한 줄에 들어갈 수 없을 정도로 긴 경우, 화살표를 별도의 줄에 위치시켜라
```
foo {
   context: Context,
   environment: Env
   ->
   context.configureEnv(environment)
}
```




## Trailing commas 후행 쉼표

```
class Person(
    val firstName: String,
    val lastName: String,
    val age: Int, // trailing comma
)
```

후행쉼표를 사용하면,
변경된 값에만 초점을 맞출 수 있어 버전관리가 더 명확해진다.
요소를 추가하거나, 순서를 변경하기 쉽다.
~~객체 조기화자에 대해 코드 생성을 간소화한다.(뭔소리임? 이해 못했음)~~

사용을 권장하지만, 없어도 완전히 작동한다.



# Documentation comments 주석


# Avoid redundant constructs 중복 구문 피하기
일반적으로, Kotlin의 특정 구문 구조가 선택 사항이고 IDE에서 중복으로 강조 표시되는 경우 
코드에서 해당 구문 구조를 생략해야 한다.
"명확성을 위해"코드에 불필요한 구문 요소를 남겨 두지 마라

## Unit return type Unit타입 반환
함수가 Unit 타입을 반환하는 경우 return type을 생략해야 한다.
```
fun foo() { // ": Unit" is omitted here

}
```


## Semicolons 세미콜론라
세미콜론은 가급적 생략하세요.

## String templates 문자열 템플릿
스트링 템플릿에 간단한 변수를 삽입할 때는 중괄호를 사용하지 마세요.
중괄호는 긴 표현식에만 사용하세요.
```
println("$name has ${children.size} children")
```




# Idiomatic use of language features 언어 기능의 관용적 사용

## Immutability 불변성
변경 가능한(mutable) 데이터보다 변경 불가능한(immutable) 데이터를 사용하는 것을 선호한다. 로컬 변수와 프로퍼티는 초기화 후 수정되지 않는 이상 항상 var가 아닌 val로 선언해라

수정하지 않을 컬렉션을 선언할 때는 항상 변경 불가능한(immutable) 컬렉션 인터페이스(Collection, List, Set, Map)을 사용해라

팩토리 함수를 사용해 컬렉션 인스턴스를 생성할 때는 가능하면 항상 변경 불가능한(immutable) 컬렉션 유형을 반환하는 함수를 사용해라.

```
// Bad: 변경되지 않는 값에 변경 가능한 컬렉션 타입을 선언
fun validateValue(actualValue: String, allowedValues: HashSet<String>) { ... }

// Good: 대신에 불변 컬렉션 타입을 사용해라!
fun validateValue(actualValue: String, allowedValues: Set<String>) { ... }

// Bad: arrayListOf() 는 ArrayList<T>를 리턴한다. 변경 가능한 타입이다.
val allowedValues = arrayListOf("a", "b", "c")

// Good: listOf() 는 List<T>를 리턴한다. 변경 불가능한 타입이다.
val allowedValues = listOf("a", "b", "c")
```

## Default parameter values 기본 매개변수 값
오버로드된 함수를 선언하는 것보다 기본 매개변수 값으로 함수를 선언하는 것을 선호한다.
```
// Bad
fun foo() = foo("a")
fun foo(a: String) { /*...*/ }

// Good
fun foo(a: String = "a") { /*...*/ }
```
(default parameter values는 함수를 호출 할 때 매개변수를 지정하지 않아도 사용할 수 있도록 해주는 값이다.)


## Type aliases 타입 별칭
함수형 타입이나 매개변수가 있는 타입이 코드상에서 여러 번 사용되는 경우, 해당 타입에 대한 타입 별칭을 정의하는 것이 좋다.
```
typealias MouseClickHandler = (Any, MouseEvent) -> Unit
typealias PersonIndex = Map<String, Person>
```
private 또는 internal 타입 별칭을 사용하는 경우 이름 충돌을 피하기 위해서,
`import ... as ...`로 packages와 imports에서 언급해라 

## Lambda parameters 람다 매개변수
짧고 중첩되지 않은 람다에 대해서는 매개변수를 명시적으로 선언하는 대신 `it` 컨벤션을 사용하는 것이 권장된다. 중첩된 람다에서 매개변수가 있는 경우는, 항상 매개변수를 명시적으로 선언해야 한다.

## Returns in a lambda 람다안에서 리턴
람다에서 여러 레이블이붙은 리턴이 있는 것을 피해라.
람다가 단일 종료 지점을 갖도록 재구조화하는 것을 고려해라.
그것이 불가능하거나 충분히 명확하지 않다면, 람다를 익명 함수로 변환하는 것을 고려해라.

람다의 마지막 구문에 레이블이붙은 리턴을 사용하지 마라.

## Named arguments 명명된 인자
메서드가 동일한 원시 타입의 매개변수를 여러개 받거나, Boolean 타입의 매개변수에모든 매개변수의 의미가 완전히 명확하지 않은 경우, 명명된 인자를 사용해라.
(비공식 해설 : Default parameter 참고)
```
drawSquare(x = 10, y = 10, width = 100, height = 100, fill = true)
```

## Conditional statements 조건문
`try`, `if`, `when`의 표현식을 사용하는 것을 선호한다.
(참고 : 공식문서에는 Good과 Bad으로 적혀있지 않고 Good의 케이스를 더 선호한다고 명시되어있다.)

```
// Good
return if (x) foo() else bar()

// Bad
if (x)
    return foo()
else
    return bar()
```
```
// Good
return when(x) {
    0 -> "zero"
    else -> "nonzero"
}

// Bad
when(x) {
    0 -> return "zero"
    else -> return "nonzero"
}
```

## if versus when if vs when
이진조건에서는 `if`보다 `when`을 더 선호한다.
```
if (x == null) ... else ...
```

```
when (x) {
    null -> // ...
    else -> // ...
}

```

3가지 이상의 옵션이 있는 경우 `when`을 사용하는 것을 선호한다.

## Nullable Boolean values in conditions 조건문에서 널러블 불린 값
조건문에서 null이 가능한(nullable) `Boolean`값(참/거짓)을 사용하려면
if (value == true) or if (value == false)로 검사를 해야한다.

## Loops 반복
반복문보다는 고차 함수(`filter`, `map` 등)를 사용하는 것을 선호한다.

예외: `forEach` 
(`forEach`보다, 일반 `for`반복문을 사용하는 것이 더 선호된다. `forEach`의 receiver가 nullable이거나 `forEach`가 더 긴 호출 체인의 일부로 사용되는 경우)

여러 고차 함수를 사용하는 복잡한 표현식과 반복문 중에서 선택할 때는 각 경우에 수행되는 작업의 비용을 이해하고 성능 고려 사항을 염두에 두어야 한다.

## Loops on range 범위의 반복
반복문의 범위를 설정할 때 `..<` 연산자를 사용해라
```
for (i in 0..n - 1) { /*...*/ }  // bad
for (i in 0..<n) { /*...*/ }  // good
```

## Strings 문자열
문자열 연결보다 문자열 템플릿을 더 선호한다.

일반 문자열 리터럴에 `\n`(이스케이프 시퀀스)를 포함하는 것보다 여러 줄 문자열을 선호한다.

여러 줄 문자열에서 들여쓰기를 유지하려면, 결과 문자열에 내부 들여쓰기가 필요하지 않은 경우 `trimIndent`를 사용하고, 내부 들여쓰기가 필요한 경우 `trimMargin`을 사용한다.

```
println("""
    Not
    trimmed
    text
    """
       )

println("""
    Trimmed
    text
    """.trimIndent()
       )

println()

val a = """Trimmed to margin text:
          |if(a > 1) {
          |    return a
          |}""".trimMargin()

println(a)
```
결과 :
```
    Not
    trimmed
    text
    
Trimmed
text

Trimmed to margin text:
if(a > 1) {
    return a
}
```

## Functions vs properties 함수 vs 속성
경우에 따라, 인자(arguments)가 없는 함수를 read-only 프로퍼티와 상호 교환해 사용할 수 있다.
의미는 비슷하지만, 어느 것을 더 선호해야 하는지에 대한 몇 가지 규칙이 있다.

함수보다 프로퍼티를 선호하는 경우
- 예외를 던지지 않을 때
- 계산 비용이 적을 때 (혹은 첫 실행 시 캐시될 때)
- 객체 상태가 변경되지 않은 경우 호출에 대해 동일한 결과를 반환할 때

## Extension functions 확장 함수
확장 함수를 자유롭게 사용해라.
주로 객체에서 작업하는 함수가 있을 때 마다, 해당 객체를 수신자로 받는 확장 함수로 만드는 것을 고려해라. API 오염을 최소화하기 위해, 의미가 통하는 한 확장 함수의 가시성을 최대한 제한해라. 필요에 따라 로컬 확장 함수, 멤버 확장 함수 또는 private 가시성을 가진 최상위 확장 함수를 사용해라

## Infix functions 중위 함수
비슷한 역할을 하는 두 객체에서 작동하는 경우에만 함수를 `infix`로 선언해라
Good example: `and`, `to`, `zip`
Bad example: `add`

receiver 객체(object)를 변경하려면, 메서드를 `infix`로 선언하지마라.


## Factory functions 팩토리 함수
클래스에 대한 팩토리 함수를 선언하는 경우, 클래스 자체와 같은 이름으로 지정하지 마라.
팩토리 함수의 동작이 왜 특별한지 명확하게 알 수 있도록 고유한 이름을 사용하는 것이 좋다.
특별한 의미가 없는 경우에만 클래스와 같은 이름을 사용할 수 있다.
```
class Point(val x: Double, val y: Double) {
    companion object {
        fun fromPolar(angle: Double, radius: Double) = Point(...)
    }
}
```
다른 상위 클래스 생성자를 호출하지 않고 기본 인수 값을 사용하는 단일 생성자로 줄일 수 없는 여러 개의 오버로드된 생성자가 있는 객체가 있는 경우 오버로드된 생성자를 팩토리 함수로 대체하는 것이 좋다.

## Platform types

## Scope functions apply/with/run/also/let 범위 함수
코틀린은 주어진 객체의 컨텍스트에서 코드 블록을 실행하기 위한 함수 집합인`let`, `run`, `with`, `apply` 그리고 `also`를 제공한다. 사례에 적합한 scope함수를 선택하는 방법에 대해서는 Scope Functions을 참조해라.

# Coding conventions for libraries 라이브러리 코딩 규칙
라이브러리를 작성할 때는 API 안정성을 보장하기 위해 추가적인 규칙을 따르는 것이 좋다:
- 항상 멤버 가시성을 명시적으로 지정해라(실수로 선언이 공용 API로 노출되는 것을 방지하기 위해)
- 함수 반환 유형과 속성 유형을 항상 명시적으로 지정해라(구현이 변경될 때 실수로 반환 유형이 변경되는 것을 방지하기 위해)
- 새 문서가 필요하지 않은 오버라이드를 제외한 모든 공용 멤버에 대해 KDoc 주석을 제공해라(라이브러리에 대한 문서 생성을 지원하기 위해)
- 라이브러리 제작자 가이드라인에서 라이브러리용 API를 작성할 때 고려해야할 모범사례와 아이디어에 대해 자세히 알아봐라
