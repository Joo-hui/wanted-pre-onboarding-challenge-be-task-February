1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- **관계형 데이터베이스 (RDBMS)**
장점 
- 정해진 스키마에 따라 데이터를 저장하여야 하므로 명확한 데이터 구조를 보장한다.
- 각 데이터를 중복없이 한 번만 저장할 수 있다.
단점
- 테이블과 테이블 간 관례를 맺고 있어 시스템이 커질 경우 JOIN문이 많은 복잡한 쿼리가 만들어질 수 있다.
- 성능 향상을 위해서는 Scale-up만을 지원. 이로 인해 비용이 기하급수적으로 늘어날 수 있다.
- 스키마로 인해 데이터가 유연하지 못 하다. 나중에 스키마가 변경될 경우 번거롭고 어렵다.

**비관계형 데이터베이스 (NoSQL)**
장점
- 스키마가 없이 때문에 유연하며 자유로운 데이터 주고를 가질 수 있다.
- 언제든 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.
- 데이터 분산이 용이하며 성능 향상을 위한 Saclue-up 뿐만 아닌 Scale-out 또한 가능하다.

단점
- 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경 될 경우 수정을 모든 컬렉션에서 수행을 해야 한다.
- 스키마가 존재하지 않기에 명확한 데이터 구조를 보장하지 않으며 데이터 구조 결정하기가 어려울 수 있다.



2. 트랜잭션(transaction)이란 무엇인가요?

- 
트랜잭션이란
데이터베이스의 상태를 변경(SELECT, UPDATE, INSERT, DELETE)시키기 위해 수행하는 작업 단위이다.
트랜잭션(Transaction)은 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 모두 수행되어야 할 일련의 연산들을 의미한다.

**트랜잭션의 특징**
1. 원자성(Atomicity)
원자성은 트랜잭션이 DB에 모두 반영되거나, 전혀 반영되지 않거나를 뜻한다.
All or Nothing을 생각하면 된다.

2. 일관성(Consistency)
일관성은 트랜잭션 작업 처리의 결과가 항상 일관되어야 한다를 뜻한다.
즉, 데이터 타입이 반환 후와 전이 항상 동일해야 한다.

3. 독립성(Isolation)
독립성은 하나의 트랜잭션은 다른 트랜잭션에 끼어들 수 없고 마찬가지로 독립적임을 의미한다.
즉, 각각의 트랜잭션은 독립적이라 서로 간섭이 불가능하다.

4. 지속성(Durablility)
지속성은 트랜잭션이 성공적으로 완료되면 영구적으로 결과에 반영되어야 함을 뜻한다.
보통 commit 이 된다면 지속성은 만족할 수 있다.

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

- JOIN 연산은 두 테이블을 결합하는 연산이다. 데이터 규모가 커지면서 하나의 테이블로 정보를 수용하기 어려워지면 테이블을 분할하고 테이블 간의 관계성을 부여한다.


**1. 내부 조인(INNER JOIN)**
- 조건을 사용하여 두 테이블의 레코드를 결합한다.
- 동등 조인, 비동등 조인, 자연 조인 등이 있다.
- 서로 중복되는 값만 나타낸다.

1) 동등 조인
- 두 테이블 사이의 같은 행들을 반환한다.
2) 비동등 조인(NON-EQUI JOIN)
- 두 테이블 사이의 같지 않은 모든 행들을 반환한다.
3) 자연 조인(NATURAL JOIN)
- 두 테이블에 같은 이름의 열이 있을때만 동작한다.
- ON이 필요없다.

**2. 외부 조인(OUTER JOIN)**
- 내부 조인과 유사하며 일치하는 것이 없을 경우 NULL로 표시한다.
- 왼쪽 테이블은 FROM 바로 다음에 나오는 테이블이고, JOIN 뒤에 나오는 테이블이 오른쪽 테이블이다.
- 왼쪽 외부 조인(LEFT OUTER JOIN)과 오른쪽 외부 조인(RIGHT OUTER JOIN)이 있다.
- 왼쪽 외부 조인을 사용할 경우 왼쪽 테이블을 오른쪽 테이블에 비교한다. 오른쪽 외부 조인도 그 반대로 동작한다. 일대다 관계에 유용한다.

**3. 크로스 조인(CROSS JOIN)**
- 한 테이블의 모든 행과 다른 테이블의 모든 행을 짝지어 반환한다.
- 카티전 조인, 카티전 프로덕트 등이 있다.
- 두 테이블의 교집합을 수행하는 교차 결합으로 두 테이블에서 모든 경우의 수를 볼 수 있으나 모든 경우의 수를 볼 일이 딱히 없기 때문에 실제로 서의 사용되지 않는다. 

**4. 셀프 조인(SELF JOIN)**
- 자기 자신을 조인한다.
- 자기 자신을 하나씩 비교하기 위해 사용한다.
- 하나의 테이블로 같은 정보를 가진 테이블이 두 개 있는 것처럼 쿼리를 보낼 수 있다.

4. MySQL에서 인덱스(index)란 무엇인가요?

- 데이터의 저장(INSERT, UPDATE, DELETE) 의 성능을 희생하고 그 대신에 데이터의 읽기 속도를 높이는 테이블의 동작속도(조회)를 높여주는 자료구조이다. 
**(두꺼운 책 가장 앞에 목차를 표기해 두어 독자들이 빠르게 원하는 목차로 찾아갈 수 있도록 하는데 이와 비슷한 개념이 MySQL 의 INDEX)**

인덱스의 특징
- select 검색 속도를 크게 향상 시킨다.
- 인덱스 생성 시 DB 크기의 약10% 정도되는 추가 공간이 필요하다.
- 인덱스 생성 시 시간이 걸린다.
- insert, update, delete같은 데이터 변경 쿼리가 잦은 경우 paging이 빈번해져 성능이 악화될 수 있다.
- 데이터 조회에는 플러즈지만, 데이터 변경이 자주 일어나면 오히려 성능이 감소된다.
