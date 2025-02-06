# 데이터 무결성과 제약 조건

## **데이터 무결성**

데이터 무결성이란 **데이터에 오류가 없고, 정확하며, 일관성을 유지하는 성질**을 의미합니다. 즉, 데이터가 변형되거나 누락되지 않고, 신뢰할 수 있는 상태로 유지되는 것을 보장합니다.

예를 들어, 회원가입 기능을 구현할 때 **아이디 중복을 체크하는 코드만으로는 데이터 무결성을 완벽히 보장할 수 없습니다.** 그 이유는 **동시성 문제(concurrency issue)**를 고려하지 않았기 때문입니다. 두 명의 사용자가 동시에 동일한 아이디로 가입을 시도하면, 각각의 요청은 아이디가 사용 가능한 상태라고 판단하여 중복된 아이디가 등록될 수 있습니다.

이처럼 **코드만으로 데이터 무결성을 보장하는 것은 어렵기 때문에, DBMS에서 제공하는 무결성 제약 조건을 활용하는 것이 중요합니다.**

---

## **DBMS에서 제공하는 세 가지 무결성**

1. **개체 무결성 (Entity Integrity)**
    
    테이블의 특정 열에 **중복된 값이 들어가지 않도록 강제하여 무결성을 보장**하는 것입니다. 개체 무결성을 보장하기 위해 테이블을 생성할 때 **UNIQUE** 또는 **PRIMARY KEY** 제약 조건을 설정해야 합니다.
    
2. **참조 무결성 (Referential Integrity)**
    
    **테이블 간의 관계를 유지하는 무결성 제약**입니다. 데이터 중복을 방지하기 위해 한 테이블에서 **외래 키(Foreign Key)**를 설정하여 다른 테이블을 참조하도록 합니다. 이를 통해 **참조된 데이터가 삭제되거나 변경될 때, 관련된 데이터도 함께 처리되도록 강제하여 무결성을 유지**합니다.
    
3. **도메인 무결성 (Domain Integrity)**
    
    특정 열에 입력될 수 있는 값의 범위를 제한하여 **허용된 값만 저장되도록 강제하는 무결성 제약**입니다. 예를 들어, 학생의 학년을 1~6 사이의 값으로 제한하려면 **CHECK** 제약 조건을 사용하여 `CHECK (GRADE BETWEEN 1 AND 6)`과 같이 설정할 수 있습니다.
    

---

## **DBMS에서 제공하는 제약 조건**

데이터 무결성을 보장하기 위해서는 **애플리케이션 코드 수준에서 검증하는 것뿐만 아니라, DBMS의 제약 조건을 함께 활용하는 것이 중요합니다.**

- **UNIQUE** : 중복되지 않는 유일한 값만 허용하며, `NULL` 입력이 가능합니다.
- **NOT NULL** : `NULL` 값을 허용하지 않고 반드시 값이 입력되도록 합니다.
- **CHECK** : 특정 조건을 만족하는 값만 입력할 수 있도록 제한합니다.

### **CHECK 제약 조건의 예제**

**1. 성인 회원 가입 조건 - 나이는 18세 이상**

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Username VARCHAR(50) NOT NULL,
    Age INT CHECK (Age >= 18) -- 나이는 18세 이상
);
```

✅ `Age` 값이 `17` 이하이면 회원가입이 제한됩니다.

**2. 직원(EMPLOYEE) 테이블에서 급여(SALARY)는 30만 원 이상만 허용**

```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    SALARY INT CHECK (SALARY >= 300000) -- 급여는 최소 30만 원 이상
);
```

✅ 급여가 `299999` 이하면 입력할 수 없습니다.

**3. 주문(ORDER) 테이블에서 결제 상태(STATUS)는 특정 값만 허용**

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(50) NOT NULL,
    STATUS VARCHAR(20) CHECK (STATUS IN ('PENDING', 'COMPLETED', 'CANCELLED'))
);
```

✅ `STATUS` 값은 `'PENDING'`, `'COMPLETED'`, `'CANCELLED'` 중 하나만 가능합니다.
