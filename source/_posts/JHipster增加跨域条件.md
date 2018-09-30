---
title: JHipster增加跨域条件
date: 2018-09-30 16:29:08
tags:
- Springboot
- Cors
categories: JHipster
---

#问题描述
一般Jhipster的请求都是/api开头，我们的程序媛美眉创造了一个/web/api的请求，前端程序猿发现跨域了。

#问题解决
找到WebConfigurer,然后，你懂的
```java
    @Bean
    public CorsFilter corsFilter() {
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        CorsConfiguration config = jHipsterProperties.getCors();
        if (config.getAllowedOrigins() != null && !config.getAllowedOrigins().isEmpty()) {
            log.debug("Registering CORS filter");
            source.registerCorsConfiguration("/api/**", config);
            source.registerCorsConfiguration("/management/**", config);
            source.registerCorsConfiguration("/v2/api-docs", config);
        }
        return new CorsFilter(source);
    }
```


