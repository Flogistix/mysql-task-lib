## Synopsis

Simple mysql helper function that abstracts the side-effects of the asynchronis mysql node library, and wraps it in task. This helper function has simple catches to detect if you have a reader/writer portion of your configuration in the case you have a read replica. Otherwise, it will use the configuration as you give it.

## Code Example

*Simple Configuration*
```
const mysql = require ('mysql-task-lib'),
      logI  = function (x) { console.log (x); return x; },
      
      conf = { host     : 'database.com'
             , user     : 'username'
             , database : 'database'
             , password : 'password01'
             },
  
      query       = "SELECT * FROM testtable.testdata",
      mysql_query = mysql.query (conf, query, []);

mysql_query.fork(logI, logI)
```

*Read-Replica Configuration*
```
const mysql = require ('mysql-task-lib'),
      logI  = function (x) { console.log (x); return x; },
      
  conf = { writer: { host:        'database.com',
                     user:        'username',
                     database:    'database',
                     dateStrings:  true,
                     password:    'password01'
                   }
         , reader: { host:        'database-reader.com',
                     user:        'username',
                     database:    'database',
                     dateStrings:  true,
                     password:    'password01'
                   }
         };
  
      query       = "SELECT * FROM testtable.testdata",
      mysql_query = mysql.query (conf, query, []);

mysql_query.fork(logI, logI)
```
## Installation

```
npm install mysql-task-lib
```
