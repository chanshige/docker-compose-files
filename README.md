# docker-compose-files
dockerfileらを置く場所 

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

### wordpress

http://localhost:8080   

起動後、インストール画面

### databases

/var に状態を永続化するデータが作成されるので、  
適宜移動してもらい、`container_name:` や `ports:` を変更してください。  
※上記名前がホスト名になる。 


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
