# mybatis

## 动态sql

### <if/>

| 属性 | 描述     |
| ---- | -------- |
| test | 判断条件 |

1. 实体类数据类型为String时：<if test="field != null and field != '' "/if>
2. 实体类数据类型为Integer时：<if test="field != null "/if> 如果加上field != ''，当field=0时，mybatis会在xml中将field=0转为field='' 此时if条件不生效，因此对于实体类为Integer类型的，不需要判断field != ''

### <trim/>

| 属性 | 描述 |
| ---- | ---- |
|  prefix    |  给sql语句拼接的前缀  |
|suffix|给sql语句拼接的后缀|
|prefixOverrides|去除sql语句前面的关键字或者字符；<br>该关键字或者字符由prefixOverrides属性指定;<br>假设该属性指定为"AND"，当sql语句的开头为"AND"，trim标签将会去除该"AND"|
|suffixOverrides|去除sql语句后面的关键字或者字符;<br>该关键字或者字符由suffixOverrides属性指定|

### <foreach/>

<foreach/>标签用于迭代一个集合，通常构建在IN条件中；

比如：

```mysql
<select id="findStudentById" resultType="Student">
  SELECT * FROM student 
  WHERE id IN
  <foreach item="item" index="index" collection="list" open="(" separator="," close=")">
      #{item}
  </foreach>
</select>
```

| 属性 | 描述 |
| ---- | ---- |
| item | <foreach/>循环集合中的一个元素 |
| index |<foreach/>循环索引|
|collection|<foreach/>循环集合|
|open|<foreach/>子句前缀；<br>一般写"("|
|close|<foreach/>字句后缀；<br>一般写")"|
|separator|<foreach/>字句分隔符;<br>一般写","|
