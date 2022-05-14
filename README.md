### powershellで実行するコマンド

```php
// -tをつけるとタグ名付与できる
docker build . -t test_almalinux

// /sbin/initを与えないとsystemed系のコマンドが使えない↓
// docker run -v //c/Users/chopp/Docker_Project/test/src/:/var/www/ -itd -p 80:80 --privileged --name test_almalinux_dockerfile test_almalinux /sbin/init
docker run -v //c/Users/chopp/Docker_Project/test/:/var/www/ -itd -p 80:80 --privileged --name test_almalinux_dockerfile test_almalinux /sbin/init

// Dcoker立ち上げ実行コマンド:今後もずっと接続する時は使用
docker exec -it test_almalinux_dockerfile /bin/bash


//接続したら、タイムゾーンの設定
cp /etc/localtime /etc/localtime.org
ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
// dnf update
// dnf install epel-release kernel-devel kernel-headers gcc perl make dkms binutils patch libgomp glibc-headers glibc-devel elfutils-libelf-deve


systemctl restart php-fpm
systemctl restart nginx
// 自動起動設定
systemctl is-enabled nginx
systemctl enable nginx
// composerインストール
wget https://getcomposer.org/installer -O composer-installer.php
php composer-installer.php --filename=composer --install-dir=/usr/local/bin
composer self-update
cd /var/www/src/sns_project/
composer install
composer --version

chown -R nginx:nginx /var/www/src/sns_project/
chown -R nginx:nginx /var/www/src/sns_project/storage/
chown -R nginx:nginx /var/www/src/sns_project/bootstrap/cache/
chmod -R 0777 /var/www/src/sns_project/storage/
chmod -R 0775 /var/www/src/sns_project/bootstrap/cache/


// php mv composer.phar /usr/local/bin/composer
chmod +x /usr/local/bin/composer

```

### 注意事項
laravelをクローンしだけでは、ファイルが足りません。
vendorフォルダは上記のcomposer installで取得できましたが、envファイルがない状態です。
envファイルの作成はもとになるファイルはすでにあるのでコピーする
```php
cp .env.example .env
```

キー発行と念のためキャッシュクリアも実行
```php
php artisan key:generate
php artisan config:clear
```
