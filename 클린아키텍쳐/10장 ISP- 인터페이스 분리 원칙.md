# 10장 ISP: 인터페이스 분리 원칙

<img width="593" alt="스크린샷 2021-03-28 14 14 56" src="https://user-images.githubusercontent.com/21329617/112743171-fbc62080-8fcf-11eb-843e-0bfa97ad0e0c.png">

 ISP는 위 다이어그램에서 이름이 유래했다.

- `User1: op1`, `User2: op2`, `User3: op3`  사용한다고 가정하면
  - OPS클래스가 정적타입언어로 작성된 클래스라면
  - User1의 소스코드는 op2, op3를 사용하지 않음에도 의존성을 가지게 된다.
  - OPS 클래스에서 op2 소스코드가 변경되면 User1도 재컴파일이 필요하다.
- 이러한 문제는 오퍼레이션을 인터페이스 단위로 분리하여 해결할 수 있다.

<img width="615" alt="스크린샷 2021-03-28 14 15 04" src="https://user-images.githubusercontent.com/21329617/112743175-008ad480-8fd0-11eb-984a-f43aaeda5f77.png">


### ISP와 언어

- 언어 타입 (정적, 동적..)에 따라 소스 코드 의존성 여부가 다르다
- 따라서 ISP를 아키텍처가 아니라, 언어와 관련된 문제라고 결론내릴 여지가 있다.



### ISP와 아키텍처

- 필요 이상으로 많은 걸 포함하는 모듈에 의존하는 것은 해로운 일이다.
- 불필요한 재컴파일과 재배포를 강제하기 때문이다.
- 아키텍처 수준에서도 마찬가지 상황이 발생한다. 
  - SYSTEM -> FRAMEWORK -> DATABASE



### 결론

- 불필요한 짐을 실은 무언가에 의존하면 예상치도 못한 문제에 빠진다.



---

[Reference]

- Clean Architecture (로버트 C.마틴)