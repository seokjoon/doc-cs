## 라라벨 사용법: 퍼블리셔 레벨

## 라우팅
* 요청 foo를 뷰 bar로 바로 연결: ``` Route::get('/foo', function() { return view('bar') }) ```
* 라우트 목록 확인: ``` php artisan route:list ```