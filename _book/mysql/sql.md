# sql语言

<!-- toc -->

### DQL语言（data query language）

#### 基础查询

1. 语法：

   ```mysql
   select 查询内容 from 表名;
   ```

2. 特点：

   + 查询的结果集，是一个虚拟表；
   + select类似于System.out.println(打印内容);，select后面的查询内容，可以有多个部分组成，中间用逗号隔开，例如：select 字段1,字段2,... from 表；
   + 执行顺序：from字句>select字句；
   + 查询内容可以是字段、表达式（select 100*3）、常量（select 100）、函数等；

##### 查询常量

```mysql
select 100;
```

##### 查询表达式

```mysql
select 100*3;
```

##### 查询字段

```mysql
select `last_name`,`email`,`employee_id` from employee;
```

##### 查询所有字段

```mysql
select * from `employees`;
```

##### 查询函数（调用函数，获取返回值）

```mysql
select database()`;
select version();
select user();
```

##### 起别名

+ 使用as关键字：

  ```mysql
  #如果别名中间有空格，则必须用引号引起来；
  SELECT USER() AS 用户名;
  SELECT USER() AS "用户名";
  SELECT USER() AS '用户名';
  
  SELECT last_name AS '姓名' FROM employees;
  ```

+ 使用空格：

  ```mysql
  SELECT USER()  用户名;
  SELECT USER()  "用户名";
  SELECT USER()  '用户名';
  
  SELECT last_name '姓名' FROM employees;
  ```

##### 拼接字段并起别名：CONCAT

```mysql
#需求：查询first_name和last_name拼接成全名，最终起别名为：姓名
SELECT CONCAT(first_name,last_name) AS '姓 名' FROM employees;
```

```markdown
mysql中+的作用：加法运算

 	两个操作数都是数值型；

  		100+1.5；

	其中一个操作数为字符型：将字符型数据强制转换为数值型，如果无法转换，则直接当作0处理；

  		'张无忌'+100；===>100;

	其中一个数为null：结果均为null；

 		 null + null ===>null;

 		 null + 100 ===>null;
```

##### 去重distinct的使用

```mysql
#需求：查询员工涉及到的部门编号有哪些
SELECT DISTINCT department_id FROM employees;
```

##### 查看表的结构

```mysql
DESC employees;
SHOW COLUMNS FROM employees;
```

##### 函数ifnull的使用

+ 格式：

  ```mysql
  ifnull(表达式1，表达式2)
  #表达式1：可能为null的字段或表达式；
  #表达式2：如果表达式1为null，则最终=结果显示的值
  
  SELECT
  	commission_pct,
  	IFNULL( commission_pct, "空" ) 
  FROM
  	employees;
  ```

+ 功能：

  如果表达式1为null，则显示表达式2，否则显示表达式1

+ 需求：

  显示出表employees的全部列，各个列之间用逗号连接，列头显示成OUT_PUT

  ```mysql
  SELECT
  	CONCAT( employee_id, ',', first_name, ',', last_name, ',', salary, ',', IFNULL( commission_pct, '' ) ) AS "OUT_PUT" 
  FROM
  	employees;
  ```


#### 条件查询

1. 语法：

   ```mysql
   select 查询列表 from 表名 where 筛选条件；
   ```

2. 特点：

   + 按关系表达式筛选：
     + 关系运算符：>、<、>=、<=、=、<>（也可以使用!=，但不建议）
   + 按逻辑表达式筛选：
     + 逻辑运算符：and、or、not
   + 模糊查询：
     + like
     + in
     + between and
     + is null

##### 按关系表达式筛选

```mysql
#查询部门编号不是100的员工信息
SELECT
	* 
FROM
	employees 
WHERE
	department_id <> 100;
#查询工资小于15k的姓名和工资
SELECT
	last_name,
	salary 
FROM
	employees 
WHERE
	salary < 15000;
```

##### 按逻辑表达式筛选

```mysql
#查询部门编号不是50-100之间的员工姓名、部门编号、邮箱
SELECT
	last_name,
	department_id,
	email 
FROM
	employees 
WHERE
	department_id < 50 OR department_id > 100;
SELECT
	last_name,
	department_id,
	email 
FROM
	employees 
WHERE
	NOT ( department_id >= 50 AND department_id <= 100 );
#查询奖金率大于0.03或者员工编号在60-110之间的员工信息
SELECT
	* 
FROM
	employees 
WHERE
	commission_pct > 0.03 
	OR employee_id >= 60 
	AND employee_id <= 100;
```

##### 模糊查询

+ like/not like：一般和通配符搭配使用，对字符型数据进行部分匹配查询；

  ```
  _：匹配任意单个字符
  %：匹配任意多个字符
  ```

  ```mysql
  #查询姓名中包含字符a的员工信息
  SELECT
  	* 
  FROM
  	employees 
  WHERE
  	last_name LIKE '%a%';
  #查询姓名中第三个字符为x的员工信息
  SELECT
  	* 
  FROM
  	employees 
  WHERE
  	last_name LIKE '__x%';
  #查询姓名中第二个字符为_的员工信息
  SELECT
  	* 
  FROM
  	employees 
  WHERE
  	last_name LIKE '_$_%' ESCAPE '$';
  ```

  *注：使用escape表名‘$’进行转义*

+ in/not in：用于查询某字段的值是否属于指定的列表之内

  ```mysql
  #查询出部门编号是30、50、90的员工姓名、部门编号
  SELECT
  	last_name,
  	department_id 
  FROM
  	employees 
  WHERE
  	department_id IN ( 30, 50, 90 );
  #查询工种编号不是SH_CLERK或IT_PROG的员工信息
  SELECT
  	* 
  FROM
  	employees 
  WHERE
  	job_id NOT IN ( 'SH_CLERK', 'IT_PROG' );
  ```

+ between and/not between and：判断某个字段的值是否介于xx之间

  ```mysql
  #查询部门编号是30-90之间的部门编号、员工姓名
  SELECT
  	department_id,
  	last_name 
  FROM
  	employees 
  WHERE
  	department_id BETWEEN 30 
  	AND 90;
  #查询年薪不是100k-200k之间的员工姓名、工资和年薪
  SELECT
  	last_name,
  	salary,
  	salary * 12 * ( 1+ IFNULL( commission_pct, 0 ) ) AS 年薪 
  FROM
  	employees 
  WHERE
  	salary * 12 * ( 1+ IFNULL( commission_pct, 0 ) ) NOT BETWEEN 100000 
  	AND 200000;
  ```

+ is null/is not null

  ```mysql
  #查询没有奖金的员工信息
  SELECT
  	* 
