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
	* findOne 에 파라미터 없을 경우 무작위 도큐먼트 리턴
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
			* foo.aggregate([ {$match: {}}, {$project: {fee:1, bee:1}} ])
		* $match: 처리될 도큐먼트 선택, find() 와 유사
		* $limit: 다음 단계에 전달될 도큐먼트 수 제한
		* $skip: 지정된 수 도큐먼트 건너뜀
		* $unwind: 배열을 확장하여 각 배열 항목당 하나의 출력 도큐먼트 생성
		* $group: 지정된 키로 도큐먼트 그룹화
			* $addToSet: 그룹에 고유 값 배열 생성
			* $first, $last: 그룹의 첫번째/마지막 값, $sort를 선행해야 의미있음
			* $mas, $min: 그룹의 필드 최대/최소값
			* $avg: 그룹 필드 평균값
			* $push: 그룹의 모든 값의 배열 반환, 중복값 제거하지 않음
			* $sum: 그룹의 모든 값의 합계
		* $sort: 도큐먼트 정렬
		* $geoNear: 지리 공간위치 근처의 도큐먼트 선택
		* $out: 파이프라인 결과를 컬렉션에 씀, materialiezed view 와 유사
		* $redact: 특정 데이터에 대한 접근 제어
	* foo.aggregate([ {$match: ..}, {$group: ..}, {$sort: ..} ])
	* sql 비교
		* select: $project, $group($sum, $min, $avg, ..)
		* from: foo.aggregate(..)
		* join: $unwind
		* where: $match
		* group by: $group
		* having: $match
* foo.aggregate([{$group: { _id: '$foo', count: { $sum: 1 } }}])
	* foo 키별 값의 개수를 그룹화
	* 입력 도큐먼트 필드 앞에 $ 추가
	* findOne 처럼 단일 결과가 아닌 목록 반환
		* foo.aggregate().next(): 결과의 첫번째 도큐먼트
	* $group 앞에 $match 위치: 질의 대상 도큐먼트가 대폭 감소
	* 평균 리뷰: 158p
		* foo.aggretate([ { $match: { .. } }, { $group: { .., average: { $avg: .., count: { $sum: .. } } }} ]).next()
			* 단일
	* 등급별 리뷰
		* foo.aggregate([ { $match: { .. } }, { $group: { .., count: { $sum: .. } } } ]).toArray()
			* 배열
	* join 과 유사한 옵션: 161p
		* forEach 의사 조인
		* foo.aggregate([{$group: {..}}]).forEach(function(val) { fee.findOne(); ..; bar.insert(val) })
			* findOne 과 insert 를 사용하는 pseudo-joing 은 느려질 수 있음
	* $out, $project
		* $out: 파이프라인 출력을 자동으로 컬렉션에 저장
			* foo.aggregate([ {$group: {}, { $out: 'bar' }} ])
				* 결과 컬렉션을 생성하거나 대체
		$project: 다음 단계로 전달할 필드 필터링
	* $unwind
		* 배열을 확장하여 모든 입력 도큐먼트 배열 항목에 대해 하나의 출력 도큐먼트 생성
		* foo.aggregate([ {$project: {}}, {$unwind: ..}, {$group: {..}}, {$out: ..} ])
	* 연도별, 월별 판매 요약: 165p
		* foo.aggregate([ {$match: {}}, {$group: { _id: { year: { $year: .. }, month: { $month: .. } }, count: { $sum: .. }, totla: { $sum: .. } }}, {$sort: {}} ])
	* 맨해튼 최고 고객 찾기: 166p
		* $match: 검색어 조건검색
		* $group: 고객별 주문합계
		* $match: 주문합계 조건검색
		* $sort: 금액으로 정렬
		* foo.aggregate([ {$match: ..}, {$group: ..}, {$match: ..}, {$sort: ..}, {$out: ..} ])
* 문자열 함수
	* $concat: 두개 이상의 문자열을 단일 문자열로 연결
	* $strcasecmp: 대소문자 구분하지 않는 비교, 숫자 반환
	* $substr: 문자열의 부분문자열 생성
	* $toLower, $toUpper: 소/대문자 변환
* 산술함수
	* $add, $divide, $mod, $multiply, $subtract
