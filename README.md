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