FROM
  	employees 
WHERE
  	commission_pct IS NULL;
  ```
```
  
*=：只能判断普通的内容；*
  
  *IS：只能判断null值；*
  
  *<=>：安全判断，既能判断普通内容，又能判断null值*
  
  ```mysql
  SELECT * FROM employees WHERE salary <=> 10000;
  SELECT * FROM employees WHERE commission_pct <=> NULL;
```

#### 排序查询

1. 语法：

   ```mysql
   select 查询列表 from 表名 where 筛选条件 order by 排序列表
   ```

2. 特点：

   + 排序列表可以是单个字段、多个字段、表达式、函数、列数、以及以上的组合；
   + 升序asc，降序desc，默认为升序；

#####  按字段排序

```mysql
#将员工编号>120的员工信息进行工资的升序
SELECT
	* 
FROM
	employees 
WHERE
	employee_id > 120 
ORDER BY
	salary ASC;
```

##### 按表达式排序

```mysql
#对有奖金的员工按年薪降序
SELECT
	*,
	salary * 12 * ( 1+ IFNULL( commission_pct, 0 ) ) 年薪 
FROM
	employees 
WHERE
	commission_pct IS NOT NULL 
ORDER BY
	salary * 12 * ( 1+ IFNULL( commission_pct, 0 ) ) DESC;
```

##### 按别名排序

```mysql
#对有奖金的员工按年薪降序
SELECT
	*,
	salary * 12 * ( 1+ IFNULL( commission_pct, 0 ) ) 年薪 
FROM
	employees 
WHERE
	commission_pct IS NOT NULL 
ORDER BY
	年薪 DESC;
```

##### 按函数的结果排序

```mysql
#按姓名的字数长度进行升序
SELECT
	LENGTH( last_name ),
	last_name 
FROM
	employees 
ORDER BY
	LENGTH( last_name );
```

##### 按多个字段排序

```mysql
#查询员工的姓名、工资、部门编号，先按工资升序，再按部门编号降序
SELECT
	last_name,
	salary,
	department_id 
FROM
	employees 
ORDER BY
	salary,
	department_id DESC;
```

##### 按列数进行排序

```mysql 
SELECT * FROM employees ORDER BY 2;
```

#### 常见函数

​	mysql中的函数相当于Java中的方法，为了解决某个问题，将编写的一系列的命令集合封装在一期，对外仅仅暴露方法名，供外部调用 。

##### 字符函数

1. CONCAT：拼接函数

   ```mysql
   SELECT
   	CONCAT( 'hello,', first_name, last_name ) 备注 
   FROM
   	employees;
   ```

2. LENGTH：获取字节长度

   ```mysql
   SELECT LENGTH('hello');
   ```

3. CHAR_LENGTH：获取字符个数

   ```mysql
   SELECT CHAR_LENGTH('hello,郭襄');
   ```

4. SUBSTR(str，起始索引，截取的字符长度)：截取字符串    

     *mysql中起始索引从1开始，截取的字符长度可以为空标识截取起始索引后面的全部内容*

   ```mysql
   SELECT SUBSTR('张三丰爱上了郭襄',1,3);
   ```

5. INSTR：获取字符第一次出现的索引

   ```mysql
   SELECT INSTR('三打白骨精%白骨精%白骨精','白骨精');
   ```

6. TRIM([remstr FROM] str)：去除前后指定的字符，默认去空格

   ```mysql
   SELECT TRIM(' 虚 竹 ');
   SELECT TRIM('x' FROM 'xxxx虚xxxx竹xxxx');
   ```

7. LPAD(str,len,padstr)/RPAD(str,len,padstr)：左填充/右填充

   str为要被填充的字符串，len为填充后的字符串长度，padstr为要填充的内容

   ```mysql
   SELECT LPAD('木婉清',10,'a');
   ```

8. UPPER/LOWER：变大写/变小写

   ```mysql
   #查询员工表中的姓名，要求格式：姓首字符大写，其他字符小写，名所有字符大写，且 姓和名之前用_分割，最后起别名“OUTPUT”
   SELECT
   	UPPER( SUBSTR( first_name, 1, 1 ) ),
   	first_name 
   FROM
   	employees;
   	
   SELECT
   	LOWER( SUBSTR( first_name, 2 ) ),
   	first_name 
   FROM
   	employees;
   	
   SELECT
   	UPPER( last_name ) 
   FROM
   	employees;
   	
   SELECT
   	CONCAT(
   		UPPER( SUBSTR( first_name, 1, 1 ) ),
   		LOWER( SUBSTR( first_name, 2 ) ),
   		'_',
   		UPPER( last_name ) 
   	) 'OUTPUT' 
   FROM
   	employees;
   ```

9. STRCMP(expr1,expr2)：比较两个字符大小，expr1>expr2返回1，expr1<expr2返回2，expr1=expr2返回0

   ```mysql
   SELECT STRCMP('abc','aca');
   ```

10. LEFT(str,len)/RIGHT(str,len)：截取字符串

    ```mysql
    SELECT LEFT('鸠摩智',1);
    ```

##### 数学函数

1. ABS：绝对值

   ```mysql
   SELECT ABS(-2.4);
   ```

2. CEIL：向上取整

   ```mysql
   SELECT CEIL(1.05);
   ```

3. FLOOR：向下取整

   ```mysql
   SELECT FLOOR(2.03);
   ```

4. ROUND：四舍五入

   ```mysql
   SELECT ROUND(1.8723);
   SELECT ROUND(1.7321,2);
   ```

5. TRUNCATE(X,D)：截断,D表示保留D位

   ```mysql
   SELECT TRUNCATE(1.48379247,2);
   ```

6. MOD(N,M)：取余

   ```mysql
   SELECT MOD(-10,3);
   ```

##### 日期函数

1. NOW()：获取当前日期时间：

   ```mysql
   SELECT NOW();
   ```

2. CURDATE()：只获取当前日期

   ```mysql
   SELECT CURDATE();
   ```

3. CURTIME()：只获取当前时间

   ```mysql
   SELECT CURTIME();
   ```

4. DATEDIFF()：获取两个日期之差

   ```mysql
   SELECT CURTIME();
   ```

