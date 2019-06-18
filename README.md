# Demo REST Server dengan implementasi key

Materi demo yang disajikan dalam presentasi Tech Lineup DiLo Makassar, Kamis 20 Juni 2019, di Makassar Digital Valley


## Download RESTful untuk CI

https://github.com/chriskacerguis/codeigniter-restserver

A fully RESTful server implementation for CodeIgniter using one library, one config file and one controller.

This project was originally written by Phil Sturgeon, however his involvement has shifted as he is no longer using it. As of 2013/11/20 further development and support will be done by Chris Kacerguis.


###  Requirements

1. PHP 5.4 or greater
2. CodeIgniter 3.0+


## Mengaktifkan Key

### menyiapkan tabel database untuk Keys

```
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


   -- * DDL ada di dalam file /application/config/rest.php
```

### enable-kan fungsi key

edit baris yang mengatur `rest_enable_keys` dalam file `/application/config/rest.php`,
dan ganti valuenya  menjadi `TRUE`

```
    $config['rest_enable_keys'] = TRUE;
```


## Mengaktifkan Logging

### menyiapkan tabel database untuk logging

```
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

   -- * DDL ada di dalam file /application/config/rest.php
```
