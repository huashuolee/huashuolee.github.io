---
title: 备忘录－简单理解Activity
layout:  post  
categories: Android
description: 简单理解Android Activity
---

##  Basic
progress 75/570
基本原则：Android程序设计讲究逻辑和试图分离

## Activity

### AndroidMenifest.xml 注册
代码示例
```xml
<application  android:label="桌面上显示的名字">
    <activity
      android:name="指定具体注册的那个Activity">
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
      </intent-filter>
    </acitivity>
</application>
```
### 加载布局
setContentView(R.layout.first_layout)

## Toast
```java
Toast.makeText(MainActivity.this,"You clicked Button1",Toast.LENGTH_LONG).show();
```
## menu
### 创建布局
res目录--> new menu目录-->new menu resouce file-->结果res/menu/main.xml
```xml
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/add_item" android:title="Add" />
    <item android:id="@+id/remove_item" android:title="Remove" />
</menu>
```
### 代码编写
1. 重写onCreateOptionmenu()方法
2. 重写onOptionItemSelected()方法

## Intent
### 显式/隐式
intent一般用于启动活动，启动服务，发送广播等情景
1. 显式, 构建一个intent,传入FirstActivity.this作为上下文，SecondActivity.class作为目标，通过StartActivity()来执行
```java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
startActivity(intent);
```
2. 隐式，不明确指明哪一个Activity，但是指明了抽象的action,category等信息，交由系统去分析这个intent
  * 如果Activity要想响应隐式intent,在AndroidMenifest.xml中注册时，必须添加action category
  * 隐式Intent代码
  ```java
  Intent intent = new Intent("android.intent.action.VIEW");
  intent.addCategroy("xxxxx"); //可加可不加，默认的categroy是DEFAULT
  startActivity(intent);
  ```
  * startActivity后，系统就会列出所有能handle此intent的Activity.
3. 更多隐式Intent用法  
![more](/images/posts/more_intent.png)
### 向下一个Activity传递数据
  第一个Activity  
```java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
intent.putExtra("key",data);
startActivity(intent);
```
第二个Activity
```java
Intent intent = getIntent();
String data = intent.getStringExtra("key");
Log.e("SecondActivity", data);
```
### 返回数据给上一个Activity
startActivityForResult(intent, requestcode)  
第一个Activity
```java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
startActivityForResult(intent, 1);
```
第二个Activity
```java
Intent intent = new Intent();
intent.putExtra("key_data_return", "Hello FirstActivity");
setResult(RESULT_OK, intent);
finish()
```
回调第一个Activity
```java
switch (resuestCode){
  case 1:
      if (result_code==RESULT_OK){
        String returnedData = data.getStringExtra("key_data_return");
      }
      break;
  default;
}
```
或者在第二个Activity中重写onBackPressed()方法

## Activity life cycle
Android是使用Task管理Activity, 一个Tast就是一组存放在栈里Activity集合
### Activity的状态
一个Activity最多有４个状态
运行状态，暂停状态，停止状态，销毁状态

### Activity生命周期（７个回调函数）
onCreate， onStart, onResume, onPause, onStop, onDestroy, onRestart

### Activity被回收了怎么办
onSaveInstanceState()函数

## Activity的启动模式(android:launch＝“”)
1. standard  
每次都创建实例
2. singleTop  
栈顶是当前实例，则不创建实例，如果不是当前实例则需要再次创建
3. singleTask  
Activity在整个应用程序的上下文中，只存在一个实例，每次启动时，系统现在返回栈中检查是否存在该Activity实例。
4. singleInstance  
Activity会启动一个新的返回栈来管理这个Activity，这样做的意义是多个应用共享该Activity实例


## 实验总结
1. 在凤凰系统下，创建一个Activity，用什么模式与两个Activity都有关系
    * 两个activity，只要有一个是singleInstance那么就会另起一个窗口
    * 其他情况下都是在当前窗口打开
2. 知晓当前是哪一个Activity.  
新建一个BaseActiviy类,普通java类，继承自AppCompatActivity,重写onCreate()方法
Log.e("BaseActivity",getClass().getSimpleName())
3. 随时随地退出程序
