---
title: RedirectAttributes使用
date: 2016-11-02 17:14:38
tags: [spring]
---
SpringMVC重定向传参数的实现。
<!--more-->

addFlashAttribute这个方法原理是放到session中，session在跳到页面后马上移除对象。所以你刷新一下后这个值就会丢失。

```java
package com.demo.controller;  
  
import java.util.Map;  
  
import org.springframework.stereotype.Controller;  
import org.springframework.ui.Model;  
import org.springframework.web.bind.annotation.ModelAttribute;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RequestParam;  
import org.springframework.web.servlet.mvc.support.RedirectAttributes;  
 
@Controller  
@RequestMapping("/user")  
public class DemoController {  
  
    @RequestMapping("/login")  
//  public String login(@RequestParam Map<String, String> user, Model model) {  
    public String login(@RequestParam Map<String, String> user, RedirectAttributes model) {  
        System.out.println("用户提交了一次表单");  
        String username;  
        if (user.get("name").isEmpty()) {  
            username = "Tom";  
        } else {  
            username = user.get("name");  
        }  
        model.addFlashAttribute("msg", username);  
//      return "home";//此方式跳转，页面刷新会重复提交表单  
        return "redirect:/user/toHome";  
    }  
      
    @RequestMapping("/toHome")  
    public String home(@ModelAttribute("msg") String msg, Model model) {  
        System.out.println("拿到重定向得到的参数msg:" + msg);  
        model.addAttribute("msg", msg);  
        return "home";  
    }  
}
```

这边我们使用@ModelAttribute注解，获取之前addFlashAttribute添加的数据，之后就可以正常使用啦。
或者

```java
Map<String,?> map = RequestContextUtils.getInputFlashMap(request); 
System.out.println(map.get("test").toString());
```
