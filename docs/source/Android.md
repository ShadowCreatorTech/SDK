# Android SDK 文档

## SDK API说明

### lvApp`SDK初始化类`

构造方法
```java
public IvApp ()
```

初始化SDK
```java
public static void init(Context context)
```

### IvAccountManager`注册登录影创账号类`

构造方法：
```java
public IvAccountManager(Activity context)
```

常量：
```java
public static final int REQUEST_ACCOUNT_MANAGER = 101; //打开注册登录应用程序的请求码
```

方法：
```java
public String getSystemAccount() //获取影创账号
public void loginAndRegister() //注册和登录影创账号
public void onActivityResult(int requestCode, int resultCode, Intent data) //注册登录返回结果处理
public void setCallback(Callback callback) //设置注册登录回调
```

### IvAccountManager.Callback`IvAccountManager回调接口`

接口：
```java
void onLoginSuccess(String accountName)//登录成功，参数为账号
void onLoginFailed(String msg)//登录失败，参数为失败信息
```

### IvDeviceManager`眼镜控制类`

构造方法：
```java
public IvDeviceManager(Context context)
```

方法：
```java
public void onResume() //恢复状态，与activity周期onResume一致。
public void onPause() //暂停状态，与activity周期onPause一致。
public void system3DSwitch(boolean open) //系统2D/3D模式切换，open为turn，切换到3D模式，open为false，切换到2D模式
```

### IvHeadPoseManager`眼镜陀螺仪位置信息`

构造方法：
```java
public IvHeadPoseManager(Context context)
```

方法：
```java
public void onResume() //恢复状态，与activity周期onResume一致
public void onPause() //暂停状态，与activity周期onPause一致
public void onDestroy() //退出注释资源，与activity周期onDestroy一致
public float[] getOrientationArray() //获取头部姿态矩阵参数
public void resetGyroData(boolean bX, boolean bY, boolean bZ) //重置陀螺仪数据
```

### IvHandShankManager`手柄控制类`

构造方法：
```java
public IvHandShankManager(Context context)
```

方法：
```java
public void onResume() //恢复状态，与activity周期onResume一致
public void onPause() //暂停状态，与activity周期onPause一致
public void onDestroy() //退出注释资源，与activity周期onDestroy一致
public boolean handShankConnected() //蓝牙手柄是否已连接
public void handShankMouseMode() //手柄切换到鼠标模式
/*
手柄2D/3D模式切换，上报3dof数据，点击报F12
open为turn，切换到3D模式，上报3dof数据，点击报F12
open为false，切换到2D模式，上报上下左右确定DPAD事件
*/
public void handShank3DSwitch(boolean open) 
public void enable3Dof(boolean enable) //设置手柄是否打开3dof数据，仅在3D模式下有效
public void enableACC(boolean enable) //设置手柄是否打开ACC(重力加速度)数据，仅在3D模式下有效
public void enableGYRO(boolean enable) //设置手柄是否打开GYRO(陀螺仪)数据，仅在3D模式下有效
public void setHandShankConnStateCallback(HandShankConnStateCallback handShankConnStateCallback) //设置手柄连接状态回调
public void setHandShankGYROCallback(HandShankGYROCallback handShankGYROCallback) //设置手柄GYRO(陀螺仪)回调
public void setHandShankACCCallback(HandShankACCCallback handShankACCCallback) //设置手柄ACC(重力加速度)回调
public void setHandShank3DofCallback(HandShank3DofCallback handShank3DofCallback) //设置手柄3dof回调
```

### IvHandShankManager.HandShankConnStateCallback`手柄连接状态回调接口`

接口：
```java
void onConnectionStateChange(boolean connected) //手柄与眼镜连接或者断开时回调
```

### IvHandShankManager.HandShank3DofCallback`3dof手柄姿态数据)回调接口`

接口：
```java
void onDataChanged(float[] value) //数据回调，value为长度为16姿态数据
```

### IvHandShankManager.HandShankACCCallback`手柄ACC(重力加速度)回调接口`

接口：
```java
void onDataChanged(float[] value) //数据回调，value为三轴上的分量
```

### IvHandShankManager.HandShankGYROCallback`手柄GYRO(陀螺仪)回调接口`

