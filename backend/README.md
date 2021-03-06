
# Backend Endpoints

### Authorization using simple jwt token - access and refresh

**Refresh Token not changed**
 * /api/auth/token/ : <!-- login -->
        **Request Type:POST**
        - Takes Email and Password
        - Returns refresh and access Token

 * /api/auth/token/refresh/ :<!-- refresh token -->

        **Request Type:POST**
        - Takes Refresh Token
        - Returns access Token

 * /api/user/ :<!-- signup -->

        **Request Type : GET**

            - Returns all the Users and their creds along with uuid

        **Request Type : POST**

            - Takes Username, Name, Email, Password, Confirm Password, Profile Picture, Bio, Home town
            - Returns the created user instance
 
* /api/user/{uuid} <!-- profile -->

       *Authorization Enabled for non-safe methods*
       **Request Type: GET**
       Returns the specific user creds
       **Request Type: PATCH, DELETE**


## Main Application(tripping) endpoints


### Vendor Details
* /api/vendor/ <!-- Vendors(Places where QR is Installed) -->

       **Request Type: GET**
       - Returns the list of all vendors and its details id,name,location,contact,image,type_of_place,is_sponsor

* /api/vendor/{id} <!-- id is the same id which gets returned when the get request is sent to /api/vendor/ -->

       **Request Type : GET**
              -Returns the specific vendor details as above


### Visit Details
* /api/visit/ <!-- Visit is the field where the the user and the vendor gets interconnected  -->

       **Request Type : GET**

              - Returns the list of all the visits of all the user which is marked as public

**Request Type : POST**


              - Only works when Authenticated user sends request

              - Send {"vendor":"{vendor_id}","public":"true" } in the body as payload if user wants the visit to be public PS: Make public default to be "true"

              - Returns the created visit of an user to the vendor

       Fields: id, user, vendor, content, public, location_score(hidden,read_only)

* /api/public-visit/

       **Request Type : POST**

              
              -H Authorization of User
              -d latitude=
              -d longitude=
              -d public=
              -d content=
              
              - Returns The visited place instances

<br/>

### Leaderboard Details
* /api/leaderbord/ <!-- Global  Leaderboard -->

       **Request Type : GET**
       -Returns the list of users and their scores based on the the total score of their visits and ranks them.
     *fields: user(user_id), visits, unique_visits, username, user_uuid, user_profile_picture, score*

 * /api/following-leaderboard/  

 
       **Request Type : GET**   
       - returns leaderboard of people user follows

### Dashboard/Profile Details
* /api/dashboard/ <!-- Personal Dashboard -->

       **Request Type : GET**
       - Returns 
       ('user','user_uuid','username','user_profile_picture','score','visited_places','score') details when the Authorization Cred. is provided in the header.


### Landing Page Details
* /api/index/

       **Request Type : GET**
       -Returns 'vendors','users','visits' as total number of vendors we have, total users we have and total visits we have

### Search Users
* /api/searchuser/

       **Request Type : GET**
       - takes the data "user" and returns the users ("uuid","first_name","last_name","profile_picture","gender").

# Endpoints for vendors
 * /api/vendor/
 
       * Request Type : post *
       - takes ('username','email','password','confirm_password','name','location','latitude','longitude','image',type_of_place','contact')
       - returns created vendor

* /api/vendor/{vendor_id}
       * request type get *  
       -vendor profile
