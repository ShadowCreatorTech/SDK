# Unity SDK 文档

## HaloMiniKit_API

### HaloMiniKit_API 说明

HaloMiniKit 内容包括HaloMini 相机、蓝牙手柄的设置

### HaloMiniSystem

HaloMini系统组件

**属性**

是否开启遥控器3D模式
```java
public bool bluetoothHandle3D = false; 
```

运行时更改此参数无效 如需更改 请使用

```java
BluetoothHandleDevice.Instance.Mode3D (bool value)
```

是否开启3d摄像机（分屏模式）
```java
public bool camera3D = true;
```

### HaloMiniCamera

相机控制器

**属性**

```java
public Camera leftCam ;
public Camera rightCam ;
public float interPupilDistance = 0.064f; //视距
```

### HaloMiniInput

蓝牙手柄姿态四元素（3d模式下可用）
```java
public static Quaternion BluetoothHandleRotation;
```

蓝牙手柄姿态欧拉角（3d模式下可用）
```java
public static Vector3 BluetoothHandleAngles;
```

蓝牙手柄重力向量（3d模式下可用）
```java
public static Vector3 BluetoothHandleAcc;
```

蓝牙手柄链接状态
```java
public static bool isControllerConnect = false;
```

蓝牙手柄连接回调
```java
public static event ControllerConnect ControllerConnectEvent;
```

蓝牙手柄断开回调
```java
public static event ControllerUnConnect ControllerUnConnectEvent;
```

触控板向前滑动回调
```java
public static event TouchPadSlideBack TouchPadSlideBackEvent;
```

触控板向后滑动回调
```java
public static event TouchPadSlideForward TouchPadSlideForwardEvent;
```

触控板向上滑动回调
```java
public static event TouchPadSlideUp TouchPadSlideUpEvent;
```

触控板向下滑动回调
```java
public static event TouchPadSlideDown TouchPadSlideDownEvent;
```

返回键按下回调 如果不使用此回调 按下返回键后将退出游戏
```java
public static event EscapeDown EscapeDownEvent;
```

### BluetoothHandleDevice

开启或关闭蓝牙手柄3d模式
```java
public void Mode3D (bool value)
```

开启或关闭3DOF数据接收
```java
public void enable3Dof(bool value)
```

开启或关闭重力数据接收
```java
public void enableAcc(bool value)
```

## ShadowKit_API

### ShadowKit_API 说明

ShadowKit 内容包括视线焦点、基础输入设备管理、按钮、登陆系统

### ShadowSystem

影创sdk系统组件

**属性**

应用获得/失去焦点代理 这里只是做了个统一处理 实际引用时也可以写在各自类中
```java
public static event onApplicationFocus onApplicationFocusEvent; 
```

头部（包括摄像机、焦点等）
```java
public static GameObject Head;
```

主摄像机
```java
public static Camera Camera;
```

应用退出方法
```java
public static Action Quit;
```

登陆系统
```java
public static LoginSystem loginSystem;
```

### LoginSystem 影创账号登陆系统

登陆方法 
```java
public void Login();
```

使用方式：
```java
ShadowSystem.loginSystem.Login();
```

### InputSystem输入设备管理器

**属性**

射线最远距离
```java
public static  OnUpdate OnUpdateEvent; 
```
```java
public float MaxRaycastDistance = 20.0f;
```

可选择物体的层 可以根据实际情况设定
```java
public LayerMask RaycastLayerMask = Physics.DefaultRaycastLayers; 
```

### SCButton 3D按钮

（3D按钮必须添加BoxCollider 脚本中已绑定 并且Layer在InputSystem的RaycastLayerMask中）

**属性**

```java
public Transition transition
```

焦点进入和移出时的状态变化
```java
//Scale
public float scalNum = 1.1f; //Scale 变化比例
public float forwardNum = 0.05f; //Scale 变化时间
//Position
public float forwardNum = 0.05f; //Position 向前位移距离
public float forwardNum = 0.05f; //Position 变化时间
```

点击 可在Inspector里配置
```java
public UnityEvent onClick; 
```

焦点移入
```java
public UnityEvent onEnter;
```

焦点移出
```java
public UnityEvent onExit;
```

焦点进入时自动触发click事件的等待时间 0为不需要此功能
```java
public float autoClickTime;
```

方法
```java
public virtual void OnPointerDown(PointerEventData data)

public virtual void OnPointerUp(PointerEventData data)

public virtual void OnPointerClick(PointerEventData data)

public virtual void OnPointerEnter(PointerEventData eventData)

public virtual void OnPointerExit (PointerEventData eventData)
```

### UIButton UI按钮
继承自UnityEngine.UI.Button 用法和UnityEngine.UI.Button相同 （UI按钮必须添加BoxCollider 脚本中已绑定 并且Layer在InputSystem的RaycastLayerMask中）

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