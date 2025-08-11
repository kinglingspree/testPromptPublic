**WooCommerce PayPal Express Checkout Payment Gateway**（官方早期插件）\
这个插件在 **版本 4.0 之前** 主要依赖 PayPal NVP API 处理支付请求

要安装兼容 **WooCommerce 3.5** 的 WordPress 版本，需选择 **WordPress 5.0 至 5.2 之间的版本**（具体为 **5.0.x 至 5.2.x**）

*   **WordPress 5.0 至 5.2** 是 WooCommerce 3.5 发布时（2018 年）的主流版本，二者核心代码库高度匹配，兼容性风险最低。

1.  **安装 MAMP <https://www.mamp.info/en/downloads/> 下载6.9 自带php7.4**

    *   下载 MAMP：访问 [MAMP 官网](https://www.mamp.info/)，下载适用于 macOS 的版本。
    *   安装并启动 MAMP，确保 **Apache** 和 **MySQL** 服务器正常运行。
    *   **配置端口**（可选）：

        *   进入 MAMP 偏好设置 → **Ports**，将 Apache 端口改为 **80**（需输入管理员密码），后续可直接通过 `http://localhost` 访问。
2.  **创建数据库**

    *   访问 <http://localhost/MAMP/> 点击页面的Mysql 点击 phpMyAdmin 或者直接访问 <http://localhost/phpMyAdmin5/>
    *   在 phpMyAdmin 中创建数据库，例如命名为 `wordpress`，字符集选择 **utf8mb4\_*****unicode***\*\*\_ci\*\*。

### 二、安装 WordPress 5.0+

1.  **下载 WordPress**

    *   访问 [WordPress 官网](https://wordpress.org/)，下载 wordpress（需兼容 WooCommerce 3.5,比如5.2）。
    *   解压后将 `wordpress` 文件夹复制到 MAMP 的 `htdocs` 目录（路径：`/Applications/MAMP/htdocs/`）
    *   &#x20;    cp -r /Users/glen/Downloads/wordpress /Applications/MAMP/htdocs/
    *   &#x20;     cd /Applications/MAMP/htdocs/wordpress 
    *         修改 wp-config-sample.php中的相关配置
        *   `define( 'DB_NAME', 'wordpress' );`\
            `/** MySQL database username */`
        *   `define( 'DB_USER', 'root' );````/** MySQL database password *`
        *   `/define( 'DB_PASSWORD', 'root' );````/** MySQL hostname */`
        *   `define( 'DB_HOST', 'localhost:8889' );`
    *   访问 http\://localhost/wordpress/wp-admin/setup-config.php
    *   根据引导步骤完成安装
    *   如果遇到错误 可以查看/Applications/MAMP/logs 下的错误日志
2.  下载 <https://github.com/woocommerce/woocommerce-gateway-paypal-express-checkout/releases/tag/2.1.3>  ，需要下载zip包
3.  在http\://localhost/wordpress/wp-admin/admin.php 在admin 界面 选择plugins，upload 上传上面下载的zip 包，然后intall active，
4.  进入woocommence 界面，点击settings，选择Payments 选项卡，paypal checkout 选择enable ，点击manager，配置相关比如 env 选择sandbox，设置相关账号密码签名
5.  左侧 Products 增加商品 

6. 鼠标放在左上角房子图标，点击visit shop或者直接访问 http\://localhost/wordpress/shop/ 访问购物地址 购买商品
