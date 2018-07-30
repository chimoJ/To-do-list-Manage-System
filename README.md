# To-do-list-Manage-System
Implement Spring MVC pattern to achieve the to-do manage System with login security. We use Eclipse and as IDEL and MAVEN to manage Spring project and handle the libraries. And use TOMCAT as web server.
在Spring MVC框架中，从“Request（请求）”开始，依次进入“DispatcherServlet（核心分发器）” —> “HandlerMapping（处理器映射）” —> “Controller（控制器）” —> “ModelAndView（模型和视图）” —> “ViewResolver（视图解析器）” —> “View（视图）” —> “Response（响应）”结束，其中DispatcherServlet、HandlerMapping和ViewResolver 只需要在XML文件中配置即可，从而大大提高了开发的效率，特别是对于 HandlerMapping 框架为其提供了默认的配置。
Core function about manage system: 
1 login security: Admin role cann't be gained without login by Spring security library.
2 add/delete/update to-do item into database
3 verified the input content by Hibernate Validation
4 Implement Logout function and end authentication and clear session.
5 Utilize RestController enable the rest users to visit to-do items in database
6 Internationlization by properties files.
