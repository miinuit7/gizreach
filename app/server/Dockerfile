FROM php:8.2-fpm-alpine

# 必要なパッケージ
RUN apk update && apk add --no-cache \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    libzip-dev \
    zip \
    unzip \
    git \
    curl \
    oniguruma-dev \
    pkgconf \
    autoconf \
    g++ \
    make

# PHP拡張をビルド＆インストール
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-install gd pdo pdo_mysql zip

# Composerのインストール
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# アプリディレクトリ
WORKDIR /var/www/html

# Laravelソース一式をコピー
COPY . .

# Composerインストール（ここで全体コピーしたあとに）
RUN composer install --no-dev --optimize-autoloader

# パーミッション調整
RUN chown -R www-data:www-data /var/www/html \
 && chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache

# 開発用サーバー起動（本番では php-fpm を使う）
EXPOSE 8000
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
