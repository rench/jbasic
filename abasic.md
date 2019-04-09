1. 简述一下Activity生命周期？
> - onCreate() 创建活动，做一些数据初始化操作 
> - onStart() 由不可见变为可见 
> - onResume() 可以与用户进行交互，位于栈顶 
> - onPause() 暂停，启动或恢复另一个活动时调用 
> - onStop() 停止，变为不可见 
> - onDestroy() 销毁 
> - onRestart() 由停止状态变为运行状态
2. Service生命周期？
> - onCreate() 首次创建服务时，系统将调用此方法。如果服务已在运行，则不会调用此方法，该方法只调用一次。
> - onStartCommand() 当另一个组件通过调用
> - startService()请求启动服务时，系统将调用此方法。
> - onDestroy() 当服务不再使用且将被销毁时，系统将调用此方法。
> - onBind() 当另一个组件通过调用bindService()与服务绑定时，系统将调用此方法。
> - onUnbind() 当另一个组件通过调用unbindService()与服务解绑时，系统将调用此方法。
> - onRebind() 当旧的组件与服务解绑后，另一个新的组件与服务绑定，onUnbind()返回true时，系统将调用此方法。
3. Service启动方式？

startService
> - 定义一个类继承service
> - 在manifest.xml文件中配置该service
> - 使用context的startService(intent)启动该service
> - 不再使用时,调用stopService(Intent)停止该服务

bindService
> - 创建bindService服务段,继承自service并在类中,创建一个实现binder接口的实例对象并提供公共方法给客户端调用
> - 从onbind()回调方法返回此binder实例
> - 在客户端中,从onserviceconnected()回调方法接收binder,并使用提供的方法调用绑定服务

4. 介绍下实现一个自定义View的基本流程？
> 1. 自定义View的属性 编写attr.xml文件
> 2. 在layout布局文件中引用，同时引用命名空间 
> 3. 在View的构造方法中获得我们自定义的属性 ，在自定义控件中进行读取（构造方法拿到attr.xml文件值） 
> 4. 重写onMesure 
> 5. 重写onDraw

5. ANR是什么？怎样避免和解决ANR Application Not Responding，即应用无响应?

出现的原因有三种： 
> a）KeyDispatchTimeout（5 seconds）主要类型按键或触摸事件在特定时间内无响应 
> b）BroadcastTimeout（10 seconds）BoradcastReceiver在特定的时间内无法处理 
> c）ServiceTimeout（20 seconds）小概率类型Service在特定的时间内无法处理完成
避免ANR最核心的一点就是在主线程减少耗时操作。

通常需要从那个以下几个方案下手： 
> - 使用子线程处理耗时IO操作 
> - 降低子线程优先级，使用Thread或者HandlerThread时，调用Process.setThreadPriority（Process.THREAD_PRIORITY_BACKGROUND）设置优先级，否则仍然会降低程序响应，因为默认Thread的优先级和主线程相同 
> - 使用Handler处理子线程结果，而不是使用Thread.wait()或者Thread.sleep()来阻塞主线程 
> - Activity的onCreate和onResume回调中尽量避免耗时的代码 
> - BroadcastReceiver中onReceiver代码也要尽量减少耗时操作，建议使用intentService处理。intentService是一个异步的，会自动停止的服务，很好解决了传统的Service中处理完耗时操作忘记停止并销毁Service的问题

6. 如何优化ListView(偶尔会问)
> - Item布局，层级越少越好，使用hierarchyview工具查看优化。 
> - 复用convertView 
> - 使用ViewHolder 
> - item中有图片时，异步加载 
> - 快速滑动时，不加载图片 
> - item中有图片时，应对图片进行适当压缩 
> - 实现数据的分页加载

