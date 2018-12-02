# Gradle

## Gradle Script \(init.gradle, settings.gradle, build.gradle ..\)

1. Gradle 은 빌드를 설정하는 DSL을 제공하며 Groovy와 Kotlin으로 사용 가능
2. 모든 Gradle script는 Script interface를 구현체로 생성된다.  그래서 gradle script는 script interface 의 모든  속성과 메서드에 access 할 수 있습니다.
3. Script 객체에는 대리 객체\(delegate object\)

   가 첨부됩니다. 예를 들어 빌드 스크립트에는 Project 인스턴스가 첨부되고 초기화 스크립트에는 Gradle 인스턴스가 첨부됩니다. 이 Script 개체에서 찾을 수없는 속성 참조 나 메서드 호출은 대리자 개체로 전달됩니다.

```text
dependencies {
    assert delegate == project.dependencies
    testCompile('junit:junit:4.12')
    delegate.testCompile('junit:junit:4.12')
}
```

| Script Type | File | Delegates to instance of |
| :--- | :--- | :--- |
| Inits script | init.gradle | Gradle |
| Settings script | settings.gradle | Settings |
| Build script | build.gradle | Project |

* [https://docs.gradle.org/current/dsl/org.gradle.api.Script.html](https://docs.gradle.org/current/dsl/org.gradle.api.Script.html)

## build.gradle = Project

1. 각 프로젝트에 대해 Gradle 는 Project 객체를 만들고 Project객체를 빌드 스크립트와 연결합니다. 
2. Project객체는 빌드 스크립트에 엑세스하기 위한 출발점입니다.
3. 따라서 빌드 스크립트에 메서드나 속성을 활용하려면 [Project Interface ](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html%20)에서 참고하면 됩니다. 
   * 빌드 스크립트에서 호출하는 모든 메소드 \(빌드 스크립트에 _정의되지 않음\)_ 는 `Project`오브젝트에 위임됩니다 .
   * 빌드 스크립트에서 액세스하는 모든 속성 \(빌드 스크립트에 _정의되지 않음\)_ 은 `Project`객체에 위임됩니다 .

{% code-tabs %}
{% code-tabs-item title="build.gradle" %}
```text
println name
// Project 객체에 project 라는 자기 자신을 참조하는 속성이 있습니다.
// name 을 사용하는 것보다 project.name을 사용하면 가독성 및
// 메서드나 클로저와 같이 다른 Scope 범위에서 프로젝트 속성에 액세스 할 수 있습니다.
println project.name

> gradle -q check
projectApi
projectApi
```
{% endcode-tabs-item %}
{% endcode-tabs %}

| 프로젝트 표준 속성 예시 |  |  |
| :--- | :--- | :--- |
| 이름 | 유형 | 기본값 |
| `project` | Project | `Project 자기 참조` |
| `name` | `String` | 프로젝트 명 |
| `group` | `Object` | 프로젝트 그룹명 |
| `version` | `Object` | `프로젝트 버전` |
| `path` | `String` | 프로젝트의 절대 경로. |
| `description` | `String` | 프로젝트 설명. |
| `projectDir` | `File` | 빌드 스크립트가 들어있는 디렉토리. |
| `buildDir` | `File` | `빌드 Working 디렉토리, /build` |
| `ant` | [AntBuilder](https://docs.gradle.org/current/javadoc/org/gradle/api/AntBuilder.html) | `AntBuilder 참조` |

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



