---
title: "[Network] RAID (Redundant Array of Independent Disks)"
categories:
  - Network
tags: [Network]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

# **RAID 란?**

RAID는 Redundant Array of Independent Disks(또는 Inexpensive Disks)의 약자로, 여러 개의 하드 디스크를 하나의 논리적인 단위로 결합하여 데이터의 안정성과 성능을 향상시키는 기술이다.
RAID를 사용하면 여러 개의 하드 디스크를 동시에 사용하여 데이터를 저장하고, 데이터의 백업 및 복원, 입출력 성능 향상 등을 가능하게 한다.

---

RAID 0 - 이 구성에는 스트라이핑이 있지만 데이터의 중복은 없다.  
최상의 성능을 제공하지만 내결함성은 제공하지 않는다.
RAID 0은 주로 입출력 성능이 중요한 작업에 사용됩니다.

RAID 1 - 디스크 미러링이라고도 하는 이 구성은 데이터 저장소를 복제하는 두 개 이상의 드라이브로 구성
RAID 1은 주로 데이터 안정성이 우선되는 시스템에 사용.

RAID 2 - RAID2는 RAID 0처럼 스트라이핑 구성이지만 일부 디스크에는 오류 검사 및 수정을 위해 ECC(Error Correction Code) 정보가 저장된다.

RAID 3 - RAID 3 구성은 스트라이핑을 사용하고 하나의 드라이브를 패리티 정보를 저장하는데 사용

RAID 4 - 주로 대용량의 순차적인 읽기 작업이 많은 환경에서 사용
그러나 현대의 기술적 발전으로 인해 RAID 5나 RAID 6와 같은 수준에서 더 나은 입출력 성능과 안정성을 제공하는 RAID 구성이 보다 일반적으로 사용다.
따라서 RAID 4는 상대적으로 덜 일반적인 선택지다

RAID 5 - 데이터와 패리티 정보를 여러 디스크에 분산하여 저장.
이로 인해 장애 시에도 데이터를 복구할 수 있으며, 저장 공간의 효율성도 높아짐.
RAID 5는 최소 3개의 디스크가 필요하며, 입출력 성능과 안정성을 균형 있게 제공하는 경우에 많이 사용

RAID 6 - RAID 5와 비슷하지만, 데이터와 패리티 정보를 여러 디스크에 중복 저장하여 안정성을 높인다.
최소 4개의 디스크가 필요하며, RAID 6는 동시에 최대 2개의 디스크 장애를 허용할 수 있다.
RAID 6은 안정성과 데이터 보호가 중요한 환경에서 사용.

RAID 10 (또는 RAID 1+0) - RAID 1과 RAID 0을 조합한 형태로, 데이터를 미러링하고, 그 미러링된 데이터를 스트라이핑한다.
이로 인해 안정성과 입출력 성능이 모두 향상되며, 최소 4개의 디스크가 필요하다. RAID 10은 안정성과 성능 모두를 중요하게 생각함

---

# **구성방식(RAID 0, 1, 4, 5, 6, 1+0, 0+1)**

![img](https://velog.velcdn.com/images/zxcvbnm5288/post/8373760b-279a-4609-a52a-5882ebb1f155/image.png)

## TL; DR

**RAID**는 Redundant Array of Independent Disk 혹은 Redundant Array of Inexpensive Disk의 약자로 말 그대로 RAID는 여러개의 디스크를 묶어 하나의 디스크처럼 사용하는 기술이다

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2Fdf65aa8c-aea8-49e9-a123-f4f47352d13a%2Fimage.png)

## RAID

**RAID**는 Redundant Array of Independent Disk 혹은 Redundant Array of Inexpensive Disk의 약자로 말 그대로 RAID는 여러개의 디스크를 묶어 하나의 디스크처럼 사용하는 기술이다

RAID를 사용할 때 기대효과는

- 대용량의 단일 볼륨을 사용하는 효과
- 디스크 I/O 병렬화로 인한 성능 향상
- 데이터 복제로 인한 안정성 향상

