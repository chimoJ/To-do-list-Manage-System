footer.jspf
---
      <script src="webjars/jquery/1.9.1/jquery.min.js"></script>
      <script src="webjars/bootstrap/3.3.6/js/bootstrap.min.js"></script>
      <script
            src="webjars/bootstrap-datepicker/1.0.1/js/bootstrap-datepicker.js"></script>
    </body>
    </html>
header.jspf
---
    <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
    <%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
    <%@taglib uri="http://www.springframework.org/tags/form" prefix="form"%>
    <%@taglib uri="http://www.springframework.org/tags" prefix="spring"%>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>welcome</title>
    <link href="webjars/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
    
navigation.jspf
---
    <nav role="navigation" class="navbar navbar-default">
	    <div class="">
		<a href="http://www.in28minutes.com" class="navbar-brand">in28Minutes</a>
	    </div>
	    <div class="navbar-collapse">
		    <ul class="nav navbar-nav">
			    <li class="active"><a href="/">Home</a></li>
			    <li><a href="/list-todos">Todos</a></li>
		    </ul>
		    <ul class="nav navbar-nav navbar-right">
		       <li><a href="/logout">Logout</a></li>
		    </ul>
	    </div>
    </nav>