5. DATE_FORMAT()：将日期转换为指定格式的字符串

   ```mysql
   SELECT
   	DATE_FORMAT( '1998-7-16', '%Y年%m月%d日 %H小时%i分钟%s秒' ) 出生日期;
   	==>1998年07月16日 00小时00分钟00秒
   ```

6. STR_TO_DATE()：按指定的格式解析字符串为日期类型

   ```mysql
   SELECT
   	STR_TO_DATE( '3/15 1998', '%m/%d %Y' );
   SELECT
   	* 
   FROM
   	employees 
   WHERE
   	hiredate < STR_TO_DATE( '3/15 1998', '%m/%d %Y' );
   ```

##### 流程控制函数

1. IF(expr1,expr2,expr3)函数：表达式1成立，显示表达式2，否则显示表达式3

   ```mysql
   #如果有奖金，显示奖金，如果没有，显示0
   SELECT
   IF
   	( commission_pct IS NULL, 0, salary * 12 * commission_pct ) 奖金,
   	commission_pct 
   FROM
   	employees;
   ```

2. CASE函数：

   + 情况1：

     CASE  表达式

     WHEN  值1  THEN 结果1

     WHEN  值1  THEN 结果1

     ...

     ELSE 结果n

     END

     ```mysql
     #部门编号是30，工资显示为2倍；部门编号是50，工资显示为3倍；部门编号是60，工资显示为4倍；否则不变
     SELECT
     	department_id,
     	salary,
     CASE
     		department_id 
     		WHEN 30 THEN
     		salary * 2 
     		WHEN 50 THEN
     		salary * 3 
     		WHEN 60 THEN
     		salary * 4 ELSE salary 
     	END AS newsalary 
     FROM
     	employees;
     
     ```

     

   + 情况2：

     类似于多重IF语句，实现区间判断

     CASE 

     WHEN  条件1  THEN  结果1

     WHEN  条件2  THEN  结果2

     ...

     ELSE  结果N

     END

     ```mysql
     #如果工资>20000，显示级别为A；工资>15000，显示级别为B；工资>10000，显示级别C；否则显示D
     SELECT
     	salary,
     CASE
     		WHEN salary > 20000 THEN
     		'A' 
     		WHEN salary > 15000 THEN
     		'B' 
     		WHEN salary > 10000 THEN
     		'C' ELSE 'D' 
     	END AS grade 
     FROM
     	employees;
     ```

#### 分组/聚合函数

 1. 说明：

    分组函数往往用于实现将一组数据进行统计计算，最终得到一个值，又称为聚合函数或者统计函数；

	2. 分组函数清单：

    + SUM(字段名)：求和

    + AVG(字段名)：求平均值

    + MAX(字段名)：求最大值

    + MIN(字段名)：求最小值

    + count(字段名)：计算非空字段值的个数

      ```mysql
      #查询员工信息表中所有员工的工资和、平均工资值、最低工资、最高工资、有工资的个数
      SELECT
      	SUM( salary ),
      	AVG( salary ),
      	MIN( salary ),
      	MAX( salary ),
      	COUNT( salary ) 
      FROM
      	employees;
      #查询员工表中总的记录数
      SELECT
      	COUNT( employee_id ) 
      FROM
      	employees;
      #查询员工表中有工资的人数
      SELECT
      	COUNT( salary ) 
      FROM
      	employees;
      #查询员工表中月薪大于2500的人数
      SELECT
      	COUNT( salary ) 
      FROM
      	employees 
      WHERE
      	salary > 2500;
      #查询有领导的人数
      SELECT
      	COUNT( manager_id ) 
      FROM
      	employees;
      ```

	3. COUNT的补充说明：

    + 统计结果集的行数，推荐使用COUNT(*)；

      ```mysql
      SELECT
      	COUNT( * ) 
      FROM
      	employees;
      ```

    + 搭配DISTINCT实现去重的统计：

      ```mysql
      #查询有员工的部门个数
      SELECT
      	COUNT( DISTINCT ( department_id ) ) 
      FROM
      	employees;
      ```

#### 分组查询

1. 语法：

   select  查询列表  from  表名  where  筛选条件  group  by  分组列表；

2. 特点：

   + 查询列表往往是分组函数和被分组的字段；

   + 分组查询中的筛选分为两类：

     

     |            | 筛选的基表     | 使用的关键字 | 位置           |
     | ---------- | -------------- | ------------ | -------------- |
     | 分组前筛选 | 原始表         | where        | group by的前面 |
     | 分组后筛选 | 分组后的结果集 | having       | group by的后面 |

     

   + 执行顺序：from - where - group by - having - select - order by；

   + 分组函数做条件只可能放在having后面；

3. 简单的分组查询：

   ```mysql
   #查询每个工种的员工的平均工资
   SELECT
   	job_id,
   	AVG( salary ) 
   FROM
   	employees 
   GROUP BY
   	job_id;
   #查询每个领导的手下人数
   SELECT
   	manager_id,
   	COUNT( * ) 
   FROM
   	employees 
   WHERE
   	manager_id IS NOT NULL 
   GROUP BY
   	manager_id;
   ```

4. 可以实现分组前的筛选：

   ```mysql
   #查询邮箱中包含a字符的每个部门的最高工资
   SELECT
   	MAX( salary ) 最高工资， department_id 
   FROM
   	employees 
   WHERE
   	email LIKE '%a%' 
   GROUP BY
   	department_id;
   #查询每个领导手下有奖金的员工的平均工资
   SELECT
   	AVG( salary ) 平均工资,
   	manager_id 
   FROM
   	employees 
   WHERE
   	commission_pct IS NOT NULL 
   GROUP BY
   	manager_id;
   ```

5. 可以实现分组后的筛选：

   ```mysql
   #查询员工个数>5的部门
   SELECT
   	department_id,
   	COUNT( * ) 员工个数 
   FROM
   	employees 
   GROUP BY
   	department_id 
   HAVING
   	员工个数 > 5;
   #求每个工种有奖金的员工的最高工资>12000的工种编号和最高工资
   SELECT
   	job_id,
   	MAX( salary ) 
   FROM
   	employees 
   WHERE
   	commission_pct IS NOT NULL 
   GROUP BY
   	job_id 
   HAVING
   	MAX( salary ) > 12000;
   #查询领导编号>102的每个领导手下的最低工资大于5000的最低工资
   SELECT
   	manager_id,
   	MIN( salary ) 
   FROM
   	employees 
   WHERE
   	manager_id > 102 
   GROUP BY
   	manager_id 
   HAVING
   	MIN( salary ) > 5000;
   ```

