Mockito
===

+ mock을 쉽게 만들고 mock의 행동을 정하는 stubbing, 정상적으로 작동하는지에 대한 verify 등 다양한 기능을 제공해주는 프레임워크이다.


Mokito 설정 방법
---

```
Maven
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-android</artifactId>
  <version>3.7.7</version>
  <type>pom</type>
</dependency>

Gradle
implementation 'org.mockito:mockito-android:3.7.7'

```

Mokc 생성 관련 어노테이션
---

+ @Mock
+ @Spy
+ @InjectMock

## @Mock

```
@Mock으로 만든 mock 객체는 가짜 객체이며 그 안에 메서드 호출해서 사용하려면 반드시 스터비(stubbing)을 해야한다.

만약, 스터빙을 하지 않고 그냥 호출 한다면 primitive type은 0, 참조형은 null을 반환합니다.
```
