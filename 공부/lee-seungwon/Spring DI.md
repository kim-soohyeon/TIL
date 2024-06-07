### **의존성 주입(Dependency Injection)** ###
- 객체를 직접 생성하는것이 아닌 외부에서 생성 후 주입하는 방식.
- 가독성과 재사용성을 높여줌.

### **Autowired annotation을 이용한 DI 방법 3가지**
- **Field Injection(필드 주입)**
    - class에 속한 field 위에 @Autowired 선언한 방식.
- **Setter Injection(수정자 주입)**
    - setter 메소드에 @Autowired 선언한 방식.
    - Spring 3 까지 권장하는 방식.
- **Constructor Injection(생성자 주입)**
    - final 키워드 사용이 가능.
    - 생성자를 통해 주입 되는 방식.
    - @Autowired 선언을 생략 가능.
    - Spring 4.3 부터 현재 가장 권장하는 방식.
    - 순환 참조 되는 설계를 사전에 막기 위해 사용