6. 可以实现排序：

   ```mysql
   #查询每个工种有奖金的员工的最高工资大于6000的工种编号和最高工资，按最高工资升序
   SELECT
   	job_id,
   	MAX( salary ) 
   FROM
   	employees 
   WHERE
   	commission_pct IS NOT NULL 
   GROUP BY
   	job_id 
   HAVING
   	MAX( salary ) > 6000 
   ORDER BY
   	MAX( salary );
   ```

7. 按多个字段进行分组

   ```mysql
   #查询每个工种每个部门的最低工资，并按最低工资降序
   SELECT
   	job_id,
   	department_id,
   	MIN( salary ) 
   FROM
   	employees 
   GROUP BY
   	job_id,
   	department_id 
   ORDER BY
   	MIN( salary ) DESC;
   ```

#### 连接查询

1. 含义：

   连接查询又称为多表查询，当查询的字段来自于多个表时，就会用到连接查询；

   笛卡尔乘积：表1有m行，表2有n行，结果=m*n行，发生原因是没有有效的连接条件

   ```mysql
   SELECT
   	girName,
   	boyName 
   FROM
   	boys,
   	beauty 
   WHERE
   	beauty.boyfriend_id = boys.id;
   ```

2. 分类：

   + 按年代分类：
     + sql92标准：mysql中仅支持内连接
     + sql99标准：mysql中支持内连接+外连接(左外联/右外联)+交叉连接
   + 按功能分类：
     + 内连接：
       + 等值连接
       + 非等值连接
       + 自连接
     + 外连接：
       + 左外连接
       + 右外连接
       + 全外连接
     + 交叉连接

##### SQL92语法

+ **等值连接**

1. 语法：

   select  查询列表  from  表名1 别名1，表名2  别名2，...  where  等值连接的连接条件；

2. 特点：

   为了解决多表中的字段名重名问题，往往为表起别名，提高语义性；

   起别名之后不能再用原始表名进行限定；

   表的顺序无要求；

   ```mysql
   简单的等值连接：
   #查询员工名和部门名
   SELECT
   	last_name,
   	department_name 
   FROM
   	employees e,
   	departments d 
   WHERE
   	e.department_id = d.department_id;
   	
   加筛选的等值连接：
   #查询部门编号>100的部门名和所在的城市名
   SELECT
   	department_name,
   	city 
   FROM
   	departments d,
   	locations l 
   WHERE
   	d.location_id = l.location_id 
   	AND department_id > 100;
   #查询有奖金的员工名、部门名
   SELECT
   	last_name,
   	department_name 
   FROM
   	employees e,
   	departments d 
   WHERE
   	e.department_id = d.department_id 
   	AND e.commission_pct IS NOT NULL;
   #查询城市名中第二个字符为o的部门名和城市名
   SELECT
   	department_name,
   	city 
   FROM
   	departments d,
   	locations l 
   WHERE
   	d.location_id = l.location_id 
   	AND l.city LIKE '_o%';
   
   添加分组+筛选的等值连接
   #查询每个城市的部门个数
   SELECT
   	city,
   	COUNT( * ) 
   FROM
   	departments d,
   	locations l 
   WHERE
   	d.location_id = l.location_id 
   GROUP BY
   	l.city;
   #查询有奖金的每个部门的部门名和部门的领导编号和该部门的最低工资
   SELECT
   	d.department_name,
   	d.manager_id,
   	MIN( salary ) 
   FROM
   	departments d,
   	employees e 
   WHERE
   	d.department_id = e.department_id 
   	AND e.commission_pct IS NOT NULL 
   GROUP BY
   	department_name,
   	manager_id;
   	
   添加排序的等值连接
   #查询每个工种的工种名和员工的个数，并且按照员工个数降序
   SELECT
   	job_title,
   	COUNT( * ) 员工个数 
   FROM
   	employees e,
   	jobs j 
   WHERE
   	e.job_id = j.job_id 
   GROUP BY
   	job_title 
   ORDER BY
   	员工个数 DESC;
   
   实现多表连接
   #查询员工名、部门名和所在的城市
   SELECT
   	last_name,
   	department_name,
   	city 
   FROM
   	employees e,
   	departments d,
   	locations l 
   WHERE
   	e.department_id = d.department_id 
   	AND d.location_id = l.location_id;
   ```

3. 总结：

   多表连接的结果为多表的交集部分；

   n表连接，至少需要n-1个连接条件；

   多表的顺序没有要求；

   一般需要为表起别名；

   可以搭配前面介绍的所有子句使用，比如排序、分组、筛选。

+ **非等值连接**

```mysql
#查询员工的工资和工资级别
SELECT
	salary,
	grade_level 
FROM
	employees e,
	job_grades g 
WHERE
	e.salary BETWEEN g.lowest_sal 
	AND g.highest_sal 
ORDER BY
	g.grade_level DESC;
```

+ **自连接**

```mysql
#查询员工名和上级的名称
SELECT
	e.employee_id,
	e.last_name,
	m.manager_id,
	m.last_name 
FROM
	employees e,
	employees m 
WHERE
	e.employee_id = m.manager_id;
```

##### SQL99语法

+ **内连接**
  + 语法：

    select  查询列表  

    from  表名1 别名  

    【inner】 join  表名2 别名  

    on  连接条件

    where  筛选条件

    group by  分组列表

    having  分组后筛选

    order by  排序列表；

  + sql92和sql99的区别：

    sql99使用join关键字代替了之前的逗号，并且将连接条件和筛选条件进行了分离，提高阅读性。

1. 等值连接：

   ```mysql
   简单的连接
   #查询员工名和部门名
   SELECT
   	last_name,
   	department_name 
   FROM
   	employees e
   	INNER JOIN departments d ON e.department_id = d.department_id;
   
   添加筛选条件
   #查询部门编号>100的部门名和所在的城市名
   SELECT
   	department_name,
   	city 
   FROM
   	departments d
   	INNER JOIN locations l ON d.location_id = l.location_id 
   WHERE
   	d.department_id > 100;
   
   添加分组+筛选
   #查询每个城市的部门个数
   SELECT
   	l.city,
   	COUNT( * ) 
   FROM
   	departments d
   	INNER JOIN locations l ON d.location_id = l.location_id 
   GROUP BY
   	l.city;
   
   添加分组+筛选+排序
   #查询部门中员工个数>10的部门名，并按照员工个数降序
   SELECT
   	d.department_name,
   	COUNT( * ) 
   FROM
   	employees e
   	INNER JOIN departments d ON e.department_id = d.department_id 
   GROUP BY
   	d.department_id 
   HAVING
   	COUNT( * ) > 10 
   ORDER BY
   	COUNT( * ) DESC;
   ```

