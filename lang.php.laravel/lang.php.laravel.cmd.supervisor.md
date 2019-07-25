```
vi laravel-echo-server.conf
supervisorctl reread
supervisorctl update
supervisorctl start laravel-worker:*
supervisorctl start laravel-horizon:*
supervisorctl start laravel-echo-server:*
```