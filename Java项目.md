# 前后端联调过程

## nginx反向代理

- 通过nginx的反向代理,将前端发送到的动态请求由nginx转发到后端服务器
  - 请求过程是由浏览器请求到nginx服务器再转发到tomcat后端服务器
- 好处:
  - 提高访问速度
  - 进行负载均衡
    - 负载均衡:把大量的请求按照我们指定的方式均衡的分配给集群中的每台服务器
  - 保证后端服务安全
    - 通过nginx走内网转发到后端服务

# 完善登录功能

### 密文密码

```java
//进行md5加密，然后再进行比对
        password= DigestUtils.md5DigestAsHex(password.getBytes());
```

### JWT令牌登录

- 全称是jsonwebtoken 使用JSON对象传输信息
- 在用户登录后获得了token,后续一些需要用户权限的请求就不会被拒绝请求

#### jwt与session比较的好处

- 在session中,第一次请求后服务器会创建一个session对话,这份登录信息会在响应时传给浏览器,储存在cookie中,会保存在内存中,服务器开销较大,并且服务器断电后session就会丢失
- session是存储在本地服务器的内存中,在分布式场景中很不实用,分布式通常是在几个服务之间调用,使用session会限制负载均衡的能力
- 不安全,基于cookie进行用户识别,如果cookie被拦截,服务器就容易被跨站请求伪造攻击
- 由于session id1只是一个特征值,表达信息不够丰富,在后端应用是多节点部署场景中,要实现session的共享机制,不方便使用

而jwt令牌本质是一个字符串

组成部分由:表头(header),有效负荷(payload),签名(singnature)

一般是在登录成功过后 通过键值对map的方式去生成jwt令牌

然后添加到实体中返回给前端

```java
//登录成功后，生成jwt令牌
        Map<String, Object> claims = new HashMap<>();
        claims.put(JwtClaimsConstant.EMP_ID, employee.getId());
        String token = JwtUtil.createJWT(
                jwtProperties.getAdminSecretKey(),
                jwtProperties.getAdminTtl(),
                claims);

        EmployeeLoginVO employeeLoginVO = EmployeeLoginVO.builder()
                .id(employee.getId())
                .userName(employee.getUsername())
                .name(employee.getName())
                .token(token)
                .build();
```



# redis

- 数据类型特点

| 字符串(string)            | 普通字符串,也是redis中最简单的数据类型                       |
| ------------------------- | ------------------------------------------------------------ |
| 哈希(hash)                | 散列,类似于Java中的HashMap结构                               |
| 列表(list)                | 按照插入顺序排序,可以有重复元素,类似Java中的LinkedList       |
| 集合(set)                 | 无序集合,没有重复元素,类似于Java中的HashSet                  |
| 有序集合(sorted set/zset) | 集合中每个元素关联一个分数(score),根据分数升序排序,没有重复元素 |

## 常用命令

- 字符串(string)操作命令

| SET key value            | 设置指定key的值                                |
| ------------------------ | ---------------------------------------------- |
| GET key                  | 获取指定key                                    |
| SETEX key secounds value | 设置指定key的值,并将key的过期时间设为seconds秒 |
| SETNX key value          | 只有在key不存在时设置key的值                   |

- Redis hash是一个string类型的field和value的映射表,hash特点适合储存对象

| HSET key field value | 将哈希表key中的字段field的值设为value |
| -------------------- | ------------------------------------- |
| HGET key field       | 将哈希表key中的字段field的值设为value |
| HDEL key field       | 获取储存在哈希表中指定字段的值        |
| HKEYS key            | 删除存储在哈希表中的指定指端          |
| HVALS key            | 获取哈希表中所有值                    |

​						value

​				 field1 value1

key->  	 

​				field2 value2



- 列表操作命令

Redis列表是简单字符串,按照插入顺序排序

| LPUSH key value1 [value2] | 讲一个或多个值插入到列表头部 |
| ------------------------- | ---------------------------- |
| LRANGE key start stop     | 获取列表指定范围内的元素     |
| RPOP key                  | 移除并获取列表最后一个元素   |
| LLEN key                  | 获取列表长度                 |

- 集合操作命令

