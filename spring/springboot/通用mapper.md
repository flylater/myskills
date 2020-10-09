## 准备数据库  

### 建表语句  

``` sql
CREATE TABLE `tabple_emp`(
`emp_id` INT NOT NULL AUTO_INCREMENT,
`emp_name` VARCHAR(500),
`emp_salary` DOUBLE(15,5),
`emp_age` INT,
PRIMARY KEY (`emp_id`)
);
```

### 前置数据  

``` sql
INSERT INTO `tabple_emp` (`emp_name`,`emp_salary`,`emp_age`) VALUES ('tom','1254.37','27');
INSERT INTO `tabple_emp` (`emp_name`,`emp_salary`,`emp_age`) VALUES ('jerry','6635.42','38');
INSERT INTO `tabple_emp` (`emp_name`,`emp_salary`,`emp_age`) VALUES ('bob','5560.11','40');
INSERT INTO `tabple_emp` (`emp_name`,`emp_salary`,`emp_age`) VALUES ('kate','2209.11','22');
INSERT INTO `tabple_emp` (`emp_name`,`emp_salary`,`emp_age`) VALUES ('justin','4203.15','30');
```

