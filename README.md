# Docker with GraphQL

# Docker file

```js

FROM node:carbon
MAINTAINER Doyoung ypd03008@gmail.com

#app 폴더 만들기 - NodeJS 어플리케이션 폴더
RUN mkdir -p /app
#winston 등을 사용할떄엔 log 폴더도 생성

#어플리케이션 폴더를 Workdir로 지정 - 서버가동용
WORKDIR /app

#서버 파일 복사 ADD [어플리케이션파일 위치] [컨테이너내부의 어플리케이션 파일위치]
#저는 Dockerfile과 서버파일이 같은위치에 있어서 ./입니다
ADD ./ /app

#패키지파일들 받기
RUN npm install
RUN npm run build

#배포버젼으로 설정 - 이 설정으로 환경을 나눌 수 있습니다.
ENV NODE_ENV=production

#서버실행
CMD node build/server
```

# Docker command

ex)

```
docker build -t gql:0.0.1 .
docker create --name gql_server -p 4000:4000 gql:0.0.1
docker start gql_server

```
