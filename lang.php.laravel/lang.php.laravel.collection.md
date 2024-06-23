
* after: 지정된 항목 뒤 항목을 반환
	* $c->after(foo)
	* $c->after(function(int $item, int $key) { return $item > 5 }
* all
* average, avg
	* $c->avg(foo)
* before: after의 반대
* chunk: 지정된 크기의 여러 컬렉션으로 분할
	* $c->chunk(3)
	* $c->chunkWhile(function(string $v, int $k, Collection $chunk) { return $v === $chunk->last() })
* collapse: 다차원 배열을 일차원 배열로
* collect
* concat: 배열 또는 컬렉션을 추가
	* $c->concat(foo)->concat(bar)
	* 키를 리인덱싱함. 연관 컬렉션 키 유지하려면 merge
* contains: 항목 포함 여부
	* $c->contains(value)
	* $c->contains(key, value)
	* $c->contains(function(int $v, int $k) { return $v > 5 })
* count
* countBy: 값의 발생 횟수
	* $c->countBy()->all()
	* $c->countBy(function (string $email) { return substr(strrchr(@email, '@', 1)) })
* crossJoin
	* collect([1,2])->crossJoin(['a','b'])
		* [ [1,'a'], [1,'b'], [2,'a'], [2,'b'] ]
* dd: 덤프하고 종료
	* 종료하지 않으려면 dump
* diff: 다른 콜렉션 또는 배열과의 차이 출력
	* $c->diff(bar)
	* diffAssoc
	* diffAssocUsing
	* diffKeys
* doesntContain: 항목 비포함 여부
	* $c->doesntContain(foo)
	* $c->doesntContain(function(int $v, int $k) { return $v < 5 })
* dot: 다차원 컬렉션을 점 표기한 일차원 컬렉션으로 변경
	* $c->dot()
* duplicates: 중복값 반환
	* $c->duplicates()
	* $c->duplicates(foo): 속성 지정
* each: 반복, 반복을 false 로 중단
	* $c->each(function(int $item, int $k) { if(cond) return false } )
* ensure: 모든 요소가 지정된 유형(목록)인지 확인
	* $c->ensure(User::class)
	* $c->ensure('int')
* every: 모든 요소 테스트 통과 여부: 비어 있을 경우 true
	* $c->every(function(int $v, $int $k) { return $v > 2 })
* except: 지정 키 제외
	* collect(['a' => 1, 'b' => 2, 'c' => 3])->except(['a','b'])
* filter
	* $c->filter(function(int $v) { return $v > 2 })
	* 콜백이 없을 경우 모든 false, null, '', 0, [] 등이 제거
* first
	* $c->first()
	* $c->first(function() {})
	* firstOrFail(): 없으면 예외 발생
	* firstWhere(key, value)
	* firstWhere(key, cond, value)
* flatten: 다차원을 평면화, 깊이 인수 가능
	* $c->flatten(1)
* flip: 키/값 반전
* forget: 키로 항목 제거: 리턴 아니고 직접 수정
	* $c->forget(key)
* get: 키로 항목 반환, 없으면 null
	* $c->get(key)
	* $c->get(key, valueDefault)
* groupBy: 키 기준으로 그룹화
	* $c->groupBy('foo')
	* $c->groupBy(function(array $items, int $key) { return substr($item['foooo'], -2) })
* has: 키 존재 여부
	* $c->has([k1, k2])
	* hasAny
* implode: 항목 결합
	* $c->implode(key, ',')
	* $c->implode(function(array $item, int $key) { return strtoupper($item['foo']) }, ',')
* intersect 존재하지 않는 값 제거(존재하는 값 반환)
	* $c->intersect([foo, bar])
	* intersectAssoc: 존재하는 키/값 반환
		* $c->intersectAssoc([foo => 1, bar => 2])
	* intersectByKeys
* isEmpty
	* isNotEmpty
* join: 값을 문자열과 결합
* keyBy: 키로 컬렉션 키 지정
	* collect([['k1' => 1, 'k2' => 2], ['k1' => 3, 'k2' => 4])->keyBy(k1)
		* [ 1 => ['k1' => 1, 'k2' => 2], 3 => ['k1' => 3, 'k2' => 4] ]
	* $c->keyBy(function() {})
* keys: 모든 키 반환
* last
* lazy
* map: 반복
	* $c->map(function(int $v, int $k) { return $v * 2 })
	* 원본을 변환할 경우 map 대신 transform
* mapInto: 인스턴스 생성(생성자에 값 전달)
	* collect(['a', 'b'])->mapInto(Foo::class)
* mapSpread
* mapToGroups: 그룹화
	* $c->mapToGroups(function(array $v, int $k) { return $v['dept'] => $v['name'] })
* mapWithKeys
	* $c->mapWithKeys(function(array $v) { return [$v['email'] => $v['name'] })
* max: 최대값
	* $c->max(foo)
* median: 중앙값
	* $c->median(foo)
* merge: 배열이나 컬렉션을 병합
	* mergeRecursive: 같은 키의 값을 덮어쓰지 않고 배열로
* min: 최소값
	* $c->min()
	* $c->min(foo)
* mode: (통계)
* nth: 모든 n번재 요소로 새 컬렉션
	* $c->nth(4)
	* $c->nth(4, 1)
* only: 해당 키만 반환
	* $c->only('foo', 'bar')
* pad: 지정 크기까지 지정 값으로 채움
	* $c->pad(5, foo)
	* $c->pad(-5, foo): 음수는 왼쪽을 채움
* partition: 테스트 통과 요소와 비통과 요소를 분리
	* [$foo, $bar] = $c->partition(function(int $i) { return $i < 3 })
* percentage: 테스트 통과하는 항목 비율
	* $c->percentage(fn ($v) => $v == 1)
	* $c->percentage(fn ($v) => $v == 1, precision: 3): 소수점 자리수
* pipe: 클로저 실행 결과 반환
	* $c->pipe(function (Collection $col) { return $col->sum() })
	* pipeInto: 새 인스턴스 생성하고 컬렉션을 생성자에 전달
		* $c->pipeInto(FooCollection::class)
	* pipeThrough
* pluck
	* $c->pluck(foo)
	* $c->pluck(foo, bar): 두번째 인수의 값을 키로
	* $c->pluck(foo.bar): dot 표기법으로 중첩 값 검색
	* 중복시 마지막 일치 요소
* pop: 마지막 항목 반환하고 제거
	* $c->pop(5): 여러개 항목 반환하고 제거
* prepend: 시작 부분에 항목 추가
	* $c->prepend(foo)
	* $c->prepend(value, key)
* pull: 키의 항목을 반환하고 제거
	* $c->pull(foo)
* push: 끝에 항목 추가
* put: 키와 값 설정
	* $c->put(key, value)
* random: 임의의 항목 반환
	* $c->random(5): 반환 개수 지정
	* $c->random(fn (Collection $items) => min(10, count($items))
* range: 범위 지정
	* $c->range(3, 6)
* reduce: 단일 값으로 줄여 각 반복 결과를 후속 반복에 전달
	* $c->reduce(function (?int $carry, int $item) { return $carry + $item })
	* $c->reduce(function (?int $carry, int $item) { return $carry + $item }, $init)
	* reduceSpread: 여러 초기값 허용
* reject: 클로저로 필터링: filter 의 반대
* replace: merge 와 유사하나 숫자키 일치도 덮어씀
  * replaceRecursive
* reverse: 키 유지하면서 순서 반전
* search: 검색 값이 있으면 키 반환
  * $c->search(foo)
  * $c->search(foo, strict: true)
  * $c->search(function(int $item, int $k) { return $item > 5 })
* select: SQL select 와 유사
  * $c->select(['foo', 'bar'])
* shift: 첫번째 항목 반환하고 제거
  * $c->shift(3): 여러 항목 반환/제거
* shuffle: 랜덤
  * $c->shuffle()
* skip: 시작부터 지정 수 요소 제거
  * $c->skip(5)
* skipUntil: 값 혹은 콜백이 참일때까지 건너뜀
  * $c->skipUntil(3)
  * $c->skipUntil(function(int $item) { return $item > 3 })
* skipWhile: skipUntil 과 유사하나 콜백결과가 false 일때 반환
* slice: 조각
  * $c->slice(4)
  * $c->slice(5, 3)
* sliding
  * collect([1,2,3,4])->sliding(2)
    * [[1,2], [2,3] [3,4]]
* sole: 테스트 통과한 첫 요소 반환, 단 정확히 하나의 요소와 일치
* sort: 정렬
* sortBy
  * $c->sortBy(foo)->values(): 정렬됐지만 원래 배열키를 유지하므로 values 로 인덱스 재설정
  * $c->sortBy(foo, SORT_NATURAL): 두번째 인자로 플래그: https://www.php.net/manual/en/function.sort.php
  * $c->sortBy(function(array $items) { return count($items[foo]) } )
  * $c->sortBy([ [foo, 'asc'], [bar, 'desc'] ]): 여러 속성 기준
  * $c->sortBy([ fn() => (), fn() => () ]): 여러 속성 클로저
  * sortByDesc
  * sortDesc
* sortKeys: 키 기준 정렬
  * $c->sortKeys()
  * sortKeysDesc
  * sortKeysUsing
* splice: 지정 위치 기준으로 분할
  * $o = $c->splice(2)
    * $o: [3,4]
    * $c: [1,2]
  * 두번째 인수는 결과 크기 제한
  * 세번째 인수는 제외를 대체하는 항목
* split: 지정된 그룹 수로 나눔
  * $c->split(3): []
* sum: 합계
  * $c->sum()
  * $c->sum(foo)
  * $c->sum(function (array $items) { return count($items[foo]) })
* take: 지정 개수만큼 반환
  * $c->take(3): [0, 1, 2]
  * $c->take(-2): 뒤에서부터
  * takeUntil: 지정된 콜백이 반환될때까지의 항목을 반환
    * $o = $c->takeUntil(function(int $i) { return $i > 3 } )
    * $o = $c->takeUntil(3)
  * takeWhile: takeUntil 과 유사하나 콜백결과가 false 일때 반환
* tap: 컬렉션에 영향을 주지 않고 작업
  * $c->sort()->tap(function (Collection $col) { ... } )-> ...
* times: 클로저를 지정 횟수만큼 호출
  * $c = Collection::times(10, function(int $num) { return $num * 9 })
* toArray
  * all
* toJson
* transform: 반복, 콜백 반환값 반영
  * $c->transform(function(int $i) { return $i * 2 })
* undot: dot 표기법 사용하는 1차원 컬렉션을 다차원 컬렉션으로 변경
* union: 배열을 컬렉션에 추가, 중복될 경우 원본 우선
  * collect(1 => ['a'], 2 => ['b'])->union([3 => ['c'], 1 => ['d'])
* unique: 모든 고유 항목 반환, values 로 인덱스 재설정 필요
  * $c->unique()->values()
  * $c->unique(foo)
  * $c->unique(function (array $item) { return $item[foo] . $item[bar] })
  * uniqueStrict
* unless: 첫째인수 조건 실패시 둘째인수 콜백 실행, 첫째인수 조건 성공시 셋째인수 콜백 실행
  * $c->unless(cond, function(Collection $col) { return $col->push(foo) })
  * $c->unless(cond, function(Collection $col) { return $col->push(foo) }, function(Collection $col) { return $col->push(bar) })
  * 반대는 when
* unlessEmpty: whenNotEmpty 의 alias
* unlessNotEmpty: whenEmpty 의 alias
* unwrap: static 메소드: 기본 항목 반환
  * Collection::unwrap(collect[user1, user2, user3])
    * [User::class]
* value: 첫 요소에서 지정값 검색
  * collect(['a' => 1, 'b' => 2], ['a' => 3, 'b' => 4])->value('a')
* values: 키인덱스 재설정
  * collect([2 => 'a', 3 => 'b'])->values()
    * [0 => 'a', 1 => 'b']
* when: 첫 인수가 참이면 콜백 실행, 두번째 콜백은 거짓일때 실행
  * $c->when(cond, function(Collection $col, int $v) { return $col->push(foo) })
  * $c->when(cond, function(Collection $col, int $v) { return $col->push(foo) }, function(Collection $col, int $v) { return $col->push(bar) })
* whenEmpty: 컬렉션이 비었을때 콜백 실행, 비어있지 않을때 두번째 콜백 실행
  * $c->whenEmpty(function() {})
  * $c->whenEmpty(function() {}, function() {})
* whenNotEmpty: 컬렉션이 비어있지 않으면 콜백 실행, 비어있으면 두번째 콜백 실행
* where: 키/값 기준으로 필터링
  * $c->where('price', 200)
  * $c->where('price', '>=',200)
  * whereStrict
* whereBetween: 범위 필터링
  * $c->whereBetween('price', [100, 200])
  * whereNotBetween: 범위 외부 필터링
* whereIn: 포함 필터링
  * $c->whereIn('price', [100, 200])
  * whereInStrict
  * whereNotIn: 포함 외부 필터링
    * whereNotInStrict
* whereInstanceOf: 지정된 클래스 유형 기준으로 필터링
  * collect([new User, new User])->whereInstanceOf(User::class)
* whereNull: 키가 null 인 항목 반환
  * $c->whereNull(foo)
* whereNotNull: 키가 null 이 아닌 항목 반환
  * $c->whereNotNull(foo)
* wrap
* zip
  * collect(['a', 'b'])->zip(1, 2)
    * ['a' => 1, 'b' => 2]


## lazy collection
* generator 활용해서 메모리 사용량 낮게 큰 데이터셋 작업: 큰 파일이나 다수의 인스턴스 처리
* LazyCollection::make(function() {}): 생성
* takeUntilTimeout: 지정된 시간까지만 열거하고 중지: 주기적으로 실행되는 예약된 작업의 최대 실행시간을 설정 가능
  * $lc = LazyCollection::times(INF)->takeUntilTimeout(now()->addMinute())
    * $lc->each(function() {})
* tapEach
* throttle: 지정된 시간(초) 후 반환
  * User::where(foo, 1)->cursor()->throttle(1)->each(function() {})
* remember: 반환된 값을 다음 반환에서 제외
  * $users = User::cursor()->remember()
    * $users->take(5)->all()
    * $users->take(20)->all()








