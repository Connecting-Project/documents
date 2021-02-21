# 랜덤 패스워드 생성기

웹 페이지 계산기는 하와이안 피자에서 제작한 세 번째 프로젝트 입니다. 

비밀번호는 주기적으로 변경해야 하며, 유추 가능하도록 설정하면 안됩니다. 랜덤 패스워드 생성기를 통해서 비밀번호를 안전하게 저장하고 개인 계정 혹은 서버의 해킹을 차단합니다. 



## Information

- 메인 주소
  - https://password.hawaiian-pizza.ml/
- API 주소
  - https://password.hawaiian-pizza.gq/
- API Documents
  - https://documenter.getpostman.com/view/9729412/TWDRrer2



### 안전하게 비밀번호 관리하기

1. 여러 개의 중요한 계정에 대해 동일한 비밀번호를 사용하지 마세요. 
2. 소문자, 대문자, 특수기호 등을 적극적으로 사용하세요. 
3. 유추하기 쉬운 비밀번호를 사용하지 마세요. 
4. SSL/TLS가 적용되지 않은 홈페이지에 접속하지 마세요. 
5. 공공 와이파이, 공용 PC에 로그인을 피해주세요. 



### Installation

Docker가 설치되어 있어야 합니다. 

```bash
$ docker-compose up -d 
```



- 벡엔드 

  ```dockerfile
  FROM openjdk:12
  LABEL seongwon="seongwon@edu.hanbat.ac.kr"
  
  COPY ./password-0.0.1-SNAPSHOT.jar .
  
  EXPOSE 8080
  
  CMD [ "java", "-jar", "password-0.0.1-SNAPSHOT.jar"]
  ```

- 프론트 엔드 

  ```dockerfile
  FROM node:14
  LABEL seongwon="seongwon@edu.hanbat.ac.kr"
  
  WORKDIR /usr/src/app
  
  COPY ./package*.json ./
  
  RUN npm install
  RUN npm install -g serve
  
  COPY . .
  
  RUN npm run build
  
  EXPOSE 5000
  
  ENTRYPOINT [ "serve", "-s", "build" ]
  ```

- docker-compose.yml

  ```yaml
  version: '3'
  services:
    front:
      image: jusk2/hawaiian-password-web
      hostname: password-web
      restart: always
      ports:
        - "8001:5000"
        
    api:
      image: jusk2/hawaiian-password-api
      hostname: password-api
      restart: always
      ports:
        - "8000:8080"
  ```

  



## Tech Stack

- Spring boot
  - API
- React
  - Front
- Docker
  - Deploy



## Author 

- 김수현 - 벡엔드
- 조용우 - 프론트 엔드
- 이성원 - 인프라, Dev/Ops



## Contact 

토이 프로젝트에 있어서 궁금한 점이 있거나 개선하고 싶은 점 등 여러분들의 다양한 의견을 기다립니다.

- [seongwon@edu.hanbat.ac.kr](mailto:seongwon@edu.hanbat.ac.kr)
- [dpfmxlfls95@naver.com](mailto:dpfmxlfls95@naver.com)



## License

Distributed under the MIT License. See `LICENSE` for more information.