| SADD key member1 [member2] | 像集合添加一个或多个成员 |
| -------------------------- | ------------------------ |
| SMEMBERS key               | 返回集合中的所有成员     |
| SCARD key                  | 获取集合的成员数         |
| SINTER key1 [key2]         | 返回给定所有集合的交集   |
| SUNIONkey1 [key2]          | 返回所有给定集合的并集   |
| SREM key member1 [member2] | 删除集合中一个或多个成员 |

- 有序集合操作命令

有序集合是string类型元素的集合,且不允许有重复成员,每个元素都会关联一个double类型的分数用于排序

| ZADD key score1 member1 [score2 member2] | 向有序集合添加一个或多个成员                |
| ---------------------------------------- | ------------------------------------------- |
| ZRANGE key start stop [WITHSCORES]       | 通过索引区间返回有序集合中指定区间内的成员  |
| ZINCRBY key increment member             | 有序集合中对指定成员的分数加上增量increment |
| ZREM key member [member ...]             | 移除有序集合中的一个或多个成员              |

- 通用命令

通用命令是不分数据类型的,都可以使用的命令:

- KEYS pattern:查找所有符合给定模式(pattern)的key
- EXISTS key:检查给定key是否存在
- TYPE key:返回key所储存的值的类型
- DEL key:该命令用于key存在是删除key



# HttpClient

- HttpClient是用来提供高效;最新;功能丰富的支持http协议的客户端编程工具包,并且支持HTTP协议最新的版本和建议







# SpringCache

- SpringCache是一个框架,实现了基于注解的缓存功能,只需要简单地加一个注解就可以实现缓存功能
- SpringCache主要是提供一层抽象,底层可以切换不同的缓存实现,例如:
  - EHCache
  - Caffeine
  - Redis
- 常用注解

| @EnableCaching | 开启缓存注解功能,通常加在启动类上                            |
| -------------- | ------------------------------------------------------------ |
| @Cacheable     | 在方法执行前先查询缓存中是否有数据,如果有数据,则直接返回缓存数据;如果没有数据,调用方法将方法返回值存在缓存中 |
| @CachePut      | 将方法的返回值放到缓存中                                     |
| @CacheEvict    | 将一条或多条数据从缓存中删除                                 |

## 案例

- 首先在主函数入口开启Cacheable

```java
@Slf4j
@SpringBootApplication
@EnableCaching//开启缓存注解功能
public class CacheDemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(CacheDemoApplication.class,args);
        log.info("项目启动成功...");
    }
}
```

- 然后再Controller层需要使用缓存的地方加入注解

```java
//@CachePut(cacheNames = "userCache",key="#user.id")//如果使用SpringCache key的生成:userCache::key  这里的key="#user.id"是一个spEL也就是Spring的EL表达式
    //@CachePut(cacheNames = "userCache",key="#result.id")//对象导航 是从return中的user获取值
    @CachePut(cacheNames = "userCache",key="#p0.id")//意思就是从第一个参数中获取到id p1 a0 a1都可以 
    @PostMapping
    public User save(@RequestBody User user){
        userMapper.insert(user);
        return user;
    }

@DeleteMapping
    @CacheEvict(cacheNames = "userCache",key="#id")//表示删除userCache::#id
    public void deleteById(Long id){
        userMapper.deleteById(id);
    }

	@DeleteMapping("/delAll")
    @CacheEvict(cacheNames = "userCache",allEntries = true)//表示全部删除userCache中的键值对
    public void deleteAll(){
        userMapper.deleteAll();
    }

    @GetMapping
    @Cacheable(cacheNames = "userCache",key = "#id")//cacheNames是表示要查询的键
    public User getById(Long id){
        User user = userMapper.getById(id);
        return user;
    }
```

# Spring Tsak

Spring Task是Spring框架提供的任务调度工具,可以按照约定的时间自动执行某个代码逻辑(也就是一个定时任务框架)

# WebSocket

WebSocket是基于TCP的一种新的**网络协议**,它实现了浏览器与服务器全双工通信-----浏览器和服务器只需要完成一次握手,两者之间就可以创建**持久性**连接,并进行**双向**数据传输

# Apache ECarts

Apache ECharts是一款基于Javascript的数据可视化图表,提供直观,生动,可交互,可个性化定制的数据可视化图表

# Apache POI

Apache POI是一个处理微软各种文件格式的开源项目,简单来说,我们可以使用POI在Java程序中对微软各种文件进行读写操作

一般情况下,POI都是用于操作Excel文件
