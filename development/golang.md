# Archlinux下Golang环境配置
## 方案一：
### 准备
1. golang安装：
> pacman -S go/$ sudo pacman -S go

2. liteide安装：
> pacman -S liteide/sudo pacman -S liteide

### 配置环境
1. golang(Archlinux中配置环境最好放到自启动中)
> vim /etc/profile.d/go.sh

2. set go environment
```
export GOPATH=/home/用户名/Workspaces/Go  #根据自己的Go工作目录替换
export GOBIN=$GOPATH/bin
export PATH=$GOBIN:$PATH
```
## 方案二：
1. 解压go到默认的安装目录
> sudo tar -C /usr/local -xzf go*****tar.gz
2. 新增环境变量
> vi ~/.profile
3. vi文件的内容
> export PATH=$PATH:/usr/local/go/bin
  export GOPATH=/home/cyper/gopath
4. 使配置生效
> . ~/.profile
5. go安装在了哪里
> which go
6. 当前go中的环境变量
> go env
7. 代码提示
> go get -u github.com/nsf/gocode

# Golang链接Oracle

## 一、安装Oracle的OCI套件

1. OCI下载链接页面下载[instantclient-basic, instantclient-sdk](http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html)

2. 解压缩到同一个目录下，比如：instantclient_12_1

3. root权限移动文件夹到目录 /usr/lib 下

4. root权限执行以下命令

    ```
    ln -s /usr/lib/instantclient_12_1/libclntsh.so.12.1 /usr/lib/libclntsh.so
    ln -s /usr/lib/instantclient_12_1/libocci.so.12.1 /usr/lib/libocci.so
    ln -s /usr/lib/instantclient_12_1/libociei.so /usr/lib/libociei.so
    ln -s /usr/lib/instantclient_12_1/libnnz12.so /usr/lib/libnnz12.so
    ln -s /usr/lib/instantclient_12_1/​libsqlplusic.so /usr/lib/libsqlplusic.so​
    ln -s /usr/lib/instantclient_12_1/libsqlplus.so /usr/lib/libsqlplus.so​
    ```

5. ​把 OCI路径加入系统加载动态库的路径中，并重新加载一次
    ```
    ​echo /opt/oracle/instantclient >> /etc/ld.so.conf
    ldconfig
    ```

6. 安装pkg-config

7. 在 /usr/lib/pkgconfig 目录下创建文件 oci8.pc，内容如下：
    ```
    prefix=<replace instantclient path>  // 路径改为/usr/lib/instantclient_12_1
    libdir=${prefix}
    includedir=${prefix}/sdk/include/

    Name: OCI
    Description: Oracle database engine
    Version: 12.1                                            
     // 版本改为实际的版本号
    Libs: -L${libdir} -lclntsh
    Libs.private:
    Cflags: -I${includedir}
    ```

8. 直接运行步骤6会报libaio不存在的错误，安装libaio库

    > sudo apt-get install libaio1

9. 安装go-oci8

    > go get github.com/mattn/go-oci8​

10. bashrc 文件中添加系统变量
    ```
    # OCI安装目录​
    export ORACLE_HOME=/usr/lib/instantclient_12_1
    # ​tnsnames.ora 文件地址​
    ​export TNS_ADMIN=$ORACLE_HOME/network/admin
    # OCI安装目录加入动态库加载路径​
    ​export LD_LIBRARY_PATH=$ORACLE_HOME
    #  oci8.pc文件所在路径
    export PKG_CONFIG_PATH=/usr/lib/pkgconfig
    ```

## 二、Golang链接Oracle代码示例
1. 增删改
```
    package main

    import (
        "database/sql"
        "fmt"
        _ "github.com/mattn/go-oci8"
        "os"
    )

    func main() {
        // 字符集
        os.Setenv("NLS_LANG", "AMERICAN_AMERICA.AL32UTF8")

        // 注意连接字符串的写法
        db, err := sql.Open("oci8", "awsdb/awsdb@192.168.0.126:1521/awsdb")
        if err != nil {
            fmt.Println(err)
            return
        }
        // 事务开启
        myTx,err:=db.Begin()
        myTx.Commit()

        // 查询与结果遍历
        rows, err := db.Query("select nodeid,nodename from AA_MT_TEST")
        if err != nil {
            fmt.Println(err)
            return
        }
        for rows.Next() {
            var f1 string
            var f2 string
            rows.Scan(&f1, &f2)
            println(f1, f2) // 3.14 foo
        }
        rows.Close()

        _, err = db.Exec("create table foo(bar varchar2(256))")
        _, err = db.Exec("drop table foo")
        if err != nil {
            fmt.Println(err)
            return
        }
        // 关闭数据库连接
        db.Close()
    }
    ```