* 날짜/시간함수
	* $dayOfYear, $dayOfMonth, $dayOfWeek
	* $year, $month, $week
	* $hour, $minute, $second, $millisecond
* 논리함수
	* $and, $or
	* $eq, $ne, $not(값의 반대 조건 반환)
	* $gt, $gte, $lt, $lte
	* $cmp(비교, 동일하면 0 반환), $cond(조건, if then else), ifNull
* 집합함수: 178p
	* $setEquals: 두 집합이 완전히 동일
	* $setIntersection: 교집합
	* $setDifference: 차집합(첫 집합 기준)
	* $setUnion: 합집합
	* $setIsSubset: 부분집합
	* $anyElementTrue: 하나라도 true 면 true
	* $allElementTrue: 모두 true 면 true
	* $not
	* $or
* 기타함수
	* $meta: 텍스트 검색 관련 정보
	* $size: 배열 크기
	* $map: 배열 각 멤버에 expression 적용
	* let, literal
* 집계 성능
	* 인덱스는 $match, $sort 에서만 가능
	* sharding 사용시 $match, $project 는 개별 샤드에서 실행
* 집계 옵션
	* explain, allowDiskUse, cursor
	* aggregate() 의 두번째 파라미터
		* foo.aggregate(pipeline, {
			explain: true, allowDiskUse: true, cursor: { batchSize: n }
		})
* 집계 기타
	* count(), distinct()
		* foo.distinct('bar')
	* 맵리듀스
		* map = function() { ..; emit(foo, { .. }) }
		* reduce = function(k, v) { ..; return foo }
		* 유연하지만 집계보다 느림


## 업데이트, 원자적 연산, 삭제
* 업데이트
	* 항상 업데이트 연산자로 시작
	* 도큐먼트 전체, 혹은 특정 필드(더 나은 성능)
	* 대치(도큐먼치 전체)
		* bar = foo.findOne({ _id: 3 })
			* bar['bee'] = 123
			* foo.update({ .. }, bar)
	* 연산자(특정 필드)
		* foo.update({ _id: 3 }, { $set: { bar: 123 } })
	* 컬럼값 증가: foo.update({ .. }, { $inc: { ctr: 1 } })
	* foo.update({ .. }, { $set: { fee: 12, bee: 34 }, { $inc: { ctr: 1 } } })
	* 계층: foo.update({ .. },  'fee.fuu': 12, { $set: { 'fee.$.faa': 34 } })
* 원자적 도큐먼트 프로세싱
	* 다른 연산이 끼어들 수 없음(대기)
	* findAndModify
		* mdb의 모든 업데이트는 원자적이지만 findAndModify 는 도큐먼트를 자동으로 반환
		* job queue 나 state machine 구축 가능, 트랜잭션
		* out = foo.findAndModify({
			query: { uid: ObjectId('fee'), state: 10, },
			update: { $set: { state: 20 } }
		})
		* 실패시: nil 반환, InventoryFetchFailure 예외 발생, 롤백
		* findOneAndUpdate, findOneAndReplace 로 대체됨
* foo.update_one({}, { $set: { fee: 12 }, $addToSet: { bee: 34 } })
* 다중 도큐먼트 업데이트
	* 다중 업데이트를 명시하지 않으면 selector 와 일치하는 첫번째 도큐먼트만 업데이트
	* foo.update({}, { $addToSet: { .. } }, { multi: true })
* 업서트
	* 도큐먼트가 있으면 업데이트, 없을 경우 새로 추가
	* foo.update({ .. }, { $addToSet: { .. } }, { upsert: true })
* 업데이트 연산자
	* $inc: 증가, 감소
		* foo.update({ .. }, { $inc: { ct: -1 } })
		* foo.update({ .. }, { $inc: { ct: 3.45 } })
	* $set, $unset: 값 설정, 값 삭제
		* foo.upate({ .. }, { $set: { fee: [1,2,3] } })
		* foo.upate({ .. }, { $set: { 'fee.fuu': 12 } })
		* foo.upate({ .. }, { $unset: { fee: 1 } })
		* foo.upate({ .. }, { $unset: { 'fee.fuu': 1 } })
		* 배열의 경우 $unset 은 요소를 삭제하지 않고 null 설정, 삭제는 $pop, $pull
	* $rename: 키 이름 변경
		* foo.updateMany({ .. }, { $rename: { fee: fuu } })
		* foo.updateMany({ .. }, { $rename: { 'fee.fuu': 'fee.faa' } })
	* $setOnInsert: 업데이트가 아닌 삽입시에만 필드 설정
