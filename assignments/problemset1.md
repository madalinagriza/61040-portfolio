# Exercise 1
## Questions
-  **Invariants:** 
    - Every item purchased has to be an item requested; 
    - For request each item, count unpurchased + sum of counts purchased = Sum of total item counts requested.
    
    The more complex invariant is #1; the purchase action depends most on it as it requires the item to exist & have a count 
- **Fixing an action:** 
    
    removeItem makes for 'orphaned' purchases. To fix, either:
    - only allow for the item to be removed if there are no purchases prior;
    - refund & notify people who purchased and delete the purchase
- **Inferring behavior:**
    
    If the registry must go through a major update/restructure, owners might want to make the registry inactive (to prevent purchases in the meantime) and activate it after it's done.
- **Registry deletion** 
    
     Not really. If there's privacy concerns, we can add an archive method to 'clean up' the space without having to guarantee deletion of records
- **Queries**  
  - **Owner:** `purchases(registry)` :\
   list of (item, purchaser, count).  
    Lets the registry owner see who bought what, matching the principle that after closing they can view purchases.  
  - **Giver:** `availableItems(registry)` :\
    list of (item, remaining count).  
    Shows which items are still available while the registry is active, so givers can decide what to buy.

    
- **Hiding purchases**
    
    Introduce a 'visible' flag in each purchase, and the action signature would be purchase (purchaser: User, registry: Registry, item: Item, count: Number, visible: boolean)

- **Generic types**

    Having items be standardized SKU codes:  
    - eliminates ambiguity in the type of products the users might want. If an owner underspecifies a product, they might be unhappy with the purchases other people are making.
    - makes it easy to execute the purchase, with additional searches from the users. 

# Exercise 2

## Full concept state
**concept** PasswordAuthentication
  
**purpose** limit access to known users


**principle** after a user registers with a username and a password,
they can authenticate with that same username and password
and be treated each time as the same user

**state**
> a set of Users with 
>> a username String\
>> a password String\
>> a status of PENDING or REGISTERED\
>> an optional pendingToken string


**actions**
> register (username: String, password: String): (user: User, pendingToken: Token)
>> *requires:*\
username doesn't match any existing user's \
 *effects:*\
creates a user with username and password, status PENDING, and a generated pendingToken\
adds the user to users in the state

> confirm (username: String, pendingToken: Token) 
>> *requires:*\
existing username in users, pendingToken corresponds to found user\
user's status is PENDING\
 *effects:*\
changes status from PENDING to REGISTERED\
removes the pendingToken

> authenticate (username: String, password: String): (user: User)
>>   *requires:*\
there exists a user matching username and password\
the user's status is REGISTERED\
*effect:*\
returns found user

> changePassword(user: User, newPassword: String)
>> *requires:*\
user exists\
>> *effects:*\
changes user's password to newPassword

> deleteUser(user: User)
>> *requires:*\
user exists\
>> *effects:*\
deletes user from users

**Invariant** 
- There is at most one user for a given username string
- (after addition of email confirmation) pendingToken has a value only when user's status is PENDING

# Exercise 3
**concept** PersonalAccessTokenAuthentication[User]
  
**purpose** allow users to authenticate 

**principle** after a user creates one or more personal access tokens, they can authenticate with any of those tokens and be treated each time as the same user

**state**
> a set of Users with 
>> a username String\
>> a tokens set of Strings

  **actions**
> createToken (user: User) : (token: String)
>> *requires:*\
 *effects:*\
creates a token string for the user, add it to user's tokens and returns it

> deleteToken (user: User, token: String) 
>> *requires:*\
token is part of user's tokens\
*effects:*\
removes token from user's tokens


> authenticate (username: String, token: String) : (user: User)
>>   *requires:*\
user with username exists and token is part of user's tokens\
*effects:*\
returns that user


**Difference:** a user can hold multiple tokens, can grant tokens different accessibilities, and the tokens can independently be created or deleted.

# Exercise 4

## URL Shortener

**concept** URLShortener[User]
  
**purpose** alias a long URL with a short and readable link

**principle** with an existing URL, the owner creates a short link that redirects to it; anyone can use the short link to be redirected to the original URL

**state**
>  a set of ShortLinks with
>> an owner User\
>> an originalLink String\
>> an alias String
>> 
  **actions**
>  createShortLink (owner: User, originalLink: String, [customAlias]: optional String) : (shortLink: String)
>> *requires:*\
originalLink is a valid link\
customAlias (if provided) isn't already used in a ShortLink
\
*effects:*\
creates a new ShortLink with owner and given alias (customAlias if provided, otherwise a fresh unique alias), and originalLink and returns it

> deleteShortLink (owner: User, alias: String) 
>> *requires:*\
a ShortLink with this alias exists and its owner = owner\
*effects:*\
removes ShortLink from the state

> redirect (alias: String) : (originalLink: String)
>> *requires:*\
a ShortLink with this alias exists\
*effects:*\
returns OriginalLink

**Invariants**
- No ShortLink have the same alias
- Each alias maps exactly to one OriginalLink 

## Billable Hours Tracking
**concept:** HourTracking[User, Project, SessionLimit]

**purpose:** track work time on projects

**principle:** after a user starts a session on a project, time is rtacked until they end the session or it ends automatically at the session's limit. 

**state:**
> a set of Sessions with
>> a user User\
>> a project Project\
>> a startTime Time\
>> a description String\
>> an optional endTime Time

**actions:**
>startSession(user: User, project: Project, description: String, startTime: Time): (session: Session)
>>*requires:*\
user has no open session\
>>*effects:*\
creates a new session associated with user, project, startTime and given description; adds it to sessions and returns the session

>endSession(user: User, session: Session, endTime: Time)
>>*requires:*\
the session belongs to the user\
session has no endTime set\
>>*effects:*\
sets session endTime

>autoEndSession(user: User, session: Session, sessionLimit : SessionLimit)
>>*requires:*
session belongs to the user and has no endTime\
session has been opened for more than the sessionLimit time\
>>*effects:*
sets endTime as the current time


**Invariants**
- At most one open session per user.  
- If session has endTime, endTime > startTime
- For any two sessions of a user, work times don't overlap
- A session lasts at most sessionLimit time (+ buffer time for detecting a forgotten openSession)

## Conference Room Booking
**concept** RoomBooking [User, Room]

**purpose** provides scheduled room spaces for users 

**principle** an organizer chooses a room to reserve for a certain amount of time; the organizer is assured to use that room freely, for the duration indicated

**state**
> a set of Bookings with
>> an organizer User\
>> a startTime Time\
>> an endTime Time\
>> a room Room

**actions**
> createBooking (organizer: Users, room: Room, startTime: Time, endTime: Time) : (booking: Booking)
>> *requires:* room exists and is not booked at all in that interval\
the user has no other booking that overlaps with [startTime, endTime]\
>> *effects:* creates a new booking, associates it with organizer, room and interval times. Returns the booking 

> cancelBooking (user: User, booking: Booking)
>> *requires:* booking exists\
>> *effects:* removes the booking from bookings

**Invariants**
- **No double-booking per room:** for any room, booking intervals do not overlap.  
- **At most one room per user at a time:** for any organizer, booking intervals do not overlap.  


