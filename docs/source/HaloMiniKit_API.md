## HaloMiniKit_API

### 说明

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

