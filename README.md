# dbhelper

##### 一个简单的基于Spring JdbcTemplate帮助包 (暂时只支持mysql)

1、Maven
```xml
<dependency>
  <groupId>com.denghb</groupId>
  <artifactId>dbhelper</artifactId>
  <version>1.5</version>
</dependency>
```
Or 
```
git clone https://github.com/deng-hb/dbhelper.git
```

2、配置


在Spring配置文件（applicationContext.xml）中增加
```xml
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
	<property name="dataSource">
		<ref bean="dataSource" />
	</property>
</bean>

<bean id="dbHepler" class="com.denghb.dbhelper.impl.DbHelperImpl">
	<property name="jdbcTemplate" ref="jdbcTemplate"></property>		
</bean>
```
Or 下载源码使用注解（jdbcTemplate需要在配置中）
```java
@Repository
public class DbHelperImpl implements DbHelper {

  	@Repository
	private JdbcTemplate jdbcTemplate;
```

3、使用
```java
	/**
	 * 创建一条纪录
	 * 
	 * @param domain
	 * @return
	 */
	public boolean insert(Object object);

	/**
	 * 更新一条纪录
	 * 
	 * @param domain
	 * @return
	 */
	public boolean updateById(Object object);

	/**
	 * 执行一条SQL
	 * 
	 * @param sql
	 * @param args
	 * @return
	 */
	public int execute(String sql, Object... args);

	/**
	 * 查询并返回分页
	 * 参考
	 * {@link com.denghb.dbhelper.DbHelper.list}
	 * @param sql
	 * @param clazz
	 * @param paging
	 * @return
	 */
	public <T> PagingResult<T> list(StringBuffer sql, Class<T> clazz, Paging paging);

	/**
	 * 查询列表
	 * 
	 * 
	 * <pre>
	 * 
	 * Example
	 * 
	 * Bean:
	 * public class User implements Serializable {
	 * 	
	 *	private String name;
	 *  
	 *	public String getName() {
	 *		return name;
	 *	}
	 *
	 *	public void setName(String name) {
	 *		this.name = name;
	 *	}
	 *}
	 *  
	 * SQL:
	 * select c_name_v as name from user;
	 * 
	 * 只要是列名和对象字段名一致就能反射赋值
	 * 
	 * @{link BeanPropertyRowMapper}
	 * </pre>
	 * 
	 * @param sql
	 * @param clazz
	 * @param args
	 * @return
	 */
	public <T> List<T> list(String sql, Class<T> clazz, Object... args);

	/**
	 * 指定参数查询返回对象
	 * 
	 * @param sql
	 * @param clazz
	 * @param args
	 * @return
	 */
	public <T> T queryForObject(String sql, Class<T> clazz, Object... args);

	/**
	 * 查询一条纪录
	 * 
	 * @param clazz
	 * @param id
	 * @return
	 */
	public <T> T queryById(Class<T> clazz, Object id);

	/**
	 * 物理删除
	 * 
	 * @param clazz
	 * @param id
	 * @return
	 */
	public <T> boolean deleteById(Class<T> clazz, Object id);
```

4、兼容 spring-jdbc 3.1.0.RELEASE 及以上版本

5、数据库表生成对应实体[Generate](https://github.com/deng-hb/dbhelper-test/blob/master/src/test/java/com/denghb/dbhelper/generate/GenerateDomainFromTable.java)

5、更多请参考 [Test Project](https://github.com/deng-hb/dbhelper-test)

6、欢迎拍砖（[issues](https://github.com/deng-hb/dbhelper/issues)||i#denghb.com）#->@

7、License
```
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to You under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

