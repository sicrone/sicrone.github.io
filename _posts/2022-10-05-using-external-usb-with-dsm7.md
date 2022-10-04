---
title: "DSM 7.0에서 USB(통신) 사용하기" 
excerpt: "DSN 7.0에서 저장 용도가 아닌 통신 목적(WIFI, Bluetooth, Zigbee 등)의 외장 USB를 사용하기 위한 방법을 설명합니다."
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#E4B1FC"

categories: 
- iot

tags: 
- synology
- dsm 7.0
- 외장 usb
- Zigbee coordinator
- CC2531

---

### 첫번째 방법

DSM 7.0 부터 저장 USB만 사용이 가능하다. 그래서 기존에 WI-FI, Serial, Bluetooth, Zigbee 등 통신 커뮤니케이션 USB들은 직접 설정 해줘야 한다.

- putty 등으로 나스 쉘에 접근
- 로그인 후 루트 권한으로 변경
- modprobe를 이용하여 필요한 내용 수행
- 스크립트 부팅 이벤트에 등록

Zigbee USB (CC2531)의 경우는 ACM 장비이므로 `/sbin/modprobe cdc-acm` 이렇게 수행하면 된다.

상기 방법은 매 부팅 시 반복해서 실행해야 한다.

### 두번째 방법

1. **제어판 - 작업 스케줄러 - 생성 - 트리거된 작업 - 사용자 정의 스크립트**을 클릭하여 새 작업 생성

2. **사용자**는 `root`로 지정

3. **이벤트**는 `부트업`으로 지정

4. **작업 설정탭 - 사용자 정의 스크립트**에서 아래의 스크립트 입력 후 저장
   
   ```
   chmod 777 /dev/ttyUSB0
   chmod 777 /dev/ttyACM0
   /sbin/modprobe usbserial
   /sbin/modprobe ftdi_sio
   /sbin/modprobe cdc-acm
   ```

이 방법은 매 부팅시마다 자동 실행되므로 한번만 작성해놓으면 된다.
