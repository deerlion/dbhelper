# dbhelper

##### 一个简单的基于Spring JdbcTemplate帮助包 (暂时只支持mysql)

1、下载
```xml
<dependency>
  <groupId>com.denghb</groupId>
  <artifactId>dbhelper</artifactId>
  <version>1.0</version>
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
Or 使用注解（jdbcTemplate需要在配置中）
```java
@Repository
public class DbHelperImpl implements DbHelper {

	private final static Logger log = LoggerFactory.getLogger(DbHelperImpl.class);
  
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
	 * 
	 * @param sql
	 * @param clazz
	 * @param paging
	 * @return
	 */
	public <T> PagingResult<T> list(StringBuffer sql, Class<T> clazz, Paging paging);

	/**
	 * 查询列表
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


4、更多请参考 [TestCase](https://github.com/deng-hb/dbhelper/blob/master/src/test/java/com/denghb/dbhelper/AppTest.java)

5、欢迎拍砖（issues||i<at>denghb.com）

6、木有版权，随意更改

