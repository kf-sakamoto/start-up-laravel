#Laravel開発環境構築手順書
■環境の立ち上げ

*以下「foo」は作成中のプロジェクト名に置き換えること

1. Docker Toolboxをインストールする
https://www.docker.com/products/docker-toolbox

2. 作業用ディレクトリを作成する
$ mkdir projects
$ cd projects/

3. プロジェクトディレクトリを作成する
$ mkdir foo
$ cd foo/

4. githubからdocker-compose一式をcloneする
$ git clone https://github.com/kf-sakamoto/startup-laravel.git
$ cd startup-laravel/

5. コンテナを立ち上げる
$ docker-compose up -d --build

6. 時間がかかるので待つ

7. 新規プロジェクトの場合はA、既存プロジェクトがある場合はBを実行する
A. workspaceコンテナに入り、laravelプロジェクトを作成する
$ docker exec -it startuplaravel_workspace_1 bash
# composer create-project laravel/laravel foo
# exit
B. 親ディレクトリに移動し、作業中のソースコードを落とす
$ cd ../
$ git clone ***/foo.git

8. docker-compose.ymlを編集する
10行目: - ../:/var/www/laravel -> - ../foo/:/var/www/laravel

9. コンテナを再起動
$ docker-compose up -d --build

10. ブラウザでアクセスする
$ docker-machine ip
192.168.99.100 <- ここに表示されたipにアクセス
* ディレクトリ構成
foo
|-- startup-laravel/
|   |-- docker-compose.yml
|   `-- 各種dockerコンテナ用ディレクトリ
`-- foo
    `-- laravelの構造

■Laravelの初期設定と確認

1. .evnファイルを編集する
DB_CONNECTION=mysql
DB_HOST=192.168.99.100 <- docker-machine ipで表示されたIPアドレス
DB_PORT=3306
DB_DATABASE=develop <- docker-compose.ymlで定義されたDB
DB_USERNAME=developer <- docker-compose.ymlで定義されたユーザー
DB_PASSWORD=developer <- docker-compose.ymlで定義されたパスワード

2. workspaceコンテナに入りmigrateする
$ docker exec -it startuplaravel_workspace_1 bash
# php artisan migrate
# exit

3. mysqlコンテナに入り確認する
$ docker exec -it startuplaravel_mysql_1 bash
# mysql -udeveloper -p
# password: developer
mysql> use develop;
mysql> show tables;
デフォルトで入っているusersテーブルとpassword_resetsテーブルが作られていれば確認完了

4. php-fpmコンテナに入りjavaが導入されているか確認する
 $ docker exec -it startuplaravel_php-fpm_1 bash
 # java -version
 # javac -version
表示されなかった場合、以下のコマンドを実行する
 # apt-get update
 # apt-get install -y default-jdk
