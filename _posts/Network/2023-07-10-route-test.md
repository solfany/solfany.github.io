---
title: "[Network] router 시험 데모"
categories:
  - Network
tags: [Network]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

Q1 . ROUTER2의 호스트 이름을'ICQA'로 설정하시오.

(호스트 이름은 대소문자를 구분하며 완료된 설정은 startup-config에 저장하시오.)

---

![image](https://github.com/solfany/solfany.github.io/assets/123814718/cca1817e-aca9-46bc-acc9-b43e95b7a670)

```bash
enable

config terminal //해당 명령을 통해 구성모드로 지입

hostname ICQA //장비의 이름을 ICQA로 설정

exit //이전 모드로 전환

copy running-config startup-config //해당 명령은 현재 실행중인 설정을 실행할 때 자동으로 로드 되는 설정을 복사한다.
```

해당 명령어 처럼 라우터 실습을 할 수 있다.

![image](https://github.com/solfany/solfany.github.io/assets/123814718/85242410-615f-46c7-ae9e-35380f8fa20f)

```bash
en

con t

l c 0 //라인 콘솔 0번

end //이전으로 돌아가기

copy r s //해당 명령은 현재 실행중인 설정을 실행할 때 자동으로 로드 되는 설정을 복사한다.
```

모든 명령어는 en으로 시작하여 copy r s 로 끝난다.
