---
id: 506
title: MVC. Knowing it, using it.
date: 2013-04-26T10:48:07+00:00
author: Matt Erickson (ME)
layout: post
guid: http://matterickson.me/?p=506
permalink: /mvc-knowing-it-using-it/
categories:
  - Development
  - Java
---
MVC. Model, view, controller. The building blocks of a extensible, reusable, wonderful code base.   

  
**Model:** The data. Does **_NOT_** depend on the controller. Not even a little! It doesn&#8217;t modify the data, it doesn&#8217;t do anything except hold the data in some way shape or form (E.G. hibernate or another ORM to take care of database interaction on the model side)   

  
**View:** Is a bit trickier. The view in a strict MVC is the layer that the user interacts with. It can or can not depend on the controller but should always be independent from the model. In cases where the view depends on the controller the view often is combined with the controller, a lot of android applications will mesh these two layers slightly where the button clicks will get attached in the controller for the activities.   

  
**Controller:** Depends on both model and view, unless of course the view is one in the same with the controller. The controller uses information from the model to send (or display) data to the user and interprets any user interactions that happen.   

  
Moving into the point, that I know I have failed at in the past: 

> The model represents the data, and does nothing else. The model does NOT depend on the controller or the view. Example that is **_WRONG!!!!_**
  


<pre class="brush: java; title: ; notranslate" title="">static class MeController() extends BaseController {
  private static MeView s_view;
}
class Person() extends BaseModel {
  private String m_name;
  public void setName(String name) {
    m_name = name;
    MeController.m_view.refresh(); //THIS IS NOT OK!!!
  }
  public String getName() {
    return m_name;
  }
}
</pre> Proper MVC use of a model: 

<pre class="brush: java; title: ; notranslate" title="">class MeController() extends BaseController {
  private MeView m_view;

  public void DoClickButton(int personIndex, String name) {
    m_view.get(personIndex).setName(name);
    m_view.refresh();
  }
}
class Person() extends BaseModel {
  private String m_name;
  public void setName(String name) {
    m_name = name;
  }
  public String getName() {
    return m_name;
  }
}
</pre> So, here, we see the main difference in this code: the model in the first example tells the controller to refresh the view. Now this model cannot be used by any other class unless every interaction with a person is meant to refresh that one list every time. Not only is the model not reusable for different classes but if we decide to give the user an option to have a grid or a list, which is becoming more and more common in web development and mobile, we cannot because we are attached to the list in the controller by hard coding. 

  

  
So this takes care of re-usability of the model but what about the controller. This is all dependent on using a specific view. If we decide that this version of jQuery is not effective on mobile or what ever the case is we need to find all references to m\_view.refresh(); and change it to (trivial but blocking) m\_view.reload();. This is where separating the view and the controller comes in. If we open up the MeView and add this: 

<pre class="brush: java; title: ; notranslate" title="">class MeController() extends BaseController {
  private MeView m_view;

  public void DoClickButton(Person person, String name) {
    m_view.changeNameButtonClick(person, name);
  }
}

class MeView() extends BaseListView {
  public changeNameButtonClick(Person person, String name) {
    person.setName(name);
    this.refresh();
  }
  private void refresh() {
    //do refresh for this specific view type
  }
}

class Person() extends BaseModel {
  private String m_name;
  public void setName(String name) {
    m_name = name;
  }
  public String getName() {
    return m_name;
  }
}
</pre> It may seem like it is slightly redundant to pass the person around the controller and view but with this setup we can swap in a new view that implements a new technology and don&#8217;t even have to bat an eye at how the controller will react. It will just work. 

  

  
So for the finale, the answer to all of your Pastafarianism problems is MVC. If done correctly you can separate the model from your view and have three distinct layers that can be unit tested, compiled, and swapped in and out with different tech stacks without a huge head ache.   

  
Hopefully this has clarified the struggle for many college CIS/CS majors.   

  
~(ME)