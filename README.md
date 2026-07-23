# make_portable_ubuntu
외장 SSD를 사용해 어디서든 부팅 가능한 ubuntu 22.04 만들기.
&nbsp;  
&nbsp;    
&nbsp;    
  
# 사용 디바이스
- 오리코 썬더볼트 4/3 40Gbps 호환 M.2 NVMe 외장 SSD 케이스 AAGM2-U4
- SK하이닉스 Gold P31 M.2 NVMe (512GB)
- 메인보드 Asus B850M Max gaming wifi
- 128GB USB (최소 8GB도 가능)

# 우분투 OS 설치하기
## 준비물
- 우분투 22.04 Desktop: https://releases.ubuntu.com/jammy/
- Rrfus: https://rufus.ie/ko/
- 외장 SSD
- OS설치용 USB (최소 8GB)
- 본 가이드는 명령줄을 많이 사용합니다. Tab키(자동완성)기능 사용을 적극 권장합니다.

**USB및 SSD는 데이터가 전부 날아갑니다. 중요한 데이터가 없거나 비어있는 저장 장치를 사용합니다.**
&nbsp;
&nbsp;   
&nbsp;   

## Rufus 실행(당시 버전 4.14)
**장치**: OS설치용 USB선택
**부팅 선택**: 다운받은 우분투(https://releases.ubuntu.com/jammy/) iso 파일 선택   
**영구 파티션 크기**: 어차피 SSD를 통째로 포맷하고 새로 깔 것이기 때문에 이 옵션은 건드리지 않고 0으로 두어도 무방합니다.   
**파티션 구성**: GPT(구형 컴퓨터 호환이 필요 시 MBR)   
**대상 시스템**: GPT선택 시 알아서 바뀝니다. (UEFI (비 CSM))   
**나머지**: 기본값   

**USB 안에 있던 파일은 전부 삭제됩니다**
---> 시작 ---> OK ---> ISO 이미지 모드로 쓰기(권장) 선택 후 OK ---> OK

초록 바가 전부 채워지면 USB 완성
USB 내용물을 확인하고 많이 채워져 있으면 다음 단계로 갑니다.

## SSD에 우분투 설치 
💡 [강력 추천] 삽질을 줄이는 최고의 꿀팁!  
    >컴퓨터 본체를 열 수 있는 환경이라면, 우분투를 설치하기 전에 Windows가 깔린 기존 내장 하드(NVMe, SATA SSD 등)의 전원이나 선을 잠시 뽑아두고 작업하시는 것을 강력히 권장합니다.  
    >컴퓨터에 설치용 USB와 외장 SSD만 연결된 상태로 진행하면, 우분투가 엉뚱한 곳에 부트로더를 심는 버그를 원천 차단할 수 있습니다.  
    >이 방법을 쓰시면 뒤에 나오는 '부트로더 분실 문제' 및 'Emergency Mode 오류' 탭을 전부 무시하고 한 방에 성공할 수 있습니다!


    
1. 컴퓨터에 우분투 부팅 USB와 우분투를 설치할 외장 SSD를 둘 다 꽂습니다.
2. 컴퓨터 전원을 켜자마자 메인보드 제조사에 맞는 BIOS/UEFI 진입 단축키를 연타합니다.(보통 F2, F12, Del, F11중 하나)
3. BIOS/UEFI 화면 진입 후 부팅 디스크 선택 화면에서 USB를 1순위로 놓고 F10을 눌러 재부팅 합니다. 혹은 직접 부팅 기기를 USB로 선택해서 부팅합니다.
&nbsp;
&nbsp;   
&nbsp;

## 우분투 라이브 환경 진입(영어 기준)
1. 검은 화면에 GNU GRUB메뉴가 뜨면 첫 번째 항목인 Try or Install Ubuntu를 선택하고 엔터를 누릅니다.
2. 우분투 로고가 지나간 뒤 설치 환영 창이 뜨면 언어 설정 후 Ubuntu 설치(Install Ubuntu) 버튼을 클릭합니다.
3. 키보드 레이아웃을 선택합니다.(English(US) 선택)
4. 서트파티 소프트웨어를 체크합니다.
5. Installaion Type에서 Something else를 선택합니다. (Erase disk and install Ubuntu는 절대 금지)  &nbsp;  
Size(용량) 필드를 보고 내가 연결한 외장 SSD의 용량(예: 약 500GB 내외)과 일치하는 디스크 장치명(/dev/sdX 또는 /dev/nvmeXn1)을 반드시 확인하세요!
6. 외장 SSD를 선택하고 +버튼을 누릅니다. Size는 넉넉히 1024MB, EFI System Partition 선택 후 확인
7. 다시 +버튼을 누릅니다. 남은 공간 전부지정, Ext4 journaling File System 선택, mount point는 "/"로 설정 후 -> OK
8. Device for boot loader installation: [중요!]외장 SSD의 장치명으로 변경 후 Install now 버튼을 클릭합니다. 꼭 제대로 확인하고 설치합시다!
9. 거주지역(Seoul), 선택 후 사용자 이름과 비밀번호를 설정하면 설치가 시작됩니다.
10. 설치 후 지금 다시 시작 팝업이 뜹니다. 화면에 (Please remove the installation medium...)가 나오면 USB만 뽑고 엔터를 누릅니다. 외장 SSD로 부팅합니다. 아까 USB로 부팅했던 방법을 사용합니다.

  
**우분투 설치는 완료**  

## 문제
그렇다면 이제 다른 컴퓨터에서도 SSD를 꽂고 바이오스 진입해서 부팅 우선순위를 바꾸면 우분투로 부팅 해야합니다만, 해보니 블루 스크린이 뜨거나 우분투 켜라니까 애먼 윈도우 파일만 찾아댑니다. 이는 부트로더 경로 및 인식 문제이며, 앞으로 설명합니다.  

## 부트로더 문제 해결
컴퓨터 메인보드에는 NVRAM이라는 비휘발성 메모리가 있습니다. 여기에는 "우리 컴퓨터에는 윈도우 부트로더가 어느 디스크, 어느 파티션에 있다"라는 정보가 주소록 형태로 등록되어 있습니다.  
  
**문제 발생 이유**: 우분투를 설치했던 내 컴퓨터에는 설치 과정에서 우분투의 위치가 이 주소록에 자동으로 등록됩니다. 하지만 외장 SSD를 뽑아 다른 윈도우 컴퓨터에 꽂으면 그 컴퓨터의 주소록에는 내 외장 SSD의 우분투 주소가 당연히 등록되어 있지 않습니다.  

'컴퓨터 전원 켬 -> efi/EFI/BOOT에서 부트로더 찾아야지 -> 없네? 그럼 나도 안켜'라는 흐름으로 안켜집니다.  
  
**해결방법**: 그럼 EFI/BOOT 경로에 BOOTX64.EFI등의 파일을 넣으면 되겠네요.
  
## 문제 해결 시작
우선 아까 파티션을 나눠서 EFI System을 설치 했습니다.(1024MB 로 나눴던 그것) 그러니 부트로더는 SSD안에 잘 있을 겁니다. 그걸 모든 컴퓨터가 약속한 주소록 자리에 복사해서 넣어주면 됩니다.

우선 명령줄을 켭니다.
```bash
sudo fdisk -l
```
자신의 외장 SSD를 찾고, 이름을 확인합니다. 여기서는 /dev/sdc라고 가정합니다. 사람마다 이름이 전부 다르므로 자신의 외장 SSD를 용량 등을 단서로 잘 확인합시다.

/dev/sdc보면 아래쪽에 이와 같이 나옵니다
```plaintext
장치(Device)  시작 위치  종료 위치  섹터 수  용량   종식(Type)
/dev/sdc1        000        000      000     000    BIOS boot
/dev/sdc2        000        000      000     1024M  EFI System  <---- 요거
/dev/sdc3        000        000      000     000    Linux filesystem
```

이제 /dev/sdc2를 마운트 해서 내부를 봅시다. 
```bash
#/dev/sdc2를 /mnt로 마운트한다.
sudo mount /dev/sdc2 /mnt     

# /mnt 내부 확인
ls /mnt
```
원래라면 ubuntu와 BOOT파일이 있을 것입니다. 만약 아무것도 안뜨면 유서깊은 버그가 발생한 겁니다. "EFI안에 ubuntu, BOOT가 없어요..." 탭으로 넘어가세요

## CASE1: ubuntu와 BOOT파일이 있어요
```plaintext
/mnt (외장 SSD의 EFI 파티션)
└── EFI/
    ├── ubuntu/          
    │   ├── grubx64.efi
    │   ├── shimx64.efi
    │   └── mmx64.efi
    └── BOOT/            
        └── BOOTX64.EFI
```
이렇게 예쁘게 파일이 들어있는 상황이라면 ubuntu 파일 안의 내용물을 BOOT안에 넣어줍시다.
```bash
# BOOT가 없다면 새로 생성
sudo mkdir -p /mnt/EFI/BOOT

# 파일 위치로 이동
cd /mnt/EFI/BOOT/

# ubuntu 안의 파일들을 현재 폴더(BOOT)로 복사
sudo cp ../ubuntu/* ./

# 우분투의 shimx64.efi 파일을 메인보드가 인식할 수 있도록 BOOTX64.EFI라는 이름으로 복사본 생성
sudo cp shimx64.efi BOOTX64.EFI

# 목록 확인
ls -l
```
아래와 같으면 성공입니다.
```plaintext
/mnt (외장 SSD의 EFI 파티션)
└── EFI/
    ├── ubuntu/          
    │   ├── grubx64.efi
    │   ├── shimx64.efi
    │   └── mmx64.efi
    └── BOOT/            
        ├── BOOTX64.EFI   <-- 🎉 shimx64.efi의 복사본으로 교체됨
        ├── grubx64.efi   <-- 🎉 새로 복사된 파일
        ├── shimx64.efi   <-- 🎉 새로 복사된 파일
        └── mmx64.efi     <-- 🎉 새로 복사된 파일
```
이제 안전하게 마운트를 끊고 재시작 합니다.
```bash
# 마운트 된 파일에서 나오기
cd ~
# 마운트 해제
sudo umount /mnt
```

## CASE2: EFI안에 ubuntu, BOOT가 없어요...
만약 EFI안에 ubuntu파일 및 BOOT가 없다면 부트로더를 SSD가 아닌현재 컴퓨터 본체의 내장 하드(윈도우 EFI 파티션)에 강제로 심어버린 버그가 발생한 것입니다. 본체 하드에서 부트로더를 탈취해 와야 합니다.
EFI 조차 없다면 먼저,
```bash
# EFI 만들어주기
sudo mkdir /mnt/EFI

# 마운트 풀기
sudo umount /mnt
```
를 실행 합니다.

```bash
# 부트로더 위치 확인
sudo fdisk -l
```
여기서 아까 확인했던 나의 SSD 및 버그로 원래 컴퓨터(윈도우 기준)의 부트로터가 심어진 파일을 찾습니다.  

자신의 외장 SSD를 찾고, 이름을 확인합니다. 여기서는 /dev/sdc라고 가정합니다. 사람마다 이름이 전부 다르므로 자신의 외장 SSD를 용량 등을 단서로 잘 확인합시다.

추가로 자신의 컴퓨터의 OS가 설치된 디스크를 찾습니다. 여기서는 /dev/sda라고 가정합니다. 물론 사람마다 이름 다르니 잘 확인합시다. (이외에도 nvme0n1p2같은 이름도 있습니다.)

```bash
# 임시 마운트 폴더 2개 생성
sudo mkdir -p /mnt/internal_efi
sudo mkdir -p /mnt/external_efi

# 내장 하드의 EFI 파티션 마운트 (예: sda1)
sudo mount /dev/sda1 /mnt/internal_efi

# 외장 SSD의 EFI 파티션 마운트 (예: sdc2)
sudo mount /dev/sdc2 /mnt/external_efi
```

내 컴퓨터 하드에 탈취 당했던 ubuntu 폴더를 외장 SSD의 EFI 폴더 안으로 그대로 복사해 옵니다.

```bash
# 내장 하드에 숨어있던 ubuntu 폴더를 외장 SSD의 EFI 폴더로 복사
sudo cp -r /mnt/internal_efi/EFI/ubuntu /mnt/external_efi/EFI/
```

**[핵심]** BOOT 폴더 만들고 안을 채웁니다.
```bash
# 1. 외장 SSD의 EFI 폴더 안에 BOOT 폴더 생성 (이미 있으면 생략 가능)
sudo mkdir -p /mnt/external_efi/EFI/BOOT

# 2. 외장 SSD의 BOOT 폴더로 이동
cd /mnt/external_efi/EFI/BOOT/

# 3. 조금 전 복사해 온 ubuntu 폴더의 파일들을 BOOT 폴더로 복사
sudo cp -r ../ubuntu/* ./

# 4. 안전 부팅(Secure Boot) 환경에서 메인보드가 인식할 수 있도록 shimx64.efi를 BOOTX64.EFI로 복사본 생성
sudo cp shimx64.efi BOOTX64.EFI
```
아래는 최종 구조이며, 이와 같으면 끝났습니다!   

   
```plaintext
/mnt/external_efi (외장 SSD의 EFI 파티션)
└── EFI/
    ├── ubuntu/          
    │   ├── grubx64.efi
    │   ├── shimx64.efi
    │   └── mmx64.efi
    └── BOOT/            
        ├── BOOTX64.EFI   <-- 메인보드가 가장 먼저 읽는 마스터 파일 (shimx64.efi의 복사본)
        ├── grubx64.efi   
        ├── shimx64.efi   
        └── mmx64.efi

BOOTX64.csv 파일은 무시하셔도 됩니다.
```

## 마운트 해제 및 재시작 
```bash
cd ~

# 두 파티션 모두 안전하게 언마운트
sudo umount /mnt/internal_efi
sudo umount /mnt/external_efi
```
이후 다른 컴퓨터에 SSD 꽂고 재시작 해서 f2(제조사 마다 다름)을 연타해 바이오스/UEFI화면 진입, SSD로 부팅 하면 우분투 화면이 로딩 될 것입니다.

## 또 다른 문제들
### 🔍 증상
외장 SSD로 부팅을 시도했으나 아래와 같은 검은 에러 화면이 뜨며 멈춤 현상 발생.
```bash
> `Failed to open \EFI\BOOT\mmx64.efi - Not Found`
> `Failed to load image : Not Found`
> `Something has gone seriously wrong: import_mok_state() failed: Not Found`
```
### 💡 원인
다른 컴퓨터의 메인보드(예: Phoenix UEFI 등)의 Secure Boot(안전 부팅) 메커니즘이 우분투의 보안 인증 파일인 `mmx64.efi`를 표준 경로(`EFI/BOOT/`)에서 강제로 요구하기 때문입니다.

### 🛠️ 해결 방법 (2가지 중 선택)
* **방법 A:** 해당 컴퓨터의 BIOS 설정 진입 ➡️ `Security` 또는 `Boot` 탭 ➡️ **`Secure Boot`를 `Disabled`로 변경** 후 재부팅 (가장 빠름).
* **방법 B:** 만약 BIOS 진입이 안 되거나 메인보드 버그로 계속 요구할 경우, 원래 컴퓨터에서 외장 SSD의 EFI 파티션을 마운트한 뒤 다음과 같이 수동으로 파일을 채워줍니다.
  ```bash
  # EFI 파티션 마운트 (예: sdc2)
  sudo mount /dev/sdc2 /mnt
  
  # 우분투 폴더에 있는 mmx64.efi를 BOOT 폴더로 복사
  sudo cp /mnt/EFI/ubuntu/mmx64.efi /mnt/EFI/BOOT/
  ```
  (🚨 주의: 만약 ubuntu 폴더 안에도 mmx64.efi가 없다면, 타 컴퓨터에서 우분투 순정 ISO를 열어 내부의 mmx64.efi 파일을 추출해와야 합니다. 다른 efi 파일의 이름을 바꾸어 대체하면 부팅 에러가 납니다.)

### 🔍 증상2
부트로더 문제를 해결하여 우분투 로고까지는 떴으나, 무한 로딩 후 아래와 같은 텍스트 화면으로 빠짐.

/dev/sdX: clean, ... files, ... blocks
You are in emergency mode. After logging in, type "journalctl -xb" to view system logs...

### 💡 원인
외장 SSD 내부의 마운트 설정 파일인 /etc/fstab에 원래 컴퓨터 본체의 내장 드라이브 UUID를 마운트하라는 고정 명령이 남아있었기 때문입니다. 컴퓨터를 옮기니 해당 드라이브(예: 원래 컴퓨터의 내장 EFI 파티션 등)를 찾지 못해 시스템이 비상을 선언한 것입니다.

### 🛠️ 해결 방법
외장 SSD가 다른 컴퓨터의 하드웨어를 기웃거리지 않고 독립적으로 작동하도록 설정을 수정해야 합니다.

1. 비상 모드 화면에서 Enter를 눌러 터미널 권한을 얻습니다.
2. 설정을 수정할 수 있도록 루트 파티션을 읽기/쓰기 모드로 다시 엽니다.
```bash
mount -o remount,rw /
```
3. 텍스트 편집기로 마운트 설정 파일을 엽니다.
```bash
nano /etc/fstab
```
4. 파일 내부를 확인하고, 외장 SSD 본인의 주소(예: / 루트 파티션)를 제외한 원래 컴퓨터의 내장 드라이브 경로 줄 맨 앞에 #을 붙여 주석(무시) 처리합니다.
&nbsp;  
🚨[주의]!!!외장 SSD 자체의 EFI 파티션 줄은 주석 처리하면 안 되며, 오직 원래 컴퓨터의 내장 하드 관련 줄만 주석 처리해야 합니다!!!🚨

⭕ 예시: # UUID=8574-9482 /boot/efi vfat umask=0077 0 1 (맨 앞에 # 추가)
(※ 주의: 루트 파티션인 / 가 적힌 줄은 절대로 건드리면 안 됩니다.)

5. Ctrl + O ➡️ Enter (저장) 후 Ctrl + X (종료)로 빠져나옵니다.

6. 다시 시작. 시스템이 완전히 먹통일 경우 아래 명령어로 강제 리부팅합니다.
```bash
reboot -f
```
여기까지만 해도 일단 부팅은 됩니다.   
&nbsp;  
&nbsp;    
&nbsp;    

## 안정성 추가 
이후 본인 SSD의 UUID를 fstab파일에 넣어줍니다. 먼저 터미널을 열고,
```bash
sudo blkid
```
우분투가 설치된 기기의 UUID를 확인합니다.
&nbsp;  
  
```plaintext
/dev/sdd3: UUID="a1c2e3gh-ab00-0000-a5a4-a5s5f6d7f8g9" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="a1s2d3f4-a1s2-a1s2-a1s2-a1s2d3f4g5h6"
```
와 같이 적혀있습니다. ext4는 우분투의 파일 관리 시스템으로, 윈도우랑 다르니 이걸 단서로 찾아봅시다.  
&nbsp;  
   
그리고 우분투가 설치된 기기의 EFI 파티션 UUID를 확인 합니다.
&nbsp;  
  
```
/dev/sdd2: UUID="A1A1-B2B2" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="aasdfsadf-asdf-4asd-9asd-asdfasdfasdf"
```

와 같이 적혀있습니다. 이번에는 TYPE="vfat"을 단서로 찾아봅시다. 또한 위의 UUID경로와 같은 이름(/sdd)을 단서로 찾아봅시다.   


```bash
sudo nano /etc/fstab
```

텍스트 편집기로 fstab를 엽니다.  
ssd기기 자체의 UUID는 이미 존재하니, 외장 드라이브 자체 EFI 부트 파티션만 기록해 주면 됩니다.

```plaintext
# 원래 있던 것
UUID=a1c2e3gh-ab00-0000-a5a4-a5s5f6d7f8g9 /               ext4    errors=remount-ro 0       1

# 외장 드라이브 자체 EFI 부트 파티션 (/dev/sdd2)
UUID=A1A1-B2B2                            /boot/efi       vfat    umask=0077      0       0    <-여기

# 아까 주석 처리한 다른 기기의 UUID
# /boot/efi was on /dev/nvme0n1p2 during installation
# UUID=1111-1111  /boot/efi       vfat    umask=0077      0       
```
🚨 복사 붙여넣기 말고 반드시 본인의 UUID를 넣으세요!
글자 사이 공백은 1칸이든 여러 칸이든 상관 없습니다. 
&nbsp;  
"ctl+o" -> "enter" -> "ctl+x"로 나오고 재부팅 해봅니다.
&nbsp;  
&nbsp;    
&nbsp;    
진짜 끝!
