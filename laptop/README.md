# laptop
## Hardware
```
$ arch
$ getconf LONG_BIT
```
- x86_64 | 64bit
- 8GB | 512GB

## Install

### 00. IDE 설치
- VSCode : https://code.visualstudio.com/docs/setup/linux#_installation
- PyCharm : https://www.jetbrains.com/ko-kr/pycharm/download/?section=linux
- IntelliJ : https://www.jetbrains.com/ko-kr/idea/download/?
section=linux 

위 목록의 경로에서 직접 설치 파일을 다운로드 받는다.\
VSCode는 Software Installer로 설치한다.\
PyCharm, intelliJ는 /opt 아래 예시와 같이 설정한다.
```commandline
# 0. /opt에 압축 해제
sudo tar -zxf pycharm-community-2023.2.tar.gz /opt

# 1. pycharm 실행
/opt/pycharm-community-2023.2/bin/pycharm.sh

# 2. 프로젝트 생성 후, 상단 메뉴 > Tools > Create Desktop Entry 

# 3. Ubuntu 작업 표시줄에서 Add to Favorites
```

### 01. anaconda 설치
- anaconda : https://www.anaconda.com/
```commandline
# 0. anaconda 설치  
chmod +x Anaconda3-2023.07-1-Linux-x86_64.sh
./Anaconda3-2023.07-1-Linux-x86_64.sh
### (필수X) 설치 시, anaconda3 경로를 .anaconda3로 바꿔줬다.

# 1. sample 환경 생성 
conda create -n sample python=3.10

# 2. pycharm 연동 확인
# Pycharm 우측 하단 > Add Local Interpreter > Conda Excutable
#  > "~/.anaconda3/condabin/conda.py"
```

### 02. microk8s 설치 
```commandline
# 0. microk8s 설치
sudo snap install microk8s --classic --channel=1.25/stable
sudo microk8s enable dashboard dns hostpath-storage ingress

# 1. kubectl alias 설정
mkdir ~/.kube
microk8s config view > ~/.kube/config
export KUBECONFIG=$KUBECONFIG:$HOME/.kube/config
sudo snap alias microk8s.kubectl kubectl

# 2. kubernetes dashboard ingress 설정
# (웹 브라우저에서 localhost/dashboard -> ~/.kube/config 파일로 접속)
kubectl apply -f ./resources/dashboard-ingress.yaml
```
