# Demo REST Server dengan implementasi key

Materi demo yang disajikan dalam *sharing session* **Tech Lineup DiLo Makassar**, Kamis 20 Juni 2019, di Makassar Digital Valley.

Demo menggunakan **RESTful Server** berbasis **PHP framework - CodeIgniter** dengan pertimbangan lebih mudah untuk dipelajari


## Download RESTful untuk CI

https://github.com/chriskacerguis/codeigniter-restserver

A fully RESTful server implementation for CodeIgniter using one library, one config file and one controller.

This project was originally written by Phil Sturgeon, however his involvement has shifted as he is no longer using it. As of 2013/11/20 further development and support will be done by Chris Kacerguis.


###  Requirements

1. PHP 5.4 or greater
2. CodeIgniter 3.0+


*Cloning repository* ini akan memberikan Anda **Codeigniter 3.1.10** dan **RESTful Server** yang siap untuk digunakan (konfigurasi database dan ```base_url``` menggunakan *server environments*, bisa dimodifikasi)


## Mengaktifkan Key

### Menyiapkan tabel database untuk Keys

```sql
   CREATE TABLE `keys` (
       `id` INT(11) NOT NULL AUTO_INCREMENT,
       `user_id` INT(11) NOT NULL,
       `key` VARCHAR(40) NOT NULL,
       `level` INT(2) NOT NULL,
       `ignore_limits` TINYINT(1) NOT NULL DEFAULT '0',
       `is_private_key` TINYINT(1)  NOT NULL DEFAULT '0',
       `ip_addresses` TEXT NULL DEFAULT NULL,
       `date_created` INT(11) NOT NULL,
       PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;


   -- *DDL tersedia di dalam file /application/config/rest.php
```

### Enable-kan fungsi key

edit baris yang mengatur `rest_enable_keys` dalam file `/application/config/rest.php`,
dan ganti valuenya  menjadi `TRUE`

```php
    $config['rest_enable_keys'] = TRUE;
```


## Mengaktifkan Logging

Dengan mengaktifkan fungsi logging maka provider API bisa melakukan penmantauan dan melakukan analisis
atas penggunaan API dan key-nya oleh pengguna

### Menyiapkan tabel database untuk Logging

```sql
   CREATE TABLE `logs` (
       `id` INT(11) NOT NULL AUTO_INCREMENT,
       `uri` VARCHAR(255) NOT NULL,
       `method` VARCHAR(6) NOT NULL,
       `params` TEXT DEFAULT NULL,
       `api_key` VARCHAR(40) NOT NULL,
       `ip_address` VARCHAR(45) NOT NULL,
       `time` INT(11) NOT NULL,
       `rtime` FLOAT DEFAULT NULL,
       `authorized` VARCHAR(1) NOT NULL,
       `response_code` smallint(3) DEFAULT '0',
       PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

   -- *DDL tersedia di dalam file /application/config/rest.php
```

### Enable-kan fungsi Key-logging

edit baris yang mengatur `rest_enable_logging` dalam file `/application/config/rest.php`,
dan ganti valuenya  menjadi `TRUE`

```php
    $config['rest_enable_logging'] = TRUE;
```

## Contoh Method

### Controller Mdv.php
```php

  use Restserver\Libraries\REST_Controller;
  defined('BASEPATH') OR exit('No direct script access allowed');

  require APPPATH . 'libraries/REST_Controller.php';
  require APPPATH . 'libraries/Format.php';

  class Mdv extends REST_Controller {

    protected $methods = [
            'test_get' => ['level' => 1],
        ];

    public function test_get(){
      $this->response( ['status'=>'OK'], REST_Controller::HTTP_OK );

    }

  }

```

### Request API tanpa key enabled

```
  http://demo1.mdv.local/mdv/test
```

### Request API dengan key enabled

```
http://demo1.mdv.local/mdv/test/API-KEY/0s4owc4k0s448swwg08o0cckggo848c0kk0k88w4
```

 *demo1.mdv.local hanya contoh, disesuikan dengan domain webserver yang digunakan *


## Documentation / Tutorials

* [NetTuts: Working with RESTful Services in CodeIgniter](http://net.tutsplus.com/tutorials/php/working-with-restful-services-in-codeigniter-2/)