2. 非等值连接：

   ```mysql
   #查询部门编号在10-90之间的员工的工资级别，并按照级别进行分组
   SELECT
   	COUNT( * ),
   	j.grade_level 
   FROM
   	employees e
   	INNER JOIN job_grades j ON e.salary BETWEEN j.lowest_sal 
   	AND j.highest_sal 
   WHERE
   	e.department_id BETWEEN 10 
   	AND 90 
   GROUP BY
   	j.grade_level;
   ```

3. 自连接：

   ```mysql
   #查询员工名和对应的领导名
   SELECT
   	e.last_name,
   	m.last_name 
   FROM
   	employees e
   	INNER JOIN employees m ON e.manager_id = m.employee_id;
   ```

+ **外连接：左外联/右外联/全外联full**
  + 说明：

    查询结果为主表中所有的记录，如果从表有匹配项，则显示匹配项，如果从表没有匹配项，则显示null值。

  + 应用场景：

    一般用于查询主表中有，从表中没有的记录。

  + 特点：

    + 外连接分主从表，两边的顺序不能任意调换；
    + 左连接的话左边为主表，右连接的话右边为主表。
    + 左外联显示左表的全部内容，右外联显示右表的全部内容，即外联显示主表的内容；

  + 语法：

    select  查询列表

    from  表1 别名

    left | right | full【outer】 join  表2 别名

    on  连接条件

    where  筛选条件；

```mysql
左连
#查询所有女神记录，以及对应的男神名，如果没有对应的男神，则显示为null
SELECT
	b.*,
	bo.* 
FROM
	beauty b
	LEFT JOIN boys bo ON b.boyfriend_id = bo.id;
#查询那个女神没有男朋友
SELECT
	b.*,
	bo.* 
FROM
	beauty b
	LEFT JOIN boys bo ON b.boyfriend_id = bo.id 
WHERE
	bo.id IS NULL;
右连
#查询所有女神记录，以及对应的男神名，如果没有对应的男神，则显示为null
SELECT
	b.*,
	bo.* 
FROM
	boys bo
	RIGHT JOIN beauty b ON b.boyfriend_id = bo.id;
#查询那个女神没有男朋友
SELECT
	b.*,
	bo.* 
FROM
	boys bo
	RIGHT JOIN beauty b ON b.boyfriend_id = bo.id 
WHERE
	bo.id IS NULL;


#查询那个部门没有员工并显示其部门编号和部门名
SELECT
	d.department_id,
	d.department_name 
FROM
	departments d
	LEFT JOIN employees e ON d.department_id = e.department_id 
WHERE
	e.employee_id IS NULL;
```

#### 子查询

+ 说明：

  当查询语句中又嵌套了另一个完整的select语句，则被嵌套的select语句被称为子查询或内容查询，外面的select语句称为主查询或外查询。

+ 分类：

  + 按子查询出现的位置进行分类：
    + select后面：要求子查询的结果为单行单列（标量子查询）；
    + from后面：要求子查询的结果可以为多行多列（表子查询）；
    + <font color='red'>where或having后面：要求子查询的结果必须为单列</font>
      + 单行子查询（标量子查询）
      + 多行子查询（列子查询）
      + 多行多列子查询（行子查询）
    + exists后面：要求子查询的结果必须为单列（相关子查询）（表子查询）
  + 按结果集的行列数不同：
    + 标量子查询（结果集只有一行一列）
    + 列子查询（结果集只有一列多行）
    + 行子查询（结果集只有一行多列）
    + 表子查询（结果集一般为多行多列）

+ 特点：

  + 子查询放在条件中，要求必须放在条件的右侧；
  + 子查询一般放在小括号中；
  + 子查询的执行优先于主查询；
  + 单行子查询（标量子查询）对应了单行操作符：>、<、 >= 、<= 、<>；多行子查询（列子查询）对应了多行操作符：any/some、all、in

##### where或者having后面

1. 标量子查询

   ```mysql
   where后面
   #查询谁的工资比Abel的工资高
   SELECT
   	* 
   FROM
   	employees 
   WHERE
   	salary > ( SELECT salary FROM employees WHERE last_name = 'Abel' );
   #返还job_id与141号员工相同，salary比143号员工多的员工姓名、job_id和工资
   SELECT
   	last_name,
   	job_id,
   	salary 
   FROM
   	employees 
   WHERE
   	job_id = ( SELECT job_id FROM employees WHERE employee_id = 141 ) 
   	AND salary > ( SELECT salary FROM employees WHERE employee_id = 143 );
   #返回公司工资最少的员工的last_name,job_id,和salary
   SELECT
   	last_name,
   	job_id,
   	salary 
   FROM
   	employees 
   WHERE
   	salary = ( SELECT MIN( salary ) FROM employees );
   	
   having后面：
   #查询最低工资大于50号部门最低工资的部门id和其最低工资
   SELECT
   	department_id,
   	MIN( salary ) 
   FROM
   	employees 
   GROUP BY
   	department_id 
   HAVING
   	MIN( salary ) > ( SELECT MIN( salary ) FROM employees WHERE department_id = 50 );
   ```

