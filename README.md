# 4. Fscrawler

------

Fscrawlers는 문서를 인덱싱하는 툴입니다.
 Apache Tika가 지원하는 종류의 문서는 모두 가능합니다.

https://fscrawler.readthedocs.io/en/fscrawler-2.5/user/options.html

https://tika.apache.org/1.24.1/formats.html#Supported_Document_Formats

## Prerequisite

1. Window의 Docker로 실행했습니다.
   1. 특정 폴더를 인식하지 못하면 지우고 다시 폴더를 만들어주세요(권한을 따로 줄 수 없어요)
2. Docker, Docker-compose가 설치되어 있어야합니다. 

------

## How to Use

소스를 클론 받아 직접 구축 해보는 튜토리얼을 아래 저의 기술 블로그에 포스팅 하였습니다.

```git clone https://github.com/MightyTedKim/elk-fscrawler_demo.git```

```
cd Fscrawler_101
docker-compose up -d s-es s-kibana
//curl localhost:9200
docker-compose up -d s-fscrawler
docker-compose down

cd ../Fscrawler_nori
docker system prune //y
docker-compose up -d s-es s-kibana
//curl localhost:9200
docker-compose up -d s-fscrawler
```

## Link

_git : [*GIT*](https://github.com/MightyTedKim/elk-fscrawler_demo)

_blog: 

 - [**Fscrawler_101**](*https://blog.naver.com/deet1107/222150681083*) : fscrawler hello-world, log4j 설정

 - [**Fscrawler_nori**](*https://blog.naver.com/deet1107/222150727429*) : dockerfile에 nori 플러그인 설치, 사전 연계

2개의 docker-compose 파일로 구성

1. Fscrawler_101 : Fscrawler로 파일 인덱싱 (기본)
   1. fscrawler hello world
   2. 로그 파일 밖으로 꺼내기 (log4j) 
2. Fscrawler_nori : Dockerfile에 Nori-plugin을 넣어서 원클릭으로 실행
   1. DockerFile에 nori 플러그인 넣기
   2. 사전(사용자/동의어) 마운트하기
   3. [cobain님의 블로그](https://cobain.me/2020/10/19/ElasticSearch-FSCrawler.html) 를 참고했습니다. 

------

## ETC

제가 생각한 장점은 logstash/filebeat를 이용하지 않고 대부분의 파일을 지원한다는 겁니다. ingest_pipeline과 혼용해서 사용할 수도 있습니다.

- 폴더에 위치시키면, 알아서 인덱싱
- 파일을 삭제하면, 알아서 인덱스 삭제 가능
- ES 6,7 에 따른 호환성(_type 유무) 해결
- 2.3 부터 OCR을 통해 이미지의 글자를 파싱
- n분마다 확인, 상태, mapping 등등

------

# Reference

_FSCrawler Github URL : [FSCrawler Github](https://github.com/dadoonet/fscrawler)_

_FSCrawler Documents URL : [FSCrawler Readthedocs](https://fscrawler.readthedocs.io)_

_ElasticSearch Document URL : [Elasticsearch Official Home](https://www.elastic.co/guide/en/elastic-stack-get-started/current/get-started-docker.html)_

_참고한 블로그 1: [URL1](https://naggingmachine.tistory.com/830)_

_참고한 블로그 2: [URL2](https://blog.naver.com/icelemonteainkr/221828689765)_

_참고한 블로그 3: [URL3](https://cobain.me/2020/10/19/ElasticSearch-FSCrawler.html)