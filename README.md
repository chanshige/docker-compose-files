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
デフォルトはphp7.2.16にしてますが、バージョンを変更したい場合は、  
docker-compose.yml内 **VERSION** を修正して、build/up してください。  
```yaml
    build:
      context: ./.php
      dockerfile: Dockerfile
      args:
        VERSION: 7.2.16
```

```text
php-apache-with-composer
 ├── .conf
 │   └── 000-default.conf ← Apacheの設定ファイル
 ├── .php
 │   └── Dockerfile
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
```

### other
```bash
# ssh
% docker exec -it container_name /bin/bash

# direct mysqld
% docker exec -it db_container_name mysql -u db_user -p -D database_name
```
