---
title: "[Spring MVC]테스트 코드 작성해보기"
categories:
  - Spring
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

# 테스트 코드 실습

> 개발 환경 : 인텔리제이
> OS : mac

## 실습해보기 🌿

### 비밀번호 유효성 검증기

요구사항

- 비밀번호는 최소 8자 이상 12자 이하여야 한다.
- 비밀번호가 8자 미만 또는 12 자 초과인 경우 \***\*IllegalArgumentException\*\*** 예외를 발생 시킨다.
- 경계조건에 대해 테스트 코드를 작성해야 한다.

build.gradle 에 의존성 추가

```java
dependencies {
    testImplementation platform('org.junit:junit-bom:5.9.1')
    testImplementation 'org.junit.jupiter:junit-jupiter'
// 아래 추가 된 코드
    testImplementation 'org.assertj:assertj-core:3.23.1'
}
```

assertj dependencies 추가 (의존성) 하기

![image](https://github.com/solfany/solfany.github.io/assets/123814718/65985fb5-8e66-466b-9b71-675af7c77803)

제대로 추가 되었는지 확인하는 방법 External Libraries 에서 확인 가능.

## Test class 만들기

비밀번호 유효성 검사를 위한
**PasswordVaildatorTest 클래스를
Java 폴더에 만들어준다.**

## 중간 폴더구조 확인

![image](https://github.com/solfany/solfany.github.io/assets/123814718/39591906-6e54-4c4e-91d2-c801e1a081d9)

파란 박스가 구동 코드를 작성하는 폴더 구조이고,
보라색 박스가 테스트 코드를 위한 폴더 구조이다.

> 테스트 코드와 실제 구동 코드의 package 구조는 되도록 동일하게 맞춰주는 것이 좋기 때문에
> 해당 폴더 구조 캡쳐 이후에 package를 메인 package 이름과 동일하게 생성해주었다.

---

## 폴더구조

```java
testcode
│
└── src
    ├── main
    │   └── java
    │       └── org
    │           └── example
    │               ├── Main.java
    │               ├── PasswordGeneratePolicy.java
    │               ├── PasswordValidator.java
    │               └── RandomPasswordGenerator.java
    └── test
        └── java
            ├── CorrectPasswordGenerator.java
            ├── PasswordValidatorTest.java
            └── WrongPasswordGenerator.java
```

## 코드

1. 비밀번호 조건 유효성 검사기 - validate
2. 조건에 맞는 비밀번호 생성기와 유효성 검사기 - validate2

PasswordValidator.java

```java
package org.example;

public class PasswordValidator {

    /**
     * 비밀번호가 8자 미만 또는 12자 초과하는 경우 IllegalArgumentException 예외가 발생한다.
     */

//    validate 메소드:
//    매개변수로 받은 password의 길이를 확인하여 8자 미만이거나 12자 초과인 경우 IllegalArgumentException 예외를 발생시킨다
//    비밀번호의 길이만을 검사하고 있으며, 외부에서 비밀번호를 생성하는 정책을 사용하지 않는다.
    public void validate(String password) {
        int length = password.length();

        if (length < 8 || length > 12) {
            throw new IllegalArgumentException("비밀번호는 최소 8자 이상 12자 이하여야 한다.");
        }
    }

//    validate2 메소드:
//    PasswordGeneratePolicy 인터페이스를 구현하는 클래스를 매개변수로 받아 사용한다.
//    passwordGeneratePolicy의 generatePassword 메소드를 호출하여 비밀번호를 생성한 뒤, 해당 비밀번호의 길이를 검사한다
//    generatePassword 메소드는 PasswordGeneratePolicy 인터페이스를 구현하는 클래스에서 구현되는 메소드로, 외부에서 비밀번호 생성 정책을 자유롭게 구현할 수 있도록 한다.
//    validate2 메소드는 다양한 비밀번호 생성 정책을 적용할 수 있도록 유연성을 제공한다.
    public void validate2(PasswordGeneratePolicy passwordGeneratePolicy) {
        String password = passwordGeneratePolicy.generatePassword();

        int length = password.length();
        if (length < 8 || length > 12) {
            throw new IllegalArgumentException("비밀번호는 최소 8자 이상 12자 이하여야 한다.");
        }
    }
}
```

> 즉, validate 메소드는 직접 비밀번호를 전달받아 길이를 검사하는 반면,
> validate2 메소드는 외부에서 비밀번호 생성 정책을 구현한 클래스를 전달받아 해당 정책에 따라 비밀번호를 생성하고 검사한다.
> 이를 통해 validate2 메소드는 다양한 비밀번호 생성 정책을 지원하며,
> PasswordGeneratePolicy 인터페이스를 구현한 클래스를 사용하여 비밀번호를 생성할 수 있다.

## 랜덤 비밀번호 생성기

RandomPasswordGenerator.java

```java
package org.example;

import org.passay.CharacterData;
import org.passay.CharacterRule;
import org.passay.EnglishCharacterData;
import org.passay.PasswordGenerator;

public class RandomPasswordGenerator implements PasswordGeneratePolicy {
    /**
     * Special characters allowed in password.
     */
    public static final String ALLOWED_SPL_CHARACTERS = "!@#$%^&*()_+";

    public static final String ERROR_CODE = "ERRONEOUS_SPECIAL_CHARS";

    @Override
    public String generatePassword() {
        PasswordGenerator gen = new PasswordGenerator();

        // 소문자 설정
        CharacterData lowerCaseChars = EnglishCharacterData.LowerCase;
        CharacterRule lowerCaseRule = new CharacterRule(lowerCaseChars);
        lowerCaseRule.setNumberOfCharacters(2); // 비밀번호에 소문자가 최소 2개 포함되도록 설정

        // 대문자 설정
        CharacterData upperCaseChars = EnglishCharacterData.UpperCase;
        CharacterRule upperCaseRule = new CharacterRule(upperCaseChars);
        upperCaseRule.setNumberOfCharacters(2); // 비밀번호에 대문자가 최소 2개 포함되도록 설정

        // 숫자 설정
        CharacterData digitChars = EnglishCharacterData.Digit;
        CharacterRule digitRule = new CharacterRule(digitChars);
        digitRule.setNumberOfCharacters(2); // 비밀번호에 숫자가 최소 2개 포함되도록 설정

        // 특수 문자 설정
        CharacterData specialChars = new CharacterData() {
            public String getErrorCode() {
                return ERROR_CODE;
            }

            public String getCharacters() {
                return ALLOWED_SPL_CHARACTERS;
            }
        };
        CharacterRule splCharRule = new CharacterRule(specialChars);
        splCharRule.setNumberOfCharacters(2); // 비밀번호에 특수 문자가 최소 2개 포함되도록 설정

        // 0 ~ 12 길이의 비밀번호 생성
        return gen.generatePassword((int) (Math.random() * 13), splCharRule, lowerCaseRule, upperCaseRule, digitRule);
    }
}
```

### 랜덤 비밀번호 출력 결과

main.java

```java
package org.example;

public class Main {
    public static void main(String[] args) {
        RandomPasswordGenerator passwordGenerator = new RandomPasswordGenerator();
        String password = passwordGenerator.generatePassword();
        System.out.println("랜덤 비밀번호 Generated password: " + password);
    }
}

//랜던 비밀번호 출력(RandomPasswordGenerator)
```

![image](https://github.com/solfany/solfany.github.io/assets/123814718/0d2895d9-d012-470d-8832-1277c8412ec7)

RandomPasswordGenerator 비밀번호 랜덤 제조기 ..

코드의 출력결과를 보고 싶어서 메인 클래스에 작성해서 조건에 맞는 비밀번호가 나오는지 궁금해서 작성해보았다..

## 테스트 코드

PasswordValidatorTest.java

```java
import static org.assertj.core.api.Assertions.*;

public class PasswordValidatorTest {

    /**
     * 비밀번호는 최소 8자 이상 12자 이하여야 한다.
     * 비밀번호가 8자 미만 또는 12자 초과인 경우 IllegalArgumentException 예외를 발생시킨다.
     * 경계조건에 대해 테스트 코드를 작성해야 한다.
     */

    // 비밀번호가 8자 이상 12자 이하인 경우, validate 메소드가
		// 예외를 발생시키지 않는지 확인하는 테스트
    @DisplayName("비밀번호가 최소 8자 이상, 12자 이하면 예외가 발생하지 않는다.")
    @Test
    void validatePasswordTest() {

        String password = "serverwizard";
				//PasswordValidator의 클래스의 인스턴스 생성
        PasswordValidator passwordValidator = new PasswordValidator();

        // when, then
        assertThatCode(() -> passwordValidator.validate(password))
                .doesNotThrowAnyException();
    }

    // 비밀번호가 8자 미만 또는 12자 초과하는 경우,
		// validate 메소드가 IllegalArgumentException 예외를 발생시키고,
    // 예외 메시지가 "비밀번호는 최소 8자 이상 12자 이하여야 한다."인지 확인하는 매개변수화 테스트
    @DisplayName("비밀번호가 8자 미만 또는 12자 초과하는 경우 IllegalArgumentException 예외가 발생한다.")
    @ParameterizedTest
    @ValueSource(strings = {"aabbcce", "aabbccddeeffg"})
    void validatePasswordTest2(String value) {
				//PasswordValidator의 클래스의 인스턴스 생성
        PasswordValidator passwordValidator = new PasswordValidator();

        // when, then
        assertThatCode(() -> passwordValidator.validate(value))
                .isInstanceOf(IllegalArgumentException.class)
                .hasMessage("비밀번호는 최소 8자 이상 12자 이하여야 한다.");
    }

    /**
     * 테스트하기 쉬운 코드를 작성하다 보면 더 낮은 결합도를 가진 설계를 얻을 수 있다.
     */

    // 비밀번호가 최소 8자 이상, 12자 이하면 예외가 발생하지 않는지 확인하는 테스트
    @DisplayName("비밀번호가 최소 8자 이상, 12자 이하면 예외가 발생하지 않는다.")
    @Test
    void validatePasswordTest2() {
        // given
        PasswordValidator passwordValidator = new PasswordValidator();

        // when, then
        assertThatCode(() -> passwordValidator.validate2(new CorrectPasswordGenerator()))
                .doesNotThrowAnyException();
    }

    // 비밀번호가 8자 미만 또는 12자 초과하는 경우, IllegalArgumentException 예외가 발생하는지 확인하는 테스트
    @DisplayName("비밀번호가 8자 미만 또는 12자 초과하는 경우 IllegalArgumentException 예외가 발생한다.")
    @Test
    void validatePasswordTest3() {
        // given
        PasswordValidator passwordValidator = new PasswordValidator();

        // when, then
        assertThatCode(() -> passwordValidator.validate2(new WrongPasswordGenerator()))
                .isInstanceOf(IllegalArgumentException.class)
                .hasMessage("비밀번호는 최소 8자 이상 12자 이하여야 한다.");
    }
}
```

**`validatePasswordTest`**:

- 주어진 비밀번호가 8자 이상 12자 이하인 경우, **`PasswordValidator`** 클래스의 **`validate`** 메서드가 예외를 발생시키지 않는지 확인하는 테스트이다
- 예상되는 동작: 주어진 비밀번호가 8자 이상 12자 이하인 경우, 예외가 발생하지 않아야 한다.

**`validatePasswordTest2`**:

- 매개변수화 테스트(Parameterized Test)
  **@ValueSource**를 사용하여 여러 비밀번호 값을 전달하고, 해당 비밀번호가 8자 미만 또는 12자 초과인 경우, **`PasswordValidator`** 클래스의 **`validate`** 메서드가 **`IllegalArgumentException`** 예외를 발생시키고 예외 메시지가 "비밀번호는 최소 8자 이상 12자 이하여야 한다."인지 확인하는 테스트이다.
- 예상되는 동작: 주어진 비밀번호가 8자 미만 또는 12자 초과인 경우, **`IllegalArgumentException`** 예외가 발생하고, 예외 메시지가 정확히 "비밀번호는 최소 8자 이상 12자 이하여야 한다."여야 한다.

**`validatePasswordTest3`**:

- 주어진 비밀번호 생성기(**`CorrectPasswordGenerator`** 또는 **`WrongPasswordGenerator`**)를 사용하여 **`PasswordValidator`** 클래스의 **`validate2`** 메서드를 호출했을 때, 비밀번호가 8자 미만 또는 12자 초과인 경우 **`IllegalArgumentException`** 예외가 발생하는지 확인하는 테스트이다.
- 예상되는 동작: 주어진 비밀번호 생성기를 사용하여 생성된 비밀번호가 8자 미만 또는 12자 초과인 경우, **`IllegalArgumentException`** 예외가 발생해야 한다.

> 따라서, **`validatePasswordTest`**, **`validatePasswordTest2`**, **`validatePasswordTest3`**은 각각 다른 테스트 시나리오를 검증하기 위해 작성된 메서드들이며, 서로 다른 조건을 테스트하기 위해 각각의 테스트 케이스를 사용한다.

- IllegalArgumentException - 자바의 내장 예외 클래스이다.
  이 예외는 메서드에 전달된 인수가 유효하지 않은 경우 발생한다.

일반적으로, **`IllegalArgumentException`**은 메서드의 매개변수나 인수를 유효성 검사하는 과정에서 사용된다. 매개변수가 특정한 범위나 규칙을 위반하는 경우에 예외를 발생시켜 호출자에게 알리는 데 사용된다고 한다.

**`PasswordValidator`** 클래스의 **`validate`** 메서드와 **`validate2`** 메서드에서도 비밀번호의 길이가 유효하지 않을 경우 **`IllegalArgumentException`** 예외를 발생시키고 있다.
이 예외는 호출자에게 비밀번호 유효성 검사 실패를 알리는 용도로 사용된다.