2. 列子查询（多行子查询）：

   + 多行操作符：

     

     | 操作符      | 含义                       |
     | ----------- | -------------------------- |
     | in/not in   | 等于列表中的任意一个       |
     | any \| some | 和子查询返还的某一个值比较 |
     | all         | 和子查询返还的所有值比较   |

   

   ```mysql
   #返还location_id是1400或1700的部门中的所有员工的姓名
   SELECT
   	last_name 
   FROM
   	employees 
   WHERE
   	department_id IN ( SELECT DISTINCT department_id FROM departments WHERE location_id IN ( 1400, 1700 ) );
   #返回其他工种中比job_id为‘IT_PROG’部门任一工资低的员工的：工号、姓名、job_id和salary
   SELECT
   	employee_id,
   	last_name,
   	job_id,
   	salary 
   FROM
   	employees 
   WHERE
   	salary < ANY ( ( SELECT DISTINCT salary FROM employees WHERE job_id = 'IT_PROG' ) ) 
   	AND job_id <> 'IT_PROG';
   或者
   SELECT
   	employee_id,
   	last_name,
   	job_id,
   	salary 
   FROM
   	employees 
   WHERE
   	salary < ( SELECT MIN( salary ) FROM employees WHERE job_id = 'IT_PROG' ) 
   	AND job_id <> 'IT_PROG';
   #返回其他工种中比job_id为‘IT_PROG’部门所有工资都低的员工的员工号、姓名、job_id以及salary
   SELECT
   	employee_id,
   	last_name,
   	job_id,
   	salary 
   FROM
   	employees 
   WHERE
   	salary < ALL ( SELECT DISTINCT salary FROM employees WHERE job_id = 'IT_PROG' ) 
   	AND job_id <> 'IT_PROG';
   ```

3. 行子查询（结果集为一行多列或者多行多列）

   ```mysql
   #查询员工编号最小并且工资最高的员工信息
   SELECT
   	* 
   FROM
   	employees 
   WHERE
   	( employee_id, salary ) = ( SELECT MIN( employee_id ), MAX( salary ) FROM employees );
   ```

##### select后面

*仅仅支持标量子查询*

```mysql
#查询每个部门的员工个数
SELECT
	d.*,
	( SELECT COUNT( * ) FROM employees e WHERE e.department_id = d.department_id ) 
FROM
	departments d;
#查询员工号为102的部门名
SELECT
	( SELECT department_name FROM departments d INNER JOIN employees e ON d.department_id = e.department_id WHERE e.employee_id = 102 ) 部门名;
```

##### from后面

*将子查询结果充当一张表要求必须取别名*

```mysql
#查询每个部门的平均工资的工资等级
SELECT
	ag_dep.*,
	g.grade_level 
FROM
	( SELECT AVG( salary ) ag, department_id FROM employees GROUP BY department_id ) ag_dep
	INNER JOIN job_grades g ON ag_dep.ag BETWEEN lowest_sal 
	AND highest_sal;
```

##### exists后面：相关子查询

1. 语法：

   exists(完整的查询语句)

2. 结果：

   1或者0

```mysql
#查询有员工的部门名
SELECT
	department_name 
FROM
	departments d 
WHERE
	EXISTS ( SELECT * FROM employees e WHERE d.department_id = e.department_id );
#查询没有女朋友的男神信息
SELECT
	bo.*
FROM
	boys bo
WHERE
	NOT EXISTS(SELECT boyfriend_id FROM beauty WHERE bo.id=boyfriend_id);
```

#### 分页查询

1. 应用场景：

   当页面上的数据一页显示不全，则需要分页显示，分页查询的sql命令请求数据库服务器，服务器响应查询到的多条数据到前台页面

2. 语法：

   select  查询列表

   from  表1 别名

   join  表2  别名

   on  连接条件

   where  筛选条件

   group by  分组

   having  分组后筛选

   order by  排序列表

   limit  起始条目索引，显示的条目数

3. 执行顺序：

   from>join>on>where>group by>having>select>order by>limit

4. 特点：

   + 起始条目索引默认是0；
   + limit后面支持两个参数：
     + 参数1：显示的起始条目索引
     + 参数2：条目数

5. 公式：

   假如要显示的页数是page，每页显示的条目数是size，

   ```
   select *
   from employees
   limit (page-1)*size,size;
   ```

   

```mysql
#查询员工信息表的前5条
SELECT
	* 
FROM
	employees 
	LIMIT 5;
#查询有奖金的且工资较高的第11名到第20名
SELECT
	* 
FROM
	employees 
WHERE
	commission_pct IS NOT NULL 
ORDER BY
	salary DESC 
	LIMIT 10,
	10;
```

#### 联合查询

1. 说明：

   当查询结果来自于多张表，但多张表之间没有关联，这个时候往往使用联合查询也称为union查询

2. 语法：

   select  查询列表  from  表1  where 筛选条件

   union

   select  查询列表  from  表2  where 筛选条件

3. 特点：

   + 多条带联合的查询语句的查询列数必须一致，查询类型、字段意义最好一致；
   + union的查询结果自动去重，union all可以支持重复项

```mysql
#查询所有国家的年龄>20岁的用户信息
SELECT * FROM chinses WHERE age > 20 UNION SELECT * FROM usa WHERE uage > 20;
```

### DDL语言(data define language)

​	说明：DDL数据定义语言是对数据库和表的管理和操作

#### 库的管理

##### 创建数据库

​	create  database stuDB;

​	create  database if not exists stuDB;

```mysql
CREATE DATABASE stuDB;
CREATE DATABASE IF NOT EXISTS stuDB;
```

##### 删除数据库

drop database stuDB;

drop database if exists stuDB;

```mysql
DROP DATABASE stuDB;
DROP DATABASE IF EXISTS stuDB;
```

#### 表的管理

##### 创建表

1. 语法：

   ```mysql
   create table if not exists 表名(
   	字段名 字段类型 【字段约束】,
       字段名 字段类型 【字段约束】,
       字段名 字段类型 【字段约束】,
       字段名 字段类型 【字段约束】,
       ...
   );
   ```

2. 案例：

   ```mysql
   #没有添加约束的案例
   CREATE TABLE IF NOT EXISTS stuinfo ( 
   	stuid INT, 
       stuname VARCHAR ( 20 ), 
   	stugender CHAR, 
   	email VARCHAR ( 20 ), 
   	birdate datetime 
   );
   #添加约束的案例
   CREATE TABLE IF NOT EXISTS major(
   	id INT PRIMARY KEY COMMENT '专业代码',
   	name VARCHAR(20) COMMENT '专业名称',
   	score VARCHAR(20) COMMENT '分数'
   );
   
   CREATE TABLE IF NOT EXISTS stuinfo ( 
   	stuid INT PRIMARY KEY COMMENT '学号', #添加了主键约束
   	stuname VARCHAR ( 20 ) UNIQUE, #添加了唯一约束
   	stugender CHAR DEFAULT '男', #添加了默认约束
   	email VARCHAR ( 20 ) NOT NULL, #添加了非空约束
   	birdate TIMESTAMP,
   	age INT CHECK(age BETWEEN 0 AND 100),#添加了check约束，MySQL中不支持
   	majorid INT,
   	CONSTRAINT fk_stuinfo_major FOREIGN KEY (majorid) REFERENCES major(id)#添加了外键约束
   );
   ```

