Enums are ***full-fledged class*** that expose instances via static final fields, they are:
1. Instance-controlled - user can not create an instance of them at runtime
2. Final - user can not extend them
3. Implements all Object methods, Serializable, Comparable
4. Can implement from any interface
5. Enum constructor is called before static fields are initialized   
   It is impossible to access static fields in enum constructor. A special case for this rule is: 
   A enum constrain can not access another from the constructor.