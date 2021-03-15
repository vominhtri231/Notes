### Problems
The main problem of serialization is its surface of attack is too broad, including the Java libraries, third-parties libraries and the application itself.  
It could lead to:

1. Remote code execution (RCE)
   
2. Denial-of-service (DoS)

### Solutions:
1. Prefer cross-platform structure data representations like JSON or protobuf
2. If you have to use serialization, never deserialize untrust data source and use object desrialization filtering (ObjectInputFilter).