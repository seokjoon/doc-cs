# 3장 노드 기능 알아보기
## 3.1 REPL 사용하기
    * Read, Eval, Pring, Loop: node 콘솔
## 3.2 JS 파일 실행하기
    * node foo.js
## 3.3 모듈로 만들기
    * const foo = 'foo'; module.exports = { foo, };
    * const { foo, } = require('./foo.js'); function bar() {}; module.exports = bar;
    * es6 스타일(node와 별개)
        * import { foo, } from './foo'; function bar() {}; export default bar;
## 3.4 노드 내장 객체 알아보기
* 3.4.1 global
* 3.4.2 console: time(), timeEnd(), log(), error(), dir(), trace(), 
* 3.4.3 타이머: setTimeout(), setInterval(), setImmediate()
* 3.4.4 __filename, __dirname
* 3.4.5 module, exports, require
* 3.4.6 process: pid, uptime(), cwd(), env, nextTick(), exit(), 
## 3.5 노드 내장 모듈 사용하기
* 3.5.1 os: arch(), platform(), type(), uptime(), hostname(), release(), homedir(), tmpdir(), release(), cpus().length, freemem()m totalmem(), constants
* 3.5.2 path: sep, delimiter, dirname(), extname(), basename(), parse(), format(), normalize(), isAbsolute(), relative(), join(), resolve(),
* 3.5.3 url: parse(), format()
    * searchParams: getAll(), get(), has()m keys(), values(), append(), set()m delete(), toString()
    * querystring: parse(), stringify()
* 3.5.4 querystring
* 3.5.5 crypto
    * createHash().update().digest()
    * createCipher(), createDecipher(), update(), final() 
* 3.5.6 util: deprecated(), promisify()
* 3.5.7 worker_threads
* 3.5.8 child_process
* 3.5.9 기타 모듈들
## 3.6 파일 시스템 접근하기
* 3.6.1 동기 메서드와 비동기 메서드
    * readFile(), readFileSync(), toString()
* 3.6.2 버퍼와 스트림 이해하기
    * Buffer: from(), length(), concat(), toString(), alloc(),
    * createReadStream()
        * on(): data, end, error
        * pipe(), zlib.createGzip()
    * createWriteStream(), write(), end()
        * on(): finish
* 3.6.3 기타 fs 메서드 알아보기
    * access(), mkdir(), open(), rename(), 
    * readdir(), unlink(), rmdir(),
    * copyFile(), const foo = require('fs').promises;
* 3.6.4 스레드풀 알아보기
## 3.7 이벤트 이해하기
    * require('events'): addListener(), on(), emit(), removeAllListeners(), removeListener(), listenerCount(), once(), off()
## 3.8 예외 처리하기


# 4장 http 모듈로 서버 만들기
## 4.1 요청과 응답 이해하기
    * require('http'): createServer().listen(), on(),
## 4.2 REST와 라우팅 사용하기
## 4.3 쿠키와 세션 이해하기
## 4.4 https와 http2
## 4.5 cluster
    * require('cluster'): isMaster, fork(), on()
    * pm2 모듈


# 5장 패키지 매니저
## 5.1 npm 알아보기
## 5.2 package.json으로 패키지 관리하기
    * init, run test, start, install, 
        * --global rimraf: 윈도용 rm -rf
    * npm install github_addr
## 5.3 패키지 버전 이해하기
## 5.4 기타 npm 명령어
    * outdate, uninstall, search, info, adduser, whoami, logout, version, deprecated, publish, unpublish
## 5.5 패키지 배포하기


# 6장 익스프레스 웹 서버 만들기
## 6.1 익스프레스 프로젝트 시작하기
    * npm i -g express-generator
    * express learn-express --view=pug, --view=ejs
    * npm i, npm start
## 6.2 자주 사용하는 미들웨어
* 6.2.1 morgan
* 6.2.2 static
* 6.2.3 body-parser
* 6.2.4 cookie-parser
* 6.2.5 express-session
* 6.2.6 미들웨어의 특성 활용하기
* 6.2.7 multer
## 6.3 Router 객체로 라우팅 분리하기
## 6.4 req, res 객체 살펴보기
## 6.5 템플릿 엔진 사용하기
* 6.5.1 퍼그(제이드)
* 6.5.2 넌적스
* 6.5.3 에러 처리 미들웨어