등이 있다

## RAID의 구성방식

### RAID 0

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2Fc992f5fb-f534-454a-8c24-ab36aea9b496%2Fimage.png)

striping이라고도 부르는 방식이다

RAID 0를 구성하기 위해서는 최소 2개의 디스크가 필요하며 RAID를 구성하는 모든 디스크에 데이터를 분할하여 저장한다

전체 디스크를 모두 동시에 사용하기 때문에 성능은 단일 디스크의 N배이며 용량 역시 N배이다

하지만 하나의 디스크라도 문제가 발생할 경우 전체 RAID가 깨지는 일이 발생하기 때문에 안정성은 1/N으로 줄어든다

### RAID 1

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F38c5405c-6c65-4063-8347-6579c63c9144%2Fimage.png)

Mirroring이라고도 부르는 방식이다

RAID 1을 구성하기 위해서는 최소 2개의 디스크가 필요하며 RAID 1은 모든 디스크에 데이터를 복제하여 기록한다

즉, 동일한 데이터를 N개로 복제하여 각 디스크에 저장하는 방식이다

이때문에 여러 개의 디스크로 RAID를 구성해도 실제 사용 가능한 용량은 단일 디스크의 용량과 동일하다

RAID 1의 최대 강점은 안정성이 높다는 것이지만 비용 문제로 인해 거의 사용하지 않는다

### RAID 4

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F1fd3864c-dc41-45f5-8a6d-ab4091f43a98%2Fimage.png)

block단위로 striping을 하고 error correction을 위해 패리티 디스크를 1개 사용한다

용량 및 성능이 단일 디스크 대비 N-1배 증가하며 최소 3개의 디스크로 구성이 가능하다

1개의 디스크가 에러시 복구가 가능하다(2개 이상의 디스크 에러시에는 복구가 불가능)

### RAID 5

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F4c74a7a9-949b-42cc-a99a-43212f304965%2Fimage.png)

block단위로 striping을 하고 error correction을 위해 패리티를 1개의 디스크에 저장한다

단, 패리티 저장은 고정된 디스크에 하지 않고, 매번 다른 디스크에 저장을 한다

(RAID 4의 단점을 개선한 것이라고 보면 된다)

용량 및 성능이 단일 디스크 대비 N-1배 증가하며 최소 3개의 디스크로 구성이 가능하다

### RAID 6

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F51436f99-9606-4886-808b-975d224caed3%2Fimage.png)

RAID 5에서 성능과 용량을 좀 더 줄이고 안정성을 좀 더 높인 방식이다

block단위로 striping을 하고 error correction을 위해 패리티를 2개의 디스크에 저장하는데 패리티 저장은 고정된 디스크에 하지 않고, 매번 다른 디스크에 저장을 한다

용량 및 성능이 단일 디스크 대비 N-2배 증가하며 최소 4개의 디스크로 구성이 가능하다

RAID 5에서 성능과 용량을 조금 줄이는 대신 안정성을 높인 방식이다

### Nested RAID(RAID 1+0, RAID 0+1)

**Nested RAID**는 Standard RAID(일반적인 방식)을 여러개 중첩하여 사용하는 방식이다

예를 들어 2개의 RAID 0를 RAID 1으로 묶는 방식을 RAID 0+1, 반대를 RAID 1+0이라고 한다

### RAID 0+1

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F90c06a8a-62b4-43ca-94fd-c531f3489e7b%2Fimage.png)

mirroring전에 striping을 진행하여 disk가 불량이 나면 그룹핑된 (RAID 0) 데이터 전체를 복구하여야 한다

### RAID 1+0

![img](https://velog.velcdn.com/images%2Fzxcvbnm5288%2Fpost%2F7b4577c7-c12e-4342-9056-9b04dad5f8ab%2Fimage.png)

mirroring후에 striping을 진행하므로 미러링으로 묶인 하드를 통하여 손실된 데이터만을 복원할 수 있다
