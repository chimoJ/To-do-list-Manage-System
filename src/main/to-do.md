all classes related with to-do function
===
Todo.java
---
    package com.in28minutes.todo;
    import javax.validation.constraints.Size;
    import java.util.Date;

    public class Todo{
    	private int id;
    private String user;
    @Size(min=6, message="Enter at least 6 Characters")
    private String desc;
    private Date targetDate;
    private boolean isDone;
    public Todo() {
    	super();
    }
    public Todo(int id, String user, String desc, Date targetDate, boolean isDone) {
		super();
		this.id = id;
		this.user = user;
		this.desc = desc;
		this.targetDate = targetDate;
		this.isDone = isDone;
	  }
	  public int getId() {
		return id;
	  }
	  public void setId(int id) {
		this.id = id;
	  }
	  public String getUser() {
		return user;
	  }
	  public void setUser(String user) {
		this.user = user;
	  }
	  public String getDesc() {
		return desc;
	  }
	  public void setDesc(String desc) {
		this.desc = desc;
	  }
	  public Date getTargetDate() {
		return targetDate;
	  }
	  public void setTargetDate(Date targetDate) {
		this.targetDate = targetDate;
	  }
	  public boolean isDone() {
		return isDone;
	  }
	  public void setDone(boolean isDone) {
		this.isDone = isDone;
	  }
	
	  public String toString() {
		return String.format("To Strnig Todo [id=%s, user=%s, desc=%s, targetDate=%s, isDone=%s]", id, user, desc, targetDate,
				isDone);
	  }
	  @Override
	  public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + id;
		return result;
	  }
	  @Override
	  public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Todo other = (Todo) obj;
		if (id != other.id)
			return false;
		return true;
	  }
    
    }

TodoController.java
---
    package com.in28minutes.todo;

    import java.text.SimpleDateFormat;
    import java.util.Date;

    import javax.enterprise.inject.Model;
    import javax.servlet.http.HttpServletRequest;
    import javax.validation.Valid;
    import org.apache.commons.logging.Log;
    import org.apache.commons.logging.LogFactory;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.propertyeditors.CustomDateEditor;
    import org.springframework.security.core.context.SecurityContextHolder;
    import org.springframework.security.core.userdetails.UserDetails;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.validation.BindingResult;
    import org.springframework.web.bind.WebDataBinder;
    import org.springframework.web.bind.annotation.ExceptionHandler;
    import org.springframework.web.bind.annotation.InitBinder;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.SessionAttributes;

    import com.in28minutes.exception.ExceptionController;

    //import org.springframework.web.bind.annotation.ResponseBody;

    @Controller
    @SessionAttributes("Name")
    public class TodoController {
	  //set the login service- auto Wiring
	  //private Log logger=LogFactory.getLog(ExceptionController.class);
	  @Autowired
	  TodoService service;
	  @InitBinder
	  protected void initBinder(WebDataBinder binder) {
		SimpleDateFormat dateFormat=new SimpleDateFormat("dd/MM/yyyy");
		binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));
	  }
	  //only support get method
	  @RequestMapping(value="/list-todos", method=RequestMethod.GET)
    public String listTodos(ModelMap model) {
		model.addAttribute("todos", service.retrieveTodos(retrieveLoggedinUserName()));
	   return "list-todos";
    }
	  private String retrieveLoggedinUserName() {
		Object principal = SecurityContextHolder.getContext()
				.getAuthentication().getPrincipal();
		if (principal instanceof UserDetails)
			return ((UserDetails) principal).getUsername();//get username
		return principal.toString();//return priciple
	  }
	   @RequestMapping(value="/add-todo", method=RequestMethod.GET)
	   public String showTodoPage(ModelMap model) {
		       //throw new RuntimeException("DummyException");
			   model.addAttribute("todo", new Todo(0,retrieveLoggedinUserName(),"Default Desc",new Date(),false));
			   return "todo";
	   }
	   @RequestMapping(value="/add-todo", method=RequestMethod.POST)
	   public String addTodo(ModelMap model,@Valid Todo todo, BindingResult result) {
		   if(result.hasErrors()) {
			   return "todo";
		   }
		   service.addTodo(retrieveLoggedinUserName(), todo.getDesc(), new Date(), false);
		   model.clear();//not pass the session parameter into list-todos
		   return "redirect:list-todos";
	   }
	    //update todo
		  @RequestMapping(value="/update-todo", method=RequestMethod.GET)
		   public String updateTodo(ModelMap model, @RequestParam int id) {
			   Todo todo=service.retrieveTodo(id);
			   model.addAttribute("todo", todo);
			   //model.clear();//not pass the session parameter into list-todos
			   return "todo";
		   }
		
		  @RequestMapping(value = "/update-todo", method = RequestMethod.POST)
		  public String updateTodo(ModelMap model, @Valid Todo todo,
				BindingResult result) {
			if (result.hasErrors())
				return "todo";

			todo.setUser(retrieveLoggedinUserName()); //TODO:Remove Hardcoding Later
			service.updateTodo(todo);

			model.clear();// to prevent request parameter "name" to be passed
			return "redirect:/list-todos";
		  }
	    @RequestMapping(value="/delete-todo", method=RequestMethod.GET)
	    public String deleteTodo(ModelMap model, @RequestParam int id) {
		   service.deleteTodo(id);
		   model.clear();//not pass the session parameter into list-todos
		   return "redirect:list-todos";
	     }
	    /*
	    @ExceptionHandler(value=Exception.class)//handle everything
	    public String handleException(HttpServletRequest request, Exception ex) {
		   logger.error("request"+request.getRequestURL()+"Threw an Exception", ex);
		   return "error-specific";
	    }*/
      }

