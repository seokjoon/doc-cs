###
* mongoexport, mongoimport
* mongodump, mongoresore, bsondump
* mongosh
	* use foo

### insert
* db.foo.insertOne({key:'val'})
	* insertMany(), insertOne()
	* for(i=0; i<5; i++) db.foo.insertOne({foo:i})

## update
* db.foo.updateMany({content: 'bar'}, {$set: {state: 100}})
	* updateMany(), updateOne()
* 주의: $set 을 제외하면 명시하지 않은 모든 컬럼이 제거됨(대체)
	* db.foo.updateMany({content: 'bar'}, {state: 100})
* 컬럼 제거
	* db.foo.updateMany({content: 'bar'}, {$unset: {title:1}})
* 조건&추가
	* db.foo.updateMany({'bee.boo': ['fee']}, {$addToSet: {'bee.boo': 'fuu'}}, false, true)
		* 배열 컬럼에 요소 추가되는 변경
		* 파라미터 3: false: upsert(update & insert, 조건 도큐먼트 없을 경우 insert) 허용 여부
		* 파라미터 4: true: 다중 업데이트 여부

## delete
* db.foo.deleteOne({foo: 'foo'})
	* deleteMany(0), findOneAndDelete()
* db.foo.deleteMany({}): 모든 도큐먼트 삭제
* 컬렉션 삭제: db.foo.drop()

## select
* db.foo.count()
* db.foo.find(), db.foo.find({foo:'foo'})
* db.foo.find({$and:[{title: 'bar'}, {content: 'bar'}]})
* db.foo.find({$or:[{title: 'bar'}, {content: 'bar'}]})
* 중첩 질의: db.foo.find({'parent.child': 'children'})
* 범위
	* $gte, $gt, $lte, $lt
	* db.foo.find({foo: {$gt: 100, $lt: 200}})
* 조건
	* $ne

## index
* db.foo.find().explain('executionStats')
* 인덱스 생성
	* db.foo.createIndex({foo:1})
		* 오름차순 1, 내림차순 -1
	* db.foo.createIndex({foo: -1}, {unique: true})
	* db.foo.getIndexes()

## 관리
* show dbs
* show collections
* db.stats(), db.foo.stats()
* 탭으로 모든 명령의 힌트/자동완성 가능


## 관계
* 조인을 지원하지 않음: 비정규화
* 일대다, 다대다
    * cat_id: ObjectId('111')
    * cat_ids: [ ObjectId('111'), ObjectId('222') ]
* 포함: 다대다: $in
	* prod = db.prod.findOne()
	* db.cats.find({_id: {$in: prod['cat_ids']}})
* 일치: 일대다
	* user = db.user.findOne({_id: pay['user_id']})
	* db.pay.find({user_id: user['_id']})
