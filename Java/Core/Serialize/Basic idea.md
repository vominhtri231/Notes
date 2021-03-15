* Serialize is the process converting object into byte stream
``` java
ABC e = ...; // ABC implements serializable
ObjectOutputStream out = ...;
out.writeObject(e);
```
* Deserialize is the process converting byte stream into object 
``` java
ObjectInputStream in = ...;
ABC e = (ABC) in.readObject(); // ABC implements serializable
```
 
=> The puporse of serialization is to transfer objects from one VM to another or save to files for later retriving (in Wicket).