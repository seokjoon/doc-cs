## queries: https://laravel.kr/docs/5.7/queries

## 목차
```
* 결과 조회, 결과 분할, 집계
* select: 선택
* raw
* join: 조인
* union: 유니온
* where, 파라미터, 존재 여부, json
* ordering, grouping, limit&offset: 정렬, 그룹, 개수/범위
* conditional: 조건
* inset: 삽입
* update, json, increment&decrement: 수정
* delete: 삭제
* pessimistic locking: 배타적 잠금
```

## 결과 조회
* 모든 레코드(collection)
	* DB::table('users')->get();
* 단일 레코드(instance)
	* DB::table('users')->where('name', 'foo')->first();
* 단일 컬럼
	* DB::table('users')->where('name', 'foo')->value('email');
* 행
	* DB::table('roles')->pluck('title');
* 결과 분할
	* DB::table('users')->orderBy('id')->chunk(100, function($users) { ... });
* 집계(aggregates)
	* DB::table('orders')->where('finalized', 1)->avg('price');
	* DB::table('users')->count(); 
	* DB::table('orders')->max(); 
	* DB::table('orders')->min(); 
	* DB::table('orders')->sum();
* 존재 확인
	* DB::table('orders')->where('finalized', 1)->doesntExist(); 
	* DB::table('orders')->where('finalized', 1)->exists();

## select: 선택
* DB::table('users')->select('name', 'email as user_email')->get();
* DB::table('users')->distinct()->get();
* $query = DB::table('users')->select('name'); 
	* $query->addSelect('age')->get();
* keyBy('id'): id 키 연관배열
	
## RAW: sql 인젝션 주의
* havingRaw, orHavingRaw;
	* DB::table('orders')->select('department', DB::raw('SUM(price) as total_sales'))
		->groupBy('department')->havingRaw('SUM(price) > ?', [2500])->get()
* orderByRaw
	* DB::table('orders')->orderByRaw('updated_at - created_at DESC')->get();
* raw
	* DB::table('users')->select(DB::raw('count(*) as user_count, status'))
		->where('status', '<>', 1)->groupBy('status')->get();
* selectRaw
	* DB::table('orders')->selectRaw('price * ? as price_with_tax', [1.0825])->get(); 
* whereRaw, orWhereRaw; 
	* DB::table('orders')->whereRaw('price > IF(state = "TX", ?, 100)', [200])->get();

## join: 조인
* inner
	* DB::table('users')
		->join('contacts', 'users.id', '=', 'contacts.user_id')
		->join('orders', 'users.id', '=', 'orders.user_id')
		->select('users.*', 'contacts.phone', 'orders.price')->get();
* left
	* DB::table('users')->leftJoin('posts', 'users.id', '=', 'posts.user_id')->get();
* cross
	* DB::table('sizes')->crossJoin('colours')->get();
* orOn
	* DB::table('users')->join('contacts', function($join) 
		{ $join->on('users.id', '=', 'contacts.user_id')->orOn(...); })->get();
* where, orWhere
	* DB::table('users')->join('contacts', function($join) 
		{ $join->on('users.id', '=', 'contacts.user_id')->where('contacts.user_id', '>', 5); })->get();
* 서브 쿼리 조인: joinSub, leftJoinSub, rightJoinSub
	* DB::table('users')->joinSub($latestPosts, 'latest_posts', function($join) 
		{ $join->on('users.id', '=', 'latest_posts.user_id'); })->get(); 

## union: 유니온
* union, unionAll
	* DB::table('users')->whereNull('last_name')->union($first)->get();

