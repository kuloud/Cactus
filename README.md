
## 使用 
> android studio

```groovy
implementation 'io.github.kuloud:cactus:0.0.1'
```


## 用法（具体api请参考api说明）

- 注册 
   
   ```kotlin
    cactus {
       setPendingIntent(pendingIntent)
       setMusicId(R.raw.main)
       isDebug(true)
       ... //其他api等
       ...
       addCallback({
          //onStop回调，可以省略
       }) { 
          //doWork回调
       }
    }
   ```
- 注销 
   ```kotlin
    cactusUnregister()
   ``` 
- 重启 
   ```kotlin
    cactusRestart()
   ```      
## 混淆规则(proguard-rules.pro)
   ```
    -keep class com.gyf.cactus.entity.* {*;} 
   ```

## api说明，★ 标识的建议用户修改，而不是使用默认值
  | api | 说明 | api | 说明 |
  | :------------- |:-------------:| :------------- | :-------------:|
  | ★ setChannelId | 渠道Id，默认是Cactus，建议用户修改，非必传 | ★ setChannelName | 渠道名，用于设置里通知渠道展示，默认是Cactus，建议用户修改，非必传 |
  | ★ setTitle | 通知栏标题，默认是Cactus，建议用户修改，非必传 | ★ setContent |通知栏内容，默认是Cactus is running，建议用户修改，非必传 |
  | ★ setSmallIcon | 通知栏小图标，默认是库里的图标，建议用户修改，非必传 | setLargeIcon  | 通知栏大图标，默认没有大图标，非必传 |
  | ★ setServiceId | 服务Id，默认是1到Int.MAX_VALUE随机数，非必传 | setPendingIntent | 设置PendingIntent，用来处理通知栏点击事件，非必传 |
  | addCallback | 增加回调，用于处理一些额外的工作，非必传 | addBackgroundCallback  | 前后台切换回调，用于处理app前后台切换，非必传 |
  | setWorkerEnabled | 是否可以使用WorkManager，默认可以使用，非必传 | setCrashRestartUIEnabled  | 奔溃是否可以重启用户界面，默认为false，google原生rom android 10 以下可以正常重启，非必传 |
  | setRemoteViews | 设置RemoteViews（自定义布局），非必传 | setBigRemoteViews |设置BigRemoteViews（自定义布局），非必传 |
  | hideNotification | 是否隐藏通知栏，经测试，除了android 7.1手机之外都可以隐藏，默认隐藏，非必传 | hideNotificationAfterO |是否隐藏Android 8.0以上通知栏，默认隐藏 |
  | setMusicEnabled | 是否可以播放音乐，默认可以播放音乐，非必传 | setBackgroundMusicEnabled  | 后台是否可以播放音乐，默认不可以后台播放音乐，非必传 |
  | setMusicId | 设置自定义音乐，默认是无声音乐，该api只要在isDebug为true才会有生效，非必传 | ★ setMusicInterval  | 设置音乐间隔时间，时间间隔越长，越省电，默认间隔时间是0，非必传 |
  | setNotification | 设置notification，非必传，如果不传，将使用用户根据其他api设置的信息构建Notification | setNotificationChannel |设置NotificationChannel，非必传，如果不传，将使用默认的NotificationChannel |
  | register | 必须调用，建议在Application里初始化，使用Kotlin扩展函数不需要调用此方法 | unregister  | 注销，并不会立马停止，而是在1s之后停止，非必须调用，比如可以在app完全退出的时候可以调用，根据你的需求调用 |
  | restart | 重启，与register区别在于不会重新配置CactusConfig信息，而是使用上一次配置的信息 | isRunning  | 是否在运行 |


## 更新说明
#### 0.0.1
- compileSdk 升级30+后通知栏flag问题处理