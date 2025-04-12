# 정적 HTML 프로젝트를 Docker로 실행시키기

## 지식 정리

### 원리

1. 정적 html 파일과 css 파일, js 파일을 복사한다.
2. nginx 기반으로 이미지를 구축해주면 끝난다.

### Dockerfile 명령어

```dockerfile
# nginx 기반 도커 이미지 구축
FROM nginx

# 프로젝트 통째로 복사
# 그리고 복사할 컨테이너의 경로는 다음과 같이 작성해준다
# 실제 nginx 도커 이미지를 보면 설명에 다음과 같이 경로를 지정하라고 적혀있다
COPY ./ /usr/share/nginx/html
```

### docker cli

```bash
# Spring Boot 프로젝트 도커 이미지로 구축하기
docker build -t "[이미지 이름]" .

# 현재 가지고 있는 도커 이미지 리스트 조회
docker image ls

# 내가 만든 Spring Boot 도커 이미지를 도커 컨테이너로 실행시키기
# -d: 컨테이너를 백그라운드에서 실행하기
# -p: 호스트와 컨테이너의 포트 설정(nginx 기반이니까 80으로)
docker run -d -p 80:80 "[이미지 이름]"
```

### 강의 주소

[비전공자도 이해할 수 있는 Docker 입문/실전](https://inf.run/GvHgg)

### 앞서 Next.js에서 했던 고민 "어떤 방식이 더 나을까?""

- 알아본 결과 Next.js는 SSR + SSG + ISR + CSR 모든 방식의 렌더링을 지원하기에 nginx 기반 환경에서 운영할 수 없는 것 같다.

- 그렇기에 node 기반 환경에서 진행해야 했고, 반면 정적 html의 경우 nginx 기반 환경에서 충분히 운영 가능하다.

- 결국 React 프로젝트의 경우 어떤 운영 환경을 선택할지 결정할 필요가 있는데, 대부분의 경우 nginx 기반 환경을 사용하는 것으로 보인다(내가 진행했던 프로젝트들도 전부 nginx 사용했기도 했고)

- 다만 React의 경우 SSR 렌더링 기능을 첨가하거나 BE 프로젝트를 node 환경인 Express.js로 구축했을 경우 node 기반 환경으로 배포, 운영하는 것으로 보인다.
