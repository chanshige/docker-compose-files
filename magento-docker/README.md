# magento-docker

docker で magentoを動かしてみる。けど激遅い

### 環境
```
php 7.1.27
mysqld 5.6
```

### 準備
auth.json.exampleをコピーして、Marketplaceで確認できるキーをセットする  
`cp .docker/composer/auth.json.example .docker/composer/auth.json`

※ Get your authentication keys  
https://devdocs.magento.com/guides/v2.0/install-gde/prereq/connect-auth.html  

お好みのmagento2 を cloneする
```bash
# 本プロジェクトに移動
% cd magento_app/

# sampleで置いているディレクトリを削除
% rm -r magento2/

# clone!!!
% git clone --depth 1 https://github.com/magento/magento2.git
% git checkout -b # お好みのタグ #　e.g.)2.2.6

# お好みで .git 削除
% rm -rf .git/
```

### docker build - run
```bash
## ↓(移動してなかったら)
% cd magento_app/

# Create and start containers (background)
% docker-compose up -d
```

### magento setup & usage
```bash
# container login
$ docker exec -it magento_app /bin/bash

# install
$ cd magento2/
$ composer install
```

Go. http://localhost:8089  

```text
※ホストからDBアクセスする場合
DBのストレージは ".docker/db"をマウントして、ポートを23306としています。 
"127.0.0.1:23306"で接続すれば、DB操作のGUIなどからアクセス可能です。
```

### [option] enable redis ("magento_app" container login)
```bash
# Configure Redis default caching
$ bin/magento setup:config:set --cache-backend=redis --cache-backend-redis-server=magento_app_redis

# Configure Redis page caching
$ bin/magento setup:config:set --page-cache=redis --page-cache-redis-server=magento_app_redis --page-cache-redis-db=1
```
