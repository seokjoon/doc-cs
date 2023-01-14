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
* 키 이름이 모든 도큐먼트에 매번 저장됨
	* 짧은 이름이 효율적
* 숫자: double, int, long
	* js의 Number는 double
	* 정수값 저장을 위해서는 NumberLong() 이나 NumberInt() 사용
		* db.numbers.save({ n: NumberLong(5) })
	* decimal 미지원

## 쿼리
* findOne 은 도큐먼트 리턴, find 는 커서 객체 리턴
	* foo.find().limit(1)
* limit, skip
	* foo.find().skip(10).limig(10)
* sort
	* foo.find().sort({foo: -1})
* foo.findOne({ bar_id: bar['id'] })
* foo.find({ bar_id: { $gt: bar['id'] } }).count()
* foo.find({ bar_id: null })
* 지정 컬럼만 리턴
	* foo.find({}, { _id: 1 })
* 정규표현식
	* foo.find({ foo: /^tes/ })
* 범위: $lt, $lte, $gte, $gt
	* foo.find({ foo: { $gt: 5, $lt: 10 } })
	* 범위 질의는 타입이 일치하는 값만 리턴
* 집합: $in, $all, $nin
	* $all
		* foo.find({ tags: { $all: [ 'foo', 'bar' ] } })
	* foo.find({ foo: { $in: [...] } })
	* $nin, $ne 는 인덱스를 사용할 수 없음
* 논리: 
	* $ne: 인수가 요소와 다르면 리턴, 인덱스 미이용이므로 다른 연산자와 조합해야 효율적
		* 값은 단일값 혹은 배열 가능
	* $not: 결과를 반전하여 리턴
	* $or: 하나라도 true 이면 리턴
		* 같은 키일때는 $or 아닌 $in 사용, $or은 서로 다른 키에 대한 논리합
		* foo.find({ $or: [ { foo: 2 }, { bar: 3 }] })
	* $nor: true 가 하나도 없어야 리턴
	* $exists: 요소가 도큐먼트 안에 존재하면 리턴
		* 컬렉션은 고정된 스키마가 필요 없으므로 도큐먼트에 특정 키가 있는지 확인 필요
		* foo.find({ foo.bar: { $exists: false } })
* 서브 도큐먼트: 마침표로 구분
	* foo.find({ foo.bar: 5 })
	* 키의 순서도 판단 조건
		* foo.find({ parent: { child_a: 'a', child_b: 'b'} })
			* child_a 와 child_b의 순서가 도큐먼트와 다를 경우 찾지 못함: 바이트 단위로 비교
* 배열
	* $elemMatch: 모든 조건이 동일 하위 도큐먼트에 존재
		* 잘못된 예: foo.find({ addr.name: 2, : addr.state: 3 })
			* addr 키가 배열이고 name 2, state 3 인 요소들이 각각 존재하면 해당 도큐먼트가 리턴: 오류
		* foo.find({ addr: { $elemMatch: { name: 2, state: 3 } } })
	* $size: 배열 하위 도큐먼트의 크기가 조건과 일치, 인덱스 불가
		* foo.find({foo: { $size: 3 }})
	* 배열도 단일 값에 대한 질의와 동일한 방식 가능
		* foo.find({ tags: 'foo' })
		* 첫번째 태그로 제한: foo.find({ tags.0: 'foo' }): 
* 자바스크립트 쿼리 연산자: $where
	* 도큐먼트 선택을 위해 js 실행, 인덱스 불가
	* foo.find({ $where: function() { return this.bar > 2; } })
		* 축약: foo.find({ $where: 'this.bar > 2' })
* 정규표현식: $regex
	* foo.find({ title: /foo|bar/i })
		* title 에 foo 나 bar 가 있는지 검색
		* i 플래그로 대소문자 구분안함(인덱스 불가)
	* 정규표현식 미지원 환경에서 $regex, $options 연산자 사용
		* foo.find({ title: { $regex: 'fo | ba', $options: 'i' } })
* $mod: 몫으로 나눈 결과가 요소와 일치할 경우
* $type: 요소 타입이 명시된 타입과 일치
* $text: 텍스트 인덱스에 텍스트 검색 수행
* 질의 옵션
	* 프로젝션: 반환/배제 필드 지정
		* foo.find({}, { foo: 1 })
		* foo.find({}, { bar: 0 })
		* $slice: 반환되는 도큐먼트의 부분집합 선택
			* foo.find({}, { tags: { $slice: 10 } })
			* foo.find({}, { tags: { $slice: -10 } })
			* foo.find({}, { tags: { $slice: 10 }, tags.rating: 1 })
			* foo.find({}, { tags: { $slice: [10, 10] } })
				* 각각 skip, limit 의미
	* 정렬
		* foo.find({}).sort({foo: -1, bar: -1})
* $skip, $limit
	* 대용량시 $skip 비효율: foo.find({}).skip(500000).limit(10)
		* 셀렉터에 조건 추가가 효율적: foo.find({ date: { $gt: date } }).limit(10)

## 집계
* 집계 프레임워크
	* 집계 파이프라인: 단계별 작업
		* $project: 출력 도큐먼트에 배치할 필드 지정
		* $match: 처리될 도큐먼트 선택, find() 와 유사
		* $limit: 다음 단계에 전달될 도큐먼트 수 제한
		* $skip: 지정된 수 도큐먼트 건너뜀
		* $unwind: 배열을 확장하여 각 배열 항목당 하나의 출력 도큐먼트 생성
		* $group: 지정된 키로 도큐먼트 그룹화
		* $sort: 도큐먼트 정렬
		* $geoNear: 지리 공간위치 근처의 도큐먼트 선택
		* $out: 파이프라인 결과를 컬렉션에 씀
		* $redact: 특정 데이터에 대한 접근 제어
	* foo.aggregate([ {$match: ...}, {$group: ...}, {$sort: ...} ])
	* sql 비교
		* select: $project, $group($sum, $min, $avg, ...)
		* from: foo.aggregate(...)
		* join: $unwind
		* where: $match
		* group by: $group
		* having: $match
* foo.aggregate([{$group: { _id: '$foo', count: { $sum: 1 } }}])
	* foo 키별 값의 개수를 그룹화
	* 입력 도큐먼트 필드 앞에 $ 추가

	




