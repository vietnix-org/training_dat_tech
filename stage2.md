# STAGE 2

## Cài đặt Windows Server 2012

Tải file ISO Windows Server về, emulate lên UTM và cài đặt như HĐH thông thường

## Cài đặt SQL Server + SSMS 

-   Tải và giải nén file ISO SQL Server (với thiết đặt mixed auth để có thể đăng nhập bằng SA hoặc Windows Authen)
-   Cài net frameworks và các yêu cầu tiên quyết
-   Cài SSMS

## Reset pwd 

### Reset sa trên SSMS

- đăng nhập vào instance bằng tài khoản sa trên SSMS, sau đó chạy query:
    ```bash
    ALTER LOGIN sa WITH PASSWORD = 'new_password';
    ```
### Reset windows pwd using chntpw in Kali Linux 

# LAMP

## Cài đặt mô hình Lamp:
-   install apache2, mysql-server php libapache2-mod-php php-mysql
    ```bash
    sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql
    ```

## Reset pwd mysql + mở remote mysql

### Reset pwd
-   Truy cập MySQL: Đăng nhập vào server qua SSH và chạy lệnh
    ```bash
    sudo mysql -u root -p
    ```

-   Reset mật khẩu: Thực hiện lệnh sau để thay đổi mật khẩu cho user root:
    ```bash
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'Vietnix@2024';
    ```

### Mở remote mysql ở port 3306

#### Bước 1: Chỉnh sửa file cấu hình MySQL

-   Mở file cấu hình MySQL:

    ```bash
    sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
    Tìm và chỉnh sửa dòng bind-address:
    ```
-   Tìm dòng bind-address và xoá.
    ```bash
    # bind-address = 127.0.0.1
    ```
-   Lưu và đóng file cấu hình.

#### Bước 2: Khởi động lại dịch vụ MySQL

-   Khởi động lại dịch vụ MySQL để áp dụng thay đổi:

    ```bash
    sudo systemctl restart mysql
    ```

#### Bước 3: Cấp quyền remote cho người dùng

-   Truy cập vào MySQL:
    ```bash
    mysql -u root -p
    ```

-   Cấp quyền remote cho người dùng (ví dụ: root):

    ```bash
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'Vietnix@2024' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
    ```

#### Bước 4: Kiểm tra cấu hình firewall (nếu cần thiết)
-   Mở cổng 3306 trong firewall:
    ```bash
    sudo ufw allow 3306/tcp
    sudo ufw reload
    ```

## Cài đặt Laravel và WP

### Laravel
-   Cài đặt composer
    ```bash
    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer
    ```
-   Tải Laravel installer từ composer
    ```bash
    sudo composer global require laravel/installer
    ```
-   Tạo Laravel project (ở trong /var/www)
    ```bash
    laravel neư VietnixTest2
    ```

### WP
-   Tải về 
    ```bash
    wget https://wordpress.org/latest.tar.gz
    ```
-   tar gz
    ```bash
    tar -xzf latest.tar.gz
    ```
-   rm gz sau khi tar
    ```bash
    rm latest.tar.gz
    ```

## Tạo database user và phân quyền
### Tạo db user

    ```bash
    sudo mysql_secure_installation
    ```

### Đăng nhập

    ```bash
    sudo mysql -u root -p
    ```

### Rồi thả

    ```sql
    CREATE DATABASE laravel_db;
    CREATE DATABASE wordpress_db;
    CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'D@t19990115';
    CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'Vietnix@2024';
    GRANT ALL PRIVILEGES ON laravel_db.* TO 'laravel_user'@'localhost';
    GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;
    ```
## Cấu hình virtual hosts

### Tạo virtual hosts:

**gen 2 files conf**

    ```bash
    sudo touch /etc/apache2/sites-available/laravel.vietnix.vn.conf /etc/apache2/sites-available/wordpress.vietnix.vn.conf
    ```

    ```bash
    <VirtualHost *:80>
        ServerName laravel.vietnix.vn
        DocumentRoot /var/www/vietnixTest2/public

        <Directory /var/www/laravel>
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/laravel_error.log
        CustomLog ${APACHE_LOG_DIR}/laravel_access.log combined
    </VirtualHost>
    ```

    ```bash
    <VirtualHost *:80>
        ServerName laravel.vietnix.vn
        DocumentRoot /var/www/vietnixTest2/public

        <Directory /var/www/laravel>
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/laravel_error.log
        CustomLog ${APACHE_LOG_DIR}/laravel_access.log combined
    </VirtualHost>
    ```

**Kích hoạt các Virtual Hosts**

    ```bash
    sudo a2ensite laravel.vietnix.vn.conf
    sudo a2ensite wordpress.vietnix.vn.conf
    sudo systemctl reload apache2
    ```

### Reset user pwd

**Vào mysql**
    ```bash
    mysql -u root -p
    ```

**Ví dụ reset pwd WP**

    ```sql
    USE wordpress_db;
    ```

**Sau đó thả**
    ```sql
    ALTER USER 'wordpress_user'@'localhost' IDENTIFIED BY 'Matkhaumoi@123changhan';
    FLUSH PRIVILEGES;
    EXIT;
    ```