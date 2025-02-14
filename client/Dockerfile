# 베이스 이미지
# 폴더 및 파일 복사
# 프로젝트 빌드 명령어 실행
# 서비스 실행 명령어 -> 컨테이너가 실행될 떄 CMD
FROM node AS build
WORKDIR /app
# 패키지 설치를 위한 패키지 목록 파일 복사
COPY package.json package-lock.json ./
RUN npm install
# 소스 코드 복사
COPY . .
RUN npm run build

# Run Stage
FROM nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf
# Build stage에서 빌드한 (/app/dist에 있는) 정적 파일을 /usr/share/nginx/html 여기로 옮긴다
COPY --from=build /app/dist /usr/share/nginx/html
# templates 폴더에 있는 파일 복사사
COPY ./templates /etc/nginx/templates
# 포트 명시
# 문서화 목적
EXPOSE 80 443
# nginx 컨테이너를 실행시키기
CMD ["nginx", "-g", "daemon off;"] 