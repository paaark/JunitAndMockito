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

## 스터빙 Stubbing

```
Mockito에선 when 메서드를 이용해서 Stubbing을 지원하고 있다.
```

### OngoingStubbing 메서드

```
OngoingStubbing 메서드란 when에 넣은 메서드의 리턴 값을 정의해주는 메서드입니다.
```

예제
---

```Java
public class StakingProductService {
  
  public Product getProduct() {
    return new Product("P001", "staking01");
  }
  
  public Product getProduct(String id, String name) {
    return new Product(id, name);
  }

}
```

```Java

@ExtendWith(MockitoExtension.class)
public class OngoingStubbingMethod {
  
  @Mock
  StakingProductService stakingProductService;
  
  @Test
  void testThenReturn() {
    Product product = new Product("P001", "staking01");
    when(stakingProductService.getProduct()).thenReturn(product);
    assertThat(stakingProductService.getProduct()).isEqualTo(product);
  }
  
  @Test
  void testThenThrows() {
    when(stakingProductService.getProduct()).thenThrow(new IllegalArgumentException());
 
    assertThatThrownBy(() -> stakingProductService.getProduct()).isInstanceOf(IllegalArgumentException.class);
  }
 
  @Test
  void testThenAnswer() {
    when(stakingProductService.getProduct(any(), any())).thenAnswer((Answer) invocation -> {
      Object[] args = invocation.getArguments();
 
      return new Product(args[0] + "1", args[1] + "_1233");
    });
 
    assertThat(stakingProductService.getProduct("P001","staking01").getSerial()).isEqualTo("P001");
  }
 
  @Test
  void testThenCallRealMethod() {
    when(stakingProductService.getProduct()).thenCallRealMethod();
 
    assertThat(stakingProductService.getProduct().getSerial()).isEqualTo("P001");
  }
    
}

```

### Stubber 메서드

```
{Stubber 메서드}.when({스터빙할 클래스}).{스터빙할 메서드}
```

## @Spy

```
@Spy로 만든 Mock 객체는 진짜 객체이며 메서드 실행시 스터빙을 하지 않으면 기존 객체의 로직을 실행한 값을, 스터빙을 한 경우엔 스터빙 값을 리턴합니다.
```

## @InjectMock

```
@InjectMock은 DI를 @Mock이나 @Spy로 생성된 mock 객체를 자동으로 주입해주는 어노테이션이다.

@InjectMocks를 사용하니@Mock, @Spy로 만든 객체들이 자동으로 주입된 것을 볼 수 있습니다.

@InjectMocks을 쓴 객체의 mock 객체를 주입 받을 수 있는 형태는 Constructor, Property Setter, Field Injection이 있습니다.
```

## Verify 메서드

```
verify 메소드를 이용해서 스터빙한 메소드가 실행됐는지, n번 실행됐는지, 실행이 초과되지 않았는지 등 다양하게 검증해볼 수 있습니다.

verify(T mock, VerificationMode mode)
```




