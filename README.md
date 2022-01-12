# Docker-ELK-SpringBoot
docker elk컨테이너 실행하여 spring boot 프로젝트 내 log파일 수집 및 시각화 테스트


### 1. 컨테이너 실행 모습
![image](https://user-images.githubusercontent.com/72364918/149055421-0185a7a3-694b-42a9-b902-2ec5ffbf17df.png)
### 2. 실행 방법
#### - [elk네트워크에 filebeat 컨테이너 생성 및 실행]
docker run -d --name filebeat --network elk -v "/root/project/workspace/telemetry/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml" -v "/mnt/c/Users/yescnc/youseon/2022_project/spring-docker-elk/TomcatLog/logs:/logs" docker.elastic.co/beats/filebeat:7.6.2
#### - [elk네트워크에 logstash 컨테이너 생성 및 실행]
docker run -d --name logstash --network elk -p 5044:5044 -v "/root/project/workspace/telemetry/logstash/logstash.conf:/usr/share/logstash/pipeline/logstash.conf" docker.elastic.co/logstash/logstash:7.6.2

#### - [elk 네트워크에 엘라스틱서치 컨테이너 생성 및 실행]
docker run -d --network=elk --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.6.2

#### - [elk 네트워크에 키바나 컨테이너 생성 및 실행]
docker run -d --network=elk --name kibana -p 5601:5601 docker.elastic.co/kibana/kibana:7.6.2

### 시각화 된 로그
![image](https://user-images.githubusercontent.com/72364918/149055233-13a31022-7726-46fb-9d4d-604f1ac0e7aa.png)
