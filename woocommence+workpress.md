**WooCommerce PayPal Express Checkout Payment Gateway**（官方早期插件）\
这个插件在 **版本 4.0 之前** 主要依赖 PayPal NVP API 处理支付请求

本次安装以WooCommerce 3.5为例

要安装兼容 **WooCommerce 3.5** 的 WordPress 版本，需选择 **WordPress 5.0 至 5.2 之间的版本**（具体为 **5.0.x 至 5.2.x**）

*   **WordPress 5.0 至 5.2** 是 WooCommerce 3.5 发布时（2018 年）的主流版本，二者核心代码库高度匹配，兼容性风险最低。

1.  **安装 MAMP <https://www.mamp.info/en/downloads/> 下载6.9 自带php7.4**

    *   下载 MAMP：访问 [MAMP 官网](https://www.mamp.info/)，下载适用于 macOS 的版本。
    *   安装并启动 MAMP，确保 **Apache** 和 **MySQL** 服务器正常运行。
    *   **配置端口**（可选）：

        *   进入 MAMP 偏好设置 → **Ports**，将 Apache 端口改为 **80**，后续可直接通过 `http://localhost` 访问。
2.  **创建数据库**

    *   访问 <http://localhost/MAMP/> 点击页面的Mysql 点击 phpMyAdmin 或者直接访问 <http://localhost/phpMyAdmin5/>
    *   在 phpMyAdmin 中创建数据库，例如命名为 `wordpress`，字符集选择 **utf8mb4\_*****unicode***\*\*\_ci\*\*。



3.  **下载安装 WordPress**

    *   访问 [WordPress 官网](https://wordpress.org/)，下载 wordpress（需兼容 WooCommerce 3.5,比如5.2）。
    *   解压后将 `wordpress` 文件夹复制到 MAMP 的 `htdocs` 目录（路径：`/Applications/MAMP/htdocs/`）
    *   &#x20;    cp -r /Users/glen/Downloads/wordpress /Applications/MAMP/htdocs/
    *   &#x20;     cd /Applications/MAMP/htdocs/wordpress 
    *         修改 wp-config-sample.php中的相关配置
        *   `define( 'DB_NAME', 'wordpress' );`
        *   `define( 'DB_USER', 'root' );`
        *   `define( 'DB_PASSWORD', 'root' );`
        *   `define( 'DB_HOST', 'localhost:8889' );`
    *   访问 <http://localhost/wordpress/wp-admin/setup-config.php>
    *   根据引导步骤完成安装
    *   如果遇到错误 可以查看/Applications/MAMP/logs 下的错误日志
4.  **安装 Express Checkout,woocommence自带只有standard**

      * 下载 <https://github.com/woocommerce/woocommerce-gateway-paypal-express-checkout/releases/tag/2.1.3>  ，需要下载zip包
      *  <http://localhost/wordpress/wp-admin/index.php> 在admin 界面 选择plugins，upload 上传上面下载的zip 包，然后intall active，
      * 点击Woocommence菜单，点击Settings，选择Payments 选项卡，paypal checkout 选择enable ，然后点击 manager，Environment选择sandbox，Sandbox API Credentials 选择点击click here to toggle manual API           credential input，然后 设置相关账号密码签名
      * 左侧 Products 增加商品 
      * 鼠标放在左上角房子图标，点击visit shop或者直接访问 <http://localhost/wordpress/shop/> 访问购物地址 购买商品
  
5. **打包**

   ```
       # 进入插件目录
      cd /Users/glen/Documents/workspace/paypal/woocommerce-gateway-paypal-express-checkout
      
      # 取版本号（来自 readme.txt 的 Stable tag）
      VERSION=$(grep "^Stable tag:" readme.txt | awk '{print $3}')
      
      # 目标目录
      DEST="/Users/glen/Documents/workspace/paypal/releases/woocommerce-gateway-paypal-express-checkout-$VERSION"
      
      # 准备干净的发布目录
      rm -rf "$DEST"
      mkdir -p "$DEST"
      
      # 只同步需要发布的文件/目录，排除开发文件
      rsync -a \
        --exclude "/wordpress_org_assets/***" \
        --exclude "/.git/***" \
        --exclude "/.github/***" \
        --exclude "/node_modules/***" \
        --exclude "/vendor/***" \
        --exclude "/tests/***" \
        --exclude "/.DS_Store" \
        --exclude "/deploy.sh" \
        --exclude "/composer.*" \
        --exclude "/package*.json" \
        --exclude "/phpcs.xml" \
        --exclude "/phpunit.xml" \
        --exclude "/README.md" \
        --exclude "/.gitattributes" \
        --exclude "/.editorconfig" \
        --exclude "/.gitignore" \
        --include "/assets/***" \
        --include "/includes/***" \
        --include "/languages/***" \
        --include "/templates/***" \
        --include "/changelog.txt" \
        --include "/DEVELOPER.md" \
        --include "/readme.txt" \
        --include "/woocommerce-gateway-paypal-express-checkout.php" \
        --exclude "/**" \
        "./" "$DEST/"
      
      # 打包为与官方一致的 zip（解压后顶层目录带版本号）
      cd /Users/glen/Documents/workspace/paypal/releases
      zip -r "woocommerce-gateway-paypal-express-checkout-$VERSION.zip" "woocommerce-gateway-paypal-express-checkout-$VERSION" -x "*/.DS_Store"  
   ```
