---
id: 299
title: Hibernate Parameter Binding
date: 2013-01-08T09:43:51+00:00
author: Matt Erickson (ME)
layout: post
guid: http://matterickson.me/?p=299
permalink: /hibernate-parameter-binding/
categories:
  - Java
  - Web
---
So, recently, I undertook the task of writing a quick project. From the ground up. I decided on a tech stack that I was familiar with and fit the criteria that was set forth by the project; struts2, hibernate, maven, java. Setup was fairly simple due to my knowledge of maven, but that is not what you are here to learn. 

## Hibernate So the first thing I did was setup a HibernateUtils class to ensure I always had an open session to access the database. 


  
**Note:** this class is fairly easy to find with a google search. 

<pre class="brush: java; title: ; notranslate" title="">public class HibernateUtils {

  private static final SessionFactory s_sessionFactory = buildSessionFactory();

  /**
   * Builds a hibernate session factory for interacting with the db
   * @return the session factory
   */
  private static SessionFactory buildSessionFactory() {
    try {
      // Create the SessionFactory from hibernate.cfg.xml
      return new Configuration().configure().buildSessionFactory();
    } catch (Throwable ex) {
      // Make sure you log the exception, as it might be swallowed
      System.err.println("Initial SessionFactory creation failed." + ex);
      throw new ExceptionInInitializerError(ex);
    }
  }

  /**
   * @return
   */
  public static SessionFactory getSessionFactory() {
    return s_sessionFactory;
  }
</pre>


  
Now is the part you were waiting for, **parameters**. 
  
So lets say I have a list of objects with names in my DB. I want object with name &#8220;world&#8221;. The **_<u>INCORRECT</strong>_</u> would be as follows:
  
THIS IS WRONG!!!! 

<pre class="brush: java; title: ; notranslate" title="">Session session = null;
session = HibernateUtils.getSessionFactory().openSession();
session.beginTransaction();
String hqlQuery = "FROM " + MyObject.class.getName() + " obj WHERE obj.name = '" + name + "'";
List&lt;MyObject&gt; returnedObjects = 
  (List&lt;MyObject&gt;) session.createQuery(hqlQuery).list();
</pre> THIS IS WRONG!!!! 

  

  
Clearly this is wrong, we should NEVER use any input possibility as a parameter in a query directly. We could have all sorts of funky characters that could break our query (e.g. *, &#8216;, &#8220;, &, ;, etc.). So what ever will we do? Simple, we use it as the built in setParameter in hibernate! 

<pre class="brush: java; title: ; notranslate" title="">Session session = null;
session = HibernateUtils.getSessionFactory().openSession();
session.beginTransaction();
String hqlQuery = "FROM " + MyObject.class.getName() + " obj WHERE obj.name = :name";
List&lt;MyObject&gt; returnedObjects = 
  (List&lt;MyObject&gt;) session.createQuery(hqlQuery).setParameter("name", name).list();
</pre> This is just one example of how to use this parameter setup, there are several more. We can explicitly tell hibernate what type we have like this: 

<pre class="brush: java; title: ; notranslate" title="">List&lt;MyObject&gt; returnedObjects = 
  (List&lt;MyObject&gt;) session.createQuery(hqlQuery).setString("name", name).list();
</pre> We can also have multiple parameters like if we want all active objects with name &#8220;world&#8221; (indexed by 0): 

<pre class="brush: java; title: ; notranslate" title="">String hqlQuery = "FROM " + MyObject.class.getName() + " obj WHERE obj.name = ? and obj.active = ?";
List&lt;MyObject&gt; returnedObjects = 
  (List&lt;MyObject&gt;) session.createQuery(hqlQuery).setParameter(0, name).setParameter(1, true).list();
</pre> Even better, we can use objects to match! This is extremely useful if you have a large object with many parameters being set. 

<pre class="brush: java; title: ; notranslate" title="">MyObject searchObject = new MyObject();
searchObject.setName("world");
searchObject.setActive(true);
searchObject.setSomeOtherAttribute("value");
String hqlQuery = "FROM " + MyObject.class.getName() +
  " obj WHERE obj.name = :searchObj and obj.active = :searchObj";
List&lt;MyObject&gt; returnedObjects = 
  (List&lt;MyObject&gt;) session.createQuery(hqlQuery).setParameter("searchObj", searchObject).list();
</pre>


  
Needless to say, you should always choose some type of parametrization when writing HQL. I prefer **Name Parameters** (the :theValue) for clarity and ease of use.