* 배열 업데이트 연산자
	* $push: 배열에 단일값 추가
		* foo.update({..}, { $push: { tags: 'fee' } })
	* $each: 배열에 다수값 추가
		* foo.update({..}, { $push: { tags: { $each: [ 'fee', 'fuu' ] } } })
		* $each 는 $addToSet 과 $push 에서만 사용가능
	* $slice: 배열 분할
		* foo.update({..}, { $push: { fee: { $each: [ 2, 3], $slice: -5 } } })
			* 값을 배열 끝에 추가한 후 처음부터 5개만 남을때까지 요소 제거
			* $slice 에 양수를 전달하면 배열의 끝에서부터 요소 제거
	* $sort: 배열 분할 전 정렬
		* foo.update({..}, { $push: { $each: [..], $slice: -2, $sort: { fee: 1 } } })
	* $addToSet: 배열에 존재하지 않을 경우에만 값 추가
		* foo.update({..}, { $addToSet: { tags: 'fee' } })
		* foo.update({..}, { $addToSet: { tags: { $each: [ 'fee', 'fuu' ] } } })
			* 다수 값에 대해 수행
	* $pop: 배열에서 마지막/첫 요소 삭제, 이름과 달리 값을 반환하지 않음
		* 마지막: foo.update({..}, { $pop: { 'tags': 1 } })
		* 처음: foo.update({..}, { $pop: { 'tags': -1 } })
	* $bit
	* $pull: 배열에서 요소 위치 대신 값으로 삭제
		* foo.update({..}, { $pull: { tags: 'fee' } })
	* $pullAll: 배열에서 삭제할 값의 목록 지정
		* foo.update({..}, { $pullAll: { tags: [ 'fee', 'fuu' ] } })
* 위치 업데이트: $
	* foo.update({..}, { $set: { 'fee.$.faa': 23 } })
		* 위치를 알 필요 없이 조건으로 하위 도큐먼트의 속성값 변경
* 삭제
	* foo.remove({..})
	* foo.remove({.., $isolated: true})
		* 고립되어 수행해서 양보하지 않음(일관성 보장)
	* foo.remove({.., $isolated: true}, { $set: {..} }, { multi: true })


## 인덱싱, 쿼리 최적화
* 단순/복합 인덱스
	* 쿼리당 하나의 인덱스: 하나 이상의 필드 질의시(복합키) 그 필드들에 대한 복합 인덱스
	* 복합 인덱스에서는 키의 순서가 중요
	* a-b 복합인덱스가 있다면 a 인덱스는 중복(제거 필요), b 인덱스는 중복 아님
	* 단일키/복합키 인덱스
	* B-tree
* 인덱스 타입
	* 고유 인덱스: unique
		* foo.createIndex({ fee: 1 }, { unique: true })
		* foo.createIndex({ fee: 1 }, { unique: true, dropDups: true })
			* 이미 존재하는 중복된 키값을 가진 도큐먼트 삭제
	* 희소 인덱스
		* 밀집(dense, 임의 도큐먼트에 해당 키가 없어도 인덱스에 null 로 존재)
			* 삽입 연산 실패 가능성
		* 희소(spare) 인덱스: 인덱스의 키가 null 이 아닌 값을 가지고 있는 도큐먼트만
			* foo.createIndex({..}, { unique: true, spare: true })
		* partial 인덱스: 희소 인덱스의 슈퍼셋(최근 버전)
	* 해시(hashed) 인덱스
		* 인덱스 엔티리의 지역성 변경, 샤드된 컬렉션에서 유용
	* 지리공간적(geospatoal) 인덱스
* 인덱스 관리
	* 생성(복합인덱스)
		* foo.createIndex({ foo: 1, bar: -1 })
	* 조회
		* foo.getIndexes()
	* 삭제
		* foo.dropIndex('foo_1')
	* 인덱스 생성
		* 백그라운드 인덱싱: foo.createIndex({..}, { background: true })
		* 오프라인 인덱싱
	* 백업
		* mongodump 나 mongorestore 는 컬렉션과 인덱스의 정의만 보관, 재생성
		* 백업에 인덱스 포함하려면 파일 백업
		* mongodump --db foo --out /foo/$(date +%y-%m-%d)'
		* mongorestore -u testuser -p testpw --authenticationDatabase admin --drop --db foo ./import
	* 파편화
		* foo.reIndex()
			* 재구축, 진행중 쓰기 잠금
