## Unity使用教程

### 导入sdk

安装需求：Unity 2017.0.3或更高

首先，你需要下载影创Unity SDK，找到SDK_HaloMini.unitypackage，创建一个工程，然后将SDK导入到Unity中。

![sc](_static/images/3-1-1.png)


![sc](_static/images/3-1-2.png)

### 初始化HaloMini场景

1.新建新的场景

2.将场景中的“Main Camera”删除

![sc](_static/images/3-2-1.png)

3.点击工具栏 ShadowCreator->Create->HaloMini 添加HaloMini组件

![sc](_static/images/3-2-2.png)

4.添加完组件后会在舞台上生成3个组件 “ShadowSystem”“HaloMiniSystem”“HaloMiniCamera”,其中“ShadowSystem”“HaloMiniSystem”会持久化在舞台上，切换场景时会自行进行匹配。“HaloMiniCamera”可以跟据实际情况进行调整，会随着场景移除而销毁

![sc](_static/images/3-2-3.png)

### 开启和关闭Bluetooth手柄3D模式

在场景制作时 选中HalominiSystem ，在Inspactor中改变Bluetooth Handle 3D开启和关闭应用启动时蓝牙手柄3d模式 

![sc](_static/images/3-3-1.png)

运行时请使用BluetoothHandleDevice.Instance.Mode3D (bool value)进行开启和变比蓝牙手柄3D模式

### 开启和关闭Camera的3D模式（分屏模式）

在场景中选中HalominiSystem ，在Inspactor中勾选Camera 3D开启或关闭摄像头3d（分屏）模式 此模式在应用启动后无法通过代码动态更改

![sc](_static/images/3-4-1.png)

### 开启和关闭头部陀螺仪（Gyroscope）方法

在场景中选中HaloMiniCamera，在Inspactor中勾选Gyroscope开启或关闭陀螺仪 此模式在应用启动后无法通过代码动态更改

![sc](_static/images/3-5-1.png)

### 添加3D物体点击脚本

选中需要添加3D点击脚本的组件 点击Compontent->ShadowCreator->SCButton

![sc](_static/images/3-6-1.png)

### 添加UI点击脚本

选中需要添加UI点击脚本的组件 点击Compontent->ShadowCreator->SCButton

![sc](_static/images/3-7-1.png)

### Bluetooth手柄使用方法

开启和关闭蓝牙手柄的3D模式

```java
BluetoothHandleDevice.Instance.Mode3D(true);
BluetoothHandleDevice.Instance.Mode3D(false);
```

开启和关闭蓝牙手柄的3Dof数据接收 

```java
BluetoothHandleDevice.Instance.enable3Dof(true);
BluetoothHandleDevice.Instance.enable3Dof(false);
```

开启和关闭蓝牙手柄的重力数据接收 

```java
BluetoothHandleDevice.Instance.enableAcc(true);
BluetoothHandleDevice.Instance.enableAcc(false);
```