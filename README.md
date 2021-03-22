# Laravel

## Testar conexão com banco de dados
* `php artisan tinker`
* `DB::connection()->getPdo();`

tem que retornar um PDO:

`PDO {#3334
     inTransaction: false,
     attributes: {
       CASE: NATURAL,
       ERRMODE: EXCEPTION,
       AUTOCOMMIT: 1,
       PERSISTENT: false,
       DRIVER_NAME: "mysql",
       SERVER_INFO: "Uptime: 8695  Threads: 2  Questions: 41  Slow queries: 0  Opens: 109  Flush tables: 1  Open tables: 18  Queries per second avg: 0.004",
       ORACLE_NULLS: NATURAL,
       CLIENT_VERSION: "mysqlnd 8.0.0",
       SERVER_VERSION: "5.7.24",
       STATEMENT_CLASS: [
         "PDOStatement",
       ],
       EMULATE_PREPARES: 0,
       CONNECTION_STATUS: "127.0.0.1 via TCP/IP",
       DEFAULT_FETCH_MODE: BOTH,
     },
   }`
