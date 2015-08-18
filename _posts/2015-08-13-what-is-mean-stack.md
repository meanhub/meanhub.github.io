---
layout: post
title: What is a MEAN Stack?
published: true
author: ashish
---

MEAN stack is a popular acronym for an amalgamation of several key JavaScript technologies for building modern single page web applications. It is similar to another popular stack for building web applications [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) or it's Windows based cousin [WAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)#WAMP).

MEAN stack technologies and their key features are as below

**_M_** stands for *[MongoDB](https://www.mongodb.org/)*, a NoSQL _database_ for storing your application data. It is known for high performance, high availability and automatic scaling

**_E_** stands for *[ExpressJS](http://expressjs.com/)*, a light weight and un-opinioted _web framework_ for building your web application backend. It is built on Node.js platform. It provides robust set of http utility methods & middle-wares for common web application operations

**_A_** stands for *[AngularJS](https://angularjs.org/)*, a _JavaScript MVC framework_ for building your web application UI. It provides two-way data-binding, dependency injection and excellent unit & end-to-end test support

**_N_** stands for *[NodeJS](https://nodejs.org/)*, a _platform_ for executing your backend code on your servers. It is built on Google Chrome browser's JavaScript engine and allows building fast and scalable network applications. It employs an event driven, non-blocking I/O model that makes it lightweight and efficient.

If you want to visualize MEAN stack, it would look something like this

<img src="/public/images/mean.png">

But how do these technologies map to the actual web application? Let's explore that via an example. Let's say you are building a Contacts Manager application that provides CRUD operations to manages your contacts.

Now in a MEAN stack, you would store data in MongoDB database. MongoDB is a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) database and it stores data in BSON format (similar to JSON in JavaScript) and your list of contacts could be represented as a collection of Contact documents. Each Contact document in MongoDB would look something like shown below

{% highlight javascript %}
{
  "first_name" : "Tony",
  "last_name" : "Stark",
  "mobile": 5,
  "email": "tony@stark.com"
}
{% endhighlight %}

If you are coming from relation databases background, a _collection_ in MongoDB is analogous to a table and a _document_ is analogous to a single record in that table.

Typically in a MEAN application, your backend serves or operates on data in response to an http request such as GET or POST. For example to show the list of Contacts, you would have a backend API route setup to fetch Contact documents from MongoDB and send them back as http response.

{% highlight javascript %}
router.get('/contacts', function (req, res, next) {
  // fetch Contact documents from MongoDB
  res.json(contacts); // send a JSON array of Contact documents as a response
});
{% endhighlight %}

On client-side you would have a view template to display data and have an Angular Controller to bind data in this view. For example for showing list of Contacts you would have a template as shown below

{% highlight html %}
<ul ng-controller="ContactsController as contactsCtrl">
  <li ng-repeat="contact in contactsCtrl.contacts">
    First Name: {{ contact.first_name }}
    Last Name: {{ contact.last_name }}
  </li>
</ul>
{% endhighlight %}

Ignore the specifics for the moment. The key thing to understand about view templates is that typically data is retrieved by an Angular Controller and filled in inside a template. In above code <code>contactCtrl</code> retrieves list of contacts via GET http request (which is then received and processed by backend code you saw earlier) and creates <code>li</code> elements by iterating over list of contacts it received from backend.

Here is the Angular code that retrieves list of contacts from backend.

{% highlight javascript %}

app.controller('ContactsController', function($http) {
  var contactsCtrl = this;
  $http.get('/contacts').success(function(contacts) {
      contactsCtrl.contacts = contacts;
    });
});

{% endhighlight %}

Once again, if you want to visualize how the data flows between client and server here is how it would look like as shown below

<img src="/public/images/mean_flow.png">

In the coming blogposts we will take an in-depth look at MEAN stack technologies with examples. Stay tuned.
