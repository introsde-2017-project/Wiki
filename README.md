# Introsde-project-2017.   

NAME: Cheema Danish Asghar  
EMAIL: danishasghar.cheema@studenti.unitn.it  

Group Partner by:  
NAME: Jan Main muhammad Faheem  
EMAIL: main.jan@unitn.it 

app URL: https://knowyourcity123.herokuapp.com/  

## introduction:  
`KnowYourCity` is an app which is used to suggest different food and movie recommendations to registered users based on there preferences, for recommendations a remote `Recombee` API is used, where we used two different Databases one for Food and another one for Movies In order to save the personal data of a user local `sqlite` DataBase is used. For the Quotes, a Remote Rest API is used which gives a random Quote with author name, each time its called.  
 

## FrontEnd Structure:  
1) A new User can easily Register and use all the services in the app, for registration a user select type of movie and food to select the preferences. username and at least 3 digit password are mandatory, rest of the field is optional.  
2) After successful signup user can login, the home page is consist of 4 tabs as follows.  

| Search | Recommandation | My Ratings | Analysis |
|--------|----------------|------------|----------|
3) In search tab, a user can select food/movie type and get all the Items save in the DB.  
4) Recommendation tab is used to get Recommendation for a user based on preferences.  
5) My Ratings show all the rating added by a user.  
6) The analysis tab shows all the items with the average rating given by different users.  
7) Detail shows the user preferences and other details.  
8) with each refresh a new random quote is displayed on the top of the page.  

## Implementation and Project Structure
As you can see in the diagram below project is consist of different layers, and multiple Rest And Soap based services.  
![alt text](https://github.com/introsde-2017-project/Wiki/blob/master/Diagram1.png)  

### Food Process Centric Layer  
API Documantation: https://documenter.getpostman.com/view/2954866/RWEcNfPB   

This layers is responsible for handling all the request coming from front-end user interface and process/redirect the requests accordingly to lower layers, all the required authentication are handled in this layer for each individual user.  
Each time a user login it gets a unique Bearer token which he has to use for all the further requests in the future.  
All the Signup and login request are handeled by this layer.  

Here is a list of services availabe for Api consumer:  
#### User Resource         
![alt text](https://github.com/introsde-2017-project/documentation/blob/master/User_Resource.png)  

### Movie Process Centric Layer
API Documantation: https://documenter.getpostman.com/view/2954866/RWEcNfmF    

Movie process-centric layer is based on Rest Service which consumes SOAP business service layer and handle all the request related to recombee movie DB, again it checks for authentication for each request. you can check all the Services available in the API documentation.    

### Business Service Layer
API Documantation: https://documenter.getpostman.com/view/2954866/RWEcNfmG    

based on SOAP Service also consumes soap service from a lower layer, handle all the business logic like converting the rating from [-1,1] to [0,5] range and initializing the recombee Database consuming the data from json file.    

here is the list of important services available for the service consumer.  
   * Method #1  `addNewPerson(Person person)`        
   * Method #2  `getPerson(String username)`   
   * Method #3  `getAllPerson()`     
   * Method #4  `getPersonByToken(String token)`      
   * Method #5  `updatePerson(Person person)`      
   * Mthod  #6  `getFoodTypes()`  
   * Method #7  `getMovieGens()`   
   * Method #8  `addNewRating(RecombeeDBType db, Evaluation rating)`  
   * Method #9  `getItemRatings(RecombeeDBType db, String itemName)`   
   * Method #10 `getUserRatings(RecombeeDBType db, Person person)`  
   * Method #11 `getRecommendations(RecombeeDBType db, Person person, int quantity) `  
   * Method #12 `getAllItem(RecombeeDBType db)`  
   * Method #13 `getItemByType(RecombeeDBType db, String itemType)`  
   
   
### Storage Service Layer  
API Documantation: https://documenter.getpostman.com/view/2954866/RWEcNfmJ   
readMe: https://github.com/introsde-2017-project/StorageService#introsde-2017-project-storageservice  

consumes and produce Soap services, takes request from the upper layer in our case business layer and redirect them to locate DataBase or recombee layer accordingly, for example saving a new user, have to save to both layers. for further detail please refer to API Documentation.    

### Local DataBase Layer  
API Documantation: https://documenter.getpostman.com/view/2954866/RWEcNfqZ   
ReadMe: https://github.com/introsde-2017-project/LocalDataService#introsde-2017-project-localdataservice  

Consumes and Produce Soap services, Uses Sqlite database and JPA in order to do all the CRUD operations, or getting all the movie gen and movie types in the DataBase.   
here is the list of services availabe to consumer:  

* `addNewPerson(Person)` it adds new person to the database.        
* `getPerson(username)` it returns person given its username.  
* `getPersonByToken(token)` returns a person.
* `getAllPerson()` return list of persons. used for debug perpose only.
* `updatePerson(Person person)` it updates person.       
* `getFoodTypes()` this method returns food type.      
* `getMovieGens()` this method returns Movie genere.   

### Recombee Adopter Layer
API Documantation: https://documenter.getpostman.com/view/2954866/RWEawhtg 
ReadMe: https://github.com/introsde-2017-project/RecombeeAdapterService#recombee-adopter-layer  

This is an adopter layer for the `knowYourCity` app which uses remote recombee Api for data storage and to get the recombee base recomondations accourding to to given user's pereferences.  
Its is designed for two differnt type of DataBases in our case it is designed for food and movie DB, but all the mehthods are reusable and can easily be extended just by adding a new attribute in anum class `RecombeeDBType.java` and saving the DB credentials in the `RecombeeImpl.java` constructor.  
Its a Soap Service which can be used via WSDL in order to save, modify, and get data like persisting new user or rating for specific food/movie by a user.  

* List of Services for client:  
  * `addUser(RecombeeDBType, userId, ListOfPreferences)`  
  -> DBType can be RecombeeFood/RecombeeMovie and preferences can be list of FoodTypes/MovieGenres.  
  * `addNewRating(RecombeeDBType, Evaluation )`  
  -> add new rating to given recombee DB. Evaluation Object contains all the required data, check the POJO class above.  
  * `getUserRatings(RecombeeDBType, userId)` 
  -> returns all the ratings given by a user identified by userId. 
  * `getRecommendations(RecombeeDBType, userId, quantity)`  
  -> get the recommendations from recombee and returns a list of ItemObject.     
  * `getItemsByType(RecombeeDBType ,ItemType)`  
  -> this method returns list of itemObject by given its type.     
  * `getAllItem(RecombeeDBType)`  
  -> it returns the list of all the items given its DBtype.    
  * `getItemRatings(RecombeeDBType, itemId)`  
  -> this method returns the list of all the ratings of the item.  
  * `initDB(RecombeeDBType)`  
  -> call `inti.java` class and initialize data to Recombee DB by it given movieDB/foodDB type.