7. RecyclerView和ListView的区别(这个是必问的) ？
> - RecyclerView可以完成ListView,GridView的效果，还可以完成瀑布流的效果。同时还可以设置列表的滚动方向（垂直或者水平）；> 
> - RecyclerView中view的复用不需要开发者自己写代码，系统已经帮封装完成了。 
> - RecyclerView可以进行局部刷新。 
> - RecyclerView提供了API来实现item的动画效果。

> 在性能上： 如果需要频繁的刷新数据，需要添加动画，则RecyclerView有较大的优势。 如果只是作为列表展示，则两者区别并不是很大。

8. Android异步消息处理机制？ 
异步消息处理机制主要是用来解决子线程更新UI的问题,主要有四个部分： 
> 1. Message （消息） 在线程之间传递，可在内部携带少量信息，用于不同线程之间交换数据 可以使用what、arg1、arg2字段携带整型数据 obj字段携带Object对象 
> 2. Handler （处理者） 主要用于发送和处理消息，sendMessage（）用来发送消息，最终会回到handleMessage（）进行处理 
> 3. MessageQueue （消息队列） 主要存放所有通过Handler发送的消息，它们会一直存在于队列中等待被处理 每个线程只有一个MessageQueue 
> 4. Looper （循环器） 调用loop（）方法后，会不断从MessageQueue 取出待处理的消息，然后传递到handleMessage进行处理

9. 内存泄漏和内存溢出是什么？一般怎么处理内存泄漏？ 
> - 内存溢出（OOM）和内存泄露（对象无法被回收）的区别。 
> - 引起内存泄露的原因 
> - 内存泄露检测工具 ------>LeakCanary
> 内存溢出 out of memory：是指程序在申请内存时，没有足够的内存空间供其使用，出现out of memory；比如申请了一个integer,但给它存了long才能存下的数，那就是内存溢出。内存溢出通俗的讲就是内存不够用。

> 内存泄露 memory leak：是指程序在申请内存后，无法释放已申请的内存空间，一次内存泄露危害可以忽略，但内存泄露堆积后果很严重，无论多少内存,迟早会被占光

> 内存泄露原因以及解决： 
> 1. Handler 引起的内存泄漏。 解决：将Handler声明为静态内部类，就不会持有外部类SecondActivity的引用，其生命周期就和外部类无关， 如果Handler里面需要context的话，可以通过弱引用方式引用外部类 
> 2. 单例模式引起的内存泄漏。 解决：Context是ApplicationContext，由于ApplicationContext的生命周期是和app一致的，不会导致内存泄漏 
> 3. 非静态内部类创建静态实例引起的内存泄漏。 解决：把内部类修改为静态的就可以避免内存泄漏了 
> 4. 非静态匿名内部类引起的内存泄漏。 解决：将匿名内部类设置为静态的。 
> 5. 注册/反注册未成对使用引起的内存泄漏。 注册广播接受器、EventBus等，记得解绑。 
> 6. 资源对象没有关闭引起的内存泄漏。 在这些资源不使用的时候，记得调用相应的类似close（）、destroy（）、recycler（）、release（）等方法释放。 
> 7. 集合对象没有及时清理引起的内存泄漏。 通常会把一些对象装入到集合中，当不使用的时候一定要记得及时清理集合，让相关对象不再被引用。

10. Android常见的两种错误(ANR和FC)？
```
先介绍下Main线程（也称为UI线程、主线程）
    功能: 1. 创建UI控件
          2. 更新UI控件状态
          3. 事件处理
    限制：Main线程不建议有超过5秒的事件
ANR
    出现条件：
        当用户输入事件5s内没有得到响应，将弹出ANR对话框
        广播接收者的onReceive()执行时间超过10s
    解决方案（原则）：
        所有可能的耗时操作都要在子线程（）中执行
        常见耗时操作：
            I/O:网络操作
            SDcard 
            数据运算
FC
原因：
        1. Error
          OOM(out of memory error)
          StackOverFlowError
        2. RuntimeException
```