3. 常见数据类型：

   + 整型：

     + int：整型

   + 浮点型：

     + double(m,n)/float(m,n)：浮点型，例如double(5,2)表示最多5位，其中必须有2位小数，即在-999.99~999.99之间；
     + decimal(m,n)：浮点型，在表示钱方面使用该类型，因为不会出现精度缺失问题；

   + 字符型：

     + char(n)：固定长度字符串类型，char(4)范围是0-255；
     + varchar(n)：可变长度字符串类型；

     <table>
         <tr>
             <td>
             	数据类型
             </td>
             <td>
                 含义
             </td>
              <td>
                 格式
             </td>
             <td>
             	n的解释
             </td>
             <td>
                 特点
             </td>
              <td>
                 效率
             </td>
         </tr>
         <tr>
             <td>
             	char
             </td>
             <td>
                 固定字符长度
             </td>
              <td>
                 char(n)
             </td>
             <td>
             	最大的字符个数，可选，默认为1
             </td>
             <td>
                 不管实际存储，开辟的空间都是n个字节
             </td>
              <td>
                 高
             </td>
         </tr>
         <tr>
             <td>
             	varchar
             </td>
             <td>
                 可变字符长度
             </td>
              <td>
                 varchar(n)
             </td>
             <td>
             	最大的字符个数，必选
             </td>
             <td>
                 根据实际存储决定开辟的空间
             </td>
              <td>
                 低
             </td>
         </tr>
     </table>

   + text：字符串类型，表示存储较长文本；

   + 二进制型：

     + blob：二进制类型，//jpg mp3 avi；

   + 日期型：

     + date：日期类型：格式为：yyyy-MM-dd

     + time：时间类型：格式为：hh:mm:ss；

     + timestamp/datetime：时间戳类型，日期+时间，yyyyMMdd hhmmss

       <table>
         <tr>
               <td>
               	数据类型
               </td>
               <td>
                   保存范围
               </td>
                <td>
                   所占字节
               </td>
           </tr>
               <tr>
               <td>
               	datetime
               </td>
               <td>
                   1900-1-1~xxxx年
               </td>
                <td>
                   8
               </td>
           </tr>
               <tr>
               <td>
               	timestamp
               </td>
               <td>
                   1970-1-1~2038-12-31
               </td>
                <td>
                   4
               </td>
           </tr>
       </table>
     

4. 常见约束：

   + 说明：

     用于限制表中字段的数据的，从而进一步保证数据的表的数据是一致的、准确的、可靠的。

   + 约束类型：

     + NOT NULL：非空约束，用于限制该字段为必填项；

     + DEFAULT：默认约束，用于限制如果该字段没有显示插入值，则直接显示默认值；

     + PRIMARY KEY：主键约束，用于限制该字段不能重复，设置为主键列的字段默认不能为空，一个表只能有一个主键（可以是组合主键），如学号；

     + UNIQUE：唯一约束，用于限制该字段值不能重复，比如身份证号；

       <font color='red'>*主键和唯一键的对比*</font>
     
       <table>
           <tr>
               <td>类别</td>
               <td>字段是否可以为空</td>
               <td>一个表可以有几个</td>
           </tr>
           <tr>
               <td>PRIMARY KEY</td>
               <td>不可以</td>
               <td>1个</td>
           </tr>
           <tr>
               <td>UNION</td>
               <td>可以</td>
               <td>n个</td>
      </tr>
       </table>

     + CHECK：检查约束，用于限制该字段的值必须满足指定条件，MySQL中不支持；

       check(age between 1 and 100)

     + <font color='red'>FOREIGN KEY：外键约束，用于限制两个表的关系，要求外键列的值必须来自于主表的关联列，要求：</font>

       ​	@one：主表的关联列和从表的关联列的类型必须一致，意思一样，名称无要					求；

       ​	@two：主表的关联列要求必须是主键；
  
       ​	@three：插入数据时，先插入主表，在插入从表；删除数据时，先删除从
       
       ​					表，再删除主表；
       
       ​	@four：要求在从表设置外键关系
   
   ```mysql
   CREATE TABLE IF NOT EXISTS major(
   	id INT PRIMARY KEY COMMENT '专业代码',
   	name VARCHAR(20) COMMENT '专业名称',
   	score VARCHAR(20) COMMENT '分数'
   );
   
   CREATE TABLE IF NOT EXISTS stuinfo ( 
   	stuid INT PRIMARY KEY COMMENT '学号', #添加了主键约束
   	stuname VARCHAR ( 20 ) UNIQUE, #添加了唯一约束
   	stugender CHAR DEFAULT '男', #添加了默认约束
   	email VARCHAR ( 20 ) NOT NULL, #添加了非空约束
   	birdate TIMESTAMP,
   	age INT CHECK(age BETWEEN 0 AND 100),#添加了check约束，MySQL中不支持
   	majorid INT,
   	CONSTRAINT fk_stuinfo_major FOREIGN KEY (majorid) REFERENCES major(id)#添加了外键约束
   );
   ```
   
5. 添加表级约束（非空和默认约束不支持）：

   在各个字段的最下面，添加：

   ​	【constraint  约束名】 约束类型(字段名)

   ```mysql
   CREATE TABLE employees (
     employee_id int(6) NOT NULL AUTO_INCREMENT,
     first_name varchar(20) DEFAULT NULL,
     last_name varchar(25) DEFAULT NULL,
     email varchar(25) DEFAULT NULL,
     phone_number varchar(20) DEFAULT NULL,
     job_id varchar(10) DEFAULT NULL,
     salary double(10,2) DEFAULT NULL,
     commission_pct double(4,2) DEFAULT NULL,
     manager_id int(6) DEFAULT NULL,
     department_id int(4) DEFAULT NULL,
     hiredate datetime DEFAULT NULL,
     PRIMARY KEY (employee_id),#主键
     unique (employee_id),#唯一键
     check (gender='男' or gender='女'),#检查
     CONSTRAINT `dept_id_fk` FOREIGN KEY (`department_id`) REFERENCES `departments` (`department_id`),#外键
     CONSTRAINT `job_id_fk` FOREIGN KEY (`job_id`) REFERENCES `jobs` (`job_id`)
   ) ENGINE=InnoDB
   ```

   

##### 修改表