接口：
```java
void onDataChanged(float[] value) //数据回调，value为三轴上的分量
```

## Android ADK使用教程

### 开发工具IDE
Android studio 3.0

### 基本事件监听EventListener
该项介绍系统DPAD件事和焦点问题，可参考实例FocusDemo。该项与sdk无关，已熟悉可跳过该项。

**1.tp与手柄（2D模式）滑动事件**

眼镜侧边TP与手柄上报五个事件:向上滑（手柄上边区域可点击），向下滑（手柄下边区域点击），向左滑（手柄左边区域点击），向右滑（手柄右边区域点击），中间点击；分别报事件
```java
KeyEvent.KEYCODE_DPAD_UP;//code:19
KeyEvent.KEYCODE_DPAD_DOWN;//code:20
KeyEvent.KEYCODE_DPAD_LEFT;//code:21
KeyEvent.KEYCODE_DPAD_RIGHT;//code:22
KeyEvent.KEYCODE_DPAD_CENTER;//code:23
```
该事件直接报给系统，应用程序只须处理系统事件。类似控制器操作。

**2.焦点处理**

通过滑动切换控件焦点来显示控件是否被选中：
![sc](_static/images/2-2-1.png)

btn_selecter.xml
![sc](_static/images/2-2-2.png)

### 初始化SDK
将sdk文件ivsdk_v1.0.0.aar放到我们项目的libs文件夹下，就是和jar放在同一个文件夹下:
![sc](_static/images/2-3-1.png)

打开主项目下的build.gradle构建文件:
![sc](_static/images/2-3-2.png)

将aar包引入项目中：
![sc](_static/images/2-3-3.png)

Rebuild项目，此时sdk已经成功导入。

### 影创ShadowCreator账号信息
**1.初始化**
```java
// 注册登录
private IvAccountManager mAccountManager;
```

在onCreate中实例：
```java
mAccountManager = new IvAccountManager(this);
```

**2.获取系统已经登录账号信息**
```java
mAccountManager.getSystemAccount()
```

**3.注册登录系统**

设置回调，并调注册登录接口：
```java
//设置回调
mAccountManager.setCallback(new IvAccountManager.Callback(){
    @Override
    public void onLoginSuccess(String accountName) {}
    @Override
    public void onLoginFailed(String msg) {}
});
mAccountManager.loginAndRegister();//注册或登录
```

在onActivityResult中接收注册登录返回信息：
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    //注册登录请求直接交给mAccountManager接口来处理
    if(IvAccountManager.REQUEST_ACCOUNT_MANAGER == requestCode){
        mAccountManager.onActivityResult(requestCode, resultCode, data);
    }
}
```

### 系统2D/3D切换
**1.初始化及周期方法调用**
```java
// 设备 3d 切换
private IvDeviceManager mDeviceManager;
```

onCreate中实例：
```java
mDeviceManager = new IvDeviceManager(this);
```

周期方法调用：
```java
@Override
protected void onPause() {
    super.onPause();
    mDeviceManager.onPause();
}

@Override
protected void onResume() {
    super.onResume();
    mDeviceManager.onResume();
}
```

**2.2/3D切换**
```java
mDeviceManager.system3DSwitch(false);// 2D
mDeviceManager.system3DSwitch(true);// 3D
```

### headPose头部姿态
**1.初始化及周期方法调用**
```java
// 头部位置信息
private IvHeadPoseManager mHeadPoseManager;
```

onCreate中实例：
```java
mHeadPoseManager = new IvHeadPoseManager(this);
```

周期方法调用：
```java
@Override
protected void onPause() {
    super.onPause();
    mHeadPoseManager.onPause();
}

@Override
protected void onResume() {
    super.onResume();
    mHeadPoseManager.onResume();
}

@Override
protected void onDestroy() {
    mHeadPoseManager.onDestroy();
    super.onDestroy();
}
```

**2.头部姿态矩阵获取**
```java
mHeadPoseManager.getOrientationArray()
```

该数据由应用主动获取，返回为长度16的float数组，表示头部当前姿态矩阵。该数据由OpenGL绘制时使用。

### handShank手柄
**1.初始化及周期方法调用**
```java
// 手柄
private IvHandShankManager mHandShankManager;
```

在onCreate中实例：
```java
mHandShankManager = new IvHandShankManager(this);
```

周期方法调用：
```java
@Override
protected void onResume() {
    super.onResume();
    mHandShankManager.onResume();
}

