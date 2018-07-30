# To-do-list-Manage-System
Implement Spring MVC pattern to achieve the to-do manage System with login security. Used Eclipse as IDEL and implemented MAVEN to manage Spring projects and handle libraries. And utilized TOMCAT as web server.
在Spring MVC框架中，从“Request（请求）”开始，依次进入“DispatcherServlet（核心分发器）” —> “HandlerMapping（处理器映射）” —> “Controller（控制器）” —> “ModelAndView（模型和视图）” —> “ViewResolver（视图解析器）” —> “View（视图）” —> “Response（响应）”结束，其中DispatcherServlet、HandlerMapping和ViewResolver 只需要在XML文件中配置即可，从而大大提高了开发的效率，特别是对于 HandlerMapping 框架为其提供了默认的配置。</br>

Core function of manage system: 
---
    1 login security: XML Filter and Spring Security configuration denied users who logged out to access system with Admin role.
    2 System Admin role: add/delete/update to-do item into database
    3 HTML5 verfication: verified the input content by Hibernate Validation
    4 Implement Logout function and end authentication and clear session.
    5 Utilized Rest-Controller to enable users who logged out to retrieve to-do items in database with Read Only role.
    6 Internationalized whole System with Spring MVC by properties files.
