# Section 4 : Spring PSA (7/6)

## Portable Service Abstraction
### 추상화를 통해 기술을 내부에서 작동시킴 + 같은 코드를 다양한 기술 스택에 적용 가능
* Servelet 직접 구현하지 않고 Annotation만으로도 매핑
* 거의 같은 코드로 톰캣, 제티, 네티, 언더토우 등 기술 스택 적용 가능

## Spring Web MVC
* `@Controller` : 클래스가 Controller 기능 수행
* `@GetMapping`, `@PostMapping` 등 : 요청을 코드와 mapping

## Spring Transaction
* `@Transactional` : 명시적인 코드 없이 atomic 작업 보장

## Spring Cache
* `@Cachable` : 구현체 직접 구현 없이 Cache Managing