11. 图片加载框架有哪些？他们之间的区别是什么？
ImageLoader ： 优点：
> 1. 支持下载进度监听； 
> 2. 可以在 View 滚动中暂停图片加载； 
> 3. 默认实现多种内存缓存算法这几个图片缓存都可以配置缓存算法，不过 ImageLoader 默认实现了较多缓存算法，如 Size 最大先删除、使用最少先删除、最近最少使用、先进先删除、时间最长先删除等； 
> 4. 支持本地缓存文件名规则定义； 
> 5. 缺点: 缺点在于不支持GIF图片加载, 缓存机制没有和http的缓存很好的结合, 完全是自己的一套缓存机制

Picasso： 优点：
> 1. 自带统计监控功能，支持图片缓存使用的监控，包括缓存命中率、已使用内存大小、节省的流量等。 
> 2. 支持优先级处理 
> 3. 支持延迟到图片尺寸计算完成加载 
> 4. 支持飞行模式、并发线程数根据网络类型而变，手机切换到飞行模式或网络类型变换时会自动调整线程池最大并发数。 
> 5. “无”本地缓存。Picasso 自己没有实现本地缓存，而由okhttp 去实现，这样的好处是可以通过请求 Response Header 中的 Cache-Control 及 Expired 控制图片的过期时间。 
> 6. 缺点： 于不支持GIF，默认使用ARGB_8888格式缓存图片，缓存体积大。

Glide： 优点：
> 1. 图片缓存->媒体缓存 ，支持 Gif、WebP、缩略图。甚至是 Video。 
> 2. 支持优先级处理 
> 3. 与 Activity/Fragment 生命周期一致，支持 trimMemory 
> 4. 支持 okhttp、Volley。Glide 默认通过 UrlConnection 获取数据，可以配合 okhttp 或是 Volley 使用。实际 ImageLoader、Picasso 也都支持 okhttp、Volley。 
> 5. 内存友好，内存缓存更小图片，图片默认使用默认 RGB565 而不是 ARGB888 
> 6. 缺点： 清晰度差，但可以设置

Fresco：优点:
> 1. 图片存储在安卓系统的匿名共享内存, 而不是虚拟机的堆内存中,所以不会因为图片加载而导致oom, 同时也减少垃圾回收器频繁调用回收Bitmap导致的界面卡顿,性能更高.
> 2. 渐进式加载JPEG图片, 支持图片从模糊到清晰加载 
> 3. 图片可以以任意的中心点显示在ImageView, 而不仅仅是图片的中心. 
> 4. JPEG图片改变大小也是在native进行的, 不是在虚拟机的堆内存, 同样减少OOM 
> 5. 很好的支持GIF图片的显示 
> 6. 缺点: 框架较大, 影响Apk体积，使用较繁琐


12. 网络框架有哪些？他们之间的区别是什么？
> - Xutils 这个框架非常全面，可以进行网络请求，可以进行图片加载处理，可以数据储存，还可以对view进行注解，使用这个框架非常方便，但是缺点也是非常明显的，使用这个项目，会导致项目对这个框架依赖非常的严重，一旦这个框架出现问题，那么对项目来说影响非常大的
> - OKhttp Android开发中是可以直接使用现成的api进行网络请求的。就是使用HttpClient,HttpUrlConnection进行操作。okhttp针对Java和Android程序，封装的一个高性能的http请求库，支持同步，异步，而且okhttp又封装了线程池，封装了数据转换，封装了参数的使用，错误处理等。API使用起来更加的方便。但是我们在项目中使用的时候仍然需要自己在做一层封装，这样才能使用的更加的顺手。
> - Volley Volley是Google官方出的一套小而巧的异步请求库，该框架封装的扩展性很强，支持HttpClient、HttpUrlConnection， 甚至支持OkHttp，而且Volley里面也封装了ImageLoader，所以如果你愿意你甚至不需要使用图片加载框架，不过这块功能没有一些专门的图片加载框架强大，对于简单的需求可以使用，稍复杂点的需求还是需要用到专门的图片加载框架。Volley也有缺陷，比如不支持post大数据，所以不适合上传文件。不过Volley设计的初衷本身也就是为频繁的、数据量小的网络请求而生。
> - Retrofit Retrofit是Square公司出品的默认基于OkHttp封装的一套RESTful网络请求框架，RESTful是目前流行的一套api设计的风格， 并不是标准。Retrofit的封装可以说是很强大，里面涉及到一堆的设计模式,可以通过注解直接配置请求，可以使用不同的http客户端，虽然默认是用http ，可以使用不同Json Converter 来序列化数据，同时提供对RxJava的支持，使用Retrofit + OkHttp + RxJava + Dagger2 可以说是目前比较潮的一套框架，但是需要有比较高的门槛。

