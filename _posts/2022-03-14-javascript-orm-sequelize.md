---
layout: single
title: "D+58 ORM, Sequelize(shortly-mvc)"
categories: Javascript
tag: [기록, Javascript, JS, 자바스크립트]
author_profile: false
---

orm과 sequelize.

## 1. ORM

[(Object Relational Mapping /객체-관계 매핑)](https://geonlee.tistory.com/207)

![](https://blog.kakaocdn.net/dn/DJMGJ/btrvWGKGvjn/kvDUPIrt374mgZkPCkTee0/img.png)

```
데이터베이스 데이터 <—매핑—> Object 필드
```

객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 것.

→ 객체 지향 프로그래밍은 클래스를 사용하고, 관계형 데이터베이스는 테이블을 사용하여 객체 모델과 관계형 모델 간에 불일치가 존재하는데, 이를 ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결한다.

→ 객체를 통해 간접적으로 데이터베이스 데이터를 다룬다. persistent API라고도 할 수 있다.
ex) JPA, Hibernate 등

<mark>⇒ ORM을 이용하면 따로 SQL문을 짤 필요 없이 객체를 통해 간접적으로 데이터베이스를 다룰 수 있다.</mark>

✷ [객체 지향 프로그래밍](https://hsly22xk.github.io/javascript/javascript-oop/)에서 객체는 상태를 나타내는 프로퍼티와 동작을 나타내는 메소드를 하나의 논리적인 단위로 묶은 복합적인 자료구조

✷ attribute: 더이상 쪼갤 수 없는 정보의 단위

### ① ORM의 장점

‣ 객체 지향적인 코드로 인해 더 직관적이고 비즈니스 로직에 더 집중할 수 있게 도와준다.

→ ORM을 이용하면 SQL Query가 아닌 직관적인 코드(메소드)로 데이터를 조작할 수 있어 개발자가 객체 모델로 프로그래밍하는 데 집중할 수 있도록 도와준다.

‣ 쿼리문을 익힐 필요가 없음 → 원래 사용하는 언어만 사용해도 됨

‣ 선언문, 할당, 종료 같은 부수적인 코드가 없거나 급격히 줄어든다.

‣ 각종 객체에 대한 코드를 별도로 작성하기 때문에 코드의 가독성을 올려준다.

‣ SQL의 절차적이고 순차적인 접근이 아닌 객체 지향적인 접근으로 인해 생산성이 증가한다.

‣ 재사용 및 유지보수의 편리성이 증가한다. → ORM은 독립적으로 작성되어있고, 해당 객체들을 재활용 할 수 있다. 때문에 모델에서 가공된 데이터를 컨트롤러에 의해 뷰와 합쳐지는 형태로 디자인 패턴을 견고하게 다지는데 유리하다.

‣ 매핑정보가 명확하여, ERD를 보는 것에 대한 의존도를 낮출 수 있다.

‣ DBMS(DataBase Management System, 데이터베이스 관리 시스템)에 대한 종속성이 줄어든다. → 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하기 때문에 RDBMS(Relatationl(관계형) DataBase Management Sysytem)의 데이터 구조와 Java의 객체지향 모델 사이의 간격을 좁힐 수 있다.

→ 대부분 ORM 솔루션은 DB에 종속적이지 않다. 종속적이지 않다는것은 구현 방법뿐만 아니라 많은 솔루션에서 자료형 타입까지 유효하다.

⇒ 프로그래머는 Object에 집중하므로 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적 적은 리스크와 시간이 소요된다. 또한 자바에서 가공할경우 equals, hashCode의 오버라이드 같은 자바의 기능을 이용할 수 있고, 간결하고 빠른 가공이 가능하다.

### ② ORM의 단점

‣ 완벽한 ORM으로만 서비스를 구현하기가 어렵다.

‣ 사용하기는 편하지만 설계는 매우 신중하게 해야 한다.

‣ 프로젝트의 복잡성이 커질 경우 난이도 또한 올라갈 수 있다.

‣ 잘못 구현된 경우에 속도 저하 및 심각할 경우 일관성이 무너지는 문제점이 생길 수 있다.

‣ 일부 자주 사용되는 대형 쿼리는 속도를 위해 SP를 쓰는 등 별도의 튜닝이 필요한 경우가 있다.

‣ DBMS의 고유 기능을 이용하기 어렵다.(하지만 이건 단점으로만 볼 수 없다 : 특정 DBMS의 고유기능을 이용하면 이식성이 저하된다.)

‣ 프로시저가 많은 시스템에선 ORM의 객체 지향적인 장점을 활용하기 어렵다. 이미 프로시저가 많은 시스템에선 다시 객체로 바꿔야 하며, 그 과정에서 생산성 저하나 리스크가 많이 발생할 수 있다.

[✷ Sequelize 메소드](https://velog.io/@cadenzah/sequelize-document-1)
[✷ 모델 쿼리 파인더(Model query finder) - 공식문서](https://sequelize.org/docs/v6/core-concepts/model-querying-finders/)

```js
// orm 예시 코드
const db = require("../db");

class Model {
  static tableName = "items";

  static async findAll() {
    return new Promise((resolve, reject) => {
      const queryString = `SELECT * FROM ${Model.tableName}`;

      db.query(queryString, (err, result) => {
        if (err) {
          console.log(err);
          reject(err);
          return;
        }
        resolve(result);
      });
    });
  }

  static async findOne({ where }) {
    return new Promise((resolve, reject) => {
      const queryString = `SELECT * FROM ${Model.tableName} WHERE id=${where.id}`;

      db.query(queryString, (err, result) => {
        if (err) {
          console.log(err);
          reject(err);
          return;
        }

        if (result.length > 0) {
          const { name, price, image } = result[0];
          const instance = new Model(name, price, image);
          instance.id = where.id;
          resolve(instance);
        } else {
          reject({ error: "id에 매칭되는 레코드가 없습니다" });
        }
      });
    });
  }

  async save() {
    return new Promise((resolve, reject) => {
      const queryString = `INSERT INTO ${Model.tableName} (name, price, image) VALUES ("${this.name}", ${this.price}, "${this.image}")`;

      db.query(queryString, (err, result) => {
        if (err) {
          console.log(err);
          reject(err);
          return;
        }
        this.id = result.insertId;
        resolve(result);
      });
    });
  }

  async destroy() {
    return new Promise((resolve, reject) => {
      const queryString = `DELETE FROM ${Model.tableName} WHERE id=${this.id}`;

      db.query(queryString, (err, result) => {
        if (err) {
          console.log(err);
          reject(err);
          return;
        }
        resolve(result);
      });
    });
  }
}

module.exports = Model;
```

## 2. Sequelize supports the standard Associations

[Associations](https://sequelize.org/docs/v6/core-concepts/assocs/)

```js
const A = sequelize.define("A" /* ... */);
const B = sequelize.define("B" /* ... */);

A.hasOne(B); // A HasOne B
A.belongsTo(B); // A BelongsTo B
A.hasMany(B); // A HasMany B
A.belongsToMany(B, { through: "C" }); // A BelongsToMany B through the junction table C

일대일 - HasOne, BelongsTo;
일대다 - HasMany, BelongsToMany;
다대다 - BelongsToMany;
```

## 3. short.ly

[bit.ly](http://bit.ly/) 와 같이 긴 URL을 짧게 단축시켜주는 앱. urls 테이블을 만들어 원본 URL과 단축 URL의 방문 횟수를 기록한다.

ORM을 이용해 아래와 같은 테이블을 만들어보기.

```
// 완성된 urls 테이블의 스키마

mysql> describe urls;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| id        | int          | NO   | PRI | NULL    | auto_increment |
| url       | varchar(255) | YES  |     | NULL    |                |
| title     | varchar(255) | YES  |     | NULL    |                |
| visits    | int          | YES  |     | NULL    |                |
| createdAt | datetime     | NO   |     | NULL    |                |
| updatedAt | datetime     | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
```

① sequelize 및 sequelize-cli 설치

```
// 시퀼라이즈 라이브러리 설치
npm install --save sequelize

// 시퀼라이즈-cli 설치
// -dev 옵션을 붙이는 이유는 배포 단계에서 필요한 모듈이 아님. 초기 단계에서만 필요한 모듈이라서.
// devDependencies에 설치하는 의존성 모듈들은 개발시에만 필요한 모듈들임.
npm install --save-dev sequelize-cli

// 부트스트래핑: 프로젝트 초기 단계를 자동으로 설정할 수 있도록 도와주는 일
// 시퀼라이즈 부트스트래핑 설치(프로젝트 시작 전 시작해야 하는 명령어)
// 이 명령어를 사용하면 models, migrations, config, seeders파일이 생성된다
npx sequelize-cli init
```

‣ sequelize-cli 설치 후 생성되는 폴더 종류

config: 데이터베이스에 연결하는 방법을 CLI에 알려주는 구성 파일이 포함되어 있음.

models: 프로젝트의 모든 모델을 포함

migrations: 모든 마이그레이션 파일 포함

seeders: 모든 시드 파일을 포함

② mysql password 변경

```js
// config > config.json
// 원본 코드
// "password" 부분을 mysql password로 변경(""로 감싸주기)
{
  "development": {
    "username": "root",
    "password": null,
    "database": "database_development",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}
```

③ cli를 통한 모델 생성

[(공식문서 참조)](https://sequelize.org/master/manual/migrations.html)

model:generate 명령을 사용하는데, 이 명령에는 두 가지 옵션이 필요하다.

name: 모델명, attributes: 모델 속성 목록

ex)

```
// 예시 형식
npx sequelize-cli model:generate --name Url --attributes url:string,title:string,visits:integer

이 명령어의 의미는

‣ 폴더에 모델 파일 Url을 만듭니다. models
‣ 폴더와 같은 이름 XXXXXXXXXXXXXX-create-user.js으로 마이그레이션 파일을 만듭니다. migrations라는 것이다.
```

④ 마이그레이션

스키마 변경에 따른 데이터 이주.

→ 데이터를 선택, 준비, 추출 및 변환하여 한 컴퓨터 저장 시스템에서 다른 컴퓨터 저장 시스템으로 영구적으로 전송하는 프로세스.

```
npx sequelize-cli db:migrate
```

**<mark>마이그레이션은 스키마가 변경이 될 때마다 실행해주어야 한다.</mark>**

```
// migration한 내역을 지움(migration 이전으로 되돌림)
// 이 명령어는 자동으로 최근에 migration한 내역만 지움
npx sequelize-cli db:migrate:undo

// migration한 내역을 '전부' 지움
npx sequelize-cli db:migrate:undo:all
```
