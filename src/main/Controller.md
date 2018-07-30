Controller
===
ExceptionController.java
---
    package com.in28minutes.exception;

    import javax.servlet.http.HttpServletRequest;
    import org.apache.commons.logging.Log;
    import org.apache.commons.logging.LogFactory;
    import org.springframework.web.bind.annotation.ControllerAdvice;
    import org.springframework.web.bind.annotation.ExceptionHandler;

    @ControllerAdvice
    public class ExceptionController {
      private Log logger=LogFactory.getLog(ExceptionController.class);
      @ExceptionHandler(value=Exception.class)//handle everything
      public String handleException(HttpServletRequest request, Exception ex) {
	      logger.error("request"+request.getRequestURL()+"Threw an Exception", ex);
	      return "error";
      }
    }
LogoutController.java
---
    package com.in28minutes.login;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import org.springframework.security.core.Authentication;
    import org.springframework.security.core.context.SecurityContextHolder;
    import org.springframework.security.web.authentication.logout.SecurityContextLogoutHandler;
    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;

    @Controller
    public class LogoutController {
	  //only support get method
	  @RequestMapping(value="/logout", method=RequestMethod.GET)
	  //to make dispatchaer know"hello world!" is not a url
	  //@ResponseBody
    public String LogoutPage(HttpServletResponse response, HttpServletRequest request) {
	   //terminate the authentication
		Authentication auth=SecurityContextHolder.getContext().getAuthentication();
		if(auth!=null) {
			new SecurityContextLogoutHandler().logout(request, response, auth);
		}
		request.getSession().invalidate();
	    return "redirect:/";
      }  
    }
    
WelcomeController.java
---
    package com.in28minutes.login;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.SessionAttributes;
    //import org.springframework.web.bind.annotation.ResponseBody;
      @Controller
      public class WelcomeController {
	    //only support get method
	    @RequestMapping(value="/", method=RequestMethod.GET)
	     //to make dispatchaer know"hello world!" is not a url
	    //@ResponseBody
      public String showWelcomePage(ModelMap model) {
	      model.put("Name", "in28Minutes");
	      return "welcome";
      }
    }