> - Volley VS OkHttp Volley的优势在于封装的更好，而使用OkHttp你需要有足够的能力再进行一次封装。而OkHttp的优势在于性能更高，因为 OkHttp基于NIO和Okio ，所以性能上要比 Volley更快。IO 和 NIO这两个都是Java中的概念，如果我从硬盘读取数据，第一种方式就是程序一直等，数据读完后才能继续操作这种是最简单的也叫阻塞式IO,还有一种是你读你的,程序接着往下执行，等数据处理完你再来通知我，然后再处理回调。而第二种就是 NIO 的方式，非阻塞式， 所以NIO当然要比IO的性能要好了,而 Okio是 Square 公司基于IO和NIO基础上做的一个更简单、高效处理数据流的一个库。理论上如果Volley和OkHttp对比的话，更倾向于使用 Volley，因为Volley内部同样支持使用OkHttp,这点OkHttp的性能优势就没了， 而且 Volley 本身封装的也更易用，扩展性更好些。

> - OkHttp VS Retrofit 毫无疑问，Retrofit 默认是基于 OkHttp 而做的封装，这点来说没有可比性，肯定首选 Retrofit。

> - Volley VS Retrofit 这两个库都做了不错的封装，但Retrofit解耦的更彻底,尤其Retrofit2.0出来，Jake对之前1.0设计不合理的地方做了大量重构， 职责更细分，而且Retrofit默认使用OkHttp,性能上也要比Volley占优势，再有如果你的项目如果采用了RxJava ，那更该使用 Retrofit 。所以这两个库相比，Retrofit更有优势，在能掌握两个框架的前提下该优先使用 Retrofit。但是Retrofit门槛要比Volley稍高些，要理解他的原理，各种用法，想彻底搞明白还是需要花些功夫的，如果你对它一知半解，那还是建议在商业项目使用Volley吧。

13. 熟悉哪些设计模式？
> - 适配器模式,Adapter
> - 单例模式,对于那些比较耗内存的类，只实例化一次可以大大提高性能，尤其是在移动开发中,持程序运行的时候该中始终只有一个实例存在内存中
> - 建造者模式,Builder
> - 观察者模式
> - 原型模式
> - 策略模式

14. Android常用的缓存？什么是三级缓存？
> - 网络加载，不优先加载，速度慢，浪费流量 
> - 本地缓存，次优先加载，速度快 
> - 内存缓存，优先加载，速度最快 
> - 首次加载Android App时，肯定要通过网络交互来获取图片，之后我们可以将图片保存至本地SD卡和内存中，之后运行APP时，优先访问内存中的图片缓存，若内存中没有，则加载本地SD卡中图片，最后选择访问网络

15. Android与服务器交互的方式中的对称加密和非对称加密是什么？ 
> - 对称加密，就是加密和解密数据都是使用同一个key，这方面的算法有DES。 
> - 非对称加密，加密和解密是使用不同的key。发送数据之前要先和服务端约定生成公钥和私钥，使用公钥加密的数据可以用私钥解密，反之。这方面的算法有RSA。ssh 和 ssl都是典型的非对称加密。