2. 执行了一个存储过程、使用结构保存结果
    ```
    package main

    import (
    	"database/sql"
    	"fmt"
    	_ "github.com/mattn/go-oci8"
    	"os"
    	"sync"
    )

    var (
    	db  *sql.DB
    	mux sync.Mutex
    )

    // 多行字符串的定义
    var userTableSql string = `
     BEGIN
        BEGIN
              EXECUTE IMMEDIATE 'DROP TABLE user_profile';
        EXCEPTION
              WHEN OTHERS THEN
                    IF SQLCODE != -942 THEN
                          RAISE;
                    END IF;
        END;
        EXECUTE IMMEDIATE 'CREATE TABLE user_profile (id int PRIMARY KEY, name VARCHAR(20) NOT NULL, created VARCHAR(20) NOT NULL)';
     END;
     `

    func init() {

    	// 锁
    	mux.Lock()
    	defer mux.Unlock()

    	os.Setenv("NLS_LANG", "AMERICAN_AMERICA.ZHS16GBK")
    	// check
    	if db != nil {
    		return
    	}

    	// open
    	oracledb, err := sql.Open("oci8", "awsdb/awsdb@192.168.0.126:1521/awsdb")
    	checkErr(err)

    	// new db
    	db = oracledb

    	// create database table
    	_, err = db.Exec(userTableSql)
    	checkErr(err)
    }

    func checkErr(err error) {
    	if err != nil {
    		panic("oracle err:" + err.Error())
    	}
    	return
    }

    func main() {
    	// insert
    	insertSql := `insert into user_profile(id,name,created) values(1,'viney','2013-03-06')`
    	_, err := db.Exec(insertSql)
    	checkErr(err)

    	// update
    	updateSql := `update user_profile set name='中国人' where id=1`
    	_, err = db.Exec(updateSql)
    	checkErr(err)

    	// select
    	querySql := `select * from user_profile where id=1`
    	rows, err := db.Query(querySql)

    	type user struct {
    		id      int // 这个地方改成string才不会报错,但是我创建数据库是int类型
    		name    string
    		created string
    	}

    	var u = &user{}
    	for rows.Next() {
    		err = rows.Scan(
    			&u.id,
    			&u.name,
    			&u.created)
    		checkErr(err)
    	}
    	rows.Close()

    	fmt.Println(*u)

    	// delete
    	deleteSql := `delete from user_profile where id=1`
    	_, err = db.Exec(deleteSql)
    	checkErr(err)

    	db.Close()
    }
    ```

3. 例3
    ```
    package main

    import (
    	"database/sql"
    	_ "github.com/mattn/go-oci8"
    	//"os"
    	"log"
    )

    func main() {
    	// 为log添加短文件名,方便查看行数
    	log.SetFlags(log.Lshortfile | log.LstdFlags)

    	log.Println("Oracle Driver example")

    	//os.Setenv("NLS_LANG", "")

    	// 用户名/密码@实例名  跟sqlplus的conn命令类似
    	db, err := sql.Open("oci8", "abelit/cy123@prod1")
    	if err != nil {
    		log.Fatal(err)
    	}
    	rows, err := db.Query("select username from all_users")
    	if err != nil {
    		log.Fatal(err)
    	}
    	defer db.Close()

    	for rows.Next() {
    		//var f1 float64
    		//var f2 string
    		//rows.Scan(&f1, &f2)
    		//log.Println(f1, f2) // 3.14 foo
    		var f1 string
    		rows.Scan(&f1)
    		log.Println(f1)
    	}
    	rows.Close()

    	// 先删表,再建表
    	db.Exec("drop table sdata")
    	db.Exec("create table sdata(name varchar2(256))")

    	db.Exec("insert into sdata values('中文')")
    	db.Exec("insert into sdata values('1234567890ABCabc!@#$%^&*()_+')")

    	rows, err = db.Query("select * from sdata")
    	if err != nil {
    		log.Fatal(err)
    	}

    	for rows.Next() {
    		var name string
    		rows.Scan(&name)
    		log.Printf("Name = %s, len=%d", name, len(name))
    	}
    	rows.Close()
    }
    ```

4. 例4
    ```
    package main

    import (
        "database/sql"
        "fmt"
        _ "github.com/wendal/go-oci8"
        "log"
    )

    type Users struct {
        UserId int
        Uname  string
    }

    func main() {
        log.Println("Oracle Driver Connecting....")
        //用户名/密码@实例名 如system/123456@orcl、sys/123456@orcl
        db, err := sql.Open("oci8", "/password@orcl")
        if err != nil {
            log.Fatal(err)
            panic("数据库连接失败")
        } else {
            defer db.Close()
            var users []Users = make([]Users, 0)
            rows, err := db.Query("select * from users")
            if err != nil {
                log.Fatal(err)
            } else {
                for rows.Next() {
                    var u Users
                    rows.Scan(&u.UserId, &u.Uname)
                    users = append(users, u)
                }
                fmt.Println(users)
                defer rows.Close()
            }

        }

    }
    ```

# Golang链接MySQL

