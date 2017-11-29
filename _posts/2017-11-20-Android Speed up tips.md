this is some tweaks for Android Studio and Gradle Build system to make them perform more faster

## 1. Android Studio Tweaks

- Launch: Notepad++ as administrator
- Open: `C:\Program Files\Android\Android Studio\bin\studio64.exe.vmoptions`

There are a lot of parameters, but we are interested in memory-related parameters:
- `Xms`: Specifies the initial size, in bytes, of the memory allocation pool.
- `Xmx`: Specifies the maximum size, in bytes, of the memory allocation pool.
- `XX:MaxPermSize`: Size of the Permanent Generation.
- `XX:ReservedCodeCacheSize`: Reserved code cache size

Now, I’m using the following values:

> -Xms1024m  
-Xmx2048m  
-XX:MaxPermSize=1024m  
-XX:ReservedCodeCacheSize=512m  


 

## 2. Gradle

Gradle is the new build system used in Android Studio
Now, we will configure the global settings of Gradle:

- Goto: `C:\Users\<UserName>\.gradle`
- make a new file called `gradle.properties`
- Add the following lines to the file:
    
    >org.gradle.parallel=true  
     org.gradle.daemon=true
    
- Launch Android Studio and goto `File -> Settings -> Gradle` then enable `Offline work`
- Restart Android Studio and check if there is any Speed Improvement.
 

Happy Development 🙂