# 7장 MySQL
## 7.6 시퀄라이즈 사용하기
* 7.6.1 MySQL 연결하기
    * ORM
    * npm i sequelize mysql2, npm i -g sequelize-cli, sequelize init
    * var foo = require('./models').sequelize; foo.sync();
* 7.6.2 모델 정의하기
    * module.exports = (sequelize, DateTypes) => { return sequelize.define('foo', { col1: {} ) }
* 7.6.3 관계 정의하기
    * db.Foo.hasMany(); db.Bar.belongsTo(); db.Foo.hasOne(); db.Foo.belongsToMany();
* 7.6.4 쿼리 알아보기
    * Foo.create({ col1: 1, }).then().catch();
    * Foo.findAll({}); Foo.find({}), Foo.findAll({ attributes: ['col1'], where: { col1: 1, col2: { [Op.gt]: 2 }, } });
* 7.6.5 쿼리 수행하기


# 8장 몽고디비
## 8.3 컴퍼스 설치하기
* 8.3.4 커넥션 생성하기
## 8.4 데이터베이스 및 컬렉션 생성하기
## 8.5 CRUD 작업하기
## 8.6 몽구스 사용하기
* 8.6.1 몽고디비 연결하기
    * ODM(object document mapping): 스키마, populate(조인), 쿼리빌더
    * npm i mongoose
* 8.6.2 스키마 정의하기
    * const foo = require('mongoose'); const { Schema } = foo; const bar = new Schema({ col1: {}, }); module.exports = foo.model('Bar', bar);
* 8.6.3 쿼리 수행하기


# 9장 익스프레스로 SNS 서비스 만들기
## 9.1 프로젝트 구조 갖추기
## 9.2 데이터베이스 세팅하기
## 9.3 Passport 모듈로 로그인 구현하기
* 9.3.1 로컬 로그인 구현하기
* 9.3.2 카카오 로그인 구현하기
## 9.4 multer 패키지로 이미지 업로드 구현하기


# 10장 웹 API 서버 만들기
## 10.1 API 서버 이해하기
## 10.2 프로젝트 구조 갖추기
## 10.3 JWT 토큰으로 인증하기
## 10.4 다른 서비스에서 호출하기
## 10.5 SNS API 서버 만들기
## 10.6 사용량 제한 구현하기
## 10.7 CORS 이해하기


# 11장 노드 서비스 테스트하기
## 11.1 테스트 준비하기
## 11.2 유닛 테스트
## 11.3 테스트 커버리지
## 11.4 통합 테스트
## 11.5 부하 테스트


# 12장 웹 소켓으로 실시간 데이터 전송하기
## 12.1 웹 소켓 이해하기
## 12.2 ws 모듈로 웹 소켓 사용하기
## 12.3 Socket.IO 사용하기
## 12.4 실시간 GIF 채팅방 만들기
## 12.5 미들웨어와 소켓 연결하기
## 12.6 채팅 구현하기


# 13장 실시간 경매 시스템 만들기
## 13.1 프로젝트 구조 갖추기
## 13.2 서버센트 이벤트 사용하기
## 13.3 스케줄링 구현하기


# 14장 CLI 프로그램 만들기
## 14.1 간단한 콘솔 명령어 만들기
    * package.json: ..., "bin": { "cli": "./index.js" }, ...
    * require('readline'): createInterface(), question(), console.clear();
    * npm i -g, npm rm -g foo
## 14.2 commander, inquirer 사용하기


# 15장 AWS와 GCP로 배포하기
## 15.1 서비스 운영을 위한 패키지
* 15.1.1 morgan과 express-session
* 15.1.2 시퀄라이즈
* 15.1.3 cross-env
* 15.1.4 sanitize-html, csurf
* 15.1.5 pm2
* 15.1.6 winston
* 15.1.7 helmet, hpp
* 15.1.8 connect-redis
* 15.1.9 nvm, n
## 15.2 깃과 깃허브 사용하기
* 15.2.1 깃 설치하기
* 15.2.2 깃허브 사용하기
## 15.3 AWS 시작하기
## 15.4 AWS에 배포하기
## 15.5 GCP 시작하기
## 15.6 GCP에 배포하기


# 16장 서버리스 노드 개발
## 16.1 서버리스 이해하기
## 16.2 AWS S3 사용하기
## 16.3 AWS 람다 사용하기
## 16.4 구글 클라우드 스토리지 사용하기
## 16.5 구글 클라우드 펑션스 사용하기