1. 语法：

   ```mysql
   alter table 表名 add|modify|change|drop column 字段名 字段类型 【字段约束】;
   ```

2. 修改表名rename：

   ```mysql
   ALTER TABLE stuinfo RENAME TO students;
   ```

3. 添加字段add：

   ```mysql
   ALTER TABLE students ADD COLUMN borndate TIMESTAMP NOT NULL;
   ```

4. 修改字段名change：

   ```mysql
   ALTER TABLE students CHANGE COLUMN borndate birthday datetime COMMENT '生日';
   ```

5. 修改字段类型modify：

   ```mysql
   ALTER TABLE students MODIFY COLUMN birthday TIMESTAMP;
   ```

6. 删除字段drop：

   ```mysql
   ALTER TABLE students DROP COLUMN birthday;
   ```

7. <font color='red'>修改表时添加约束：</font>

   + 添加列级约束：

     ```mysql
     alter table 表名 modify column 字段名 字段类型 新约束;
     ```

   + 添加表级约束：

     ```mysql
     alter table 表名 add 【constraint 约束名】 约束类型(字段名)【外键的引用】;
     ```

   ```mysql
   #添加非空约束
   alter table stuinfo modify column stuname varchar(20) not null;
   #添加默认约束
   alter table stuinfo modify column gender char default '男';
   #添加主键
   alter table stuinfo modify column id int primary key;#列级约束
   alter table styinfo add primary key(id);#表级约束
   #添加唯一键
   alter table stuinfo modify column seat int unique;#列级约束
   alter table stuinfo add unique(seat);#表级约束
   #添加外键
   alter table stuinfo add 【constraint fk_stuinfo_major】foreign key(majorid) references major(id);
   ```

8. <font color='red'>修改表时删除约束：</font>

   ```mysql
   #删除非空约束
   alter table stuinfo modify column stuname varchar(20) null;
   #删除默认约束
   alter table stuifo modify column gender char;
   #删除主键
   alter table stuinfo drop primary key;
   #删除唯一键
   alter table stuinfo drop index seat;
   #删除外键
   alter table stuinfo drop foreign key fk_stuinfo_major;
   ```

9. 修改表时设置自增：

   ```mysql
   alter table 表名 modify column id int primary key auto_increment;
   ```

10. 修改表示删除自增：

    ```mysql
    alter table 表名 modify column id int;
    ```

    

##### 删除表

```mysql
drop table if exists students;
```

##### 复制表

1. 仅仅复制表的结构

   ```mysql
   create table newtable like stuinfo;
   ```

2. 复制表的结构+数据

   ```mysql
   create table newtable2 select * from major;#复制本库的表
   create table newtable2 select * from myemployees.jobs;#复制其他库的表
   
   #复制employees表中的last_name,department_id,salary字段到新表emp表，但不复制数据
   CREATE TABLE emp SELECT last_name,department_id,salary FROM myemployees.employees WHERE 1=2;
   ```



### DML语言(data manipulation language)

​	使用insert、update、delete实现对表中数据的增删改

#### 插入数据

1. 语法：

   ```mysql
   #插入单行
   insert into 表名(字段1,字段2,...) values (值1,值2,...);
   #插入多行：
   insert into 表名(字段1,字段2,...) values (值1,值2,...),(值1,值2,...),(值1,值2,...),(值1,值2,...),...;
   ```

2. 注意事项：

   + 字段和值列表一一对应，包含类型、约束必须匹配；
   + 数值型的值，不用单引号，非数值型的值，必须使用单引号
   + 字段顺序无要求

3. 插入为空的数据：

   + 字段名写上，value值使用null
   + 字段名和值都不写

4. 插入默认的数据：

   + 字段名写上，value值使用default
   + 字段名和值都不写

5. 省略字段列表，默认所有字段

6. 设置自增列：

   + 创建表时添加auto increment，插入数据时该自增列以null取值；
   + 自增长列表要求必须设置在一个奸商，比如主键或者唯一键；
   + 自增长列要求数据类型为数值型；
   + 一个表至多有一个自增长列。

```mysql
#案例一：要求字段和值列表一一对应，且遵循类型和约束的限制
INSERT INTO students ( stuid, stuname, stugender, email, birdate, age, majorid )
VALUES
	( 1, '吴倩', '女', '4378491@qq.com', '1997-8-9', '18', 1 );
#案例二：可以为空的字段如何插入
INSERT INTO students ( stuid, stuname, stugender, email, age, majorid )
VALUES
	( 3, '吴淼', '女', '7568491@qq.com', '20', 1 );
	
INSERT INTO students ( stuid, stuname, stugender, email, birdate, age, majorid )
VALUES
	( 4, '吴群', '女', '4378491@qq.com', '1997-8-9', '18', null );
#案例三：默认字段如何插入
INSERT INTO students ( stuid, stuname, stugender, email, birdate, age, majorid )
VALUES
	( 5, '吴彦', DEFAULT, '4378491@qq.com', '1997-8-9', '18', null );
#案例四：可以省略字段列表，默认所有字段
INSERT INTO students
VALUES
	( 6, '吴赏', '女', '4378491@qq.com', '1997-8-9', '18', 2 );
```

#### 修改数据

```mysql
update 表名 set 字段名 = 新值,字段名 = 新值,...where 筛选条件;
```

```mysql
#修改年龄<20的专业编号为2号，且邮箱修改为3473817@qq.com
UPDATE students SET majorid=2,email='3473817@qq.com' WHERE age<20;
```

#### 删除数据

+ delete语句：

  ```mysql
  delete from	表名 where 筛选条件;
  ```

  ```mysql
  #删除学号为3的学生信息
  DELETE FROM students WHERE stuid=3;
  ```

+ truncate语句：

  ```mysql
  truncate table 表名;
  ```

  ```mysql
  #删除students表中所有的数据
  DELETE FROM students WHERE stuid=3;
  ```

+ <font color='red'>delete和truncate的区别：</font>

  + delete可以添加where条件，truncate不能添加where语句，一次性清除所有数据；
  + truncate的效率较高；
  + 如果删除带自增长列的表，使用delete删除后重新插入的数据，记录从断点开始；使用truncate删除后重新插入的数据，记录从1开始；
  + delete删除数据，会返回受影响的行数，truncate删除数据，不返回受影响的行数；
  + delete删除数据，可以支持事务回滚；truncate删除数据，不支持事务回滚。

