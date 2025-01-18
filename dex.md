Android 9

# InMemoryDexClassLoader
```java
InMemoryDexClassLoader(ByteBuffer[] dexBuffers, ClassLoader parent)
 BaseDexClassLoader(ByteBuffer[] dexFiles, ClassLoader parent)
  DexPathList(ClassLoader definingContext, ByteBuffer[] dexFiles)
   DexPathList.makeInMemoryDexElements(ByteBuffer[] dexFiles, List<IOException> suppressedExceptions)
    DexFile(ByteBuffer buf)
     DexFile.openInMemoryDexFile(ByteBuffer buf)
      native DexFile.createCookieWithDirectBuffer(ByteBuffer buf, int start, int end);
      native DexFile.createCookieWithArray(byte[] buf, int start, int end);
```

```c++
DexFile_createCookieWithDirectBuffer(JNIEnv* env, jclass, jobject buffer, jint start, jint end)
DexFile_createCookieWithArray(JNIEnv* env, jclass, jbyteArray buffer, jint start, jint end)
 CreateSingleDexFileCookie(JNIEnv* env, std::unique_ptr<MemMap> data)
  CreateDexFile(JNIEnv* env, std::unique_ptr<MemMap> dex_mem_map)
   ArtDexFileLoader::Open(const std::string& location, uint32_t location_checksum, std::unique_ptr<MemMap> map, bool verify, bool verify_checksum, std::string* error_msg)
    ArtDexFileLoader::OpenCommon(const uint8_t* base, size_t size, const uint8_t* data_base, size_t data_size, const std::string& location, uint32_t location_checksum, const OatDexFile* oat_dex_file, bool verify, bool verify_checksum, std::string* error_msg, std::unique_ptr<DexFileContainer> container, VerifyResult* verify_result)
```

# DexClassLoader
```java
DexClassLoader(String dexPath, String optimizedDirectory, String librarySearchPath, ClassLoader parent)
 BaseDexClassLoader(String dexPath, File optimizedDirectory, String librarySearchPath, ClassLoader parent)
  BaseDexClassLoader(String dexPath, File optimizedDirectory, String librarySearchPath, ClassLoader parent, boolean isTrusted)
   DexPathList(ClassLoader definingContext, String dexPath, String librarySearchPath, File optimizedDirectory, boolean isTrusted)
    DexPathList.makeDexElements(List<File> files, File optimizedDirectory, List<IOException> suppressedExceptions, ClassLoader loader, boolean isTrusted)
     DexPathList.loadDexFile(File file, File optimizedDirectory, ClassLoader loader, Element[] elements)
      DexFile(File file, ClassLoader loader, DexPathList.Element[] elements)
       DexFile(String fileName, ClassLoader loader, DexPathList.Element[] elements)
      DexFile.loadDex(String sourcePathName, String outputPathName,int flags, ClassLoader loader, DexPathList.Element[] elements)
       DexFile(String sourceName, String outputName, int flags, ClassLoader loader, DexPathList.Element[] elements)
DexFile.openDexFile(String sourceName, String outputName, int flags, ClassLoader loader, DexPathList.Element[] elements)
 native DexFile.openDexFileNative(String sourceName, String outputName, int flags, ClassLoader loader, DexPathList.Element[] elements)
```

```c++
DexFile_openDexFileNative(JNIEnv* env, jclass, jstring javaSourceName, jstring javaOutputName ATTRIBUTE_UNUSED, jint flags ATTRIBUTE_UNUSED, jobject class_loader, jobjectArray dex_elements)
 OatFileManager::OpenDexFilesFromOat(const char* dex_location, jobject class_loader, jobjectArray dex_elements, const OatFile** out_oat_file, std::vector<std::string>* error_msgs)
```