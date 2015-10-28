# JavaServerFacesTheGoodParts

We will not focus on a special JSF implementation.

Java Server Faces - Using an External Renderer

- Just like every component has an ID called the compnent type, every renderer has an ID called the renderer type.

How to deal with a GET-Request in JSF before version 2.0

 - JSF is in the critic for not allowing GET-requests.
   That's not correct in this way. Well maybe before version 2.0.

The JSF Life Cycle and Ajax:

JSF 2.0 splits the JSF life cycle into two parts: 

1. execute (components are executed)
2. render

Custom Components:

1. Saving and Restoring State

The JSF implementation saves and restores the view state between requests.

<code>public Object saveState(FacesContext context)</code>

2. Using Managed Beans and Stateless Session Beans

A stateless session bean is annoted with @Stateless. You inject an entity manager and simply use it, without 
declaring any transactions:

<code>
 @Stateless
 public class CredentialManager {
  @PersistenceContext(unitName="default")
  private EntityManager em;
  
  public int checkCredentials(String name, String password) {
   Query query  = em.createQuery(...).setParameter("username", name);
  }
 }
</code>

RESTful Navigation and Bookmarkable URLs
========================================

By default, a JSF application makes a sequence of POST requests to the server.

Each POST contains form data. This makes sense for an application that collects lots of user input. But much of the web doesn't work like that. 

An architectural style called REST advocates that web applications should use HTTP as it was originally envisioned. Lookups should use GET requests. PUT, POST and DELETE requests should be used for creation, mutation and deletion.

Event Handling
==============

Events and the JSF Life Cycle
Value Change Events
Action Events
Event Listener Tags
 f:actionListener and f:valueChangeListener
 Tags
Immediate Components
Passing Data from the UI to the Server
Phase Events
System Events

ad 1)

Requests in JSF applications are processed by the JSF implementation with a controller servlet, which in turn executes the JSF life cycle. 

Starting with the Apply Request Value phase, the JSF implementation may create events and add them to an event queue during each life cycle phase. After those phases, the JSF implementation broadcasts queued events to registered listeners.

ad 2)

Components in a web application often depend on each other ( yes, they do :-) ). 

Like all value change listeners, the preceding listener is passed a value change event. The listener uses that event to access the component's new value.

That form submit is crucial because the JSF implementation handles all events on the server.

ad 3)

Action events are fired by buttons and links. 

Command components submit requests when they are activated, so there is no need to use onchange to force submits as we did with value change events in "Value Change Events". 

It's important to distinguish between action listener and actions. In a nutshell, actions are designed fur business logic and participate in navigation handling.

Ajax and JSF

Conceptually, Ajax is simple. In fact, Ajax requests differ from regular HTTP requests in only two ways:

1. Ajax partially processes forms on the server during the Ajax call.
2. Ajax partially renders DOM elements on the client after the Ajax call returns from the server.

Problems with JSF execute and render
====================================

You can use render="@this" for rendering particular parts of your page.
You can use render="@form" for rendering the whole form focussed on.
You can use render="@all" for rendering the whole view in the underlaying container.

What exactly is seam weld:
==========================

Well it's just shifting the CDI reference implementation to Tomcat, or what do you think ?

Managed Beans
=============

A central theme of web application design is the seperation of presentation and business logic.

JSF uses beans to achieve this seperation. JSF pages refer to bean properties, and th program logic is contained in the
bean implementation code. Because beans are so fundamental to JSF programming, we discuss them in detail here.

Different bean scopes:
======================

@RequestScoped
@ViewScoped
@FlowScoped
@SessionScoped
@ApplicationScoped

A @RequestScoped bean lives as long as a single HTTP request-response cycle (note that an Ajax request counts as a single HTTP request too). A @ViewScoped bean lives as long as you're interacting with the same JSF view by postbacks which call action methods returning null/void without any navigation/redirect. A @FlowScoped bean lives as long as you're navigating through the specified collection of views registered in the flow configuration file. A @SessionScoped bean lives as long as the established HTTP session. An @ApplicationScoped bean lives as long as the web application runs.


 















