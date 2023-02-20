---
title: Webinars/2023/Advanced Kotlin Techniques for Spring Developers
---

Advanced Kotlin Techniques for Spring Developers
===

The webinar was offered by JetBrains, you can also find the recording on
their [YouTube channel](https://www.youtube.com/watch?v=cjpSaeIfq9M).

## Validation

- JSR 305 compiler option for kotlin adds @NotNull annotations for
kotlin non-nullables ` -Xjsr305=strict`


## JPA

- Gradle plugin for Kotlin JPA generates no arg constructor
- hashCode should return technical id -> something i saw the first time,
usually you see the typcial *calculate all attributes one*
- data class is not only a bad idea because of immutability but also
because of the unnecessary methods created for this usecase

## Extensions

- there are kotlin extensions for the most common parts in the spring
framework already e.g. query for Spring JDBC
- bean/s function allows DSL bean registration, but is not a replacement for `@Bean` methods in Spring Boot
  ```kotlin
  fun main(args: Array<String>) {
      runApplication<DemoApplication>(*args) {
        addInitializers(
            beans {
                // Define your bean with Kotlin DSL here
            }
        )
    }
  }
  ```

## Security

- [ref](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.native.ref/)
  can also be used to transform security DSL into a more kotlinish DSL (also
  works in beans block, could also be just return value for `@Bean`
  annotated method)
  ```kotlin
  val http = ref<HttpSecurity>()
  http {
    csrf {
        disable()
    }
  }
  http.build()
  ```
  
  > ref generally also works outside of spring and is a kotlin builtin feature
