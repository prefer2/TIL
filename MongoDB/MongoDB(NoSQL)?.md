## NoSQL

Non Relational Operation Database SQL의 줄임말이다. 몽고디비는 NoSQL의 대표주자이다. 

![Untitled](https://user-images.githubusercontent.com/67692759/136345726-1ba1db9e-0eed-473b-a5e1-45e5b72da666.png)

NoSQL은 JOIN 기능이 없다. 하지만 위 그림처럼 중첩 도큐먼트를 가질 수 있다(JOIN 불필요). 이는 보다 쉽고 빠르게 데이터를 사용할 수 있도록 해준다.

NoSQL은 고정된 테이블이 없다. 테이블에 상응하는 `컬렉션(collection)`이라는 개념이 있기는 하지만, 컬럼을 따로 정의하지 않는다. row는 NoSQL에서 `다큐먼트(document)`라고 부른다.


| SQL(MySQL)               | NoSQL(MongoDB)               |
|--------------------------|------------------------------|
| 규칙에 맞는 데이터 입력  | 자유로운 데이터 입력         |
| 테이블 간 JOIN 지원      | 컬렉션 간 JOIN 미지원        |
| 안전성, 일관성           | 확장성, 가용성               |
| 용어(테이블, 로우, 컬럼) | 용어(컬렉션, 다큐먼트, 필드) |

## BSON

mongoDB가 사용하는 데이터 포맷. JSON과 비슷한 형식이지만 type이 있다. key-value값으로 이루어져 있다. 각 document는 primary key인 id를 가지고 있다(자동으로 생성됨).
