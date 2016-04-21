```
Author: holdlg
Last updated: 2016-04-21 16:20:04
```

# spring data jpa 生成表的表名和表字段
- 生成的全是小写，驼峰命名法的用下划线“_”链接
- class.Table ->  table.table
- class.TableName ->  table.table_name
- 指定表名@Table和表字段@column
- 建议全部用小写，1.spring data jpa默认写法的坑。2. linux下大小写敏感问题
- spring data jpa默认写法的坑在于
- <code>@column(name="UserName")</code> -> <code>table.user_name</code>
- <code>@column(name="userName")</code> -> <code>table.user_name</code>
- <code>@column(name="username")</code> -> <code>table.username</code>
- <code>@column(name="USERNAME")</code> -> <code>table.username</code>
- 非全大写的名称若出现大写字符（开头大写除外）在生成数据库的时候就会用下划线<code>_</code>链接
- 可以设置忽略<code>spring.jpa.hibernate.naming-strategy=org.hibernate.cfg.DefaultNamingStrategy</code>
- yml写法

```
spring.jpa:
    hibernate:
        ddlAuto: update
        naming-strategy: org.hibernate.cfg.DefaultNamingStrategy
    showSql: true
```

- 参考：[spring data jpa表名@Table和表字段@column大小写敏感](https://github.com/spring-projects/spring-boot/issues/2129)

# spring data jpa 分页排序

```
    // contorller.java 配置Pageable

    import org.springframework.data.domain.Page;
    import org.springframework.data.domain.PageRequest;
    import org.springframework.data.domain.Pageable;
    import org.springframework.data.domain.Sort;


    @RequestMapping("/console/list/{page}")
    public Page<ConsoleInfo> getConsoleInfoList(@PathVariable int page){
        int pageSize = 10; 
        // new Sort() 排序 其中"id", "honId"和  实体类  的  字段名  一样

        // 简洁写法
        // Pageable pageable = new PageRequest(page, pageSize, Sort.Direction.DESC, "id", "honId");
        
        // 灵活写法，可以定义不同字段的DESC和ASC
        Pageable pageable = new PageRequest(page, pageSize,
                new Sort(Sort.Direction.DESC, "id").and(new Sort(Sort.Direction.DESC, "honId")));
        return consoleInfoService.getConsoleInfoList(pageable);
    }



    // PagingAndSortingRepository 
    public interface ConsoleInfoRepository extends PagingAndSortingRepository<ConsoleInfo, Integer> { }
```

参考：[spring boot 开发](https://github.com/holdlg/trap)