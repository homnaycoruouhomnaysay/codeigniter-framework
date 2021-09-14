# CodeIgniter v3.1.12 - vendor packages build

[![Latest Stable Version](http://poser.pugx.org/nguyenanhung/codeigniter-framework/v)](https://packagist.org/packages/nguyenanhung/codeigniter-framework) [![Total Downloads](http://poser.pugx.org/nguyenanhung/codeigniter-framework/downloads)](https://packagist.org/packages/nguyenanhung/codeigniter-framework) [![Latest Unstable Version](http://poser.pugx.org/nguyenanhung/codeigniter-framework/v/unstable)](https://packagist.org/packages/nguyenanhung/codeigniter-framework) [![License](http://poser.pugx.org/nguyenanhung/codeigniter-framework/license)](https://packagist.org/packages/nguyenanhung/codeigniter-framework)

Bản đóng gói lại thư mục system framework của CodeIgniter, sử dụng tương thích với Composer và PHP 7, PHP 8

## Bổ sung thêm 1 số thư viện mở rộng, helpers liên quan

- [x] Support mô hình HMVC
- [x] Support class Base Model với 1 số hàm cơ bản
- [x] Hỗ trợ Output Response trên giao diện CLI thông qua hàm `ResponseOutput::writeLn($message)`
- [x] Bổ sung class `StatusCodes` khai báo sẵn các HTTP code tuân chuẩn (from Symfony framework), VD: `StatusCodes::HTTP_OK`. Chi tiết tham khảo thêm tại class `StatusCodes`

## Hướng dẫn viết Model kế thừa Base Model

1. Xây dựng 1 model theo tài liệu CodeIgniter 3
2. Kế thừa class từ `HungNG_Custom_Based_model` thay vì `CI_Model`, ví dụ như sau

```php
<?php
defined('BASEPATH') or exit('No direct script access allowed');

/**
 * Class Credentials_model
 *
 * @author    713uk13m <dev@nguyenanhung.com>
 * @copyright 713uk13m <dev@nguyenanhung.com>
 * @property \CI_DB_query_builder $db
 */
class Credentials_model extends HungNG_Custom_Based_model
{
    const IS_ACTIVE = 1;
    const ROLE_PUSH = 1;
    const ROLE_PULL = 2;
    const ROLE_FULL = 3;

    protected $fieldUsername;
    protected $fieldStatus;
    protected $fieldRole;

    /**
     * Credentials_model constructor.
     *
     * @author   : 713uk13m <dev@nguyenanhung.com>
     * @copyright: 713uk13m <dev@nguyenanhung.com>
     */
    public function __construct()
    {
        parent::__construct();
        $this->db            = $this->load->database('default', true, true);
        $this->tableName     = 'credentials';
        $this->primary_key   = 'id';
        $this->fieldUsername = 'username';
        $this->fieldStatus   = 'status';
        $this->fieldRole     = 'role';
    }
}
```

## Hướng dẫn tích hợp mô hình HMVC vào dự án

1. Create folder: `modules` trong thư mục `application`. Tham khảo cấu trúc thư mục `modules` tại `sample/modules/` trong thư viện này

```shell
.
└── modules
    └── startup
        ├── config
        │   ├── index.html
        │   └── routes.php
        ├── controllers
        │   ├── Startup.php
        │   └── index.html
        ├── index.html
        ├── models
        │   ├── Startup_model.php
        │   └── index.html
        └── views
            └── index.html

6 directories, 8 files
```

2. Create file `hmvc.php` với nội dung như sau

```php
<?php
defined('BASEPATH') or exit('No direct script access allowed');
/*
| -------------------------------------------------------------------------
| HMVC settings
| -------------------------------------------------------------------------
| See: https://github.com/nguyenanhung/CodeIgniter-HMVC
|
*/
$config['modules_locations'] = array(
    APPPATH . 'modules/' => '../modules/'
);

```

3. Nạp file `hmvc.php` vào file `config.php`

```php
require_once __DIR__ . '/hmvc.php';
```

4. Create file `MY_Loader.php` trong thư mục `application/core/` có nội dung như sau

```php
<?php
defined('BASEPATH') or exit('No direct script access allowed');
/**
 * Class MY_Loader
 *
 * @author    713uk13m <dev@nguyenanhung.com>
 * @copyright 713uk13m <dev@nguyenanhung.com>
 */
class MY_Loader extends HungNG_Loader
{

}
```

5. Create file `MY_Router.php` trong thư mục `application/core/` có nội dung như sau

```php
<?php
defined('BASEPATH') or exit('No direct script access allowed');
/**
 * Class MY_Router
 *
 * @author    713uk13m <dev@nguyenanhung.com>
 * @copyright 713uk13m <dev@nguyenanhung.com>
 */
class MY_Router extends HungNG_Router
{

}

```

6. Triển khai viết code trong thư mục modules mới

## Liên hệ

| Name        | Email                | Skype            | Facebook      |
| ----------- | -------------------- | ---------------- | ------------- |
| Hung Nguyen | dev@nguyenanhung.com | nguyenanhung5891 | @nguyenanhung |

