# JniCompressImage

1、AndroidManifest.xml中授权限。因为要从手机读取图片，压缩后写回手机本地。

```
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

2、将main\cpp下的文件复制到自己项目的main\cpp目录下。

3、将app\libs下的文件复制到自己项目的app\libs目录下。

4、将app\CMakeLists.txt复制到自己项目的app\CMakeLists.txt下

5、修改main\cpp\effective-bitmap.c文件的compressBitmap方法的路径。

6、修改app\build.gradle,

```
//defaultConfig节点中添加

externalNativeBuild {
    cmake {
        cppFlags ""
    }
}

ndk {
   abiFilters 'armeabi'
}

//在android节点中添加
sourceSets {
    main {
        jni.srcDirs = []
        jniLibs.srcDirs = ['libs']
    }
}

externalNativeBuild {
    cmake {
        path "CMakeLists.txt"
    }
}
```


