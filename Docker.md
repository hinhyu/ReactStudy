# Docker
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
