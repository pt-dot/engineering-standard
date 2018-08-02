# DOT ENGINEERING STANDARD

DOT engineering standard merupakan panduan bagi developer internal atau partner vendor untuk memastikan output software yang dihasilkan sesuai dengan kualitas perusahaan.

## Table of Contents
----
1. Backend Engineering Standard

    1.1 Tools & Development Stacks

    1.2 General Standard

    1.3 PHP Coding Standard

    1.4 Laravel / Lumen / PHP Framework Engineering Standard

2. Database Engineering Standard

    2.1 Tools & Development Stacks

    2.2 RDBMS Engineering Standard

3. Frontend Engineering Standard

4. QA Engineering Standard
    4.1 Tools & Development Stacks
    4.2 Documents

5. Contribution

## 1. Backend Engineering Standard

### 1.1 Tools & Development Stacks

+ PHP 7.0+, PHP 7.1+
+ Apache 2.4
+ Nodejs LTS
+ NPM, Yarn
+ GIT
+ GIT client: Source Tree, GitKraken
+ PHPStorm, VSCode, Sublime Text

### 1.2 General Standard
a. Hal-hal berikut ini seharusnya dimasukkan ke dalam list `.gitignore` dan tidak boleh di push ke dalam repository:

+ direktori `vendors`, `node_modules`
+ file upload dari user, file `.env`
+ Informasi credential penting atau krusial

b. Gunakan penamaan variable atau method yang singkat & jelas, serta tidak membingungkan.

good:

`user`, `storeData`, `debetAccount`

bad:

`aaaa`, `name1`, `thisistoloongvariableyoumaynotseeit`

c. Error message / debug message hanya boleh ditampilkan pada mode `development` atau `staging`. Gunakan default error message ketika di mode `production`

### 1.3 PHP Coding Standard

a. Harus mengikuti PHP [PSR-1: Basic Coding Standard](http://www.php-fig.org/psr/psr-1/)

b. Harus Mengikuti PHP [PSR-2: Coding Style Guide](http://www.php-fig.org/psr/psr-2/)

PSR-2 overview:
```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleMethod($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

c. Jika menggunakan autoloading, ikuti standard [PSR-4: Autoloading](http://www.php-fig.org/psr/psr-4/)

d. Agar source code lebih mudah dibaca dan dipahami sertakan `DockBlock` pada fungsi atau attribute. Manfaatkan DockBlock untuk menginformasikan proses, variable, dan output yang digunakan. Acuan penggunaan DockBlock dapat dilihat di [PHPDOC - DOCKBLOCK Basic Syntax](http://docs.phpdoc.org/references/phpdoc/basic-syntax.html)
    
Overview:
```php
<?php

class Foo {
    
    /**
    * @var string
    */
    protected $propertiesOne;

    /**
    * @var string
    */
    protected $propertiesTwo;

    /**
    * This is description of this class
    * this class may use recursion bla bla bla
    *
    * @param string $arg1
    * @param integer $arg2
    * @return array
    */
    public function bar($arg1, $arg2)
    {
        // some code

    }
}
```

e. Tidak boleh ada `Dead Code` saat merge ke branch `master`. `Dead Code` adalah source code (method, attributes, class) yang sudah tidak digunakan akan tetapi masih tersimpan di dalam codebase dan biasanya hanya dinonaktifkan menggunakan `comment`

Overview:
```php
<?php

class Foo {
    
    /**
    * This is description of this class
    * this class may use recursion bla bla bla
    *
    * @param string $arg1
    * @param integer $arg2
    * @return array
    */
    public function bar($arg1, $arg2)
    {
        // some code

    }
    
    //public function deadcode($arg1, $arg2)
    //{
    // some DEAD CODE
    //
    //}
}
```

f. Penggunaan PHP framework yang disarankan adalah [Laravel](https://laravel.com/) atau microframework [Lumen](https://lumen.laravel.com/).

### 1.4 Laravel / Lumen / PHP Framework Engineering Standard

a. Untuk project yang bersifat longterm disarankan menggunakan framework versi LTS (Long Term Support) atau disesuaikan dengan kebutuhan.

b. Gunakan fitur `Database Transaction` untuk operasi persistence yang menggunakan lebih dari 1 tabel database.

c. Untuk aplikasi yang kompleks, kumpulkan class `Model`, `Controller`, atau `Views` dalam direktori tersendiri sesuai dengan konteks / domain aplikasinya.

d. Untuk efisiensi masa development, gunakan library-library yang sudah umum digunakan dengan kriteria sebagai berikut:

+ library aktif di maintain oleh kontributor / owner
+ Sesuai dengan kebutuhan engineering project
+ Sesuai dengan development stack yang sedang digunakan
+ Penggunaan library harus benar-benar dapat mempermudah proses development

e. [Khusus Laravel] Gunakan perintah berikut untuk optimasi saat deployment:
```
php artisan route:cache
php artisan config:cache
composer dumpautoload --classmap-authoritative
```

f. Manfaatkan fitur `event` untuk fungsi yang tidak dependen dengan hasil outputnya. Misal: kirim email, logging, push notification.

## 2. Database Engineering Standard

### 2.1 RDBMS Engineering Standard

a. Gunakan `index` pada kolom-kolom yang sering dilakukan `select` query.

b. Gunakan nama table dan kolom dengan jelas dan konsisten. 

+ Wording: semua term menggunakan bahasa inggris
+ Wording Format: semua term menggunakan format `snake_case`

c. Hindari penggunaan query `SELECT *`, gunakan select hanya yang PERLU di-select saja.

## 3. Frontend Engineering Standard

## 4. QA Engineering Standard

### 4.1 Tools & Development Stacks

+ Postman
+ Newman
+ Codeception
+ Katalon / Laravel Dusk / Selenium
+ Jenkins
+ Jmeter
+ Firebase Test Lab
+ Sentry

### 4.2 Documents

+ User Story
+ Test Scenario
+ Manual Book
+ TSD
+ FSD
