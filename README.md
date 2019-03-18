# docker-compose-files
@chanshige が使っているdocker-composeファイルを置く場所 

### dockerfiles
Dockerfile に引数としてVERSIONをもたせているので、入れたいバージョンを指定してください。  
引数がない場合は、各ファイルのデフォルトでbuildされます。  
```bash
# image build Dockerfile
% docker build -t repository-name -f dockerfile-name --build-arg VERSION=7.x.x docker-file-path

# run
% docker run -it -d --name container-name repository-name

#run with mount dir
% docker run -it -d -v /mount/path/to/dir:/home/workspace --name container-name repository-name
```

### php-apache-with-composer
Debian  
Apache2.4  

http://localhost:8000  

build時にcomposerとxdebug、mod_rewriteを入れてます。
デフォルトはphp73にしてます。 

```text
php-apache-with-composer
 ├── .conf
 │   └── 000-default.conf ← Apacheの設定ファイル
 ├── .phpenv
 │   ├── php56
 │   ├── php71
 │   └── php73
 ├── docker-compose.yml
 └── html ← DocumentRoot（ここにアプリケーションを置く)
```

### wordpress

http://localhost:8080   

起動後、インストール画面

### usage
```bash
# build
% docker-compose build

# run
% docker-compose up -d
( $ docker-compose start)

# stop
% docker-compose stop

# ssh
% docker exec -it [container_name] /bin/bash
```
