# 实验1：SQL语句的执行计划分析与优化指导

## 实验目的

分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。

## 实验内容

- 对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。



### 实验步骤

```sql
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;
```

得到：

![image-20210316191428373](README.assets/image-20210316191428373.png)





### 教材样例分析

##### 教材中的查询语句

查询1：

```sql
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;
```

显示：

![image-20210316191511785](README.assets/image-20210316191511785.png)

优化指导：

![image-20210316191526969](README.assets/image-20210316191526969.png)



- 查询2

```sql
set autotrace on
SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY d.department_name
HAVING d.department_name in ('IT','Sales');
```

结果：

![image-20210316191632984](README.assets/image-20210316191632984.png)

### 查询语句

```sql
set autotrace on
SELECT d.department_name,e.EMPLOYEE_id,e.job_id
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('Shipping')
GROUP BY department_name,e.EMPLOYEE_id,e.job_id;
```

![image-20210316191707134](README.assets/image-20210316191707134.png)

