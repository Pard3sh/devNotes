# Aysnc functions

When doing any sort of web development (and plenty of other use cases
 where you need to wait on the return of a function to do other things), 
 asynchronous functions are essential. 

 Here is a basic example of a log in async function. Notice the usage
of res.status. That is a result status message sent to the front end. 
The front end code is a web interface allowing for the user to enter the 
user name and email, being stored in a data base. (password is encrypted in the database). One of the SOLID principles (D for Dependency Inversion Principle) states that

> Entities must depend on abstractions, not on concretions. It states that the high level module must not depend on the low-level module, but they should depend on abstractions.

So essentially, we don't need to know everything about the front end details, just that we will be given a user name and a hashed password. We will then validate if this user exists, if the password is correct, and then respond with a Javascript web token (JWT). JWTs are useful, will create a different note page for more info about them.

anyways enough explanation, here is the code.

```javascript
async function loginUser(req, res) {
  const { email, password } = req.body;

  console.log(req);

  // Read user data from the file
  fs.readFile("userData.txt", "utf8", async (err, data) => {
    if (err) {
      return res.status(500).json({ error: "Internal Server Error" });
    }
    if (!data) {
      return res.status(400).json({ error: "Invalid file content" });
    }
    try {
      // Parse the file data as an array of user objects
      const userDataArray = JSON.parse(data);

      // Log the user data to verify it's correctly parsed
      console.log("userData: ", userDataArray);

      // Log the email addresses being compared
      console.log("Requested email:", email);
      console.log(
        "User emails:",
        userDataArray.map((user) => user.email)
      );

      // Find the user with the provided email
      const user = userDataArray.find((user) => user.email === email);
      if (!user) {
        console.log(":(((( User not found whyyyy");
        return res.status(404).json({ error: "User not found" });
      }

      // Compare the provided password with the hashed password stored in the user data
      const passwordMatch = await bcrypt.compare(password, user.password);
      if (!passwordMatch) {
        return res.status(401).json({ error: "Invalid credentials" });
      }

      const token = jwt.sign({ email: user.email }, process.env.JWT_KEY, {
        expiresIn: "1h",
      });
      return res.status(200).json({ token });
    } catch (error) {
      return res.status(500).json({ error: "Error parsing JSON data" });
    }
  });
}
```

The only confusing part may be the text file reading. At this phase of development, we opted out of using MongoDB in favor of a relational database. We are still working on said relational DB so right now it is being done in a text file to continue development.

There is a lot in this snippet missing for the back end here. We are missing the api route set up, the server file and the middle ware information. However, it is enough as an example to illustrate async functions. The front end needs to wait on a response from the server for a login validation check to update the display. 
