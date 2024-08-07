# [JavaScript] location.replace와 location.href의 차이점

JavaScript를 사용하여 웹 페이지를 다른 URL로 이동시키는 방법에는 여러 가지가 있습니다. 그중에서 `location.replace`와 `location.href`는 가장 자주 사용되는 두 가지 방법입니다. 이 글에서는 `location.replace`와 `location.href`의 정의와 차이점을 살펴보고, 각각의 활용 예시에 대해 설명하겠습니다.

---

### 1. `location.href`란?

`location.href`는 JavaScript에서 현재 페이지의 URL을 변경하여 사용자를 다른 페이지로 이동시키는 속성입니다. 이는 브라우저의 주소창에 새로운 URL을 설정하는 것과 동일합니다.

**특징:**

- **브라우저 기록에 저장됨**: 사용자가 뒤로 가기 버튼을 클릭하면 이전 페이지로 돌아갈 수 있습니다.
- **페이지 리디렉션**: 페이지가 새로운 URL로 변경되며, 서버로부터 새 페이지를 로드합니다.

**사용 예시:**

- **상황**: 사용자가 페이지를 탐색하면서 이전 페이지로 쉽게 돌아갈 수 있어야 하는 경우.
- **코드**:
    
    ```jsx
    // 사용자가 'https://example.com/about' 페이지로 이동
    location.href = 'https://example.com/about';
    ```
    

### 2. `location.replace`란?

`location.replace`는 현재 페이지를 새로운 URL로 교체하는 방법입니다. 이 방법은 브라우저의 기록을 변경하지 않기 때문에 뒤로 가기 버튼을 클릭해도 이전 페이지로 돌아갈 수 없습니다.

**특징:**

- **브라우저 기록에 저장되지 않음**: 사용자가 뒤로 가기 버튼을 클릭해도 이전 페이지로 돌아갈 수 없습니다.
- **페이지 리디렉션**: 페이지가 새로운 URL로 변경되며, 서버로부터 새 페이지를 로드합니다.

**사용 예시:**

- **상황**: 로그인 후 사용자가 다시 로그인 페이지로 돌아가지 않도록 해야 하는 경우.
- **코드**:
    
    ```jsx
    // 로그인 후 사용자를 'https://example.com/dashboard'로 이동시키며, 이전 페이지 기록을 남기지 않음
    location.replace('https://example.com/dashboard');
    ```
    

### 3. `location.href`와 `location.replace`의 차이점

| 특징 | location.href | location.replace |
| --- | --- | --- |
| 브라우저 기록 | 기록에 남음 | 기록에 남지 않음 |
| 뒤로 가기 버튼 지원 | 사용 가능 | 사용 불가능 |
| 사용 사례 | 일반적인 페이지 이동 | 로그인 후 메인 페이지로 이동 등 |

---

---

### 결론

`location.href`와 `location.replace`는 모두 페이지를 다른 URL로 이동시키는 데 유용하지만, 그 사용 목적과 상황에 따라 적절한 방법을 선택하는 것이 중요합니다. `location.href`는 브라우저 기록을 남기므로 사용자가 뒤로 가기 버튼을 사용할 수 있는 경우에 적합합니다. 반면, `location.replace`는 기록을 남기지 않으므로 사용자가 특정 페이지로 돌아가면 안 되는 경우에 유용합니다.

이 두 가지 방법을 잘 이해하고 적절히 활용하여 사용자에게 더 나은 경험을 제공하는 웹 애플리케이션을 개발해 보세요!
