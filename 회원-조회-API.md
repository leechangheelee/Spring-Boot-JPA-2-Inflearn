## **API 개발 기본**

![image](https://user-images.githubusercontent.com/79301439/177965904-cba095ec-024e-4f9b-89e0-ae0ade21348d.png)

```java
// ...
@RestController
@RequiredArgsConstructor
public class MemberApiController {
  
    private final MemberService memberService;
  
    // ...
  
    @GetMapping("/api/v1/members")
    public List<Member> membersV1() {
        return memberService.findMembers();
    }
  
    // ...
  
}
```

![image](https://user-images.githubusercontent.com/79301439/177966453-fdb99cfa-2d82-42db-aaae-105cc6c08636.png)

![image](https://user-images.githubusercontent.com/79301439/177966541-90034845-464b-41fe-adcd-40bb871e1672.png)

![image](https://user-images.githubusercontent.com/79301439/177966594-9d0b8717-93e6-49a4-95f6-7ca76477929c.png)

```java
    // ...

    @GetMapping("/api/v2/members")
    public Result memberV2() {
      
        List<Member> findMembers = memberService.findMembers();
        //엔티티 -> DTO 변환
        List<MemberDto> collect = findMembers.stream()
                .map(m -> new MemberDto(m.getName()))
                .collect(Collectors.toList());

        return new Result(collect.size(), collect);
    }

    @Data
    @AllArgsConstructor
    static class Result<T> {
        private int count;
        private T data;
    }

    @Data
    @AllArgsConstructor
    static class MemberDto {
        private String name;
    }

    // ...
```

![image](https://user-images.githubusercontent.com/79301439/177966843-d0893520-4a26-40b5-9459-40d351ad5114.png)