TodoRestController.java
---
    package com.in28minutes.todo;

    import java.util.*;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class TodoRestController {
    @Autowired
    TodoService service;
    @RequestMapping(path="/todos")
    public List<Todo> retreiveAllTodos(){
	   return service.retrieveTodos("in28Minutes");
    }
    @RequestMapping(path="/todos/{id}")
    public Todo retreivTodo(@PathVariable int id){
	   return service.retrieveTodo(id);
    }
    }
TodoService.java
---
    package com.in28minutes.todo;
    import java.util.*;
    import org.springframework.stereotype.Service;
    @Service
    public class TodoService {
	  private static List<Todo> todos = new ArrayList<Todo>();
	  private static int todoCount = 3;

	  static {
		todos.add(new Todo(1, "in28Minutes", "Learn Spring MVC", new Date(),
				false));
		todos.add(new Todo(2, "in28Minutes", "Learn Struts", new Date(), false));
		todos.add(new Todo(3, "in28Minutes", "Learn Hibernate", new Date(),
				false));
	  }
    //retrieve all to-do items put inside to-do list
	  public List<Todo> retrieveTodos(String user) {
		List<Todo> filteredTodos = new ArrayList<Todo>();
		for (Todo todo : todos) {
			if (todo.getUser().equals(user))
				filteredTodos.add(todo);
		}
		return filteredTodos;
	  }
    //add new to-do item
	  public void addTodo(String name, String desc, Date targetDate, boolean isDone) {
		todos.add(new Todo(++todoCount, name, desc, targetDate, isDone));
	  }
    //delete  to-do item user want to delete
	  public void deleteTodo(int id) {
		Iterator<Todo> iterator = todos.iterator();
		while (iterator.hasNext()) {
			Todo todo = iterator.next();
			if (todo.getId() == id) {
				iterator.remove();
			  }
		  }
	  }
	  public Todo retrieveTodo(int id) {
		for (Todo todo : todos) {
			if (todo.getId() == id)
				return todo;
		}
		return null;
	  }
	  public void updateTodo(Todo todo) {
		todos.remove(todo);
		todos.add(todo);
	  }
    }
