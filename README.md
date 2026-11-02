# codyssey
codyssey

## 1) 실행 환경
- OS: Ubuntu 22.04
- Shell: bash
- Docker: 26.x
- Git: 2.

  ## 2) 수행 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 변경 실습
- [x] Docker 설치/점검
- [x] hello-world 실행
- [x] Dockerfile 빌드/실행
- [x] 포트 매핑 접속(2회)
- [x] 바인드 마운트 반영
- [x] 볼륨 영속성
- [x] Git 설정 + VSCode GitHub 연동

 ## 3) 수행 로그(발췌)
bash$ pwd
/home/user
$ mkdir -p ~/codyssey/practice
$ ls -la

### Dockerfile 커스텀 예시
FROM nginx:alpine
LABEL org.opencontainers.image.title="my-custom-nginx"
ENV APP_ENV=dev
COPY site/ /usr/share/nginx/html/ 

### Docker 포트 매핑 실행 로그 예시
$ docker build -t my-web:1.0 .
$ docker run -d -p 8080:5000 --name my-web-8080 my-web:1.0
$ curl <http://localhost:8080>
Hello

$ docker run -d -p 8081:5000 --name my-web-8081 my-web:1.0
$ curl <http://localhost:8081>
Hello

### 볼륨 영속성 예시
$ docker volume create mydata
$ docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
$ docker exec -it vol-test bash -lc "echo hi > /data/hello.txt && cat /data/hello.txt"
hi
$ docker rm -f vol-test

$ docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity
$ docker exec -it vol-test2 bash -lc "cat /data/hello.txt"
hi

