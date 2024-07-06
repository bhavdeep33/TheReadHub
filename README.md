# The Read-hub

The Read Hub is a full-featured public library website project which is currently under development. Some functionalities are implemented, overview of same is given below:

# Project structure:
## Libraries:
### APIDBLib:
- Creates and manage connection pool.
- Provides connection from connection pool for database operation when required.
- Automatically adds and removes connections if necessary.

### APIBase:
- Creates and initializes API listener as per configuration of ini file
- Handles different kind of requests like GET,POST,PUT,DELETE and call appropriate API function.
- Provides functionality to send OK and Fault reply to client.
- Provides other functionalities which can used by different APIs for ex. string encryption, decryption etc.
- APIErrorCodes.h file contains base fault codes which can be used by different APIs.

## Listeners:
Listeners are actual APIs which can be called to perform required operation.
### User API:
- Provides API endpoints for user related functionalities like registering new user, changing and reseting password, viewing and modifying profile, visiting other user's profile, delete account etc.
  
# Current implementation:

Currently below API endpoints are implimented:

## Initialize user registration:
```bash
GET : /User/registration/init
```
### Description:
Check if specified userid is taken by another user or not and if userid is available, registration token is issued to client for further registration process.

### Query Parameters:
#### User id:
- Parameter: userId<br>
- Type: string<br>
- Required: Yes

### Response:
On success:
```{'Success': '{"registrationToken":"bba811b92c7b7d124085b828e874baf6"}'}```

On failure: 
```{'fault': {'code': intcode, 'description': 'string fault desc.', 'message': 'string fault message'}}```


## Post registration details and get OTP:
```bash
POST : /User/registration/details
```
### Description:
Validates the registration token first and send onetimetoken on user's email id for registration. 

### Header Parameters:
#### Registration token:
- Parameter: registrationToken<br>
- Type: string<br>
- Required: Yes

### Request body:
{
  "username" : string, <br>
  "userId" : string, <br>
  "emailId" : string, <br>
  "password" : string, <br>
  "birthDate" : string, <br>
  "about" : string, <br>
  "profilePic" : base64 encoded string 
}

### Response:
On success:
```{'Success': '{"message":"OTP has been sent to the email id provided"}'}```

On failure: 
```{'fault': {'code': intcode, 'description': 'string fault desc.', 'message': 'string fault message'}}```

## Enter OTP recieved and complete registration:
```bash
POST : /User/registration/onetimetoken
```
### Description:
Validates entered Onetimetoken and registers user.

### Header Parameters:
#### One time token:
- Parameter: oneTimeToken<br>
- Type: string<br>
- Required: Yes

### Response:
On success:
```{'Success': '{"sessionToken":"bbas1fb92g7b75124085b828e874baf6"}'}```<br>
**Note: Currently providing session token as response is not implemented yet, instead we are giving successul message as response.**

On failure: 
```{'fault': {'code': intcode, 'description': 'string fault desc.', 'message': 'string fault message'}}```


# To be Implemented:

Below functionalities are still remaining to be implemented:
- User should be able to login into their account
- Users should be able to logout from their account
- Users should be able to delete account with/without deleting their published books
- User should be able to read books
- User should be able to publish their books
- User should be able to rate books
- Users should be able to search the books from book name or author name
- Users should be able to create multiple bookmarks
- Users should be able to add books to specific bookmark
- Users should be able to rearrange the bookmark
- User should be able to view their profile
- Users should be able to view other users profile
- Users should be able to modify their profile
- Users should be able to change their password
- Users should be able to reset the password by forgot password
