# STEP2_build_example
## 1. 뉴로메카 홈페이지에서 STEP2용 SDK를 다운로드합니다.
```bash
wget https://s3.ap-northeast-2.amazonaws.com/download.neuromeka.com/SDK-Installer/PlatformSDK/STEP2-Linux/NRMKPlatformPC2_v3.0.5_b20191001.tar.gz
tar xvf NRMKPlatformPC2_v3.0.5_b20191001.tar.gz
```
## 2. 설치를 진행합니다. 
 ```bash
  cd NRMKPlatformPC2_v3.0.5_b20191001
  bash install.sh
  source /opt/neuromeka/NRMKFoundation/script/nrmk_env.sh
 ```
## 3. example이 설치된 폴더로 이동합니다.
```bash
  cd /opt/neuromeka/NRMKPlatformPC2/example/workspace
```
## 4. Repository를 다운받고 빌드를 진행합니다.
```bash
  cd /opt/neuromeka/NRMKPlatformPC2/example/workspace
  git clone https://github.com/tjdalsckd/STEP2_build_example.git
  cd STEP2_build_example
  mkdir build
  cd build
  cmake ..
  make -j16
```
## 5. 빌드 후에 나온 실행파일을 STEP에 옮긴 후 실행합니다.
```
  scp HYU_SPA user@192.168.0.39:/home/user/release
  
```
