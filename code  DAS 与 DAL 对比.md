# 1
```java
public interface DalShardingStrategy {
    String locateDbShard(DalConfigure configure, String logicDbName, DalHints hints);
    String locateTableShard(DalConfigure configure, String logicDbName, String tabelName, DalHints hints);    
}
```

# 2
```java
public interface ShardingStrategy {
    Set<String> locateDbShards(ShardingContext ctx);
    Set<String> locateTableShards(TableShardingContext ctx);    
}
```
# 3
```java
PersonDefinition p = Person.PERSON;
p = p.inShard("0");
builder = SqlBuilder.selectAllFrom(p).where(p.Name.eq(name)).into(Person.class);
Person pk = dao.queryObject(builder);
```
# 4
```java
query(selectAllFrom(p).where(p.PeopleID.eq(1)), i, 1);
query(selectAllFrom(p).where(p.PeopleID.equal(1)), i, 1);
query(selectAllFrom(p).where(p.PeopleID.neq(1)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.notEqual(1)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.greaterThan(1)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.gteq(1)), i, 4);
query(selectAllFrom(p).where(p.PeopleID.greaterThanOrEqual(1)), i, 4);
query(selectAllFrom(p).where(p.PeopleID.lessThan(3)), i, 2);
query(selectAllFrom(p).where(p.PeopleID.lt(3)), i, 2);
query(selectAllFrom(p).where(p.PeopleID.lessThanOrEqual(3)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.lteq(3)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.between(1, 3)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.notBetween(2, 3)), i, 2);
query(selectAllFrom(p).where(p.PeopleID.notBetween(2, 4)), i, 1);
query(selectAllFrom(p).where(p.PeopleID.in(pks)), i, 3);
query(selectAllFrom(p).where(p.PeopleID.notIn(pks)), i, 1);
query(selectAllFrom(p).where(p.Name.like("Te%")), i, 4);
query(selectAllFrom(p).where(p.Name.notLike("%s")), i, 4);
query(selectAllFrom(p).where(p.Name.isNull()), i, 0);
query(selectAllFrom(p).where(p.Name.isNotNull()), i, 4);
```

# 5
```java
import static com.ppdai.das.client.SqlBuilder.*;
 
// 查询
SqlBuilder builder = selectAllFrom(p).where(p.PeopleID.eq(j+1)).into(Person.class);
Person pk = dao.queryObject(builder);
 
builder = selectAllFrom(p).where(p.PeopleID.eq(j+1)).into(Person.class).withLock();
Person pk = dao.queryObject(builder);
 
SqlBuilder builder = select(p.Name).from(p).where().allOf(p.PeopleID.eq(k+1), p.Name.eq("test")).into(String.class);
String name = dao.queryObject(builder);
 
SqlBuilder builder = select(p.PeopleID, p.CountryID, p.CityID).from(p).where(p.PeopleID.eq(k+1)).into(Person.class);
Person pk = dao.queryObject(builder);
 
// 插入
SqlBuilder builder = insertInto(p, p.Name, p.CountryID, p.CityID).values(p.Name.of("Jerry" + k), p.CountryID.of(k+100), p.CityID.of(k+200));
assertEquals(1, dao.update(builder));
 
// 更新
SqlBuilder builder = update(Person.PERSON).set(p.Name.eq("Tom"), p.CountryID.eq(100), p.CityID.eq(200)).where(p.PeopleID.eq(k+1));
assertEquals(1, dao.update(builder));
 
// 删除
SqlBuilder builder = deleteFrom(p).where(p.PeopleID.eq(k+1));
assertEquals(1, dao.update(builder));
```
