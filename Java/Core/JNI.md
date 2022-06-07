# JNI

## Why we need JNI

JNI is a bridge between the bytecode and the native code (usually written in C or C++).

Some reasons for using native code:

- Handling hardware
- Performance improvement
- Use existing library instead of rewrite in Java

Disadventages of using native code:

- Lose the "write once, run anywhere" feature of Java
- Add a layer of communication between JVM and native code
- Sometimes we need to declare our specific type conventions

## Components

The shared lib wil be kept within .so/.dll/.dylib files.  
Java provides some pre-defined C/C++ elements for building shared libs, (inside `JAVA_HOME/include/jni.h`):

- JNIEXPORT,JNICALL: use them to mark a funciton as exportable so JNI can find it
- JNIEnv: contains methos for accessing Java elements
- JavaVM: lets us manipulate a running JVM

The `native` keyword will transforms our method into a abstract-like method
and indicate that it will be implemented in shared libraries.  
`System.loadLibrary(String)` will load the shared lib into memory
and makes its exported functions available in Java code

```java
static {
    System.loadLibrary("native");
}

private native void aMethod();
```

## Implementation

- Firstly, declare the Java code with the native method and load library function
- Compile the Java code to generate the C/C++ method definition (`.h` file) via `javac -h <where-to-save-header> <source>` command
- Declare the C++ code the implement the method definition

```cpp
JNIEXPORT void JNICALL Java_com_baeldung_jni_HelloWorldJNI_sayHello
  (JNIEnv* env, jobject thisObject) {
    std::cout << "Hello from C++ !!" << std::endl;
}
```

- Compile C++ code with included JNI header from Java home to `.o` file
- Link the compiled file into shared library with the pre-defined name (`.so`/`.dll`/`.dylib` file) via G++ linker
