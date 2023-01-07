###
* mongoexport, mongoimport
* mongodump, mongoresore, bsondump
* mongosh
	* use foo
	* foo = db['foo']
	* foo = db.foo

### insert
* foo.insertOne({key:'val'})
	* insertMany(), insertOne()
	* for(i=0; i<5; i++) foo.insertOne({foo:i})

## update
* foo.updateMany({content: 'bar'}, {$set: {state: 100}})
	* updateMany(), updateOne()
* 주의: $set 을 제외하면 명시하지 않은 모든 컬럼이 제거됨(대체)
	* foo.updateMany({content: 'bar'}, {state: 100})
* 컬럼 제거
	* foo.updateMany({content: 'bar'}, {$unset: {title:1}})
* 조건&추가
	* foo.updateMany({'bee.boo': ['fee']}, {$addToSet: {'bee.boo': 'fuu'}}, false, true)
		* 배열 컬럼에 요소 추가되는 변경
		* 파라미터 3: false: upsert(update & insert, 조건 도큐먼트 없을 경우 insert) 허용 여부
		* 파라미터 4: true: 다중 업데이트 여부

## delete
* foo.deleteOne({foo: 'foo'})
	* deleteMany(0), findOneAndDelete()
* foo.deleteMany({}): 모든 도큐먼트 삭제

## select
* foo.count()
* foo.find(), foo.find({foo:'foo'})
* foo.find({$and:[{title: 'bar'}, {content: 'bar'}]})
* foo.find({$or:[{title: 'bar'}, {content: 'bar'}]})
* 중첩 질의: foo.find({'parent.child': 'children'})
* 범위
	* $gte, $gt, $lte, $lt
	* foo.find({foo: {$gt: 100, $lt: 200}})
* 조건
	* $ne

## index
* foo.find().explain('executionStats')
* 인덱스 생성
	* foo.createIndex({foo:1})
		* 오름차순 1, 내림차순 -1
	* foo.createIndex({foo: -1}, {unique: true})
	* foo.getIndexes()
* foo.dropIndex('foo_1')

## 관리
* show dbs
* show collections
* db.stats(), foo.stats()
* 탭으로 모든 명령의 힌트/자동완성 가능

## 관계
* 조인을 지원하지 않음
	* 다른 컬렉션에 질의하거나 비정규화
* 일대다, 다대다
    * cat_id: ObjectId('111')
    * cat_ids: [ ObjectId('111'), ObjectId('222') ]
* 포함: 다대다: $in
	* prod = db.prod.findOne()
	* db.cats.find({_id: {$in: prod['cat_ids']}})
* 일치: 일대다
	* user = db.user.findOne({_id: pay['user_id']})
	* db.pay.find({user_id: user['_id']})
* 도뮤먼트 내 배열의 크기 질의 불가: 개수를 필드로 저장

## 데이터베이스
* /data/db
* db 삭제: db.dropDatabase()
* 컬렉션 삭제: db.foo.drop()
* 컬렉션 생성: db.createCollection('foo')
* 컬렉션 변경: db.foo.renameCollection('bar')
* 캡드 컬렉션: 고정 크기, rotate, 로깅에 적합, 도큐먼트 삭제/변경 불가
	* db.createCollection('bar', {capped: true, size: 100, max:5})
		* count 해보면 도큐먼트가 고정된 크기/개수 이상 생성되지 않음
* TTL 컬렉션: 특정 시간 경과후 도큐먼트 만료(expire, 삭제)
	* 인덱스 생성시 옵션 추가로 구현
		* foo.createIndex({createdAt: 1}, {expireAfterSeconds: 5})
		* foo.insertOne({createdAt: new Date()})
	* 주기적으로(실시간 아닌듯) 타임스탬프 값을 현재 시간과 비교: 두 값의 차가 설정 값보다 크면 삭제
	* 제약: 다른 인덱스에서 사용되는 필드 불가, 캡드 컬렉션에서 불가, 타임스탬프 배열 불가

115p 진행중
