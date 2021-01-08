# MySql注释

- 单行注释

  ```mysql
  #这是单行注释
  -- 单行注释，需要在--后面加空格
  ```

- 多行注释

  ```mysql
  /*
  这是多行注释
  */
  ```

# 常用命令

- 新增字段

  ```mysql
  alter table <table_name> add column  <column_name> <data_type> default <default_value> comment <annotation>;
  
  #例子
  alter table student add column name varchar(40) default null comment '学生名称默认空';
  alter table student add column name varchar(40) not null comment '学生名称';
  alter table student add column name varchar(40) not null default '学生' comment '学生名称默认值';
  ```

- 