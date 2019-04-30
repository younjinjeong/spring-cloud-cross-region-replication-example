# 멀티 리전 캐시 데이터 복제 데모  

## 설명 

본 데모는 클라우드 서비스에서 서로 다른 리전간 데이터 복제를 캐시 레이어에서 수행하는 방법을 소개합니다. 이는 넷플릭스의 EVCache에서 사용하는 글로벌 리전 복제의 컨셉을 구현한 것입니다. 캐시 수준에서 메세지 큐와 함께 복제를 구현하는 방법은 데이터베이스 수준에서의 복제보다 빠르며 다양한 방법으로 응용 및 확장될 수 있습니다. 
아래의 링크들은 넷플릭스 EVCache에 대한 설명이 있는 링크들 입니다. 

- Announcing EVCache Distributed in Memory Database  https://medium.com/netflix-techblog/announcing-evcache-distributed-in-memory-datastore-for-cloud-c26a698c27f7 

- Cache Warming Agility for a Stateful service 
https://medium.com/netflix-techblog/cache-warming-agility-for-a-stateful-service-2d3b1da82642 

- Application Data Caching Using SSDs
https://medium.com/netflix-techblog/application-data-caching-using-ssds-5bf25df851ef 

- Evolution of Application Data Caching from RAM to SSD 
https://medium.com/netflix-techblog/evolution-of-application-data-caching-from-ram-to-ssd-a33d6fa7a690 




## 데모 동작 다이어그램 

![Diagram](https://github.com/kpiljoong/spring-cloud-cross-region-replication-example/wiki/images/diagram.png) 



## 구성요소  

### Producer 

데이터를 받아서 리전 로컬의 캐시에 저장하고, 다시 메세지큐에 퍼블리싱하는 역할을 합니다. 


### Relay 

메세지큐의 컨슈머로 동작하며, 새로운 데이터가 큐에 유입되면 이를 가져다가 다른 리전에서 동작하는 프락시에 전잘합니다. 


### Proxy 

프락시는 다른 리전에서 전달받은 데이터를 로컬 리전의 캐시에 저장하는 역할을 합니다. 


## Future works 

본 데모는 높은 가용성으로 동작하도록 구성되지는 않았습니다. 따라서 이 컨셉을 프로덕션에 반영하기 위해서는 몇가지 부분에 대한 고가용성 준비가 필요하겠습니다. ELB의 사용이나 메세지큐의 카운터 모니터링을 통한 큐의 확장등이 고려되어야 합니다. 



Thanks! 
