

* chunk: https://laravel.com/docs/11.x/eloquent#chunking-results
	* User::chunk(200, function (Collection $users) { foreach($users as $user) { ... } })
	* 첫번째 인수는 chunk 당 수신하는 레코드 수
	* chunking using by lazy
		* User::where()->lazyById(200, $column = 'id')->each->...
* cursor


* factory
	* Foo::factory()
	* Foo::factory()->make()
	* Foo::factory()->make([ ... ])
	* Foo::factory()->count(10)->make()
	* Foo::factory()->create(): DB에 저장
