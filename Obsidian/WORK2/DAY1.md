# 添加拦截器
## 1  新建拦截器类
```java
public class LoginInterceptor implements HandlerInterceptor{
}
```

==继承`HandlerInterceptor`接口,根据需求实现对应方法,其中包括以下三种方法==

>![[Pasted image 20231024201525.png]]

## 2  新建MVC配置类
```java
@Configuration  
public class MvcConfig implements WebMvcConfigurer {  
    @Override  
    public void addInterceptors(InterceptorRegistry registry) {  
        registry.addInterceptor(new LoginInterceptor())  
                .excludePathPatterns(  
                        "/user/code",  
                        "/user/login"  
                );  
    }  
}
```

==同样实现`WebMvcConfigurer`接口,同时添加需要排除的路径==


# 基于Redis实现登录校验功能
*注意点*

==需要保证,Redis存储的key唯一,且用户信息不被泄露==
>![[Pasted image 20231024211316.png]]


# Redis和数据库中的一致性
>![[Pasted image 20231025215506.png]]

==主动更新策略==

>![[Pasted image 20231025220112.png]]

>![[Pasted image 20231026161735.png]]

# 缓存击透
>![[Pasted image 20231026170401.png]]

>![[Pasted image 20231026172437.png]]


# 缓存雪崩
>![[Pasted image 20231026173216.png]]

# 缓存击穿
>![[Pasted image 20231028091515.png]]
>![[Pasted image 20231028091107.png]]

>![[Pasted image 20231028091439.png]]

>![[Pasted image 20231028111449.png]]

# Redis无侵入式添加数据
==1==
创建redisData类,将需要封装的数据都定义相应的属性;添加`@Data`注释
```java
@Data  
public class RedisData {  
    private LocalDateTime expireTime;  
    private Object data;  
}
```

==2==
创建对象并注入具体值

==总结==
[redis缓存总结](https://www.bilibili.com/video/BV1cr4y1671t/?p=47&spm_id_from=pageDriver&vd_source=c9f01c4138ffca623361215fe6c00336)












