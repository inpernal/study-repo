# 7장 SRP: 단일 책임 원칙

D-DAY: D +6
Date: Mar 20, 2021
완료: No

SOLID 원칙 중에서 가장 의미가 잘 전달되지 못한 원칙은 단일 책임 원칙(SRP)이다.

이름 때분에 사람들은 모듈이 단 하나의 일만 해야 한다는 의미로 받아들이기 쉽지만 이 의미는 함수에 적절하다.

재해석 하자면

- 단일 모듈은 변경의 이유가 하나, 오직 하나뿐이어야 한다.
- 하나의 모듈은 하나의, 오직 하나의 액터에 대해서만 책임져야 한다.

액터: 변경을 요청하는 한 명 이상의 사람들

'모듈'은 무슨 뜻일까?

- 가장 단순한 정의는 소스 파일이다.
- 코드를 소스 파일에 저장하지 않는 경우 모듈은 단순히 함수와 데이터 구조로 구성된 응집된 집합이다.

'응집된(cohesive)'이란 단어가 SRP를 암시하며 단일 액터를 책임지는 코드를 함께 묶어주는 힘을 응집성(cohesion)이라 한다.

## 징후 1: 우발적 중복

---

- 서로 다른 액터가 의존하는 코드를 너무 가까이 배치하면 문제가 생긴다.
- SRP는 **서로 다른 액터가 의존하는 코드를 서로 분리하라**고 말한다.

## 징후 2: 병합

---

- 하나의 소스 파일에 다양하고 많은 메서드를 포함하면 병합이 자주 발생한다.
- 병합을 할때는 항상 위험이 뒤따른다.
- **서로 다른 액터를 뒷받침하는 코드를 서로 분리**하여 병합 문제를 해결한다.

## 해결책

---

- 가장 확실한 해결책으로는 데이터와 메서드를 분리하는 것이다.
    - 서로의 존재를 모르고 따라서 '우연한 중복'을 피할 수 있다.
    - 하지만 이는 각각 클래스를 인스턴스화하고 추적해야 한다는 단점이 있다.
    - 위 문제를 해결하는 기법으로 퍼사드(Facade) 패턴이 있다.
- 가장 중요한 메서드만 유지하고 그 클래스를 덜 중요한 메서드들에 대한 퍼사드로 사용할 수도 있다.

## 결론

---

- 단일 책임 원칙은 객체지향에서의 메서드와 클래스 수준의 원칙이다. 하지만 상위 수준에서 다른 형태로도 존재한다.
    - 컴포넌트 수준 → 공통 폐쇄 원칙(Common Closure Principle)이 된다.
    - 아키텍처 수준 → 아키텍처 경계(Architectural Boundary)의 생성을 책임지는 변경의 축(Axis of Change)이 된다.

**Facade Pattern**

```java
/* Complex parts */

class CPU {
	public void freeze() { ... }
	public void jump(long position) { ... }
	public void execute() { ... }
}

class Memory {
	public void load(long position, byte[] data) {
		...
	}
}

class HardDrive {
	public byte[] read(long lba, int size) {
		...
	}
}

/* Façade */

class Computer {
	public void startComputer() {
        CPU cpu = new CPU();
        Memory memory = new Memory();
        HardDrive hardDrive = new HardDrive();
		cpu.freeze();
		memory.load(BOOT_ADDRESS, hardDrive.read(BOOT_SECTOR, SECTOR_SIZE));
		cpu.jump(BOOT_ADDRESS);
		cpu.execute();
	}
}

/* Client */

class You {
	public static void main(String[] args) throws ParseException {
		Computer facade = /* grab a facade instance */;
		facade.startComputer();
	}
}
```