## **API 개발 기본**

![image](https://user-images.githubusercontent.com/79301439/177952219-24352781-8eaf-4b75-a77a-f688ee655b97.png)

```java
    /**
     * 수정 API
     */
    @PutMapping("/api/v2/members/{id}")
    public UpdateMemberResponse updateMemberV2(
            @PathVariable("id") Long id,
            @RequestBody @Valid UpdateMemberRequest request) {

        memberService.update(id, request.getName());
        Member findMember = memberService.findOne(id);
        return new UpdateMemberResponse(findMember.getId(), findMember.getName());
    }

    @Data
    static class UpdateMemberRequest {
        private String name;
    }

    @Data
    @AllArgsConstructor
    static class UpdateMemberResponse {
        private Long id;
        private String name;
    }
```

![image](https://user-images.githubusercontent.com/79301439/177952439-267196e7-d588-4cc4-af87-6cf6dc4e6d4e.png)

```java
// ...
public class MemberService {

    private final MemberRepository memberRepository;

    // ...

    /**
     * 회원 수정
     */
    @Transactional
    public void update(Long id, String name) {
        Member findMember = memberRepository.findOne(id);
        findMember.setName(name);
    }
}
```

![image](https://user-images.githubusercontent.com/79301439/177953071-e076ea90-43f1-45e3-a618-9734c0b73b53.png)
