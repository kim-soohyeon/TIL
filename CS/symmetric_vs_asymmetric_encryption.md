# 대칭 키 vs 비대칭 키 암호화

**암호화 (Encryption)**: 평문을 의미를 알 수 없는 암호문으로 변환하는 과정

**복호화 (Decryption)**: 암호문을 원래의 평문으로 되돌리는 과정

---

## 대칭 키 암호화 (Symmetric Key Encryption)

대칭 키 암호화는 암호화와 복호화에 **동일한 키**를 사용하는 방식입니다. 이 방식은 **속도가 빠르고 효율적**이지만, 키를 안전하게 공유하는 것이 어렵다는 단점이 있습니다. 대표적인 대칭 키 암호화 알고리즘은 다음과 같습니다.

### 주요 대칭 키 암호화 알고리즘 및 키 길이

- **DES (Data Encryption Standard)**: 64비트 (실제 키 길이는 56비트)
- **3DES (Triple DES)**: 112비트 또는 168비트
- **AES (Advanced Encryption Standard)**: 128비트, 192비트, 256비트
- **ARIA**: 128비트, 192비트, 256비트
- **SEED**: 128비트
- **LEA (Lightweight Encryption Algorithm)**: 128비트, 192비트, 256비트

보안성을 위해 **최소 128비트 이상의 키 길이**를 사용하는 것이 권장됩니다.

---

## 블록 암호화 모드 (Block Cipher Modes)

블록 암호화는 데이터를 일정한 크기의 **블록 단위**로 나누어 암호화하는 방식입니다. 각 블록을 암호화하는 방식에 따라 다양한 모드가 존재합니다.

### 1. **ECB (Electronic Codebook Mode)**

- 블록 단위로 독립적으로 암호화
- **같은 입력값은 항상 같은 암호문**을 생성 (패턴 분석이 가능하여 보안 취약)
- 일반적으로 사용을 **권장하지 않음**

### 2. **CBC (Cipher Block Chaining Mode)**

- 이전 블록의 암호화 결과를 다음 블록 암호화에 **연결**하여 보안성을 강화
- *초기 벡터(IV, Initialization Vector)**를 사용하여 첫 번째 블록을 암호화
- ECB보다 **보안성이 강함**

## 패딩 방식 (Padding Schemes)

블록 암호화에서는 데이터 크기가 블록 크기의 배수가 되지 않을 경우 **패딩을 추가하여 크기를 맞춤**.

- **PKCS#5**: 블록 크기가 8바이트일 때 사용
- **PKCS#7**: 최대 255바이트까지 패딩 가능 (AES 같은 16바이트 블록 암호화에 사용)

**자바에서는 PKCS5Padding을 사용하더라도 내부적으로 PKCS7Padding으로 동작함.**

---

## 암호문 인코딩 (Ciphertext Encoding)

암호화된 데이터는 **이진 데이터** 형태이므로, 이를 문자열로 변환하기 위해 **Base64 인코딩**을 사용하여 전송 및 저장할 수 있습니다.

---

## 자바 AES 예제 코드 (CBC 모드)

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.IvParameterSpec;
import java.util.Base64;

public class AESExample {
    public static void main(String[] args) throws Exception {
        // 128비트 AES 키 생성
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        keyGenerator.init(128);
        SecretKey secretKey = keyGenerator.generateKey();

        // 초기 벡터(IV) 생성
        byte[] iv = new byte[16];
        IvParameterSpec ivParameterSpec = new IvParameterSpec(iv);

        // 암호화
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, ivParameterSpec);
        String plainText = "Hello, World!";
        byte[] encryptedBytes = cipher.doFinal(plainText.getBytes());
        String encryptedText = Base64.getEncoder().encodeToString(encryptedBytes);
        System.out.println("Encrypted: " + encryptedText);

        // 복호화
        cipher.init(Cipher.DECRYPT_MODE, secretKey, ivParameterSpec);
        byte[] decryptedBytes = cipher.doFinal(Base64.getDecoder().decode(encryptedText));
        String decryptedText = new String(decryptedBytes);
        System.out.println("Decrypted: " + decryptedText);
    }
}
```

### 코드 설명

1. **AES 키 생성**: `KeyGenerator`를 사용하여 128비트 AES 키 생성
2. **IV(초기 벡터) 생성**: `IvParameterSpec`을 사용하여 16바이트 IV 설정
3. **암호화**: `Cipher` 클래스를 사용하여 AES CBC 모드로 암호화 수행
4. **복호화**: 암호문을 다시 복호화하여 원래의 평문을 출력

---

## 비대칭 키 암호화 (Asymmetric Key Encryption)

비대칭 키 암호화는 **암호화와 복호화에 다른 키를 사용하는 방식**입니다. **공개 키(Public Key)**로 암호화하고, **비밀 키(Private Key)**로 복호화하는 방식입니다.

### 비대칭 키 개념

- **공개 키 (Public Key)**: 암호화에 사용되며, 누구에게나 공개 가능
- **비밀 키 (Private Key)**: 복호화에 사용되며, 절대 노출되면 안 됨

비대칭 키 암호화는 **보안성이 뛰어나지만 속도가 느리다는 단점**이 있습니다.

### 대표적인 비대칭 키 암호화 알고리즘

- **RSA** (Rivest-Shamir-Adleman)
- **DSA** (Digital Signature Algorithm)
- **ECC** (Elliptic Curve Cryptography)

---

## 자바 RSA 암호화 예제

```java
import java.security.*;
import javax.crypto.Cipher;
import java.util.Base64;

public class RSAExample {
    public static void main(String[] args) throws Exception {
        // 키 생성
        KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
        keyGen.initialize(2048);
        KeyPair keyPair = keyGen.generateKeyPair();
        PublicKey publicKey = keyPair.getPublic();
        PrivateKey privateKey = keyPair.getPrivate();

        // 암호화
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        String plainText = "Hello, RSA!";
        byte[] encryptedBytes = cipher.doFinal(plainText.getBytes());
        String encryptedText = Base64.getEncoder().encodeToString(encryptedBytes);
        System.out.println("Encrypted: " + encryptedText);

        // 복호화
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        byte[] decryptedBytes = cipher.doFinal(Base64.getDecoder().decode(encryptedText));
        String decryptedText = new String(decryptedBytes);
        System.out.println("Decrypted: " + decryptedText);
    }
}
```

---

## 대칭 키 vs 비대칭 키 비교

| 구분 | 대칭 키 암호화 | 비대칭 키 암호화 |
| --- | --- | --- |
| 키 개수 | 1개 | 2개 (공개 키, 비밀 키) |
| 속도 | 빠름 | 느림 |
| 보안성 | 키 공유 문제 있음 | 높은 보안성 |
| 사용 예시 | 파일 암호화, VPN | 전자서명, SSL/TLS |

대칭 키는 속도가 빠르지만 키 공유가 어렵고, 비대칭 키는 보안성이 높지만 속도가 느립니다. 보통 **하이브리드 방식**으로 두 가지를 함께 사용합니다.
