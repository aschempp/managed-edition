# Contao 4 Managed Edition

Contao is an Open Source PHP Content Management System for people who want a
professional website that is easy to maintain. Visit the [project website][1]
for more information.

## System Requirements

 * Web server
 * PHP 7.3+ with GDlib and DOM
 * MySQL 5.5.7+
 * InnoDB with `innodb_large_prefix` enabled

## InnoDB Large Prefix

MySQL versions prior to 5.7.7 do not have the `innodb_large_prefix` option
enabled by default. To enable it in one of these versions, add the following
to your `my.cnf` file:

```
innodb_large_prefix = 1
innodb_file_format = Barracuda
innodb_file_per_table = 1
```

If the option cannot be enabled on your server, please configure a different
database engine and character set in your `config/config.yml` file:

```yml
doctrine:
    dbal:
        connections:
            default:
                default_table_options:
                    charset: utf8
                    collate: utf8_unicode_ci
                    engine: MyISAM
```

## MySQL Strict Mode

It is recommended to run MySQL in "strict mode" to prevent corrupt or truncated
data and to guarantee data integrity. As of Contao 4.12, the install tool shows
a warning if the database server is not running in strict mode. To enable it,
add the following to your `my.cnf` file or make sure that the setting is adjusted
accordingly:

```
[mysqld]
…
sql_mode="TRADITIONAL"
…
```

If the setting cannot be enabled on your server, please configure the connection
options in your `config/config.yml` file:

```yml
doctrine:
    dbal:
        connections:
            default:
                options:
                    # Depending on the DB driver, the option key is either 1002 (pdo_mysql) or 3 (mysqli)
                    1002: "SET SESSION sql_mode=(SELECT CONCAT(@@sql_mode, ',TRADITIONAL'))"
```

## Browser Compatibility

Chrome, Firefox, Safari 12+, IE 11, Edge 17+, Opera, Chrome for Android, Safari for iOS 11.3+, Samsung Internet 8.2+

## Installation

See the [installation chapter][2] of the user's manual.

## Documentation

 * [User Manual][3]
 * [Developer Documentation][4]

## License

Contao is licensed under the terms of the LGPLv3.

## Getting Support

Visit the [support page][5] to learn about the available support options.

[1]: https://contao.org
[2]: https://docs.contao.org/dev/getting-started/initial-setup/
[3]: https://docs.contao.org/manual/
[4]: https://docs.contao.org/dev/
[5]: https://contao.org/en/support.html