* 쿼리 최적화
	* 프로파일러
		* 활성화
			* use foo; db.setProfilingLevel(2)
				* 레벨 2: 모두 기록, 레벨 1: 100밀리 이상만 기록
		* system.profile 에 저장(capped 컬렉션)
			* db.system.profile.find().sort({ $natural: -1 }).limit(5).pretty()
	* explain()
		* foo.find({}).explain()
		* foo.find({}).explain('executionStats')


## 텍스트 검색
* 단지 패턴 매칭만은 아님
	* 대소문자 구분하지 않음
	* 전체 단어 일치 지정: ex) java 와 javascript 구분
	* stemming: 검색 단어가 줄기(stem) 또는 뿌리(root) 단어로 변환됨
	* facets: 그룹화, 동의어 라이브러리
	* 형태소 분석, 불용어
* mdb 지원
	* 형태소 분석, 불용어 삭제
	* 필드 이름 가중치
	* 다국어 지원
	* 구문/단어 일치, 구/단어 결과 제외
* 지원 방법: 인덱스 정의, 텍스트 검색 사용
	* foo.createIndex({ title: 'text', desc: 'text', tags: 'text' })
	* foo.find(
		{ $text: { $search: 'fee' } },
		{ _id: 0, title: 1, desc: 1, tags: 1 }
	)
		* '_id:0' 표기: 출력에 _id 제외
* 텍스트 검색 인덱스 정의
	* 각 필드의 가중치 정의
	* foo.createIndex(
		{ title: 'text', desc: 'text' },
		{ weights: { title: 10, desc: 2 } }
	)
	* 텍스트 인덱스 크기: 컬렉션보다 큼, 대부분의 텍스트를 복제
	* 인덱스 이름의 길이: 필드명의 연결, 인덱스 최대 길이 제한(123바이트) 고려하여 사용자 정의 이름 할당 필요
	* 인덱스 이름을 사용자 정의
		* foo.createIndex({..}, { .., name: 'foo_text_index' })
	* 와일드카드 필드명: 모든 필드를 문자열로 인덱싱
		* foo.createIndex({ '$**': 'text', {..} })
* find 텍스트 검색
	* 단순: 문자열을 단어로 파싱 => 불용어 제거 => 어간
	* 정확한 구문 매칭, 단어가 결과에 포함: 큰따옴표 내부의 단어/구문
		* foo.find({ $text: { $search: 'foo "fee" fuu' } }, {..})
	* 특정 단어/구 포함한 도큐먼트를 제외: 단어/구 앞에 빼기 기호
		* foo.find({ $text: { $search: 'foo -fee fuu' } }, {..})
		* foo.find({ $text: { $search: 'foo -"fee fuu"' } }, {..})
	* 제약
		* 다중 키 복합 인덱스, 지리공간 복합 키 인덱스
		* $text 쿼리 표현식이 쿼리에 포함되면 hint() 사용불가
		* 정렬은 텍스트 필드 인덱스에서 정렬 순서를 가져올 수 없음
* 텍스트 검색 스코어
	* 도큐먼트의 관련성 평가
		* 단어가 도큐먼트에 표시된 횟수 기반
		* 인덱스 생성시 필드에 할당된 가중치도 사용
	* fs.find(
		{$text: {$search: 'test'}},
		{_id:0, title:1, desc:1, score: {$meta: 'textScore'}}
	)
	* 가중치 기본값 1, 스코어에 영향 미침
	* 가중치 정렬
		* fs.find({..}, {..}).sort({ score: { $meta: 'textScore' } })
