# Redis

### 1. Redis란?

- Redis란 (Remote Dictionary Server) 를 의미한다. 
- Redis 는 Key-value구조로 데이터를 저장 하고 매핑한다.
- No-SQL 데이터베이스 타입종류중 하나이며 스키마가 존재하지 않고 SELECT, INSERT, UPDATE, DELETE 쿼리를 사용하지 않는다.
- Redis는 데이터를 저장하기 위하여 Data Structures을 사용 사용한다.
  - String
  - Lists
  - Sets
  - Sorted Sets
  - Hashes
  - bitmaps
  - hyperloglogs
  - Geospatial indexes 

- Command 를 기반으로 데이터와 상호작용한다. > [command](https://redis.io/commands)
- In-memory Database로 Redis는 데이터를 memory 와 cache안에 유지하여 매우 빠르며 일부 옵션을 통해 Disk에도 적용할 수 있다.

### 2. Redis 특징

- Speed: redis는 데이터를 memory와 cache안에 유지하기 때문에 매우 빠르다. > [benchmarks](https://redis.io/topics/benchmarks)
- Simple and Flexible: 
  - table, column, rows를 정의할 필요가 없다.
  - Insert, select, update, delete를 직접 작성할 필요 없다.
  - 데이터를 읽고 쓰는게 매우 간단하며 직관적이다.
- Durable: 
  - redis는 disk에 데이터를 작성하는 옵션을 가진다.
  - Data write oprions들은 설정에 따라 변경이 가능하다(Configurable)
  - Caching System으로 사용되거나 완전한 DB로 사용 될 수 있다.
- Language support: 여러 언어가 지원된다. > [Clients](https://redis.io/clients)

- Compatibility: Redis는 Transaction을 빠르게 하기위하여  보조 Database로 사용될 수 있다.
  - 기존 : Service - Request/Response - DB
  - Redis 사용: Service - Request/Response - Redis(Cache) - Request/Response - DB
  - Service는 먼저 Cache에 저장되어 있는데 데이터를 먼저 검색한다.
  - 만약 Cache에 저장되어 있지 않으면 DB에서 해당 데이터를 불러와 Cache에 저장한다.
- Scalling: 
  - Redis는 매우 강력한 Master-slave 특징을 가지고 있다.
  - Master는 오직 작성용으로 사용하고 slave중 하나는 읽기전용 다른 slave는 디스크에 작성 등 역할을 나누어 사용할 수 있다.
- 모든 설정들이(Configurations) 하나의 text file에 저장 되어 있다.
- Single Threaded(싱글 쓰레드)로 한 번에 하나의 동작만 작동한다.
- Piplining: 여러 command를 묶어서 한 번에 전달 할 수 있다.



*[Redis Official Site](https://redis.io)*

