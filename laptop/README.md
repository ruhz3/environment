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

### 03. Scala 개발 환경 구성
```
# 0. jdk 설치
sudo apt install openjdk-11-jdk

# 1. Scala 설치 (cs setup)
curl -fL https://github.com/coursier/coursier/releases/latest/download/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup

# 2. IntelliJ Scala Plugin 설치

# 3. IntelliJ 에서, Settings > Build, Execution, Deployment > Build Tools > sbt > sbt project: sbt shell > Allow overring sbt version 을 uncheck.
```
build.properties에 버전을 지정하면, sbt의 version을 지정하여 사용할 수 있다(지정하지 않으면 latest를 default로 가져온다). 그런데 3번 과정을 진행하지 않으면, build.properties의 지정 버전을 무시하고 IntelliJ 자체적으로 latest 버전으로 덮어쓰는 경우가 있다.