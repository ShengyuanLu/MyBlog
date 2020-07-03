# 1
```java
public static void main (String[] args) throws IOException {
    InputStream resourceAsstream = Resources.getResourceAsStream("cc/sq1MupConfig.xml");
    SqlSessionFactory ssf = new SqlSessionFactoryBuilder().build(resourceAsstream); 
    SqlSession sqlSession = ssf.openSession();
    //mapper 就是 UserMapper 接口的实现类
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User u = mapper.finduserById(10);
    System.out.println(u);
}
```
# 2
```java
Person pk = new Person();
pk.setName("test");
DasClient dao = DasClientFactory.getClient("logicDbName");
List<Person> plist = dao.queryBySample(pk);
```
# 3
```xml
<select id="selectByExample" parameterType="com.ppdai.xxxx.StrategyAccountDetailExample" resultMap="BaseResultMap">
    select 
    <if test="distinct">
      distinct
    </if>
    'false' as QUERYID,
    <include refid="Base_Column_List" />
    from strategyaccountdetail${tableSuffix} 
    <if test="_parameter != null">
        <include refid="Example_Where_Clause" />
    </if>
    <if test="orderByClause != null">
      order by ${orderByClause}
    </if>
</select>
```

# 4
```java
public List<Strategyaccountdetail> selectByExample(Strategyaccountdetail detail) throws SQLException { 
    return client.queryBySample(detail);
}
```
# 5
```xml
<select id="selectListByUserIdExample" parameterType="java.util.Map" resultMap="BaseResultMap">
    select * from (select ROW_NUMBER() OVER ( ORDER BY inserttime DESC ) rownum,  <include refid="Base_Column_List" />
    from strategyaccountdetail${tableSuffix} WITH(NOLOCK)
    where userid = #{userid,jdbcType=INTEGER}    
    <if test="strategyid != null and strategyid != ''">
      and strategyid = #{strategyid,jdbcType=VARCHAR}    
    </if>
    <if test="typeid != null">
      and typeid = #{typeid,jdbcType=INTEGER}
    </if>
    <if test="beginInserttime != null">
      and inserttime <![CDATA[>= ]]> #{beginInserttime,jdbcType=TIMESTAMP}
    </if>
    <if test="endInserttime != null">
      and inserttime <![CDATA[<= ]]> #{endInserttime,jdbcType=TIMESTAMP}   
    </if>
    AND isactive=1) tpage WHERE tpage.rownum BETWEEN ${startPage} AND ${pageSize}  
</select>
```

# 6
```java
public List<Strategyaccountdetail> selectListByUserIdExample (Long userId, String strategyid, Integer typeId,
        Date beginInserttime, Date endInserttime, Integer pageNum, Integer pageSize) throws SQLException {
    SqlBuilder builder = SqlBuilder.selectAllFrom(definition).where()
        .allOf(
            definition.Userid.eq(userId),
            definition.Isactive.eq(1),
            definition.Strategyid.eq(strategyid).nullable(),
            definition.Typeid.eq(typeId).nullable(),
            definition.Inserttime.greaterThanOrEqual(beginInserttime).nullable(),
            definition.Inserttime.lessThanOrEqual(endInserttime).nullable())
        .orderBy(definition.Inserttime.desc())
        .into(Strategyaccountdetail.class)
        .offset(pageNum, pageSize).withLock();  
      return client.query(builder);
}
 ```
# 7
```java
public string selectPersonLike(String id, String firstName, String lastName) {
    return new SQL() {
        {
           SELECT("P.ID, P.USERNAIE, P.PASSWORD, P.FIRST_NANE, P.LAST_NAME");
           FROM("PERSON P");                
           if (id != **null**) {
               WHERE(" P.ID like#{id}");
           }                
           if (firstlame != null) {
               WHERE("P.FIRST_NANE like #{firstliase}");
           }      
           if (lastlame != null) {
               WHERE("P.LAST_NAMIE like #{lastName}");
           } 
           ORDER BY("P.LAST_NAMIE");
         }
     }.toString();
}
```

# 8
```java
public SqlBuilder seletPersonLike (String id, String firstName, String lastName) {
        Person.PersonDefinition P = Person.PERSON;       
        return sqlBuilder.selectAllFrom(p).where()
            .allOf(
                p.id.like(id).nullable(),
                p.firstName.like(firstNane).nullable(),
                p.lastName.1ike(lastName).nullab1e()
            )
            .orderBy(p.lastName);
}
```
 

# 9
```java
// Sharding database and table with using hintManager ，
String sql = "SELECT * FROM t order";    
try(HintManager hintManager = HintManager.getInstance();
        Connectlon conn = dataSource.getConnection();
        PreparedStatement preparedstatement conn.prepareStatement(sql)) {
        hintManager.addDatabaseShardingValue("t_order", 1);
        hintManager.addTableShardingValue("t_order", 2);        
        try (ResultSet rs = preparedStatement.executeQuery()) {  
            while (rs.next()) {               
                ...
            }
        }
}
```
 
