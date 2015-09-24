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

for example:

<code>
 <h:selectOnMenu value="#{form.country}" onchange="submit()"
  valueChangeListener="#{form.countryChanged}">
   <f:selectItems value="#{form.countries}" var="loc"
    itemLabel="#{loc.displayCountry}" itemValue="#{loc.country}"/>
 </h:selectOneMenu>
 </code>
 
 Here, #{form.countries} is bound to an array of Local objects.











