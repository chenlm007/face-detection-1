
[toc]

---

#<center>**Eclipse ���� OpenCV ����֮ face-detection**</center>

---

#***TODO***

- [] 

---

#**Reference**

* [eclipse��������ɾ��������Ŀʱ ��ʾ�����ռ��ڸ���Ŀ��Ȼ����](http://blog.csdn.net/xiabo851205/article/details/8234828 "http://blog.csdn.net/xiabo851205/article/details/8234828")

---

#**׼������**

##**���ز���װ OpenCV �� Andorid SDK**

>�ٷ���ַ��http://opencv.org/downloads.html

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/01.png)

��ѹ����

�����ѹ���� D:\OpenCV-3.2.0-android-sdk

##**���ز���װ NDK**

>�ٷ���ַ��https://developer.android.com/ndk/downloads/index.html

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/02.png)

��ѹ����

�����ѹ���� D:\android-ndk

---

#**���빤��**

##**�� Eclipse ����ʼ���빤��**

>File -> Import...

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/03.png)

##**ѡ����Ŀ����Ϊ Android**

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/04.png)

##**ѡ����� OpenCV ����**

���� OpenCV �� lib �� face-detection ���̡�

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/05.png)

###**���������**

####**�����ռ��в����ڸ���Ŀȴ�޷�����**

#####**Question**

>Select at least one project

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/06.png)

#####**Why**

��ǰ�����������̣�û��ɾ���ɾ���ɾ��������̺�Eclipse ���м��䡣

#####**Answer**

ˢ�¹����ռ䣬�� Package Explorer ���Ҽ���ѡ�� Refresh��ɾ�������ڵĹ��̡�

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/07.png)

---

#**���ù���**

##**���� lib**

###**��δ�ҵ�**

####**Question**

>The import android.hardware.camera2 cannot be resolved

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/08.png)

####**Why**

Project Build Target �汾���ͣ����ɸ��ߵİ汾��

####**Answer**

>�Ҽ����� -> Properties

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/09.png)

ѡ��ϸ߰汾������ Android 7.1.1��

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/10.png)

##**���� face-detection**

###**lib δ�ҵ�**

####**Question**

>The import org.opencv.* cannot be resolved

####**Why**

lib ���� Eclipse ���ļ�λ�÷����˱仯��

####**Answer**

�������� lib ���á�

>�Ҽ����� -> Properties

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/11.png)

ɾ���ɵ� lib ���ã���Ӧ�á�

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/12.png)

����µ� lib ���ã���Ӧ�á�

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/13.png)

###**ndk-build.cmd δ�ҵ�**

####**Question**

>Program "/ndk-build.cmd" is not found in PATH

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/14.png)

####**Why**

Ĭ�ϵ� C/C++ build command �����á�

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/15.png)

####**Answer**

#####**����1**

�޸� C/C++ build command��

>�Ҽ����� -> Properties

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/16.png)

�޸�Ϊ NDK �İ�װ·����

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/17.png)


#####**����2**

��ӻ������� NDKROOT��ֵΪ NDK Ŀ¼��

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/18.png)

rebuild ���̡�

###**OpenCV.mk δ�ҵ�**

####**Question**

>make: *** No rule to make target `../../sdk/native/jni/OpenCV.mk'.  Stop.

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/19.png)

####**Why**

Ĭ�ϵ� OpenCV.mk ·�������á�

####**Answer**

�޸�·����

�� Android.mk��

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/20.png)

Դ���룺

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/21.png)

�޸�Ϊ��

    LOCAL_PATH := $(call my-dir)
    
    include $(CLEAR_VARS)
    
    #OPENCV_CAMERA_MODULES:=off
    #OPENCV_INSTALL_MODULES:=off
    #OPENCV_LIB_TYPE:=SHARED
    ifdef OPENCV_ANDROID_SDK
      ifneq ("","$(wildcard $(OPENCV_ANDROID_SDK)/OpenCV.mk)")
        include ${OPENCV_ANDROID_SDK}/OpenCV.mk
      else
        include ${OPENCV_ANDROID_SDK}/sdk/native/jni/OpenCV.mk
      endif
    else
      include D:\OpenCV-3.2.0-android-sdk\sdk\native\jni\OpenCV.mk
    endif
    
    LOCAL_SRC_FILES  := DetectionBasedTracker_jni.cpp
    LOCAL_C_INCLUDES += $(LOCAL_PATH)
    LOCAL_LDLIBS     += -llog -ldl
    
    LOCAL_MODULE     := detection_based_tracker
    
    include $(BUILD_SHARED_LIBRARY)

---

#**����**

##**��װ��Ӧƽ̨�� OpenCV Manager**

�ļ�����Ŀ¼��D:\OpenCV-3.2.0-android-sdk\apk

##**��װ������ face-detection**

���гɹ���

![](https://github.com/weichao66666/face-detection/raw/master/README.md-images/22.png)

---














