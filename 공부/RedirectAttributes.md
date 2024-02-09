### **RedirectAttributes** ###
- 스프링프레임워크의 인터페이스
- Redirect을 수행 할 때 데이터를 전달하는데 이용되는 방법중 하나
- RedirectAttributes 클래스를 통해 String 형태의 object 형태로 넘김

### **RedirectAttributes을 이용한 데이터 전달 방법 2가지 메서드**
- addAttribute
- addFlashAttribute

- **addAttribute**
    - URL에 정보 노출이 있다
    - /URL?key=value 형식 전달 
- **addFlashAttribute**
    - URL에 정보 노출이 없다
    - 임시로 저장하는 방식
    - 세션에 저장되어 사용된 뒤에 자동으로 삭제된다.