1. 例1
    ```
    package main

    import (
    	"database/sql"
    	"fmt"
    	_ "github.com/go-sql-driver/mysql"
    )

    func main() {
    	query()
    }

    //插入demo
    func insert() {
    	db, err := sql.Open("mysql", "root:cy123@/dataforum?charset=utf8")
    	checkErr(err)
    	stmt, err := db.Prepare(`INSERT users (name,email,password) values (?,?,?)`)
    	checkErr(err)
    	res, err := stmt.Exec("tony", "ychenid@gmail.com", "cy123")
    	checkErr(err)
    	id, err := res.LastInsertId()
    	checkErr(err)
    	fmt.Println(id)
    }

    //查询demo
    func query() {
    	db, err := sql.Open("mysql", "root:cy123@/dataforum?charset=utf8")
    	checkErr(err)

    	rows, err := db.Query("SELECT * FROM users")
    	checkErr(err)
    	//字典类型
    	//构造scanArgs、values两个数组，scanArgs的每个值指向values相应值的地址
    	columns, _ := rows.Columns()
    	scanArgs := make([]interface{}, len(columns))
    	values := make([]interface{}, len(columns))
    	for i := range values {
    		scanArgs[i] = &values[i]
    	}

    	for rows.Next() {
    		//将行数据保存到record字典
    		err = rows.Scan(scanArgs...)
    		record := make(map[string]string)
    		for i, col := range values {
    			if col != nil {
    				record[columns[i]] = string(col.([]byte))
    			}
    		}
    		fmt.Println(record)
    	}
    }

    //更新数据
    func update() {
    	db, err := sql.Open("mysql", "root:cy123@/dataforum?charset=utf8")
    	checkErr(err)

    	stmt, err := db.Prepare(`UPDATE user SET user_age=?,user_sex=? WHERE user_id=?`)
    	checkErr(err)
    	res, err := stmt.Exec(21, 2, 1)
    	checkErr(err)
    	num, err := res.RowsAffected()
    	checkErr(err)
    	fmt.Println(num)
    }

    //删除数据
    func delete() {
    	db, err := sql.Open("mysql", "root:cy123@/dataforum?charset=utf8")
    	checkErr(err)

    	stmt, err := db.Prepare(`DELETE FROM users WHERE id=?`)
    	checkErr(err)
    	res, err := stmt.Exec(1)
    	checkErr(err)
    	num, err := res.RowsAffected()
    	checkErr(err)
    	fmt.Println(num)
    }

    func checkErr(err error) {
    	if err != nil {
    		panic(err)
    	}
    }
    ```

2. 例2
    ```
    package main

    import (
    	"database/sql"
    	"fmt"
    	_ "github.com/go-sql-driver/mysql"
    )

    type Users struct {
    	UserId int
    	Uname  string
    }

    func main() {
    	//db, err := sql.Open("mysql", "user:password@/dbname")
    	db, err := sql.Open("mysql", "root:cy123@/dataforum")
    	if err != nil {
    		fmt.Println("连接数据库失败")
    	}
    	defer db.Close()
    	var users []Users = make([]Users, 0)
    	sqlStr := "select * from users"
    	rows, err := db.Query(sqlStr)
    	if err != nil {
    		fmt.Println(err)
    	} else {
    		for i := 0; rows.Next(); i++ {
    			var u Users
    			rows.Scan(&u.UserId, &u.Uname)
    			users = append(users, u)
    		}
    		fmt.Println(users)
    	}
    }
    ```

3. 例3
    ```
    package main

    import (
    	"database/sql"
    	"fmt"
    	_ "github.com/go-sql-driver/mysql"
    )

    type userinfo struct {
    	name  string
    	email string
    }

    func main() {
    	// db, err := sql.Open("mysql", "root:cy123@tcp(127.0.0.1:3306)/dataforum?charset=utf8")
    	db, err := sql.Open("mysql", "root:cy123@/dataforum?charset=utf8")
    	checkErr(err)
    	rows, err := db.Query("SELECT name,email FROM users")
    	checkErr(err)
    	for rows.Next() {
    		var name, email string
    		if err := rows.Scan(&name, &email); err == nil {
    			fmt.Println(err)
    		}
    		fmt.Println(name)
    		fmt.Println(email)
    	}
    }

    func checkErr(err error) {
    	if err != nil {
    		panic(err)
    	} else {
    		fmt.Println("No error found!")
    	}
    }
    ```

# Golang连接Sqlite3

1. 例
    ```
    package main

    import (
    	"database/sql"
    	"fmt"
    	_ "github.com/mattn/go-sqlite3"
    	"log"
    	"os"
    )

    type Users struct {
    	UserId int
    	Uname  string
    }

    func main() {
    	os.Remove("./foo.db")

    	db, err := sql.Open("sqlite3", "./foo.db")
    	if err != nil {
    		log.Fatal(err)
    	}
    	defer db.Close()

    	sql := `create table users (userId integer, uname text);`
    	db.Exec(sql)
    	sql = `insert into users(userId,uname) values(1,'Mike');`
    	db.Exec(sql)
    	sql = `insert into users(userId,uname) values(2,'John');`
    	db.Exec(sql)
    	rows, err := db.Query("select * from users")
    	if err != nil {
    		log.Fatal(err)
    	}
    	defer rows.Close()
    	var users []Users = make([]Users, 0)
    	for rows.Next() {
    		var u Users
    		rows.Scan(&u.UserId, &u.Uname)
    		users = append(users, u)
    	}
    	fmt.Println(users)
    }
    ```
