WEB-INF下的jsp文件
===
error.jsp
---
    <%@ include file="common/header.jspf" %>
    <%@ include file="common/navigation.jspf" %>
      <div class="container">
          Application has encountered an error.
          Please contact support on ...
      </div> 
    <%@ include file="common/footer.jspf"%>

error-specific.jsp
---
    <%@ include file="common/header.jspf" %>
    <%@ include file="common/navigation.jspf" %>
    <div class="container">
      Specific Exception page
      Please contact support on ...
    </div>
    <%@ include file="common/footer.jspf"%>

list-todos.jsp
---
    <%@ include file="common/header.jspf" %>
    <%@ include file="common/navigation.jspf" %>

    <div class="container">
     <table class="table table-striped"><!-- two classes -->
      <caption><spring:message code="todo.caption" /></caption>
      <thead>
        <tr>
          <th>Description</th>
          <th>Terget Date</th>
          <th>Is Completed?</th>
          <th></th>
        </tr>
     </thead>
     <tbody>
     <c:forEach items="${todos}" var="todo">
       <tr>
	     <td>${todo.desc}</td>
	    <td><fmt:formatDate pattern="dd/MM/yyyy"
									value="${todo.targetDate}" /></td>
	     <td>${todo.done}</td>
	     <td>
	       <a href="/update-todo?id=${todo.id}" class="btn btn-success">Update</a>
	       <a href="/delete-todo?id=${todo.id}" class="btn btn-danger">Delete</a>
	     </td>
	   </tr>
      </c:forEach> 
        </tbody>
      </table>
      <div>
         <a class="btn btn-success" href="/add-todo">Add</a>
      </div>
    </div>
    <%@ include file="common/footer.jspf" %>
    
    todo.jsp
    ---
    <%@ include file="common/header.jspf" %>
    <%@ include file="common/navigation.jspf" %>
    <div class="container">
    <h1>Add a Todo!</h1>
    <form:form  method="post" commandName="todo">
    <form:hidden path="id"/>
      <fieldset class="form-group">
      <form:label path="desc">Description</form:label>
	  <form:input path="desc" type="text" class="form-control" required="required"/>
	  <form:errors path="desc" cssClass="text-warning" />
    </fieldset>
    <fieldset class="form-group">
      <form:label path="targetDate">TargetDate</form:label>
	  <form:input path="targetDate" type="text" class="form-control" required="required"/>
	  <form:errors path="targetDate" cssClass="text-warning" />
    </fieldset>
   <input class="btn btn-success" type="submit" value="submit"/>
    </form:form>
    </div>
    <%@ include file="common/footer.jspf"%>
    <script>
	    $('#targetDate').datepicker({
		    format : 'dd/mm/yyyy'
	    });
    </script>
    
welcome.jsp
---
    <%@ include file="common/header.jspf" %>
    <%@ include file="common/navigation.jspf" %>
    <div class="container">
    <spring:message code="welcome.message" />, ${Name}, you are now authenticated.</br>
        Now, you can <a href="/list-todos">manage your to-dos</a>
    </div>
    <%@ include file="common/footer.jspf"%>