@Override
protected void onPause() {
    super.onPause();
    mHandShankManager.onPause();
}

@Override
protected void onDestroy() {
    mHandShankManager.onDestroy();
    super.onDestroy();
}
```

**2.手柄连接状态监听**

判断当时手柄是否处于连接状态
```java
mHandShankManager.handShankConnected()
```

设置连接状态监听
```java
mHandShankManager.setHandShankConnStateCallback(new IvHandShankManager.HandShankConnStateCallback() {
    @Override
    public void onConnectionStateChange(boolean connected) {
    }
});
```

**3.模式切换**

切换到鼠标模式
```java
mHandShankManager.handShankMouseMode();
```
鼠标模式下，手柄仅有点击事件（指操作圆形区域事件，不包括返回键，下同），该点击报鼠标左键给系统处理，应用程序仅须处理系统点击事件。

切换到2D模式
```java
mHandShankManager.handShank3DSwitch(false);
```

2D模式下，手柄上报五个事件:向上滑（上边区域点击），向下滑（下边区域点击），向左滑（左边区域点击），向右滑（右边区域点击），中间点击；分别报事件
```java
KeyEvent.KEYCODE_DPAD_UP;//code:19
KeyEvent.KEYCODE_DPAD_DOWN;//code:20
KeyEvent.KEYCODE_DPAD_LEFT;//code:21
KeyEvent.KEYCODE_DPAD_RIGHT;//code:22
KeyEvent.KEYCODE_DPAD_CENTER;//code:23
```

该事件直接报给系统，应用程序只须处理系统事件。

切换到3D模式
```java
mHandShankManager.handShank3DSwitch(true);
```

3D模式下，手柄3dof/acc/gyro数据下面介绍，点击事件报F12(KeyEvent.KEYCODE_F12;//code:142)给系统，应用程序只须监听处理系统F12：
```java
@Override
public boolean onKeyUp(int keyCode, KeyEvent event) {
    if(keyCode == KeyEvent.KEYCODE_F12){
        //3d 手柄点击事件
    }
    return super.onKeyUp(keyCode, event);
}
```

**4.3dof数据(融合后的手柄姿态数据)获取**

获取该数据需要手柄3D模式，设置数据回调，打开3Dof开关：
```java
mHandShankManager.handShank3DSwitch(true);//切换3D模式
//设置数据回调
mHandShankManager.setHandShank3DofCallback(new IvHandShankManager.HandShank3DofCallback() {
    @Override
    public void onDataChanged(float[] value) { 
    }
});
mHandShankManager.enable3Dof(true);//打开3Dof开关
```
onDataChanged中连续收到手柄当前姿态数据。该长度为16的float的数组表示的是手柄当前的姿态矩阵。该数据在openGL绘制时使用。



**5.acc数据(加速度)获取**
获取该数据需要手柄3D模式，设置数据回调，打开acc开关：
```java
mHandShankManager.handShank3DSwitch(true);//切换3D模式
//设置数据回调
mHandShankManager.setHandShankACCCallback(new IvHandShankManager.HandShankACCCallback() {
    @Override
    public void onDataChanged(float[] value) {
    }
});
mHandShankManager.enableACC(true);//打开ACC开关
```
onDataChanged中连续收到手柄当前加速度数据（包括重力加速度）。该长度为3的float的数组表示的是手柄当前xyz三轴上的加速度数据。

**6.gyro数据(陀螺仪数据)获取**
获取该数据需要手柄3D模式，设置数据回调，打开gyro开关：
```java
mHandShankManager.handShank3DSwitch(true);//切换3D模式
//设置数据回调
mHandShankManager.setHandShankGYROCallback(new IvHandShankManager.HandShankGYROCallback() {
    @Override
    public void onDataChanged(float[] value) {
    }
});
mHandShankManager.enableGYRO(true);//打开GYRO开关
```
onDataChanged中连续收到手柄当前陀螺仪数据。该长度为3的float的数组表示的是手柄当前xyz三轴上的陀螺仪数据。