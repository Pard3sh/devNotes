# Password Reset Form

As part of my work in Hack4Impact's Impact Team, I completed login and register functionality for the non profit group Project Access's volunteer portal. The only part I have yet to implement is the forgot password functionality. This note will include my plan for implementation and then notes on how I implemented it.



## Flow

1. User will click *forgot password*
    * the front end for this has already been set up, there is a component called forgot which allows the user to submit an email address

2. The back end will take this email address, validate that the email exists in the database, and then send an email to this email address

3. The link should take them to a page that allows them to enter a new password. There will be a second form entry for confirm password. The passwords will be hashed before writing to the database. 

4. Redirect user to the login page