* 집계 프레임워크 텍스트 탐색
	* foo.aggregate([
		{ $match: { $text: { $search: 'foo in fee' } } },
		{ $project: { title: 1, score: { $meta: 'textScore' } } },
		{ $sort: { score: -1 } },
	])
	* sort score -1 내림차순, 1 오름차순(낮은 스코어)
	* 제약
		* $text 포함한 $match 연산자는 파이프라인 첫 연산자, $text 함수는 파이프라인에 한번만 가능
		* $text 는 $or 혹은 $not 과 함께 사용 불가
	* 없는 필드 보정: 325p
		* foo.aggregate([
			{ $match: .. },
			{ $project: { .., multiplier: { $cond [ 'descLong', 1, 3 ] } } },
			{ $project: { .., multiplier: 1, scoreAdj: { $multiplier: [ '$score', '$multiplier' ] } } },
			{ $sort: ..}
		])
* 텍스트 검색 언어
	* 언어 설정 시점: 인덱스, 도큐먼트 삽입시, find() 혹은 aggregate() 텍스트 검색시
	* mdb 는 형태소 분석 등에서 전문 검색 엔진보다 간단하지만 제한적
	* 인덱스 언어 지정
		* foo.crateIndex({..}, {.., default_language: 'french'})
	* 도큐먼트 언어 지정
		* foo.insert({.., language: 'french'})
	* 검색 언어 지정
		* foo.find({ $text: { $search: 'fee', $language: 'french' } })
	* none 지정시 정확한 단어 일치만 포함


## 관리
* 진단
	* mongostat: 시스템
	* mongotop: 연산
	* mongosniff: 네트워크 트래픽 덤프
	* bsondump: bson 파일을 json 표시
* 백업 방식
	* mongodump, mongorestore
		* mongodump -h localhost --port 27017
		* mongodump --db foo --collection fee --out fuu
		* mongorestore -h localhost --port 27017 dump --drop
		* mongorestore -d foo -c values path
	* 데이터 파일 복사
		* db 잠금 필요
			* use admin
			* db.fsyncLock()
			* db.fsyncUnlock(): 해제 요청일 뿐 즉시 완료되지는 않음
	* MMS 백업
* 보안
	* mongod --bind_ip 127.0.0.1,xxx.xxx.xxx.xxx
	* 암호화: ssl
		* mongod --sslMode requireSSL --sslPEMKeyFile foo.pem
	* 인증
		* 서비스 인증: 인증서 인증
		* 사용자 인증
			* mongod --auth
			* use admin
				* db.createUser({ user: 'foo', pwd: 'fee', roles: [{ role: 'userAdminAnyDatabase', db: 'admin' }] })
				* db.auth('foo', 'fee')
				* db.logout()
				* db.createUser({ user: 'bar', pwd: 'bee', roles: [{ role: 'readWrite', db: 'fuu' }] })
				* db.createUser({ user: 'bar', pwd: 'bee', roles: [{ role: 'read', db: 'fuu' }] })
			* 사용자 삭제
				* use fuu
					* db.dropUser('bar')
			* revokeRolesFromUser, grantRolesToUser
		* 로컬 호스트 예외
			* 첫번째 사용자가 추가되면 인증되지 않은 연결에 권한 없음
			* --setParameter enableLocalhostAuthBypass = 0
* 들여오기/내보내기
	* mongoimport, mongoexport
		* mongoimport -d foo -c fee --type csv --headerline fee.csv
		* mongoimport --db foo --collection fee --type json --drop ---file fuu.json
		* mongoexport -d foo -c fee -o fee.csv
	* 스크립트
* 압축/복구
	* 복구: 데이터를 압축하고 인덱스를 재구축
		* mongod --repair
		* use foo
			* db.runCommand({ repairDatabase: 1 })
	* 인덱스 재구축
		* use foo
			* db.fee.reIndex()
	* 컬렉션 압축
		* db.runCommand({ compact: 'fee' })
		* db.runCommand({ compact: 'fee', force: true })


## 설계 패턴
* 임베드 vs 레퍼런스
* 일대다, 다대다
* 트리
* 작업 큐
* 동적 속성
* 트랜잭션
* 지역성 및 선 계산
* 안티 패턴
	* 인덱싱 부주의
	* motley 타입: 컬렉션 내 동일 키는 모두 같은 타입이어야 함
	* bucket 컬렉션: 컬렉션은 하나의 개체에 대해서만 사용
	* 깊게 중첩된 대용량 도큐먼트: 도큐먼트는 크기를 작게, 적은 중첩구조
	* 사용자당 한 컬렉션
	* 샤드 불가능한 컬렉션



