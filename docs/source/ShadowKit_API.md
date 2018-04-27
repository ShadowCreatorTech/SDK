## ShadowKit_API

### 说明

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

