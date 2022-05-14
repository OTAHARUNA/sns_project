## システムを使っている上でよく実行するコマンド
* リモート接続する為に使用
docker exec -it -w /var/www/src/sns_project test_almalinux_dockerfile /bin/bash

* 再起動
systemctl restart php-fpm
systemctl restart nginx
systemctl restart postgresql


* ポスグレ接続
* su - postgres

## インストールできている（バージョン）か確認コマンド
* cat /etc/redhat-release   Almalinux
（上記きかないときOSが何かを確認
grep -H "" /etc/*version ; grep -H "" /etc/*release）

* nginx -v nginx
* php -v php
* php artisan -v laravel
* psql --version
