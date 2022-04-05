# Docker
컨테이너 기반의 오픈소스 가상화 플랫폼

## Container
플랫폼에 상관없이 Application을 실행할 수 있는 기술을 의미<br>
도커를 이용하여 각종 Application들을 어떤 환경에서든 자유롭게 사용할 수 있다.(+ 버전 관리와 배포를 도와줌)<br>
<b>To summarize, a container:</b>
1. is a runnable instance of an image. You can create, start, stop, move, or delete a container using the DockerAPI or CLI.
2. can be run on local machines, virtual machines or deployed to the cloud.
3. is portable (can be run on any OS)
4. Containers are isolated from each other and run their own software, binaries, and configurations.

## Docker를 사용할 때의 흐름 감잡기
1. 도커 CLI에 커맨드를 입력한다.
2. 도커 서버 (Docker Daemon)이 그 커맨드를 받아서 그것에 따라 이미지를 생성하든 컨테이너를 실행하는 모든 작업을 하게 된다.

![image](https://user-images.githubusercontent.com/62804036/161577294-2cf6a8a4-c153-439d-8344-e7d59eb26585.png)

### 설명
1. 도커 클라이언트에 커맨드를 입력하니 클라이언트에서 도커 서버로 요청을 보냄
2. 서버에서 hello-world라는 이미지가 이미 로컬에 cache가 되어 있는지 확인
3. 현재는 없기에 Unable to Find image~라는 문구가 2번째 줄에 표시
4. 그러면 Docker Hub이라는 이미지가 저장되어 있는 곳에 가서 그 이미지를 가져오고 로컬에 Cache로 보관
5. 그 후 이제는 이미지가 있으니 그 이미지를 이용해서 컨테이너를 생성
6. 그리고 이미지로 생성된 컨테이너는 이미지에서 받은 설정이나 조건에 따라 프로그램을 실행<br>
![image](https://user-images.githubusercontent.com/62804036/161578092-8a4ebb32-a173-4946-a820-4873daeb03d2.png)
7. 이제 hello-world 이미지가 캐시가 되어 있으니 한 번 더 docker run hello-world를 실행하면
![image](https://user-images.githubusercontent.com/62804036/161578437-9baad098-f5e0-4b56-a60d-e700dc59695a.png)
8. Unable to find image~라는 문구가 없이 프로그램이 실행됨.
9. 결국은 캐쉬 된 이미지를 이용해서 컨테이너를 만든 후 프로그램을 실행.

## 도커 이미지로 컨테이너를 만들기
도커 이미지 : 컨테이너를 만들기 위해 필요한 설정이나 종속성들을 갖고 있는 소프트웨어 패키지

### 이미지는 응용 프로그램을 실행하는데 필요한 모든 것을 포함
### 필요한 모든 것?
1. 컨테이너가 시작될 때 사용되는 명령어 ex) run kakaotalk
2. 파일 스냅샷 ex)컨테이너에 카카오톡을 실행하고 싶다면 카카오톡 파일(카카오톡을 실행하는데 필요한 파일) 스냅샷
*  파일 스냅샷은 디렉토리나 파일을 카피한 것

### 이미지로 컨테이너 만드는 순서
1. Docker클라이언트에 docker run<이미지> 입력
2. 도커 이미지에 있는 파일 스냅샷을 컨테이너 하드 디스크에 옮겨준다.
3. 이미지에 가지고 있는 명령어 (컨테이너가 실행될 때 사용될 명령어)를 이용해서 파일을 실행시켜 준다.

## 도커 이미지 생성하는 순서
도커 파일 작성 ▶ 도커 클라이언트 ▶ 도커 서버 ▶ 이미지 생성 <br>
* 도커 파일 : 도커 이미지를 만들기 위한 설정 파일. 컨테이너가 어떻게 행동해야 하는지에 대한 설정을 정의
* 도커 클라이언트 : 도커 파일에 입력된 명령어들이 도커 클라이언트에 전달되어야 함
* 도커 서버 : 도커 클라이언트에 전달된 모든 중요한 작업들을 하는 곳

### Dockerfile을 만들기
Dockerfile : 도커 이미지를 만들기 위한 설정 파일, 컨테이너가 어떻게 행동해야 하는지에 대한 설정들을 정의해 주는 곳

### Dockerfile만드는 순서 (도커 이미지가 필요한 것이 무엇인지를 생각하기)
Dockerfile작성 ▶ 도커 클라이언트 ▶ 도커 서버 ▶ 이미지 생성 <br>

1. 베이스 이미지를 명시(파일 스냅샷에 해당)
2. 추가적으로 필요한 파일을 다운받기 위한 몇 가지 명령어를 명시 (파일 스냅샷에 해당)
3. 컨테이너 시작 시 실행될 명령어를 명시 (시작 시 실행될 명령어에 해당)

#### 베이스 이미지
- 도커 이미지는 여러개의 레이어들로 되어 있다. 그 중에서 베이스 이미지는 이 이미지의 기반이 되는 부분
- 레이어는 중간 단계의 이미지라고 생각하면 된다.
![image](https://user-images.githubusercontent.com/62804036/161752233-1568822c-d6b9-49b7-a5ee-8f692547003b.png)
- 베이스 이미지에 레이어들이 쌓여서 이미지가 됨


## Practice
### hello world를 출력하는 도커 파일 만들기
1. dockerfile을 만들 폴더 하나 만들기
2. dockerfile폴더를 에디터를 이용해서 실행
3. 파일 하나를 생성 ex)dockerfile
4. 그 안에 먼저 어떻게 진행해 나갈지 기본적인 토대를 명시
![image](https://user-images.githubusercontent.com/62804036/161762163-fca33b01-9ad5-4b14-b8a5-73ef827f3ce5.png)
<b>FROM RUN CMD 등은 도커 서버에게 무엇을 하라고 알려주는 것</b>
* FROM
  * 이미지 생성 시 기반이 되는 이미지 레이어
  * <이미지 이름>:<태그> 형식으로 작성
  * 태그를 안 붙이면 자동적으로 가장 최신 것으로 다운 받음
* RUN
  * 도커 이미지가 생성되기 전에 수행할 쉘 명령어
* CMD
  * 컨테이너가 시작되었을 때 실행할 실행 파일 또는 쉘 스크립트
  * 해당 명령어는 DockerFile 내 1회만 쓸 수 있음
5. 이제 베이스 이미지부터 실제 값 추가해주기
6. 베이스 이미지는 ubuntu를 써도 되고 centos 등을 써도 되지만 hello를 출력하는 기능은 굳이 사이즈가 큰 베이스 이미지를 쓸 필요가 없기에 사이즈가 작은 alpine 베이스 이미지를 사용
7. hello 문자를 출력해주기 위해 echo를 사용하게 할 수 있는 파일이 있기에 RUN 부분은 생략
8. 마지막으로 컨테이너 시작 시 실행될 명령어 echo hello를 적어줌
![image](https://user-images.githubusercontent.com/62804036/161763265-e0236793-db10-4043-8da6-ea80be6778fa.png)
### 도커 파일로 도커 이미지 만들기
#### 완성된 도커 파일로 어떻게 이미지를 생성하는지
도커 파일 ▶ 도커 클라이언트 ▶ 도커 서버 ▶ 이미지 <br>
도커 파일에 입력된 것들이 도커 클라이언트에 전달되어서 도커 서버가 인식하게 해야함 <br>
그렇게 하기 위해서 docker build ./ 또는 docker build . <br>
Build 명령어는
* 해당 디렉토리 내에서 dockerfile이라는 파일을 찾아서 도커 클라이언트에게 전달시켜줌
* docker build 뒤에 ./와 .는 둘 다 현재 디렉토리를 가리킴
그래서 docker build .를 해보면 <br>
![image](https://user-images.githubusercontent.com/62804036/161767778-818dec5e-ae1b-40f2-99b7-0dac5e7fefee.png)
#### 실행과정 정리
![image](https://user-images.githubusercontent.com/62804036/161766918-afdb5065-c807-4f9f-a682-d342460b93a7.png)
1. 베이스 이미지 alpine 이미지를 먼저 다운
2. alpine 파일 스냅샷은 임시 컨테이너 하드디스크에 넣기
3. 실행할 명령어를 컨테이너 안에 넣기
4. 임시 컨테이너를 기반으로 새로운 이미지 만들기(그리고 임시 컨테이너는 삭제)
#### 실행
![image](https://user-images.githubusercontent.com/62804036/161767905-f7f4b040-e08c-49d2-9d3e-310f06e09eed.png)
sha256:4026~~ 이 부분 코드(imageID)를 넣어서 run 해주면 된다. <br>

## 리액트를 위한 도커 파일 작성하기
도커로 어플을 실행하기 위해서는 <br>
![image](https://user-images.githubusercontent.com/62804036/161770834-0a92609f-cc3d-4db4-a168-86d8a722f1d1.png)
* 실제로는 Dockerfile을 개발단계를 위한 것과 실제 배포 후를 위한 것을 따로 작성하는게 좋음 그러므로 개발단계를 위해서 Dockerfile이 아닌 Dockerfile.dev라는 파일을 작성!

#### node이미지 사용
alpine이미지는 가장 최소한의 경량화된 파일들이 들어있기에 npm을 위한 파일이 들어있지 않아서 RUN부분에 npm install을 할 수가 없음 <br>
npm이 들어있는 베이스 이미지를 찾아야 함 <br>
그것들중 하나가 바로 node 이미지 <br>

![image](https://user-images.githubusercontent.com/62804036/161773504-86bfc150-5689-4478-9eb0-7d1bd07c889c.png) <br>
❗ 원래 있던 node_modules파일은 지워준다 << 용량이 커지므로

![image](https://user-images.githubusercontent.com/62804036/161774670-eaa57c66-7d10-4f60-9f25-fd00beba76cd.png)<br>
![image](https://user-images.githubusercontent.com/62804036/161775114-151b640e-8577-47de-8899-a1f4802a22cb.png)<br>
![image](https://user-images.githubusercontent.com/62804036/161775358-72e6b12b-9df4-4de9-a1fa-6c6fe4a001a4.png)<br>
localhost로 react실행이 안됨❗❗❗ <br>
WHY?!이유는 아래에 👇👇👇<br>


## 생성한 이미지로 어플리케이션 실행 시 접근이 안되는 이유(포트 맵핑)
![image](https://user-images.githubusercontent.com/62804036/161777934-84670175-c6c5-442e-9398-9f8872e4352f.png)
#### 새롭게 추가된 부분은 무엇을 위한 부분인가? 포트맵핑!
기존에 이미지를 만들 때 로컬에 있던 파일(package.json)등을 컨테이너에 복사해줘야 했었음 <br>
그것과 비슷하게 네트워크도 로컬 네트워크에 있던 것을 컨테이너 내부에 있는 네트워크에 연결을 시켜줘야 함 <br>
![image](https://user-images.githubusercontent.com/62804036/161778056-3b2eb9a6-e829-406d-b0a0-8e541c753e1e.png)<br>
-p 3000 : 3000 👉 p(port) 3000번으로 접근을 하면 컨테이너 안의 3000번으로 접근을 가능하게 하라는 의미 <br>
![image](https://user-images.githubusercontent.com/62804036/161779604-f12e1f56-dc95-42b4-a2f3-466d8658d021.png)<br>
![image](https://user-images.githubusercontent.com/62804036/161779737-de8b9af6-bb05-45d5-a71e-d17e79a232a7.png)<br>
🎉실행이 잘 된다!🎉

## EC2에서 도커 설치 및 실행
[How to install and Use Docker on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)<br>
![image](https://user-images.githubusercontent.com/62804036/161781535-8be2a8ea-f6ed-42d9-a5ca-9167170cb952.png)
![image](https://user-images.githubusercontent.com/62804036/161781698-fc3f44f4-8dc6-4b46-99f5-95427e7b5138.png)
![image](https://user-images.githubusercontent.com/62804036/161781847-764c278b-4829-4765-b027-ea53d5147f0d.png)
![image](https://user-images.githubusercontent.com/62804036/161782038-4f5a6e70-4490-4fd2-b01e-c92f08e0a930.png)
![image](https://user-images.githubusercontent.com/62804036/161782429-0ac20d16-88df-47d7-b928-cbff0947dcd5.png)<br>
docker를 설치하기 위한 준비단계 명령어 입력<br>
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
```
docker 설치<br>
```
sudo apt install docker-ce
```
docker 설치 확인<br>
```
sudo systemctl status docker
```
![image](https://user-images.githubusercontent.com/62804036/161783405-0ab4d667-370c-4051-8dc7-6228fcda9bb0.png)
active running이 뜨면 잘 되고 있는 것! <br>
#### EC2로 리액트 파일 가져가기
1. 깃허브로 리액트 파일 올린 후에 EC2 인스턴스에서 Clone하기
2. FTP를 이용해서 파일 올려주기(Filezilla)
