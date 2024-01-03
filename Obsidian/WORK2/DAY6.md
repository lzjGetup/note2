# 多级缓存

>![[Pasted image 20231221101652.png]]

# 本地缓存
>![[Pasted image 20231221105216.png]]

# Caffeine
Caffeine是一个用Java编写的高性能缓存库，旨在提供快速、高效的内存缓存解决方案。
```java
@Test  
void testBasicOps() {  
    // 创建缓存对象  
    Cache<String, String> cache = Caffeine.newBuilder().build();  
    // 存数据  
    cache.put("gf", "AAA");  
    // 取数据，不存在则返回null  
    String gf = cache.getIfPresent("gf");  
    System.out.println("gf = " + gf);  
    // 取数据，不存在则自动去数据库查询  
    String defaultGF = cache.get("defaultGF", key -> {  
        // 这里可以去数据库根据 key查询value  
        return "BBB";  
    });  
    System.out.println("defaultGF = " + defaultGF);  
}
```

>![[Pasted image 20231221114215.png]]

**Springboot使用Caffeine**
```java
@Configuration  
public class CaffeineConfig {  
    @Bean  
    public Cache<Long, Item>itemCache(){  
        return Caffeine.newBuilder()  
                .initialCapacity(100)  
                .maximumSize(10_000)  
                .build();  
    }
```

*在配置类中定义,用`@Bean`让spring管理,在使用时只需要`@Autowired`*

# Lua语言
Lua是一种轻量级的、高效的、可嵌入的脚本语言。它最初由巴西里约热内卢天主教大学（PUC-Rio）的一个研究小组开发，于1993年首次发布。Lua的设计目标是作为一种嵌入式脚本语言，用于扩展应用程序的功能。它具有简洁的语法、动态类型、自动内存管理和强大的表达能力，使得它在游戏开发、嵌入式系统、Web开发以及其他领域中得到广泛应用。Lua还被广泛用于编写插件和脚本扩展，例如在游戏引擎中用于实现游戏逻辑和用户界面。Lua的灵活性和可扩展性使得它成为许多开发者喜爱的工具之一。

>![[Pasted image 20231221193346.png]]

==遍历table==
1. 遍历数组
2. 遍历table(类比map)

>![[Pasted image 20231221194332.png]]

==条件判断==
>![[Pasted image 20231221195950.png]]


==定义函数==

>![[Pasted image 20231221195859.png]]

# OpenResty

>![[Pasted image 20231221200205.png]]













