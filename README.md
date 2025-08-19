# User-Management-System
JSP and Servlet POC (Java, Maven, Spring boot)

in the jsp project explain in brief every concept of jsp and serve servlet

claude-v4.0-sonnet
JSP & Servlet Concepts - Brief Explanation
1. SERVLET CONCEPTS
1.1 What is a Servlet?
Server-side Java class that handles HTTP requests and generates responses
Runs in servlet container (like Tomcat)
Platform independent and protocol independent

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        // Handle GET request
    }
}
1.2 Servlet Lifecycle

public class LifecycleServlet extends HttpServlet {
    public void init() { /* Called once when servlet loads */ }
    public void service() { /* Called for each request */ }
    public void destroy() { /* Called when servlet unloads */ }
}
1.3 HTTP Methods

protected void doGet(HttpServletRequest req, HttpServletResponse resp) { }    // GET
protected void doPost(HttpServletRequest req, HttpServletResponse resp) { }   // POST
protected void doPut(HttpServletRequest req, HttpServletResponse resp) { }    // PUT
protected void doDelete(HttpServletRequest req, HttpServletResponse resp) { } // DELETE
1.4 Request Handling

// Reading parameters
String name = request.getParameter("name");
String[] hobbies = request.getParameterValues("hobbies");

// Reading headers
String userAgent = request.getHeader("User-Agent");

// Request attributes
request.setAttribute("message", "Hello");
1.5 Response Generation

// Set response type
response.setContentType("text/html");

// Write response
PrintWriter out = response.getWriter();
out.println("<h1>Hello World</h1>");

// Redirect
response.sendRedirect("/login.jsp");
1.6 Session Management

HttpSession session = request.getSession();
session.setAttribute("user", "john");           // Store
String user = (String) session.getAttribute("user"); // Retrieve
session.invalidate();                           // Destroy
1.7 Cookie Handling

// Create cookie
Cookie cookie = new Cookie("username", "john");
cookie.setMaxAge(3600); // 1 hour
response.addCookie(cookie);

// Read cookies
Cookie[] cookies = request.getCookies();
2. JSP CONCEPTS
2.1 What is JSP?
Java Server Pages - HTML with embedded Java code
Compiled to servlet by container
Separates presentation from logic
2.2 JSP Elements
Scriptlets - Java code blocks

<%
    String name = "John";
    int age = 25;
%>
Expressions - Output values

<h1>Hello <%= name %></h1>
<p>Age: <%= age %></p>
Declarations - Methods and variables

<%!
    private int counter = 0;
    public String getMessage() {
        return "Hello World";
    }
%>
Comments

<%-- JSP Comment (server-side) --%>
<!-- HTML Comment (client-side) -->
2.3 JSP Directives
Page Directive - Page configuration

<%@ page language="java" contentType="text/html" pageEncoding="UTF-8" 
         import="java.util.*" session="true" errorPage="error.jsp" %>
Include Directive - Static include

<%@ include file="header.jsp" %>
Taglib Directive - Tag libraries

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
2.4 JSP Implicit Objects

<%
    request     // HttpServletRequest
    response    // HttpServletResponse  
    session     // HttpSession
    application // ServletContext
    out         // JspWriter
    config      // ServletConfig
    pageContext // PageContext
    page        // Current JSP instance
    exception   // Throwable (error pages only)
%>
2.5 JSP Scopes

<%
    pageContext.setAttribute("var", "value", PageContext.PAGE_SCOPE);     // Page
    request.setAttribute("var", "value");                                 // Request
    session.setAttribute("var", "value");                                 // Session
    application.setAttribute("var", "value");                             // Application
%>
2.6 JSP Actions
Standard Actions

<jsp:forward page="welcome.jsp" />                    <!-- Forward -->
<jsp:include page="menu.jsp" />                       <!-- Include -->
<jsp:useBean id="user" class="User" scope="session"/> <!-- JavaBean -->
<jsp:setProperty name="user" property="name" value="John" />
<jsp:getProperty name="user" property="name" />
2.7 JSTL (JSP Standard Tag Library)
Core Tags

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!-- Variables -->
<c:set var="name" value="John" />
<c:out value="${name}" />

<!-- Conditionals -->
<c:if test="${age >= 18}">Adult</c:if>

<c:choose>
    <c:when test="${age < 18}">Minor</c:when>
    <c:otherwise>Adult</c:otherwise>
</c:choose>

<!-- Loops -->
<c:forEach items="${users}" var="user">
    <p>${user.name}</p>
</c:forEach>
Formatting Tags

<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

<fmt:formatDate value="${date}" pattern="yyyy-MM-dd" />
<fmt:formatNumber value="${price}" type="currency" />
2.8 Expression Language (EL)

${user.name}              <!-- Property access -->
${users[0].email}         <!-- Array/List access -->
${sessionScope.user}      <!-- Scope access -->
${param.username}         <!-- Request parameter -->
${header['User-Agent']}   <!-- Request header -->

<!-- Operators -->
${age > 18 ? 'Adult' : 'Minor'}    <!-- Ternary -->
${empty users}                     <!-- Empty check -->
${user.name eq 'John'}             <!-- Equality -->
2.9 Error Handling

<!-- Error page -->
<%@ page isErrorPage="true" %>
<h1>Error: ${exception.message}</h1>

<!-- Page with error handling -->
<%@ page errorPage="error.jsp" %>
