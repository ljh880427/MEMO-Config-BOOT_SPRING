## Boot 스프링 초기 설정

### 아래와 같이 BOOT 스프링을 생성합니다.

### 1. Spring Starter Project 신규 생성
![image](https://github.com/user-attachments/assets/5888a1ed-0401-48d1-9a65-fea2fa307b68)
<br/>
### 2. Gradle 사용
![image](https://github.com/user-attachments/assets/aead4302-c64c-41c4-9678-1b8d07d47082)
<br/>
### 3. Spring Web 선택 후 Finish
![image](https://github.com/user-attachments/assets/2f9236eb-5a1e-4ec4-96d5-037f55c36e42)
<br/><br/>

### HomeController.java , templates 경로 아래 test.html 파일을 생성합니다. <br/>
![image](https://github.com/user-attachments/assets/d30d1dd2-188e-4a75-90fd-02ded9d4caef)<br/>
```
package com.java.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HomeController {
	
	@RequestMapping(value = "/")
	public String test() {
		
		System.out.println("test");
		
		return "test";
	}

}

```
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	안녕
</body>
</html>
```
<br/>


### Boot 스프링을 실행하여 http://localhost:8080/ 요청하였으나 아래와같이 에러코드 404로 페이지를 찾지 못합니다. <br/>
![image](https://github.com/user-attachments/assets/4b238c5c-711e-4775-ad9c-940d9ad53bf9) <br/>

<br/> 

### 위 문제를 해결하기 위해 config 패키지를 만들고, MvcConfiguration 파일을 생성합니다.
```
package com.java.config;

import java.util.concurrent.TimeUnit;

import org.springframework.context.annotation.Configuration;
import org.springframework.http.CacheControl;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class MvcConfiguration implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**")
                .addResourceLocations("classpath:/templates/", "classpath:/static/")
                .setCacheControl(CacheControl.maxAge(10, TimeUnit.MINUTES));
    }
}
```
```
설명 내용
Spring Boot는 기본으로 바라보는 정적 자원의 위치가 있습니다.
classpath:/META-INF/resources/
classpath:/resources/
classpath:/static/
classpath:/public/
```
