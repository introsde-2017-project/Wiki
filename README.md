## Description.   
# Basic idea.    
The general idea of my project is a user  comes on my app, gets registered and then he/she select from movie and from food and hit     enter.these are the services which are my business services and these services are declared in business interface and implemented by      a class and made  it accessable through soap service.     
# Implementation  
 There is the user interface which has a form ,the user comes fill the form for the registration in order to be able to select items my   app offering. he then chose items i.e he choses food and movie. these are the soap services which are granted through the business   layer.  the business layer then communicate with the local database. and on the base of the selection the recombee server then recommend items   to the user. as given in the diagram.  

![alt text](https://github.com/introsde-2017-project/Wiki/blob/master/Diagram1.png)

### Food Resource  
# Implementation    
 When a user chooses a food item he is able to evaluate the item as well so he makes his rating about the item through the function     
 `addFoodRatings()`. this user is then added to the local database and also to the recombee database .after the item got selected the     recombee server recommends a few items to the user on the basis of his selection.the user can even see all the ratings given to the     specific item in past through the function `getfoodRatings()`. The overall scenario is given in the following diagrame.   
![alt text](https://github.com/introsde-2017-project/documentation/blob/master/Food_Resource.png)

### User Resource
![alt text](https://github.com/introsde-2017-project/documentation/blob/master/User_Resource.png)
