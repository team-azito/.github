# 백엔드
## 기술 스택

- Java 17
- Spring Boot
- Spring Security
- Spring Data Jpa
- Lombok
- H2, MySQL
- Spring Rest Docs
- Junit 5, AssertJ, RestAssured
- Docker, Github Actions

## 역할 분담

- 이도현: 회원 가입 및 로그인
- 권찬: 투표 기능

## 개발 과정

- 기능별로 이슈 생성
- 깃 플로우에 따라 브랜치 이름을 `feature/#이슈번호-내용`으로 작성
- 기능 구현을 마친 뒤에 PR을 날려 리뷰를 하고 수정사항이 없으면 머지

## ERD
<image src="https://github.com/team-azito/.github/assets/116694226/29cb3d24-7647-45f8-82f9-8bd62f08be10" height="500">

<image src="https://github.com/team-azito/.github/assets/116694226/a0d3ac6e-fe71-4a40-b20c-a0b406c2de23" height="500" width="700">

## API 문서

[API 문서의 링크](http://43.200.141.226/docs/index.html)는 다음과 같습니다.

백엔드 과제에서 사용한 Swagger가 아니라 `Spring Rest Docs`를 사용해서 API 문서를 작성했습니다.

### Spring Rest Docs를 사용한 이유

Swagger는 API를 테스트해 볼 수 있다는 장점이 있을 뿐만 아니라 Swagger UI가 개인적으로 보기에는 더 이뻤습니다. 그럼에도 불구하도 Swagger를 사용하지 않은 이유는 다음과 같이 프로덕션 코드에서 문서와 관련된 애노테이션들이 붙어 코드가 지저분해지기 때문입니다.

컨트롤러 뿐만 아니라 DTO까지도 Swagger에 의존하게 됩니다. 이를 분리하고자 `Spring Rest Docs`를 사용했습니다.

```java
@Tag(name = "User Controller", description = "사용자 API")
@RestController
@RequiredArgsConstructor
@RequestMapping("/api/users")
public class UserController {

    private final UserService userService;

    @Operation(summary = "회원 가입", description = "회원 가입을 합니다.")
    @PostMapping
    public ResponseEntity<Void> signUp(@RequestBody final UserSaveRequestDto request) {
        userService.saveUser(request);
        return ResponseEntity.status(HttpStatus.CREATED).build();
    }
}
```

최대한 프로덕션 코드와 문서와 관련된 코드를 분리하고 싶었을 뿐만 아니라, 과제를 진행하면서 테스트 코드를 꼼꼼하게 작성하고 싶었습니다. `Spring Rest Docs`를 사용하면 문서 생성을 위해 해당 기능에 대한 테스트 코드를 작성해야 합니다. 테스트가 성공적으로 통과해야 문서가 생성되므로, 자연스럽게 **테스트 코드 작성을 강제**할 수 있습니다.

테스트 코드를 작성함으로써 코드의 신뢰성을 높일 수 있었습니다.

# 서브모듈

중요한 정보(applicatoin.yml, env 등)를 외부에 노출하지 않기 위해 서브 모듈을 사용했습니다.

![image](https://github.com/team-azito/.github/assets/116694226/7c45eedf-9af3-4198-96d0-8bb73e1c3cfb)

서브모듈은 private 레포지토리를 하나 생성해서 쉽게 등록할 수 있습니다.


# 프론트엔드
[발표자료](https://mellow-ziconium-509.notion.site/7-2e76b29db8504be1aa5184d6234779bc)

