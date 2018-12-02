# Gradle

## Gradle Script

1. 모든 Gradle script는 Script interface를 구현체로 실행된다.
2. Script 객체에는 대리 객체가 첨부됩니다. 예를 들어 빌드 스크립트에는 Project 인스턴스가 첨부되고 초기화 스크립트에는 Gradle 인스턴스가 첨부됩니다. 이 Script 개체에서 찾을 수없는 속성 참조 나 메서드 호출은 대리자 개체로 전달됩니다.

* [https://docs.gradle.org/current/dsl/org.gradle.api.Script.html](https://docs.gradle.org/current/dsl/org.gradle.api.Script.html)

## build.gradle

1. gradle 로 실행하는 groovy script 파일 - 그래서 위에서 순차적으로 실행한다.
2. script 가 실행되면 Project 의 인스턴스로 실행된다.
3. 
* [https://docs.gradle.org/current/userguide/writing\_build\_scripts.html](https://docs.gradle.org/current/userguide/writing_build_scripts.html)
* [https://docs.gradle.org/current/dsl/org.gradle.api.Project.html](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html)

 

## buildscript

빌드 스크립트 자체에 필요한 repository 및 dependency 관리등을 설정한다.

```groovy
import org.apache.commons.codec.binary.Base64

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'commons-codec:commons-codec:1.2'
    }
}

task encode {
    doLast {
        def byte[] encodedString = new Base64().encode('hello world\n'.getBytes())
        println new String(encodedString)
    }
}
```

* buildscript block 는 Script 객체의 