16. 跨进程通信的几种方式 ？
> - Intent,比如拨打电话 
> - ContentProvider数据库存储数据 
> - Broadcast广播通信 AIDL通信，通过接口共享数据
wait和sleep 的区别？
> wait是Object的方法，wait是对象锁，锁定方法不让继续执行，当执行notify方法后就会继续执行，sellp是Thread的方法，sellp是使线程睡眠，让出cpu，结束后自动继续执行
String,StringBuffer,StringBuilder？
> String,StringBuffer,StringBuilder的区别 String不可改变对象，一旦创建就不能修改 String str="aaa"; str="bbb"

17. View和SurfaceView的区别？
> View基于主线程刷新UI，SurfaceView子线程又可以刷新UI

18. 简述JNI？
> 是java和c语言之间的桥梁，由于java是一种半解释语言，可以被反编译出来，一种重要涉及安全的代码就使用了C编程，再者很多底层功能调用C语言都实现了Java没必要重复造轮子，所以定义了JNI接口的实现

19. 简单谈一下MVC，MVP，MVVM ？
> - MVC:View是可以直接访问Model的！从而，View里会包含Model信息，不可避免的还要包括一些 业务逻辑。 在MVC模型里，更关注的Model的不变，而同时有多个对Model的不同显示，及View。所以，在MVC模型里，Model不依赖于View，但是 View是依赖于Model的。不仅如此，因为有一些业务逻辑在View里实现了，导致要更改View也是比较困难的，至少那些业务逻辑是无法重用的。
> - MVP：MVP 是从经典的模式MVC演变而来，它们的基本思想有相通的地方：Controller/Presenter负责逻辑的处理，Model提供数据，View负 责显示。作为一种新的模式，MVP与MVC有着一个重大的区别：在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部，而在MVC中View会从直接Model中读取数据而不是通过 Controller。 
> - MVVM：数据双向绑定，通过数据驱动UI，M提供数据，V视图，VM即数据驱动层

20. Hander原理？
> Handler，loop轮询检测发送消息到MessagerQuery,MessageQuery对Message入列，Handler回调方法处理消息，重写handMessage方法刷新ui

21. SharedPreference跨进程使用会怎么样？如何保证跨进程使用安全？ 
> 在两个应用的manifest配置中好相同的shartdUserId属性，A应用正常保存数据，B应用 createPackageContext("com.netease.nim.demo", CONTEXT_IGNORE_SECURITY) 获取context然后获取应用数据，为保证数据安全，使用加密存储

22. 推送到达率如何提高？
> 判手机系统，小米使用小米推送，华为使用华为推送，其他手机使用友盟推送

23. activity，fragment传值问题？
> 通过Bundle传值，在activty定义变量传值，扩展fragment创建传值

24. Dalvik虚拟机与java虚拟机的区别?
> 1. java虚拟机运行的是Java字节码，Dalvik虚拟机运行的是Dalvik字节码；传统的Java程序经过编译，生成Java字节码保存在class文件中，java虚拟机通过解码class文件中的内容来运行程序。而Dalvik虚拟机运行的是Dalvik字节码，所有的Dalvik字节码由Java字节码转换而来，并被打包到一个DEX(Dalvik Executable)可执行文件中Dalvik虚拟机通过解释Dex文件来执行这些字节码。
> 2. Dalvik可执行文件体积更小。SDK中有一个叫dx的工具负责将java字节码转换为Dalvik字节码。
> 3. java虚拟机与Dalvik虚拟机架构不同。java虚拟机基于栈架构。程序在运行时虚拟机需要频繁的从栈上读取或写入数据。这过程需要更多的指令分派与内存访问次数，会耗费不少CPU时间，对于像手机设备资源有限的设备来说，这是相当大的一笔开销。Dalvik虚拟机基于寄存器架构，数据的访问通过寄存器间直接传递，这样的访问方式比基于栈方式快的多.