## where 
* where, orWhere	
	* DB::table('users')->where('votes', '=', 100)->get();
		* '=' 생략 가능: where('votes', 100)->get();
		* '>=', '<>', 'like'
	* 배열: DB::table('users')->where([ ['status', '=', '1'], ['subscribed', '<>', '1'] ])->get();
	* 함수: DB::table('users')->where(function($query) { $query->where()->orWhere(); });
	* orWhere
		* DB::table('users')->where('votes', '>', 100)->orWhere('name', 'foo')->get();
		* DB::table('users')->where('name', '=', 'foo')->where(function($query) 
			{ $query->where('votes', '>', 100)->orWhere('title', '=', 'Admin' })->get();
			* 생성 SQL: select * from users where name = 'foo' and (votes > 100 or title = 'Admin');
			* 항상 orWhere 그룹을 호출해야 함
* whereBetween, whereNotBetween
	* DB::table('users')->whereBetween('votes', [1, 100])->get();
	* DB::table('users')->whereNotBetween('votes', [1, 100])->get();
* whereColumn
	* DB::table('users')->whereColumn('first_name', 'last_name')->get();
	* DB::table('users')->whereColumn('updated_at', '>', 'created_at')->get();
	* DB::table('users')->whereColumn([ ['first_name', '=', 'last_name'], ['updated_at', '>', 'created_at'] ])->get();
* whereDate, whereDay, whereMonth, whereTime, whereYear
	* DB::table('users')->whereDate('created_at', '2016-12-31')->get();
	* DB::table('users')->whereDay('created_at', '31')->get();
	* DB::table('users')->whereMonth('created_at', '12')->get();
	* DB::table('users')->whereTime('created_at', '=', '11:20:45')->get();
	* DB::table('users')->whereYear('created_at', '2016')->get();
* whereExists
	* DB::table('users')->whereExists(function($query) 
		{ $query->select(DB::raw(1))->from('orders')->whereRaw('orders.user_id = users.id'); });
		* 생성 SQL: select * from users where exists ( select 1 from orders where orders.user_id = users.id );
* whereIn, whereNotIn
	* DB::table('users')->whereIn('id', [1,2,3])->get();
	* DB::table('users')->whereNotIn('id', [1,2,3])->get();
* whereNull, whereNotNull
	* DB::table('users')->whereNull('updated_at');
	* DB::table('users')->whereNotNull('updated_at');
* where json: mysql 5.7+, postgresql
   	* DB::table('users')->where('options->language', 'en')->get();
   	* DB::table('users')->where('preferences->dining->meal', 'salad')->get();

## ordering, grouping, limit & offset: 정렬, 그룹, 개수/범위
* grouping, having
	* DB::table('users')->groupBy('account_id')->having('account_id', '>', 100)->get();
	* DB::table('users')->groupBy('first_name', 'status')->having('account_id', '>', 100)->get();
* inRandomOrder
	* DB::table('users')->inRandomOrder()->first();
* latest, oldest
	* DB::table('users')->latest()->first(); 
* limit/offset, skip/take, 
	* DB::table('users')->offset(10)->limit(5)->get();
	* DB::table('users')->skip(10)->take(5)->get();
* orderBy
	* DB::table('users')->orderBy('name', 'desc')->get();
	
## conditional: 조건
* DB::table('user')->when($role, function($query, $role) { return $query->where('role_id', $role); })->get();
* DB::table('users)->when($sortBy, function($query, $sortBy) { return $query->orderBy($sortBy); },
	function($query) { return $query->orderBy('name'); })->get();

## insert: 삽입
* DB::table('users')->insert([ 'email' => 'a@b.c', 'votes' => 0 ]);
* DB::table('users')->insert([ ['email' => 'b@c.d', 'votes' => 0], ['email' => 'c@d.e', 'votes' => 0] ]);
* auto incrementing id: auto incrementing id일 경우 추가된 id 리턴
	* $id = DB::table('users')->insertGetId([ 'email' => 'd@e.f', 'votes' => 0 ]);
	
## update: 수정
* DB::table('users')->where('id', 1)->update(['votes' => 1]);
* update(json)
	* DB::table('users')->where('id', 1)->update(['options->enabled' => true]);
* 컬럼값 증가/감소
	* DB::table('users')->decrement('votes', 5); 
	* DB::table('users')->increment('votes');
	* DB::table('users')->increment('votes', 1, ['name' => 'foo']);
	
## delete: 삭제
* DB::table('users')->delete();
* DB::table('users')->where('votes', '>', 100)->delete(); 
* 테이블 전체 비움: auto-incrementing id를 0으로
	* DB::table('users')->truncate();

## 배타적 잠금(pessimistic locking)
* DB::table('users')->where('votes', '>', 100)->lockForUpdate()->get(); 
* DB::table('users')->where('votes', '>', 100)->sharedLock()->get();



# 라라벨 appkr 예제

## raw query
* DB::insert('insert into tests(foo, bar) values(?,?)', ['FOO','BAR']); 
* DB::select('select * from tests'); 
* DB::selectOne('select * from tests where id = ?', [1]); 

## query builder		
* DB::table('tests')->delete(1); 
* DB::table('tests')->get(); 
* DB::table('tests')->find(1); 
* DB::table('tests')->first(); 
* DB::table('tests')->insert(['nameCol' => 'valueCol']);
* DB::table('tests')->limit(1)->get();
* DB::table('tests')->orderBy('name', 'desc')->get();
* DB::table('tests')->pluck('name', 'id');
* DB::table('tests')->update(['nameCol' => 'valueCol']);
* DB::table('tests')->where('id', '=', 1)->get(); 
* DB::table('tests')->where('id', 1)->get(); 
* DB::table('tests')->where(function($query) { $query->where('id', 1); })->get(); 
* DB::table('tests')->whereId(1)->get(); 
* DB::table('test')->...
	* count(), distinct(), groupBy(), having(), join(), union(), whereNull(), whereNotNull(), 
	* select(DB::raw('count(*) as cnt'));