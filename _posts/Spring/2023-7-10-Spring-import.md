---
title: "[Java]외부 파일 import 또는 export"
categories:
  - Spring
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

# 외부 파일 import

## Spring 프로젝트 불러오기, 내보내기 (Import, Export)

![img](https://t1.daumcdn.net/cfile/tistory/99BBC0495AF8562001)

Package Explorer에 마우스 오른쪽 클릭 후 Import... 클릭

![img](https://t1.daumcdn.net/cfile/tistory/99BE343A5AF84C3813)

General,Git,Maven등 여러 종류를 import할 수 있지만 다운로드된 프로젝트를 불러오기 위해

General에서 Existing Projects into Workspace를  선택

General엔 5개의 형태를 불러올 수 있는데

Archive File - 압축된 파일을 불러올 경우

Existing Projects into Workspace - 프로젝트를 불러올 경우 (압축된 프로젝트도 포함, 사용 권장)

File System - 특정 파일만 선택해서 import할 때 사용 (java, jsp, xml 등)

Preferences - 스프링, 이클립스 환경변수를 불러올 때 사용

Projects from Folder or Archive - 폴더, 압축 형식 파일 불러옴

(Existing Projects into Workspace와 다른점은 사용자가 설정한 Maven,JRE등을 못 불러 올 수 있음)

![img](https://t1.daumcdn.net/cfile/tistory/99C27C395AF9B06E1B)

import할려는 프로젝트가 폴더로 돼있으면 Select root directory 선택 후 Browse...클릭

압축 파일 형태로 돼있으면 Select archive file 선택 후 Browse...클릭

![img](https://t1.daumcdn.net/cfile/tistory/99E0D4405AF9B3B016)

프로젝트를 폴더/압축파일을 선택 후 열기

![img](https://t1.daumcdn.net/cfile/tistory/99D27D405AF9B3B126)

하단의 Finish 클릭

![img](https://t1.daumcdn.net/cfile/tistory/99E7AF405AF9B3B224)

좌측 Package Explorer에 프로젝트가 생성되면 Import 완료

# Export(내보내기)

![img](https://t1.daumcdn.net/cfile/tistory/99383D375AF9B90D29)

내보내기 할려는 프로젝트 마우스 오른쪽 클릭 후 Export... 클릭

![img](https://t1.daumcdn.net/cfile/tistory/99D0C2375AF9B90D0E)

General에서 내보내기 형식을 선택

---

Archive File - 압축 형식으로 내보내기

File System - 파일 형식으로 내보내기

Preferences - 프로젝트의 환경변수를 내보내기

![img](https://t1.daumcdn.net/cfile/tistory/9952C9375AF9B90E25)

Browse... 클릭 후 저장할 경로와 파일명을 지정해준 후 Finish 클릭하면

파일을 가져오고 내보낼 수 있게 된다.
