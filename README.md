## Script Format

There are two hard requirements that you need to keep in mind when developing scripts:

* All of the script files must be bundled inside a JAR file
* The JAR must contain a Javascript file called `main.js` within the **root of the classpath** that implements the
 following functions:

```
function isCompleted(user: User): Boolean
function getAbout(): String
function getDescription(): String
```

The `User` class has the following definition:

```
class User {
    username: String;
    firstName: String;
    lastName: String;
}
```

You are welcome to use Java libraries and import them using the Nashorn Javascript syntax, however be aware that you
will need to import these libraries in a manner that is compliant with the
[JAR File Specification](https://docs.oracle.com/javase/7/docs/technotes/guides/jar/jar.html).

## Script Upload

You may want to upload your script to the Sharebot either for deployment or debugging purposes. Note that there are
two running versions of the Sharebot at any given time; the production version and the debugging version. If you are
still developing your script, you should upload the script to the debugging server. Once you're done and your script
is well-tested, you can deploy to the production server.

First, make sure that you have a JAR file which conforms to the requirements outlined in the *Script Format*
section.

Then, set a couple of dynamic environment variables that are dependent on your use case:

```
PATH_TO_JAR='example.jar'
SHAREBOT_SERVER='example.com'
ACCESS_TOKEN='F4494CBFCF42B4...'
```

Finally, upload your JAR to the respective sharebot server using this command: 

`curl --insecure -i --header "Authorization: Bearer $ACCESS_TOKEN" --header "Content-Type:application/octet-stream" --data-binary @$PATH_TO_JAR https://$SHAREBOT_SERVER:8443/upload`

If you did not receive any errors during the file upload, the sharebot should have processed your script and is ready
to execute it. Try out some commands to see if it's working!