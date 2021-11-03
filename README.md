## Games guide project

### Firestore database rules

Addind a reference here in the readme instead of always having to go to firebase to get this. Copy and paste this and modify as needed in subsequent projects:

````
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    //match /{document=**} {
      //allow read, write: if
          //request.time < timestamp.date(2021, 11, 30);
    //}
    
    //match logged in user doc in users collection: allow the user to create if logged in, allow the user to read only his/her own data
    match /users/{userId} {
    	allow create: if request.auth.uid != null;
      allow read: if request.auth.uid == userId;
    }
    
    //match docs in the guides collection, and allow access if user exists
    match /guides/{guideId} {
    	allow read, write: if request.auth.uid != null;
    }
  }
}
````

### Custom claims and cloud functions

Commands from [Tutorial #17 - Intro to custom claims](https://www.youtube.com/watch?v=SSiLsIkPQWs&list=PL4cUxeGkcC9jUPIes_B8vRjn1_GaplOPQ&index=17) to be able to use firebase cloud functions:

Install firebase tools if you haven't:
````
npm i -g firebase-tools
````

Login to firebase accout if you haven't:
````
firebase login
````

Install firebase cloud functions (folder and files) in your project:
````
firebase init functions
````