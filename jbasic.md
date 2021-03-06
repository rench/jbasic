- https://github.com/Snailclimb/JavaGuide
- https://www.cnblogs.com/over/p/10468747.html
- https://blog.csdn.net/u011665991/article/details/89206148
- https://blog.csdn.net/weixin_41607887/article/details/88803193
# 基础
- JDK 和 JRE 有什么区别？
> JDK是面向开发者的工具包,包含jre以及其他的更多的像编译javac以及java性能方面的工具比如jconsole，jstat等。JRE是java运行时环境，没有多余的依赖，精简小巧，包括了java运行的java虚拟机，基础类库等。
- == 和 equals 的区别是什么？
> ==作用于基础类型，判断的是两个基础类型的值知否相等，作用于对象引用类型，判断的两个对象的引用地址是否相等。equals，不能作用于基础类型，作用于对象引用类型是，判断的是两个对象中包含的值是否相等。
- 两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？
> 错，equals相等，hashcode一定要相等；hashcode相等，equals不一定相等；equals不相等，hashcode不一定不相等，但是作为程序员应该要知道为不相等的对象生成不同整数结果可以提高哈希表的性能。
- final 在 java 中有什么作用？
> 修饰类，类不能被继承；修饰方法，方法不能被重写；修饰变量，变量值（引用）不能被修改。
- java 中的 Math.round(-1.5) 等于多少？
> -1。floor 返回不大于的它最大整数，round 则是4舍5入的计算，入的时候是到大于它的整数。round方法，它表示“四舍五入”，算法为Math.floor(x+0.5)，即将原来的数字加上0.5后再向下取整，所以，Math.round(11.5)的结果为12，Math.round(-11.5)的结果为-11。ceil 则是不小于他的最小整数。
- String是基本的数据类型吗？
> String不是基本的数据类型，是final修饰的java类，java中的基本类型一共有8个，它们分别为：字符类型：byte，char,基本整型：short，int，long,浮点型：float，double,布尔类型：boolean。String是final修饰，不能被继承，String的值存储其实是`char[] value`。
- java 中操作字符串都有哪些类？它们之间有什么区别？
> 查看StringUtils，常见的empty,blank,trim,startWith,indexOf,contains等。
- String str="i"与 String str=new String("i")一样吗？
> 不一样，前者是一个常量，后者是一个new的对象，存储的位置不一样。前者的定义是常量定义，在编译期间，会在常量池中寻找是否存在i，如果不存在，则在常量池开辟新空间，存储i，然后在栈内存中开辟一个变量空间，存储常量池中i的引用地址，如果存在，则不用开辟新空间，直接在栈内存中开辟一个变量空间，存储常量池中i的引用地址。new String，在编译期也会现在常量池中是否存在i，如果不存在则开辟空间存储i，如果存在则返回引用地址。在运行时，通过new的关键字，会将之前存储在常量池的i复制一份，存放到堆内存中，在栈内存中，开辟变量空间存储堆内存中的字符串地址。
- 如何将字符串反转？
```
//递归模式
public String reverseStringRecur(String str) {
    if ((str == null) || str.length() <2) return str;
    return  reverseString(str.subString(1))+str.charAt(0);
}
//非递归方式
//1.定义中间变量，第n个和倒数N-n个交换
```
- 抽象类和普通类的区别?
> 抽象类不能被实例化，抽象类的访问权限限于Public和Protected，如果一个类继承于抽象类，则该子类必须实现父类的抽象方法
> 抽象类是否可以有构造函数？答案是可以有。抽象类的构造函数用来初始化抽象类的一些字段，而这一切都在抽象类的派生类实例化之前发生。不仅如此，抽线类的构造函数还有一种巧妙应用：就是在其内部实现子类必须执行的代码
- final可以修饰抽象类吗？
> final关键字不能用来抽象类和接口。
- java 中 IO 流分为几种？
> https://www.cnblogs.com/moonpool/p/5488463.html
> https://www.cnblogs.com/Buffalo-L/p/4446379.html
- BIO、NIO、AIO 有什么区别？
> BIO，阻塞io；NIO，非阻塞IO；AIO，异步IO；

# 集合
- java 容器都有哪些？
> Collection: List[ArrayList,LinkedList,Vector,Stack]

> Collection: Set[HashSet,TreeSet,LinkedSet]

> Map: HashTable,HashMap,TreeMap

- Collection 和 Collections 有什么区别?
> Colleciton是集合接口，Collections是类似工具的一个类，封装了操作集合的相关方法。
- HashMap和Hashtable的区别
> 都实现了Map接口，HashMap非线程安全，HashTable线程安全，方法上加synchronized。
- 如何决定使用 HashMap 还是 TreeMap？
> 根据是否需要按顺序输出结果。
- 说一下 HashMap 的实现原理？
> HashMap实现Map<K,V>接口，可以存储null，jdk<=1.7，内部使用数组+链表方式实现存储，>=1.8，内部使用数组+链表+红黑树，转换为红黑色条件：当某个链表的长度>=8且整个链表数组的大小<64个时，则扩容链表数组到64个，当链表数组的大小>=64时，则会将指定链表转换为树。
- 说一下 HashSet 的实现原理？
> 内部存储就是一个HashMap，key为hashset的key，value为实例化构造的new Object()
- 如何实现数组和 List 之间的转换？
> Arrays.asList(),userList.toArray()
- ArrayList 和 Vector 的区别是什么？
> 两者内部存储都是数组，前者非线程安全。扩容是，前者默认是1/2，后者默认是1倍。
- 在 Queue 中 poll()和 remove()有什么区别？
> poll，remove返回队列头部元素，队列为空时，前者返回null，后者抛异常。
- 怎么确保一个集合不能被修改？
> Collections.unmodifiableCollection,Collections.unmodifiable*()
- 常见的线程安全集合类有哪些？
> Vector,HashTable,StringBuffer,Statck,Enumeration,ConcurrentHashMap
- 常见的非线程安全集合类有哪些？
- ArrayList,LinkedList,HashMap,HashSet,TreeMap,TreeSet,StringBuilder
- TreeMap实现原理？
> 有序的红黑树结构，遍历使用的时候后续遍历，root在后
> 1. https://blog.csdn.net/chenssy/article/details/26668941
> 2. https://my.oschina.net/90888/blog/1626065
> 3. https://www.cnblogs.com/jeriffe/articles/2433942.html
> 4. https://segmentfault.com/a/1190000012728513

# 多线程
- 并行和并发有什么区别？
> 并行，是同时可以进行，没有资源竞争。并发是依靠CPU是的时间片轮转来达到表面上的同时进行。
- 线程和进程的区别？
> 进程是操作系统资源分配的基本单位，而线程是任务调度和执行的基本单位，线程是进程的一部分。
- 守护线程是什么？
> 守护线程是一种特殊的线程，优先级比较低，可以被jvm终止，通常这类线程被用于做一些空间垃圾回收的工作，如果jvm的所有非守护进程被终止了，那么jvm会终止jvm线程，所以守护进程一般不会进行一些可持久的数据操作，随时可能会被中断或停止。
- 创建线程有哪几种方式？
> 继承Thread，实现Runnable，Callable接口，优缺点主要在不能多继承，和获取当前线程的方法Thread.currentThread()。
- Runnable和Callable的差别？
> 两者都是接口，前者实现的方法异常需要内部处理，后者会抛出异常；前者没有返回值，后者有返回值，后者通过FutureTask.get()获取返回结果。
- 线程有哪些状态？
> NEW,RUNABLE,BLOCKED
> - WAITING(Object.wait, Thread.joinLockSupport.park)
> - TIMED_WAITING(Thread.sleep, objct.wait,Thread.join，LockSupport.parkNanos,LockSupport.parkUntil),
>- TERMINATED
- sleep 和 wait的区别？
> sleep是Thread类中的方法，不会放弃对象锁，到时间后自动恢复运行状态。wait是Object类中的方法，调用后，会放弃对象锁，进入等待，待其他线程针对此对象调用notify()/notifyAll()时，唤醒所有等待的线程，就可以恢复运行。锁是针对于synchronized 同步块或方法。
> https://blog.csdn.net/xyh269/article/details/52613507
- synchronized是否可重入？对于方法的同步有哪些区别？
> synchronized 的关键点在于锁持有的线程，以及锁住的对象。
> - 针对方法：
> 1. 非静态方法，锁住的对象是类的实例，不同实例互补干扰。
> 2. 静态方法，锁住的对象是类本身，所有实例共享。
> 3. 同一个线程，可以对同一个实例进行多次锁访问，称为锁重入，通过关联持有锁的线程+计数器来实现。
> - 在使用synchronized块来同步方法时，
> - 非静态方法：
> 1. 用this当做参数；
> - 静态方法：
> 1. 用类名.class当参数  
> 2. 通过实例的getClass()方法当参数。
- 创建线程池的方法有哪些？
> Executors类来创建，常见的newCachedThreadPool，newFixedThreadPool，newWorkStealingPool(jdk8)等。
```
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          RejectedExecutionHandler handler) {
    this(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue,
         Executors.defaultThreadFactory(), handler);
}
```
> 什么时候会触发RejectedExecutionHandler，当poolsize达到最大值，并且queue队列已满。

- Java中如何保证线程安全性?
> - 原子性--Atomic*,通过CAS完成。
> - https://www.cnblogs.com/skywang12345/p/3514623.html
> - 原子性--synchronized
> - 可见性--volatile
> 1. volatile的可见性是通过内存屏障和禁止重排序实现的
> 2. volatile在进行读操作时，会在读操作前加一条load指令，从内存中读取共享变量
> 3. 但是volatile不是原子性的，进行++操作不是安全的
> - 有序性,通过volatile、synchronized、lock保证有序性
> https://blog.csdn.net/weixin_40459875/article/details/80290875
> https://blog.csdn.net/tjreal/article/details/80548662
- 多线程锁的升级原理是什么？
> - https://blog.csdn.net/always_younger/article/details/79462684
> - https://blog.csdn.net/tjreal/article/details/80548662
```
在锁对象的对象头里面有一个 threadid 字段，在第一次访问的时候 threadid 为空，JVM 让其持有偏向锁，并将threadid 设置为其线程 id，再次进入的时候会先判断 threadid 是否尤其线程 id 一致，如果一致则可以直接使用，如果不一致，则升级偏向锁为轻量级锁，通过自旋循环一定次数来获取锁，不会堵塞，执行一定次数之后就会升级为重量级锁，进入堵塞，整个过程就是锁升级的原理。

锁的升级的目的：在 Java 6 之后优化 synchronized 的实现方式，使用了偏向锁升级为轻量级锁再升级到重量级锁的方式，减低了锁带来的性能消耗。

锁升级是为了减低了锁带来的性能消耗。
--------------------- 
作者：MrBlackWhite 
来源：CSDN 
原文：https://blog.csdn.net/u011665991/article/details/89206148 
版权声明：本文为博主原创文章，转载请附上博文链接！
```

- synchronized 原理？
> synchronized 关键字编译后会在同步块的前后添加上 montorenter 和 monitorexit 两个字节码指令，这两个字节码指令都需要一个指向锁定和解锁对象的 reference，如果指定了同步的对象reference就指向这个对象，如果修饰的是方法，如果是类方法就指向Class对象，如果是实例方法就指向这个实例。
- synchronized 锁的分类？
> - https://blog.csdn.net/qq_38462278/article/details/81976428
> - 无状态锁
> - 偏向锁,在锁定的对象的头部（Mark Word)存储偏向线程的ID,以后同一个线程再次进入该同步块时和退出同步块时,不需要进行CAS操作解锁和加锁，直接判断线程ID是否等于该线程即可。锁标志01。
> - 轻量级锁,会在当前线程的栈帧中创建一个锁定记录(Lock Record),然后把锁对象的对象头中的Mark Word复制到刚才创建的Lock Record,把所记录中的Owner替换成所对象，然后把锁对象的对象头的Mark Word替换为指向所记录的指针。锁标志00。
> - 重量级锁,重量级锁是依赖对象内部的monitor锁来实现的，而monitor又依赖操作系统的MutexLock(互斥锁)来实现的，所以重量级锁也被成为互斥锁.锁对象头部的会被替换为指向MutexLock的指针,锁标志10.
- synchronized与Lock的区别？
> 1. 首先synchronized是java内置关键字，在jvm层面，Lock是个java类；
> 2. synchronized无法判断是否获取锁的状态，Lock可以判断是否获取到锁；
> 3. synchronized会自动释放锁(a 线程执行完同步代码会释放锁 ；b 线程执行过程中发生异常会释放锁)，Lock需在finally中手工释放锁（unlock()方法释放锁），否则容易造成线程死锁；
> 4. 用synchronized关键字的两个线程1和线程2，如果当前线程1获得锁，线程2线程等待。如果线程1阻塞，线程2则会一直等待下去，而Lock锁就不一定会等待下去，如果尝试获取不到锁，线程可以不用一直等待就结束了；
> 5. synchronized的锁可重入、不可中断、非公平，而Lock锁可重入、可判断、可公平（两者皆可）
> 6. Lock锁适合大量同步的代码的同步问题，synchronized锁适合代码少量的同步问题。
- 说一下 atomic 的原理？
> - https://www.jb51.net/article/129690.htm
> - 最核心的CAS操作,`sun.misc.Unsafe`, `compareAndSwapObject`
- 讲一下ReentrantLock实现原理？
> ReentrantLock实现Lock接口，内部拥有NonfairSync和FairSync，实现公平锁和非公平锁，公平锁是先进先出的原理，谁先等待锁，谁就在下次先获得锁。Sync实现AQS，内部的线程锁等待使用CAS交换状态和LockSupport进行park(),unpark();
> - https://blog.csdn.net/u011521203/article/details/80186741

- Java技术之AQS详解
> AQS是AbstractQueuedSynchronizer的简称。AQS提供了一种实现阻塞锁和一系列依赖FIFO等待队列的同步器的框架，如下图所示。AQS为一系列同步器依赖于一个单独的原子变量（state）的同步器提供了一个非常有用的基础。子类们必须定义改变state变量的protected方法，这些方法定义了state是如何被获取或释放的。鉴于此，本类中的其他方法执行所有的排队和阻塞机制。子类也可以维护其他的state变量，但是为了保证同步，必须原子地操作这些变量。

> https://www.jianshu.com/p/da9d051dcc3d

# 反射
- 什么是反射？
> 主要是指程序可以访问、检测和修改它本身状态或行为的一种能力
- 什么是Java序列化？为什么序列化？序列化有哪些方式？
> 简单来说序列化就是把Java对象储存在某一地方（硬盘、网络），也就是将对象的内容进行流化，可以使二进制数据，也可是可存储数据的字符串等。
- 什么是动态代理？动态代理是如何实现的？动态代理有哪些应用？
> - 动态代理: 当想要给实现了某个接口的类中的方法，加一些额外的处理。比如说加日志，加事务等。可以给这个类创建一个代理，故名思议就是创建一个新的类，这个类不仅包含原来类方法的功能，而且还在原来的基础上添加了额外处理的新类。这个代理类并不是定义好的，是动态生成的。具有解耦意义，灵活，扩展性强。
> - 动态代理实现：首先必须定义一个接口，还要有一个InvocationHandler(将实现接口的类的对象传递给它)处理类。再有一个工具类Proxy(习惯性将其称为代理类，因为调用他的newInstance()可以产生代理对象,其实他只是一个产生代理对象的工具类）。利用到InvocationHandler，拼接代理类源码，将其编译生成代理类的二进制码，利用加载器加载，并将其实例化产生代理对象，最后返回。
> - 动态代理的应用：Spring的AOP，加事务，加权限，加日志。
- 动态代理实现？
> 1. jdk动态代理，jdk动态代理是由Java内部的反射机制来实现的，目标类基于统一的接口（InvocationHandler）
> 2. cglib动态代理，cglib动态代理底层则是借助asm来实现的，cglib这种第三方类库实现的动态代理应用更加广泛，且在效率上更有优势。可以直接代理实现类，不需要接口。
> 3. 参考 JpaRepositoryFactoryBean

# Web/安全
- 什么是 XSS 攻击，如何避免？
> XSS，跨站脚本攻击，主要是在参数/连接/内容存储中构造恶意js脚本导致的攻击。
- 什么是 CSRF 攻击，如何避免？
> CSRF，跨站请求伪造，用户已经登录B网站，在A网站中，构造一个请求B网站的连接，引导用户访问，访问后A网站后，隐身的就访问了B网站的数据或者请求。
> - https://www.cnblogs.com/lovesong/p/5233195.html

- session 和 cookie 有什么区别？
> - 存储位置不同：session 存储在服务器端；cookie 存储在浏览器端。
> - 安全性不同：cookie 安全性一般，在浏览器存储，可以被伪造和修改。
> - 容量和个数限制：cookie 有容量限制，每个站点下的 cookie 也有个数限制。
> - 存储的多样性：session 可以存储在 Redis 中、数据库中、应用程序中；而 cookie 只能存储在浏览器中。
```
IE 每个域名限制为50 个。
Firefox 每个域名cookie 限制为50 个。
Opera 每个域名cookie 限制为30 个。
Safari/webkit 貌似没有cookie 限制。但是假如cookie 很多，则会使header 大小超过服务器的处理的限制，导致错误发生。
不同浏览器间每个cookie 文件大小也不同
Firefox 和safari 是4097 个字节，包括名（name）、值（value）和等号。
Opera 是4096 个字节，包括：名（name）、值（value）和等号。
IE 是4095 个字节，包括：名（name）、值（value）和等号。
```

- spring mvc 和 struts 的区别是什么？

> - 拦截级别：struts2 是类级别的拦截；spring mvc 是方法级别的拦截。
> - 数据独立性：spring mvc 的方法之间基本上独立的，独享 request 和 response 数据，请求数据通过参数获取，处理结果通过 ModelMap 交回给框架，方法之间不共享变量；而 struts2 虽然方法之间也是独立的，但其所有 action 变量是共享的，这不会影响程序运行，却给我们编码和读程序时带来了一定的麻烦。
> - 拦截机制：struts2 有以自己的 interceptor 机制，spring mvc 用的是独立的 aop 方式，这样导致struts2 的配置文件量比 spring mvc 大。
> - 对 ajax 的支持：spring mvc 集成了ajax，所有 ajax 使用很方便，只需要一个注解 @ResponseBody 就可以实现了；而 struts2 一般需要安装插件或者自己写代码才行。

- 如何避免 sql 注入？
> 1. 使用预处理 PreparedStatement。
> 2. 使用正则表达式过滤掉字符中的特殊字符。

# 异常
- throw 和 throws 的区别？
> throw是指定抛出异常动作， throws是用于申明异常，不执行抛出异常动作。
- final、finally、finalize 有什么区别？
> 1. final关键字用于修饰类，方法，变量，修饰类时，该类不能被继承(String.java)，修饰方法时，方法不能被继承，修饰变量时，变量不能被重新赋值。
> 2. finally用于try-catch-finally组合，finally中的代码块，在可执行条件下，都会被执行，不管try-catch中是否有return，不管try-catch语句中是否有异常，如果finally中有return将覆盖try-catch中的return。
> 3. finalize是Object类中的一个方法，默认该方法没有任何操作，当gc进行垃圾回收时，会调用一次finalize，如果需要针对特殊的class进行gc后续清理，可以在该方法中实现逻辑，但是需要注意的时，jvm只会调用一次finalize，调用一次finalize后，如果该对象没有被回收，再次gc清理时，不会再次调用finalize方法。
- java中常见的异常类？
> Throwable派生出Error类和Exception类。
> - Exception: NPE,IllegalArgumentException,ClassNotFoundException,IOException等
# 网络
- http 响应码 301 和 302 代表的是什么？有什么区别？
> - 301 redirect: 301 代表永久性转移(Permanently Moved)。
> - 302 redirect: 302 代表暂时性转移(Temporarily Moved )。 
> - 301重定向是永久的重定向，搜索引擎在抓取新内容的同时也将旧的网址替换为重定向之后的网址。
302重定向是临时的重定向，搜索引擎会抓取新的内容而保留旧的网址。因为服务器返回302代码，搜索引擎认为新的网址只是暂时的。
- forward 和 redirect 的区别？
> forward直接转发request请求，redirect返回30x状态码，让浏览器执行跳转到新的url。
- TCP和UDP的区别和优缺点？
> 1. TCP面向连接（如打电话要先拨号建立连接）;UDP是无连接的，即发送数据之前不需要建立连接。
> 2. TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保证可靠交付。Tcp通过校验和，重传控制，序号标识，滑动窗口、确认应答实现可靠传输。如丢包时的重发控制，还可以对次序乱掉的分包进行顺序控制。
> 3. UDP具有较好的实时性，工作效率比TCP高，适用于对高速传输和实时性有较高的通信或广播通信。
> 4. 每一条TCP连接只能是点到点的;UDP支持一对一，一对多，多对一和多对多的交互通信
- TCP 为什么三次握手？四次断开？
> * https://blog.csdn.net/lengxiao1993/article/details/82771768
> * https://www.cnblogs.com/lms0755/p/9053119.html
```
为什么要三次握手？
> 1. 为了实现可靠数据传输， TCP 协议的通信双方， 都必须维护一个序列号， 以标识发送出去的数据包中， 哪些是已经被对方收到的。 三次握手的过程即是通信双方相互告知序列号起始值， 并确认对方已经收到了序列号起始值的必经步骤
> 2. 如果只是两次握手， 至多只有连接发起方的起始序列号能被确认， 另一方选择的序列号则得不到确认
```
> - 三次握手
> 1) 第一次握手：Client将标志位SYN置为1，随机产生一个值seq=J，并将该数据包发送给Server，Client进入SYN_SENT状态，等待Server确认。
> 2) 第二次握手：Server收到数据包后由标志位SYN=1知道Client请求建立连接，Server将标志位SYN和ACK都置为1，ack (number )=J+1，随机产生一个值seq=K，并将该数据包发送给Client以确认连接请求，Server进入SYN_RCVD状态。
> 3) 第三次握手：Client收到确认后，检查ack是否为J+1，ACK是否为1，如果正确则将标志位ACK置为1，ack=K+1，并将该数据包发送给Server，Server检查ack是否为K+1，ACK是否为1，如果正确则连接建立成功，Client和Server进入ESTABLISHED状态，完成三次握手，随后Client与Server之间可以开始传输数据了。
```
为什么要4次挥手？
确保数据能够完整传输。
当被动方收到主动方的FIN报文通知时，它仅仅表示主动方没有数据再发送给被动方了。
但未必被动方所有的数据都完整的发送给了主动方，所以被动方不会马上关闭SOCKET,它可能还需要发送一些数据给主动方后，
再发送FIN报文给主动方，告诉主动方同意关闭连接，所以这里的ACK报文和FIN报文多数情况下都是分开发送的。
```
> - 四次挥手
> * 第一次挥手：Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。

> * 第二次挥手：Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态。

> * 第三次挥手：Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。

> * 第四次挥手：Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSED状态，完成四次挥手。

- 说一下 tcp 粘包是怎么产生的？
> https://blog.csdn.net/qq_36359022/article/details/78840093
```
1. TCP粘包是什么？
粘包发生在发送或接收缓冲区中；应用程序从缓冲区中取数据是整个缓冲区中有多少取多少；那么就有可能第一个数据的尾部和第二个数据的头部同时存在缓冲区，而TCP是流式的，数据无边界，这时发生粘包。 
2. TCP粘包的产生?
1) 发送方产生粘包 
采用TCP协议传输数据的客户端与服务器经常是保持一个长连接的状态（一次连接发一次数据不存在粘包），双方在连接不断开的情况下，可以一直传输数据；但当发送的数据包过于的小时，那么TCP协议默认的会启用Nagle算法，将这些较小的数据包进行合并发送（缓冲区数据发送是一个堆压的过程）；这个合并过程就是在发送缓冲区中进行的，也就是说数据发送出来它已经是粘包的状态了； 
2) 接收方产生粘包 
接收方采用TCP协议接收数据时的过程是这样的：数据到底接收方，从网络模型的下方传递至传输层，传输层的TCP协议处理是将其放置接收缓冲区，然后由应用层来主动获取（C语言用recv、read等函数）；这时会出现一个问题，就是我们在程序中调用的读取数据函数不能及时的把缓冲区中的数据拿出来，而下一个数据又到来并有一部分放入的缓冲区末尾，等我们读取数据时就是一个粘包；（放数据的速度 > 应用层拿数据速度） 

3. TCP粘包解决方案
目前应用最广泛的是在消息的头部添加数据包长度，接收方根据消息长度进行接收；在一条TCP连接上，数据的流式传输在接收缓冲区里是有序的，其主要的问题就是第一个包的包尾与第二个包的包头共存接收缓冲区，所以根据长度读取是十分合适的；
1) 解决发送方粘包 
（1）发送产生是因为Nagle算法合并小数据包，那么可以禁用掉该算法； 
（2）TCP提供了强制数据立即传送的操作指令push，当填入数据后调用操作指令就可以立即将数据发送，而不必等待发送缓冲区填充自动发送； 
（3）数据包中加头，头部信息为整个数据的长度（最广泛最常用）； 
2) 解决接收方粘包 
（1）解析数据包头部信息，根据长度来接收； 
（2）自定义数据格式：在数据中放入开始、结束标识；解析时根据格式抓取数据，缺点是数据内不能含有开始或结束标识； 
（3）短连接传输，建立一次连接只传输一次数据就关闭；（不推荐）
```
- OSI七层模型？
1. 应用层 网络服务与最终用户的一个接口。 协议有：HTTP FTP TFTP SMTP SNMP DNS TELNET HTTPS POP3 DHCP
2. 表示层
数据的表示、安全、压缩。（在五层模型里面已经合并到了应用层）
格式有，JPEG、ASCll、DECOIC、加密格式等
3. 会话层
建立、管理、终止会话。（在五层模型里面已经合并到了应用层）
对应主机进程，指本地主机与远程主机正在进行的会话
4. 传输层
定义传输数据的协议端口号，以及流控和差错校验。
协议有：TCP UDP，数据包一旦离开网卡即进入网络传输层
5. 网络层
进行逻辑地址寻址，实现不同网络之间的路径选择。
协议有：ICMP IGMP IP（IPV4 IPV6） ARP RARP
6. 数据链路层
建立逻辑连接、进行硬件地址寻址、差错校验 [2]  等功能。（由底层网络定义协议）
将比特组合成字节进而组合成帧，用MAC地址访问介质，错误发现但不能纠正。
7. 物理层
建立、维护、断开物理连接。（由底层网络定义协议）
TCP/IP 层级模型结构，应用层之间的协议通过逐级调用传输层（Transport layer）、网络层（Network Layer）和物理数据链路层（Physical Data Link）而可以实现应用层的应用程序通信互联。
- 说一下jsonp原理实现？
> 什么是跨域: 跨域是浏览器同源策略而产生的，在不同协议，不同端口，不同域名下（以上任意一个不同都算是跨域）的客服端和服务端之间是无法互相访问的。
> 就是利用<script>标签没有跨域限制的特点来达到与第三方通讯的目的。当需要通讯时，本站脚本创建一个<script>元素，地址指向第三方的API网址，形如： 
`<script src="http://www.example.net/api?param1=1&param2=2"></script>` 并提供一个回调函数来接收数据（函数名可约定，或通过地址参数传递）。 第三方产生的响应为json数据的包装（故称之为jsonp，即json padding），形如： `callback({"name":"hax","gender":"Male"}) `这样浏览器会调用callback函数，并传递解析后json对象作为参数。本站脚本可在callback函数里处理所传入的数据。 

# 设计模式
- 说一下你熟悉的设计模式？
> 1. 创建型：Abstract Factory（抽象工厂模式），Builder（建造者模式），Factory Method（工厂方法模式），Prototype（原始模型模式），Singleton（单例模式）；
> 2. 结构型：Facade（门面模式），Adapter（适配器模式），Bridge（桥梁模式），Composite（合成模式），Decorator（装饰模式），Flyweight（享元模式），Proxy（代理模式）；
> 3. 行为型：Command（命令模式），Interpreter（解释器模式），Visitor（访问者模式），Iterator（迭代模式），Mediator（调停者模式），Memento（备忘录模式），Observer（观察者模式），State（状态模式），Strategy（策略模式），Template Method（模板方法模式）， Chain Of Responsibility（责任链模式）。
> * 工厂模式：工厂类可以根据条件生成不同的子类实例，这些子类有一个公共的抽象父类并且实现了相同的方法，但是这些方法针对不同的数据进行了不同的操作（多态方法）。当得到子类的实例后，开发人员可以调用基类中的方法而不必考虑到底返回的是哪一个子类的实例。

> * 代理模式：给一个对象提供一个代理对象，并由代理对象控制原对象的引用。实际开发中，按照使用目的的不同，代理可以分为：远程代理、虚拟代理、保护代理、Cache代理、防火墙代理、同步化代理、智能引用代理等。
> * 适配器模式：把一个类的接口变换成客户端所期待的另一种接口，从而使原本因接口不匹配而无法在一起使用的类能够一起工作。
> * 模板方法模式：提供一个抽象类，将部分逻辑以具体方法或构造器的形式实现，然后声明一些抽象方法来迫使子类实现剩余的逻辑。不同的子类可以以不同的方式实现这些抽象方法（多态实现），从而实现不同的业务逻辑。
- 简单工厂和抽象工厂有什么区别？
> https://blog.csdn.net/jerry11112/article/details/80618420
> https://www.cnblogs.com/qiaoconglovelife/p/5750290.html
> https://blog.csdn.net/michael_yt/article/details/82112443
> https://blog.csdn.net/auuea/article/details/84673570
> - 简单工厂模式，我们在实例化对象的时候通常用的是 New关键字，但是有了工厂，我们在声明对象的时候就可以用工厂了，用new导致代码不够灵活，用工厂来实例化对象很灵活！定义一个方法，根据传入的参数返回不同的实例。需要在方法中判断。
> - 工厂方法模式，定义一个创建对象的接口I和接口方法C，不同的实现B去继承这个接口I，并实现方法C，返回实例对象X。使用时，只需要new不同的实现类B，调用接口I的实现方法C即可。
> - 抽象工厂模式，在工厂方法模式上扩展，定义一个创建多个对象的抽象类I和多个产品的方法C1,C2,C3，C1,C2,C3创建的也是抽象类型，定义一个抽象类I的实现A，使用的时候分别调用A.C1(),A.C2(),A.C3()。
> - 工厂方法模式： 只有一个抽象产品类，具体工厂类只能创建一个具体产品类的实例 
> - 抽象工厂模式： 有多个抽象产品类 ，具体工厂类能创建多个具体产品类的实例

> 单例模式: 懒汉，饿汉，双重校验，静态内部类，枚举
# Spring
- 为什么要用Spring？
> 说到Spring肯定离不开它的两大特性AOP和IOC。
> - IOC：把我们的类上交，由Spring来进行统一的管理和配置，在需要使用的地方注入。好处是减少了各个类之间的相互依赖，依赖控制交给Spring管理。
> - AOP：封装了jdk和cglib的动态代理，结合IOC提供了更方便的增强类的方法。
- 没有Spring会怎么样？
> - 想知道为什么使用，最好的办法就是想想如果没有会怎样，没有手机、没有电脑、没有操作系统……。没有Spring框架。
如果没有Spring，我们不得不在使用每个类之前，实例化一个对象。当然我们可以用工厂方法来做这件事，就可以集中管理并且让调用者和被调用者之间的耦合更松散。于是需要大量的工厂类，并且在增加或改变接口实现的时候，还需要对工厂进行调整。而Spring就像一个大工厂一样，使用了大量的反射机制来生成需要实例的对象。
> - 除此之外Spring还带来了强大的代理，我们使用的每个注入的对象都是经过代理的增强对象，同时可以使用aop包来定义一些与业务逻辑不相关的切面。增强功能模块的内聚，拆分功能模块和非业务模块。而AOP又是建立在IOP基础之上，因此如果没有Spring，功能模块和非功能模块混在一起，导致逻辑混乱不清晰。

> - 为什么要用Spring
    现在已经很清晰了，用Spring可以让各个模块耦合更松散，可以在业务逻辑之外进行增强代理，实现非业务功能。所以就算没了Spring，也会有类似的其他框架来实现这些目的，而现在Spring的生态比较大，社区又比较活跃，为什么不用呢？
- 解释一下 Spring Aop？
> https://www.cnblogs.com/songanwei/p/9417343.html

> 这种在运行时，动态地将代码切入到类的指定方法、指定位置上的编程思想就是面向切面的编程。AOP是Spring提供的关键特性之一。AOP即面向切面编程，是OOP编程的有效补充。使用AOP技术，可以将一些系统性相关的编程工作，独立提取出来，独立实现，然后通过切面切入进系统。从而避免了在业务逻辑的代码中混入很多的系统相关的逻辑——比如权限管理，事物管理，日志记录等等。这些系统性的编程工作都可以独立编码实现，然后通过AOP技术切入进系统即可。从而达到了 将不同的关注点分离出来的效果。
> 1. AOP相关的概念
> 1) Aspect ：切面，切入系统的一个切面。比如事务管理是一个切面，权限管理也是一个切面；
> 2) Join point ：连接点，也就是可以进行横向切入的位置；
> 3) Advice ：通知，切面在某个连接点执行的操作(分为: Before advice , After returning advice , After throwing advice , After (finally) advice , Around advice )；
> 4) Pointcut ：切点，符合切点表达式的连接点，也就是真正被切入的地方；
> 2. AOP 的实现原理
> - AOP分为静态AOP和动态AOP。静态AOP是指AspectJ实现的AOP，他是将切面代码直接编译到Java类文件中。动态AOP是指将切面代码进行动态织入实现的AOP。Spring的AOP为动态AOP，实现的技术为： JDK提供的动态代理技术 和 CGLIB(动态字节码增强技术) 。尽管实现技术不一样，但 都是基于代理模式 ， 都是生成一个代理对象 。
> - 实现方式，JDK动态代理，InvocationHandler接口和Proxy.newProxyInstance() 方法；CGLIB ，字节码生成技术实现AOP，其实就是继承被代理对象，然后Override需要被代理的方法，在覆盖该方法时，自然是可以插入我们自己的代码的。
> - DefaultAopProxyFactory.java
```
@Override
	public AopProxy createAopProxy(AdvisedSupport config) throws AopConfigException {
		if (config.isOptimize() || config.isProxyTargetClass() || hasNoUserSuppliedProxyInterfaces(config)) {
			Class<?> targetClass = config.getTargetClass();
			if (targetClass == null) {
				throw new AopConfigException("TargetSource cannot determine target class: " +
						"Either an interface or a target is required for proxy creation.");
			}
			if (targetClass.isInterface() || Proxy.isProxyClass(targetClass)) {
				return new JdkDynamicAopProxy(config);
			}
			return new ObjenesisCglibAopProxy(config);
		}
		else {
			return new JdkDynamicAopProxy(config);
		}
	}
```
- 说一下什么是IOC/DI？
> https://www.cnblogs.com/xdp-gacl/p/4249939.html

> Ioc—Inversion of Control，即“控制反转”，不是什么技术，而是一种设计思想。在Java开发中，Ioc意味着将你设计好的对象交给容器控制，而不是传统的在你的对象内部直接控制。如何理解好Ioc呢？理解好Ioc的关键是要明确“谁控制谁，控制什么，为何是反转（有反转就应该有正转了），哪些方面反转了”。
> * 谁控制谁，控制什么：传统Java SE程序设计，我们直接在对象内部通过new进行创建对象，是程序主动去创建依赖对象；而IoC是有专门一个容器来创建这些对象，即由Ioc容器来控制对 象的创建；谁控制谁？当然是IoC 容器控制了对象；控制什么？那就是主要控制了外部资源获取（不只是对象包括比如文件等）。
> * 为何是反转，哪些方面反转了：有反转就有正转，传统应用程序是由我们自己在对象中主动控制去直接获取依赖对象，也就是正转；而反转则是由容器来帮忙创建及注入依赖对象；为何是反转？因为由容器帮我们查找及注入依赖对象，对象只是被动的接受依赖对象，所以是反转；哪些方面反转了？依赖对象的获取被反转了。
> * IoC 不是一种技术，只是一种思想，一个重要的面向对象编程的法则，它能指导我们如何设计出松耦合、更优良的程序。传统应用程序都是由我们在类内部主动创建依赖对象，从而导致类与类之间高耦合，难于测试；有了IoC容器后，把创建和查找依赖对象的控制权交给了容器，由容器进行注入组合对象，所以对象与对象之间是 松散耦合，这样也方便测试，利于功能复用，更重要的是使得程序的整个体系结构变得非常灵活。
> * 其实IoC对编程带来的最大改变不是从代码上，而是从思想上，发生了“主从换位”的变化。应用程序原本是老大，要获取什么资源都是主动出击，但是在IoC/DI思想中，应用程序就变成被动的了，被动的等待IoC容器来创建并注入它所需要的资源了。
> * IoC很好的体现了面向对象设计法则之一—— 好莱坞法则：“别找我们，我们找你”；即由IoC容器帮对象找相应的依赖对象并注入，而不是由对象主动去找。

> DI—Dependency Injection，即“依赖注入”：组件之间依赖关系由容器在运行期决定，形象的说，即由容器动态的将某个依赖关系注入到组件之中。依赖注入的目的并非为软件系统带来更多功能，而是为了提升组件重用的频率，并为系统搭建一个灵活、可扩展的平台。通过依赖注入机制，我们只需要通过简单的配置，而无需任何代码就可指定目标需要的资源，完成自身的业务逻辑，而不需要关心具体的资源来自何处，由谁实现。

> IoC和DI由什么关系呢？其实它们是同一个概念的不同角度描述，由于控制反转概念比较含糊（可能只是理解为容器控制对象这一个层面，很难让人想到谁来维护对象关系），所以2004年大师级人物Martin Fowler又给出了一个新的名字：“依赖注入”，相对IoC 而言，“依赖注入”明确描述了“被注入对象依赖IoC容器配置依赖对象”。
- Spring中的Bean在什么时候被实例化？
> - 如果你使用BeanFactory作为Spring Bean的工厂类，则所有的bean都是在第一次使用该Bean的时候实例
> - 如果你使用ApplicationContext作为Spring Bean的工厂类，则又分为以下几种情况：
> 1) 如果bean的scope是singleton的，并且lazy-init为false（默认是false，所以可以不用设置），则 ApplicationContext启动的时候就实例化该Bean，并且将实例化的Bean放在一个map结构的缓存中，下次再使 用该 Bean的时候，直接从这个缓存中取
> 2) 如果bean的scope是singleton的，并且lazy-init为true，则该Bean的实例化是在第一次使用该Bean的时候进 行实例化
> 3) 如果bean的scope是prototype的，则该Bean的实例化是在第一次使用该Bean的时候进行实例化

- spring常用的三种依赖注入方式？
> 1. 构造器注入，在构造方法上加上`@Autowired`
> 2. setter注入(方法参数注入)，在方法上加上`@Autowired`
> 3. 字段注入（接口注入），在字段上加上`@Autowired`

> `@Autowired`和`@Resource`的区别：`@Autowired`默认按照类型匹配，如果需要按照名称匹配与`@Qualifier`组合使用；`@Resource`默认按照名称匹配，如果没有指定名称，会先进行默认名称匹配在进行类型匹配。
- spring 中的 bean 是线程安全的吗？
> Spring容器中的Bean是否线程安全，容器本身并没有提供Bean的线程安全策略，因此可以说spring容器中的Bean本身不具备线程安全的特性，但是具体还是要结合具体scope的Bean去研究。

> 对于原型Bean,每次创建一个新对象，也就是线程之间并不存在Bean共享，自然是不会有线程安全的问题。
对于单例Bean,所有线程都共享一个单例实例Bean,因此是存在资源的竞争。
如果单例Bean,是一个无状态Bean，也就是线程中的操作不会对Bean的成员执行查询以外的操作，那么这个单例Bean是线程安全的。
比如spring mvc 的 Controller、Service、Dao等，这些Bean大多是无状态的，只关注于方法本身。
对于有状态的bean，spring官方提供的bean，一般提供了通过ThreadLocal去解决线程安全的方法。
比如RequestContextHolder、TransactionSynchronizationManager、LocaleContextHolder等。
- Spring中Bean的五个作用域？
> 当通过spring容器创建一个Bean实例时，不仅可以完成Bean实例的实例化，还可以为Bean指定特定的作用域。Spring支持如下5种作用域：
> - singleton：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例
> - prototype：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例

> - request：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效

> - session：对于每次HTTP Session，使用session定义的Bean豆浆产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效

> - globalsession：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效

> 其中比较常用的是singleton和prototype两种作用域。对于singleton作用域的Bean，每次请求该Bean都将获得相同的实例。容器负责跟踪Bean实例的状态，负责维护Bean实例的生命周期行为；如果一个Bean被设置成prototype作用域，程序每次请求该id的Bean，Spring都会新建一个Bean实例，然后返回给程序。在这种情况下，Spring容器仅仅使用new 关键字创建Bean实例，一旦创建成功，容器不在跟踪实例，也不会维护Bean实例的状态。

> 如果不指定Bean的作用域，Spring默认使用singleton作用域。Java在创建Java实例时，需要进行内存申请；销毁实例时，需要完成垃圾回收，这些工作都会导致系统开销的增加。因此，prototype作用域Bean的创建、销毁代价比较大。而singleton作用域的Bean实例一旦创建成功，可以重复使用。因此，除非必要，否则尽量避免将Bean被设置成prototype作用域。
- Spring自动装配Bean的方式有哪些？
> XML方式与注解方式
> - byName
> - byType
> - constructor
> - autodetect
- Spring事务管理之几种方式实现事务？
> https://blog.csdn.net/chinacr07/article/details/78817449
> https://blog.csdn.net/baidu_36327010/article/details/79632915
> - 事务认识
> 1) 原子性（Atomicity）
事务最基本的操作单元，要么全部成功，要么全部失败，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚到事务开始前的状态，就像这个事务从来没有执行过一样。
> 2) 一致性（Consistency）
事务的一致性指的是在一个事务执行之前和执行之后数据库都必须处于一致性状态。如果事务成功地完成，那么系统中所有变化将正确地应用，系统处于有效状态。如果在事务中出现错误，那么系统中的所有变化将自动地回滚，系统返回到原始状态。
> 3) 隔离性（Isolation）
指的是在并发环境中，当不同的事务同时操纵相同的数据时，每个事务都有各自的完整数据空间。由并发事务所做的修改必须与任何其他并发事务所做的修改隔离。事务查看数据更新时，数据所处的状态要么是另一事务修改它之前的状态，要么是另一事务修改它之后的状态，事务不会查看到中间状态的数据。
> 4) 持久性（Durability）
指的是只要事务成功结束，它对数据库所做的更新就必须永久保存下来。即使发生系统崩溃，重新启动数据库系统后，数据库还能恢复到事务成功结束时的状态。
> - 事务的传播特性
> 1) propagation_requierd：如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这个事务中，这是Spring默认的选择。
> 2) propagation_supports：支持当前事务，如果没有当前事务，就以非事务方法执行。
> 3) propagation_mandatory：使用当前事务，如果没有当前事务，就抛出异常。
> 4) propagation_required_new：新建事务，如果当前存在事务，把当前事务挂起。
> 5) propagation_not_supported：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
> 6) propagation_never：以非事务方式执行操作，如果当前事务存在则抛出异常。
> 7) propagation_nested：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与propagation_required类似的操作。
> - 事务的隔离级别
> https://www.cnblogs.com/huanongying/p/7021555.html
> 1) read uncommited：是最低的事务隔离级别，它允许另外一个事务可以看到这个事务未提交的数据。
> 2) read commited：保证一个事物提交后才能被另外一个事务读取。另外一个事务不能读取该事物未提交的数据。**只要是当前语句执行前已经提交的数据都是可见的。**
> 3) repeatable read：这种事务隔离级别可以防止脏读，不可重复读。但是可能会出现幻象读。它除了保证一个事务不能被另外一个事务读取未提交的数据之外还避免了以下情况产生（不可重复读）。**只要是当前事务执行前已经提交的数据都是可见的**
> 4) serializable：这是花费最高代价但最可靠的事务隔离级别。事务被处理为顺序执行。除了防止脏读，不可重复读之外，还避免了幻象读
> 5) 脏读、不可重复读、幻象读概念说明：
>    - 脏读：指当一个事务正字访问数据，并且对数据进行了修改，而这种数据还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。因为这个数据还没有提交那么另外一个事务读取到的这个数据我们称之为脏数据。依据脏数据所做的操作肯能是不正确的。
>    - 不可重复读：指在一个事务内，多次读同一数据。在这个事务还没有执行结束，另外一个事务也访问该同一数据，那么在第一个事务中的两次读取数据之间，由于第二个事务的修改第一个事务两次读到的数据可能是不一样的，这样就发生了在一个事物内两次连续读到的数据是不一样的，这种情况被称为是不可重复读。
>    - 幻象读：一个事务先后读取一个范围的记录，但两次读取的纪录数不同，我们称之为幻象读（两次执行同一条 select 语句会出现不同的结果，第二次读会增加一数据行，并没有说这两次执行是在同一个事务中）
>    - 可重复读,快照读和当前读。https://www.cnblogs.com/TeyGao/p/7846695.html
>    - Record Lock,Gap Lock,Next-Key Lock
>    - https://www.cnblogs.com/songwenjie/p/8643684.html
>    - https://www.cnblogs.com/songwenjie/p/8643684.html
>    - https://wangxinchun.iteye.com/blog/2341296
>    - https://www.cnblogs.com/hellopretty/p/5020093.html
>    - InnoDB存储引擎MVCC的工作原理
>    - https://my.oschina.net/xinxingegeya/blog/505675
>    - https://www.colabug.com/5354263.html
>    - https://blog.csdn.net/u013360850/article/details/86030084

> - 事务几种实现方式
> 1) 编程式事务管理对基于 POJO 的应用来说是唯一选择。我们需要在代码中调用beginTransaction()、commit()、rollback()等事务管理相关的方法，这就是编程式事务管理。
> 2) 基于 TransactionProxyFactoryBean的声明式事务管理
> 3) 基于 @Transactional 的声明式事务管理
> 4) 基于Aspectj AOP配置事务
- Spring的PROPAGATION_NESTED和PROPAGATION_REQUIRES_NEW的区别？
> https://blog.csdn.net/z69183787/article/details/76208998
> https://www.iteye.com/topic/35907
> https://sharajava.iteye.com/blog/78270
> 1. PROPAGATION_REQUIRES_NEW，原有事务B新起事务A，事务A中的commit和rollback不会影响外部事务B的commit和rollback，相互独立，如果事务A抛出异常，肯定会影响外部是B的。
> 2. PROPAGATION_NESTED，表示嵌套事务，看如下示例:
```
ServiceA {  
    /** 
     * 事务属性配置为 PROPAGATION_REQUIRED 
     */  
    @Transactional(propagation=Propagation.REQUIRED) // 1
    void methodA() {
        insertData(); //2
        try {
            ServiceB.methodB();   //3
        } catch (SomeException) {  
            // 执行其他业务, 如 ServiceC.methodC();   //5
        }
        updateData(); //6
    }  
}
ServiceB {
    
    @Transactional(propagation=Propagation.NESTED)
    void methodB(){
        //
        updateData(); //4
    }
}
```
> 在上面的1，将开起新事务A，2的时候会插入数据，此时事务A挂起，没有commit，3的时候，使用**PROPAGATION_NESTED**传播，将在3点的时候新建一个savepoint保存2插入的数据，不提交。
> 1. 如果methodB出现异常，将回滚4的操作，不影响2的操作，同时可以处理后面的5,6逻辑，最后一起commit: 2,5,6
> 2. 如果methodB没有出现异常，那么将一起commit: 2,4,6。
> 3. 假如methodB使用的**PROPAGATION_REQUIRES_NEW**，那么B异常，会commit: 2,5,6，和NESTED一致，如果methodB没有出现异常，那么会先commit4，再commit:6，那么事务将分离开，不能保持一致，假如执行6报错，2和6将回滚，而4却没有被回滚，不能达到预期效果。
- 说一下SpringMVC处理请求流程？
> https://blog.csdn.net/qq_31279347/article/details/82462421
> https://blog.csdn.net/zhangjun665635/article/details/71122989
> - DispatcherServlet前端控制器接收发过来的请求，交给HandlerMapping处理器映射器
> - HandlerMapping处理器映射器，根据请求路径找到相应的HandlerAdapter处理器适配器（处理器适配器就是那些拦截器或Controller）
> - HandlerAdapter处理器适配器，处理一些功能请求，返回一个ModelAndView对象（包括模型数据、逻辑视图名）
> - ViewResolver视图解析器，先根据ModelAndView中设置的View解析具体视图
> - 然后再将Model模型中的数据渲染到View上
> - 这些过程都是以DispatcherServlet为中轴线进行的。
- Spring mvc 有哪些组件？
> https://www.jianshu.com/p/a728acd817b7
> - HandlerMapping 我们可以看到HandlerMapping接口中只定义了一个方法，就是通过request找到HandlerExecutionChain，而HandlerExecutionChain包装了一个Handler和一组Interceptors。
> - HandlerAdapter 之所以需要HandlerAdapter是因为Spring MVC没有对Handler做任何规定，它可以是类，可以是方法，也可以是任何其他东西，我们可以看到Handler的类型是Object，这样会非常灵活。但是怎么让任意类型的Handler处理固定格式的请求呢？没错，就是使用适配器，每种Handler都要有对应的HandlerAdapter才能处理请求。我们来看下HandlerAdapter接口的定义。
> - HandlerExceptionResolver 在处理请求的过程中，难免会出现异常，HandlerExceptionResolver就是专门来处理异常的组件，它能根据异常设置ModelAndView，然后交给render进行渲染。我们来看下HandlerExceptionResolver的接口定义
> - ViewResolver ViewResolver用来将String类型的视图名和本地化信息Local解析成View类型的视图
> - RequestToViewNameTranslator ViewResolver是根据viewName查找View，但有的Handler处理完后并没有设置View也没有设置viewName，这时就需要RequestToViewNameTranslator从request中找到默认的View了
> - LocalResolver
> - ThemeResolver
> - MultipartResolver
> - FlashMapManager
- SpringMVC的拦截器（Interceptor）和过滤器（Filter）的区别与联系？
> https://blog.csdn.net/xiaoyaotan_111/article/details/53817918
> - 过滤器 依赖于servlet容器。在实现上基于函数回调，可以对几乎所有请求进行过滤，但是缺点是一个过滤器实例只能在容器初始化时调用一次。使用过滤器的目的是用来做一些过滤操作，获取我们想要获取的数据，比如：在过滤器中修改字符编码；在过滤器中修改HttpServletRequest的一些参数，包括：过滤低俗文字、危险字符等
> - 拦截器 依赖于web框架，在SpringMVC中就是依赖于SpringMVC框架。在实现上基于Java的反射机制，属于面向切面编程（AOP）的一种运用。由于拦截器是基于web框架的调用，因此可以使用Spring的依赖注入（DI）进行一些业务操作，同时一个拦截器实例在一个controller生命周期之内可以多次调用。但是缺点是只能对controller请求进行拦截，对其他的一些比如直接访问静态资源的请求则没办法进行拦截处理

# Spring Boot/Spring Cloud
- 什么是 spring boot？
> https://www.cnblogs.com/hcw110/p/9786451.html

> Spring Boot 是由 Pivotal 团队提供的全新框架，其设计目的是用来简化新 Spring 应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。用我的话来理解，就是 Spring Boot 其实不是什么新的框架，它默认配置了很多框架的使用方式，就像 maven 整合了所有的 jar 包，Spring Boot 整合了所有的框架（不知道这样比喻是否合适）。

> Spring Boot 简化了基于 Spring 的应用开发，通过少量的代码就能创建一个独立的、产品级别的 Spring 应用。 Spring Boot 为 Spring 平台及第三方库提供开箱即用的设置，这样你就可以有条不紊地开始。Spring Boot 的核心思想就是约定大于配置，多数 Spring Boot 应用只需要很少的 Spring 配置。采用 Spring Boot 可以大大的简化你的开发模式，所有你想集成的常用框架，它都有对应的组件支持。
- 为什么要使用Spring Boot？
> Spring Boot 让开发变得更简单
> Spring Boot 使测试变得更简单
> Spring Boot 让配置变得更简单
> Spring Boot 让部署变得更简单
> Spring Boot 让监控变得更简单
- Spring Boot 核心注解与配置文件？
> - 入口类与`@SpringBootApplication`注解，Spring Boot项目都会有一个*Application 类，这个类作为Spring Boot 项目的入口类，在这个入口类中有main 方法，如果我们想要运行该项目，可以在该入口类中run 我们的项目。
```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
```
> - 关闭自动配置 在默认的情况下，Spring Boot会根据项目中的jar包依赖，自动做出配置，Spring Boot支持的自动配置非常多。如果我们想要关闭一些自动配置的话，我们可以通过手动修改核心注解配置我们不想要自动配置的jar 包。比如(但是一般我们不这么做)：
```
@SpringBootApplication(exclude = {DispatcherServlet.class})
```
> - 自定义Banner 在我们启动Spring Boot 项目的时候会在控制台输出一个SPRING 的图案。我们可以对这个图案做出修改也可以关闭输出图案。 
> - Spring Boot 全局配置文件 pring Boot项目使用一个全局的配置文件application.properties或者是application.yml，在resources目录下或者类路径下的/config下，一般我们放到resources下。在这个配置文件中你可以做一些服务器与Spring 的相关配置以及日志打印等等(在这个配置文件中可以作大量的配置)。
> - Xml 配置文件 虽然Spring Boot 已经为我们做了很多的配置，但是如果在相关的项目中你仍然需要xml 文件做一些额外的配置，那么Spring Boot 也是支持的。你可以在入口类通过@ImportResource 进行xml 配置文件的导入并且支持对多个xml 文件的配置。
```
@ImportResource({"classpath:scio-*.xml","classpath:**.xml"})
```
> Spring Boot配置文件详解 https://www.cnblogs.com/itdragon/p/8686554.html
- SpringBoot热部署四种方式
> 1. 模板引擎 在Spring Boot中开发情况下禁用模板引擎的cache
页面模板改变ctrl+F9可以重新编译当前页面并生效
> 2. Spring Loaded Spring官方提供的热部署程序，实现修改类文件的热部署
下载Spring Loaded（项目地址https://github.com/spring-projects/spring-loaded）
添加运行时参数；
-javaagent:C:/springloaded-1.2.5.RELEASE.jar –noverify
> 3. JRebel 收费的一个热部署软件安装插件使用即可
> 4. Spring Boot Devtools
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>
IDEA使用ctrl+F9或做一些小调整
Intellij IEDA和Eclipse不同，Eclipse设置了自动编译之后，修改类它会自动编译，而IDEA在非RUN或DEBUG情况下才会自动编译（前提是你已经设置了Auto-Compile）。
设置自动编译（settings-compiler-make project automatically）

ctrl+shift+alt+/（maintenance）
勾选
compiler.automake.allow.when.app.running
```
- jpa 和 hibernate 有什么区别？
> 1. 什么是Java Persistence API？Java Persistence API提供了一个规范，用于将数据通过Java对象持久化、读取和管理到数据库中的关系表。
> 2. 什么是Hibernate框架？Hibernate是Java环境的对象关系映射解决方案。对象关系映射或ORM是将应用程序域模型对象映射到关系数据库表的编程技术。Hibernate是一个基于Java的ORM工具，它提供了一个框架，用于将应用程序域对象映射到关系数据库表，反之亦然。

> Hibernate提供了Java Persistence API的参考实现，使其成为具有松散耦合优势的ORM工具的绝佳选择。请注意，JPA是一个规范，Hibernate是一个JPA提供者或实现。

- Hibernate和Spring Data JPA有什么区别？
> https://cloud.tencent.com/developer/ask/113708
> - Hibernate是一个JPA实现，而Spring Data JPA是一个JPA数据访问抽象。Spring Data提供了GenericDao自定义实现的解决方案，它还可以通过方法名称约定代表您生成JPA查询。
> - 通过Spring Data，您可以使用Hibernate、Eclipse Link或任何其他JPA提供程序。一个非常有趣的好处是您可以使用@Transactional注释以声明方式控制事务边界。
- SpringCloud是什么？
> https://www.cnblogs.com/lexiaofei/p/6808152.html
> 1. Spring Cloud是一个微服务框架，相比Dubbo等RPC框架, Spring Cloud提供的全套的分布式系统解决方案。 
> 2. Spring Cloud对微服务基础框架Netflix的多个开源组件进行了封装，同时又实现了和云端平台以及和Spring Boot开发框架的集成。 
> 3. Spring Cloud为微服务架构开发涉及的配置管理，服务治理，熔断机制，智能路由，微代理，控制总线，一次性token，全局一致性锁，leader选举，分布式session，集群状态管理等操作提供了一种简单的开发方式。
> 4. Spring Cloud 为开发者提供了快速构建分布式系统的工具，开发者可以快速的启动服务或构建应用、同时能够快速和云平台资源进行对接。 
- Spring Cloud的中的断路器是什么？
> Spring Cloud断路器Hystrix，断路器模式源于Martin Fowler的Circuit Breaker一文。“断路器”本身是一种开关装置，用于在电路上保护线路过载，当线路中有电器发生短路时，“断路器”能够及时的切断故障电路，防止发生过载、发热、甚至起火等严重后果。

> 在分布式架构中，断路器模式的作用也是类似的，当某个服务单元发生故障（类似用电器发生短路）之后，通过断路器的故障监控（类似熔断保险丝），向调用方返回一个错误响应，而不是长时间的等待。这样就不会使得线程因调用故障服务被长时间占用不释放，避免了故障在分布式系统中的蔓延。
- SpringCloud五大核心组件？
> https://blog.csdn.net/springML/article/details/82492643
> - 服务发现——Netflix Eureka
> - 客服端负载均衡——Netflix Ribbon
> - 断路器——Netflix Hystrix
> - 服务网关——Netflix Zuul
> - 分布式配置——Spring Cloud Config

# Hibernate
- 什么是ORM？
> https://blog.csdn.net/cillyb/article/details/79464374
> - ORM，即Object-Relational Mapping（对象关系映射），它的作用是在关系型数据库和业务实体对象之间作一个映射，这样，我们在具体的操作业务对象的时候，就不需要再去和复杂的SQL语句打交道，只需简单的操作对象的属性和方法。

- Hibernate工作原理及为什么要用？
> https://www.cnblogs.com/dashi/p/3597969.html
> - hibernate是一个开源框架，它是对象关联关系映射的框架，它对JDBC做了轻量级的封装，而我们java程序员可以使用面向对象的思想来操纵数据库。
> - hibernate核心接口
> 1. session：负责被持久化对象CRUD操作
> 2. sessionFactory:负责初始化hibernate，创建session对象
> 3. configuration:负责配置并启动hibernate，创建SessionFactory
> 4. Transaction:负责事物相关的操作
> 5. Query和Criteria接口：负责执行各种数据库查询
```
hibernate工作原理：
1.通过Configuration config = new Configuration().configure();//读取并解析hibernate.cfg.xml配置文件
2.由hibernate.cfg.xml中的<mapping resource="com/xx/User.hbm.xml"/>读取并解析映射信息
3.通过SessionFactory sf = config.buildSessionFactory();//创建SessionFactory
4.Session session = sf.openSession();//打开Sesssion
5.Transaction tx = session.beginTransaction();//创建并启动事务Transation
6.persistent operate操作数据，持久化操作
7.tx.commit();//提交事务
8.关闭Session
9.关闭SesstionFactory
```
> - 为什么要用hibernate：
> 1. 对JDBC访问数据库的代码做了封装，大大简化了数据访问层繁琐的重复性代码。
> 2. Hibernate是一个基于JDBC的主流持久化框架，是一个优秀的ORM实现。他很大程度的简化DAO层的编码工作
> 3. hibernate使用Java反射机制，而不是字节码增强程序来实现透明性。
> 4. hibernate的性能非常好，因为它是个轻量级框架。映射的灵活性很出色。它支持各种关系数据库，从一对一到多对多的各种复杂关系。

- Hibernate在控制台打印sql语句以及参数？
> https://blog.csdn.net/Randy_Wang_/article/details/79460306
```
spring.jpa.properties.hibernate.show_sql=true //控制台是否打印
spring.jpa.properties.hibernate.format_sql=true //格式化sql语句
spring.jpa.properties.hibernate.use_sql_comments=true //指出是什么操作生成了该语句
```
- hibernate 六种查询方法？
> https://blog.csdn.net/HandSome_He/article/details/79234160
> 1. HQL查询(适用情况：常用方法，比较传统，类似jdbc。缺点：新的查询语言，适用面有限，仅适用于Hibernate框架)
> 2. 对象化查询Criteria方法(适用情况：面向对象操作，革新了以前的数据库操作方式，易读。缺点：适用面较HQL有限。)
> 3. 动态查询DetachedCriterid(适用情况：面向对象操作，分离业务与底层，不需要字段属性摄入到Dao实现层。  缺点：适用面较HQL有限。)
> 4. 例子查询(适用情况：面向对象操作。   缺点：适用面较HQL有限，不推荐。)
> 5. SQL查询(适用情况：不熟悉HQL的朋友，又不打算转数据库平台的朋友，万能方法   缺点：破坏跨平台，不易维护，不面向对象。)
> 6. 命名查询(适用情况：万能方法，有点像ibatis轻量级框架的操作，方便维护。  缺点：不面向对象。基于hql和sql，有一定缺陷。)
- Hibernate实体类创建注意事项？可以使用final修饰实体类吗？
> 1. 持久化类必须有无参的构造函数，因为反射的原因。
> 2. 要有set/get方法
> 3. 使用包装类型，解决数据库中值为null的问题
> 4. 持久化类需要提供id与数据库中的主键相对应
> 5. 不要用finall修饰class（hibernate是使用cglib代理生成的代理对象），但是依然可以保存成功，但是无法生成代理优化对象。
- 在 hibernate 中使用 Integer 和 int 做映射有什么区别？
> 数据库中字段为null，转换为int时，会空指针错误。
- Hibernate工作原理？
> https://www.cnblogs.com/bile/p/4030575.html
> 1) SessionFactory：这是Hibernate的关键对象，它是单个数据库映射关系经过编译后的内存镜像，它也是线程安全的。它是生成Session的工厂，本身要应用到ConnectionProvider，该对象可以在进程和集群的级别上，为那些事务之间可以重用的数据提供可选的二级缓存。
> 2) Session：它是应用程序和持久存储层之间交互操作的一个单线程对象。它也是Hibernate持久化操作的关键对象，所有的持久化对象必须在Session的管理下才能够进行持久化操作。此对象的生存周期很短，其隐藏了JDBC连接，也是Transaction 的工厂。Session对象有一个一级缓存，现实执行Flush之前，所有的持久化操作的数据都在缓存中Session对象处。
> 3) 持久化对象：系统创建的POJO实例一旦与特定Session关联，并对应数据表的指定记录，那该对象就处于持久化状态，这一系列的对象都被称为持久化对象。程序中对持久化对象的修改，都将自动转换为持久层的修改。持久化对象完全可以是普通的Java Beans/POJO，唯一的特殊性是它们正与Session关联着。
> 4) 瞬态对象和脱管对象：系统进行new关键字进行创建的Java 实例，没有Session 相关联，此时处于瞬态。瞬态实例可能是在被应用程序实例化后，尚未进行持久化的对象。如果一个曾今持久化过的实例，但因为Session的关闭而转换为脱管状态。
> 5) 事务(Transaction)：代表一次原子操作，它具有数据库事务的概念。但它通过抽象，将应用程序从底层的具体的JDBC、JTA和CORBA事务中隔离开。在某些情况下，一个Session 之内可能包含多个Transaction对象。虽然事务操作是可选的，但是所有的持久化操作都应该在事务管理下进行，即使是只读操作。
> 6) 连接提供者(ConnectionProvider)：它是生成JDBC的连接的工厂，同时具备连接池的作用。他通过抽象将底层的DataSource和DriverManager隔离开。这个对象无需应用程序直接访问，仅在应用程序需要扩展时使用。
> 7) 事务工厂(TransactionFactory)：他是生成Transaction对象实例的工厂。该对象也无需应用程序的直接访问。Hibernate进行持久化操作离不开SessionFactory对象，这个对象是整个数据库映射关系经过编译后的内存镜像，该对象的openSession()方法可打开Session对象。SessionFactory对想是由Configuration对象产生。每个Hibernate配置文件对应一个configuration对象。在极端情况下，不使用任何配置文件，也可以创建Configuration对象。
- get()和 load()的区别？
> 1. 查询的时机不一样，get方法任何时刻都是立即加载，只要调用get方法，就马上发起数据库查询。
> 1) load方法默认情况下是延迟加载，真正用到对象的非OID字段数据才发起查询。
> 2) load方法是可以通过配置的方式改为立即加载。
> 3) 配置的方式，由于load方法是hibernate的方法所以只有XML的方式：
    <classname="Customer" table="cst_customer"lazy="false">
> 2. 返回的结果不一样
>  1) get方法永远返回查询的实体类对象
>  2) load方法返回的是代理对象
>  3) 立即加载：是不管用不用马上查询。
>  4) 延迟加载：是等到真正用的时候才发起查询
- 说一下 hibernate 的缓存机制？
> https://blog.csdn.net/jsnhux/article/details/81117867
> https://www.cnblogs.com/xiaoluo501395377/p/3377604.html
> 1. N+1问题
> - list()方法会发送一条sql语句
> - iterator()方法会发送一条sql语句，同时在每次next的时候，再次发送用主键查询的sql语句，这就是N+1
> 2. 一级缓存(session级别)
> - 在同一个session中，多次查询同一个实体，只会发送一次sql语句查询。session关闭后，再次查询则会再次发送sql语句查询。
> 3. 二级缓存(sessionFactory级别)
> - hibernate并没有提供相应的二级缓存的组件，所以需要加入额外的二级缓存包，常用的二级缓存包是EHcache。这个我们在下载好的hibernate的lib->optional->ehcache下可以找到(我这里使用的hibernate4.1.7版本)，然后将里面的几个jar包导入即可。
> - 二级缓存的使用策略一般有这几种：read-only、nonstrict-read-write、read-write、transactional。注意：我们通常使用二级缓存都是将其配置成 read-only ，即我们应当在那些不需要进行修改的实体类上使用二级缓存，否则如果对缓存进行读写的话，性能会变差，这样设置缓存就失去了意义。
> 4. 查询缓存(sessionFactory级别)
> - 针对HQL，SQL进行查询缓存
- hibernate 对象有哪些状态？
> 1. Transient 瞬时 ：对象刚new出来，还没设id，设了其他值。
> 2. Persistent 持久：调用了save()、saveOrUpdate()，就变成Persistent，有id
> 3. Detached  脱管 ： 当session  close()完之后，变成Detached。
- Hibernate 中的 openSession和getCurrentSession 方法的区别？
> - openSession 从字面上可以看得出来，是打开一个新的session对象，而且每次使用都是打开一个新的session，假如连续使用多次，则获得的session不是同一个对象，并且使用完需要调用close方法关闭session。
> - getCurrentSession ，从字面上可以看得出来，是获取当前上下文一个session对象，当第一次使用此方法时，会自动产生一个session对象，并且连续使用多次时，得到的session都是同一个对象，这就是与openSession的区别之一，简单而言，getCurrentSession 就是：如果有已经使用的，用旧的，如果没有，建新的。
- hibernate 实体类必须要有无参构造函数吗？为什么？
> 因为一个对象new出来的时候，必须要使用无参构造函数，然后调用setter方法进行赋值。
# Mybatis

- Mybatis中#{}和${}的区别？
> `#{orderId}`会对orderId进行转义，增加引号，可以尽量防止sql注入
> `${pageSize}`不会对pageSize进行多余操作，原样拼接，主要用于表名，order by，limit等语句。
- Mybatis四种分页方式？
> 1. 读取出来，自己用subList分页
> 2. 在sql语句中些limit
> 3. 使用拦截器分页，`Interceptor`
> 4. 使用`RowBounds`
- RowBounds 是一次性查询全部结果吗？为什么？
> 是的，rowbounds实际上就是内存分页。
- mybatis逻辑分页与物理分页？
> 逻辑分页是把sql语句的查询内容全部读取，在内存中进行逻辑分页。物理分页是基于数据库的分页，通过rownum()、limit等方式进行分页查询。
- mybatis 是否支持延迟加载？延迟加载的原理是什么？
> mybatis支持延迟加载，需要开启配置，` <setting name="lazyLoadingEnabled" value="true"/>`。默认是关闭的，和hibernate一样，在需要加载依赖另一方的时候，才会向数据库发送查询语句进行查询。不同点是基于hibernate只有当访问了非主键的属性才会懒加载，mybatis会默认全部加载。
- mybatis 详解（九）------ 一级缓存、二级缓存？
> https://www.cnblogs.com/ysocean/p/7342498.html
- mybatis都有哪些Executor执行器？它们之间的区别是什么？
> SimpleExecutor、ReuseExecutor、BatchExecutor。
> - **SimpleExecutor**：每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。
> - **ReuseExecutor**：执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map内，供下一次使用。简言之，就是重复使用Statement对象。
> - **BatchExecutor**：执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。

> 与JDBC批处理相同。作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。
> - Mybatis中如何指定使用哪一种Executor执行器？
> 答：在Mybatis配置文件中，可以指定默认的ExecutorType执行器类型，也可以手动给DefaultSqlSessionFactory的创建SqlSession的方法传递ExecutorType类型参数。
- mybatis 分页插件的实现原理是什么？
- mybatis 如何编写一个自定义插件？

# RabbitMQ
- RabbitMQ的几种应用场景？
> https://www.cnblogs.com/luxiaoxun/p/3918054.html
> 1. 单发送单接收
> 2. 单发送多接收
> 3. Publish/Subscribe,发布订阅模式
> 4. Routing (按路线发送接收)
> 5. Topics (按topic发送接收)
- RabbitMQ的交换机类型？
> https://www.cnblogs.com/julyluo/p/6265775.html
> 1. direct exchange
> 2. topic exchange
> 3. fanout exchange
> 4. header exchange
- RabbitMQ的用户角色分类？
> * none
> * management
> * policymaker
> * monitoring
> * administrator
- RabbitMQ 如何保证消息不丢失？
> https://www.cnblogs.com/flyrock/p/8859203.html
> 1. **消息持久化**,Exchange 设置持久化,Queue 设置持久化,Message持久化发送：发送消息设置发送模式deliveryMode=2，代表持久化消息
> 2. **ACK确认机制**,这个使用就要使用Message acknowledgment 机制，就是消费端消费完成要通知服务端，服务端才把消息从内存删除
> 3. **设置集群镜像模式**,单节点模式,普通集群模式,镜像模式(复制数据到每个节点)
> 4. **消息补偿机制**，业务补偿
- 使用RabbitMQ实现延迟任务？
> https://www.cnblogs.com/haoxinyue/p/6613706.html
> https://blog.csdn.net/ujsleo/article/details/79225360
> 1. 消息的TTL（Time To Live）
> 2. Dead Letter Exchanges
> 3. 通过对队列或者消息设置TTL过期时间,同时绑定DLQ，消息过期后,会自动投递到DLQ，通过监听DLQ来实现延迟消息队列。
- rabbitmq集群操作与启停？
> https://blog.csdn.net/btnode/article/details/81564783
- rabbitmq集群操作顺序？
> http://new.nginxs.net/tag.php/rabbitmq%E9%9B%86%E7%BE%A4%E5%90%AF%E5%8A%A8%E9%A1%BA%E5%BA%8F/
> - 加入集群之前rabbitmq必须关闭app以免消息冲突（为了保证数据正常在形成集群的时候没有数据写入新节点）
集群的启动顺序，必须先启动硬盘节点然后然能启动内存节点（否则无法启动）
> - 当集群所有节点都停止运行的时候应该按照后停的服务先启动的顺序启动，否则将导致个别节点消息时空错乱

> - RabbitMQ 对集群的停止的顺序是有要求的，应该先关闭内存节点，最后再关闭磁盘节点。如果顺序恰好相反的话，可能会造成消息的丢失。

-  RabbitMQ 集群有什么用？
> - 高可用：某个服务器出现问题，整个 RabbitMQ 还可以继续使用；
> = 高容量：集群可以承载更多的消息量。
- RabbitMQ 节点的类型有哪些？
> - 磁盘节点：消息会存储到磁盘。
> - 内存节点：消息都存储在内存中，重启服务器消息丢失，性能高于磁盘类型。

- RabbitMQ 每个节点是其他节点的完整拷贝吗？为什么？
> 不是(**镜像模式除外**)，原因有以下两个：
> 1. 存储空间的考虑：如果每个节点都拥有所有队列的完全拷贝，这样新增节点不但没有新增存储空间，反而增加了更多的冗余数据；
> 2. 性能的考虑：如果每条消息都需要完整拷贝到每一个集群节点，那新增节点并没有提升处理消息的能力，最多是保持和单节点相同的性能甚至是更糟。

- RabbitMQ 集群中唯一一个磁盘节点崩溃了会发生什么情况？
> - 不能创建队列
> - 不能创建交换器
> - 不能创建绑定
> - 不能添加用户
> - 不能更改权限
> - 不能添加和删除集群节点
> > 唯一磁盘节点崩溃了，集群是可以保持运行的，但你不能更改任何东西。


# Kafka
- kafka 可以脱离 zookeeper 单独使用吗？为什么？
> 1. kafka单纯只是脱离zookeeper可以吗？
zookeeper只是个服务注册中心，如果kafka可以找到替代品换掉zookeeper是没有问题的。
现有的服务器注册中心有很多比如淘宝就有自已研发的服务注册中心产品。
所以如果用其他的服务注册中心系统换掉zookeeper是可行的（事实上zookeeper作为服务注册中心功能性并不是很理想），比如它的状态检测并不能真实反应broker的状态（可连接就一定是状态ok吗？不是吧。）。
> 2. kafka脱离zookeeper为代表的服务注册中心可以吗？
不可以，kafka的集群管理的核心是zookeeper虽然它并不完美（甚至缺点很多）。但是没了zk，kafka是不可用的。所以没有服务注册中心的kafka是不可用的。
- Kafka消息保留策略？
> Kafka Broker默认的消息保留策略是：要么保留一定时间，要么保留到消息达到一定大小的字节数。

> 当消息达到设置的条件上限时，旧消息就会过期并被删除，所以，在任何时刻，可用消息的总量都不会超过配置参数所指定的大小。

> topic可以配置自己的保留策略，可以将消息保留到不再使用他们为止。

> 因为在一个大文件里查找和删除消息是很费时的事，也容易出错，所以，分区被划分为若干个片段。默认情况下，每个片段包含1G或者一周的数据，以较小的那个为准。在broker往leader分区写入消息时，如果达到片段上限，就关闭当前文件，并打开一个新文件。当前正在写入数据的片段叫活跃片段。当所有片段都被写满时，会清除下一个分区片段的数据，如果配置的是7个片段，每天打开一个新片段，就会删除一个最老的片段，循环使用所有片段。
- kafka集群搭建注意事项？
> https://blog.csdn.net/jing_jing0909/article/details/82862541
- kafka 同时设置了 7 天和 10G 清除数据，到第五天的时候消息达到了 10G，这个时候 kafka 将如何处理？
> 这个时候 kafka 会执行数据清除工作，时间和大小不论那个满足条件，都会清空数据。
- 什么情况会导致 kafka 运行变慢？
> - cpu 性能瓶颈
> - 磁盘读写瓶颈
> - 网络瓶颈

- 使用 kafka 集群需要注意什么？
> - 集群的数量不是越多越好，最好不要超过 7 个，因为节点越多，消息复制需要的时间就越长，整个群组的吞吐量就越低。
> - 集群数量最好是单数，因为超过一半故障集群就不能用了，设置为单数容错率更高。

- kafka之六：为什么Kafka那么快
> https://www.cnblogs.com/duanxz/p/4705164.html

- 突发宕机，Kafka写入的数据如何保证不丢失？
> https://blog.csdn.net/z1941563559/article/details/88797272
# zookeeper
- zookeeper 是什么？
> https://blog.csdn.net/chengxuyuanyonghu/article/details/80403879

> ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现，是Hadoop和Hbase的重要组件。它是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。
- zookeeper 有几种部署模式？
> * 单机模式
> * 集群模式
> * 伪集群模式
- zookeeper原理（二）集群选主和同步
> https://blog.csdn.net/wutian713/article/details/53262616

> * 恢复模式，zookeeper配置为集群模式时，系统启动或者是当前leader崩溃或者是当前leader丢失大多数的follower,zk进入恢复模式,恢复模式需要重新选举出一个新的leader,当领导者被选举出来，且大多数Server的完成了和leader的状态同步以后，恢复模式就结束了。
> * 广播模式，状态同步保证了Leader和所有Server都具有相同的系统状态。这时候当Server加入Zookeeper集群后，会先在恢复模式下启动该Server，发现Leader后，并和Leader进行状态同步，待到同步结束，它也参与消息广播，即进入广播状态。Zookeeper服务一直维持在Broadcast状态，直到Leader崩溃了或者Leader失去了大部分的Followers支持，才会进入恢复模式，从新选举Leader。
- ZooKeeper为何要求分布式集群至少有3个节点？
> 在zookeeper的选举过程中，为了保证选举过程最后能选出leader，就一定不能出现两台机器得票相同的僵局，所以一般的，要求zk集群的server数量一定要是奇数，也就是2n+1台，并且，如果集群出现问题，其中存活的机器必须大于n+1台，否则leader无法获得多数server的支持，系统就自动挂掉。所以一般是3个或者3个以上节点。
- Zookeeper集群节点数量为什么要是奇数个？
> https://blog.csdn.net/u010476994/article/details/79806041
- 说一下 zookeeper 的通知机制？
> https://blog.csdn.net/u014636209/article/details/85475190
> https://blog.csdn.net/hohoo1990/article/details/78617336

> 这让我想到一种模式，观察者模式（发布订阅模式）：一个典型的发布/订阅模型系统定义了一种一对多的订阅关系，能够让多个订阅者同时监听某一个主题对象，当这个主题自身状态变化时，会通知所有订阅者，试它们能够做出相应的处理。那 ZooKeeper 是不是也是使用了这个经典的模式呢？

> 在 ZooKeeper 中，引入了 Watcher 机制来实现这种分布式的通知功能。ZooKeeper 允许客户端向服务端注册一个 Watcher 监听，当服务器的一些特定事件触发了这个 Watcher，那么就会向指定客户端发送一个事件通知来实现分布式的通知功能。
> 1. zookeeper提供了分布式数据发布和订阅功能,是一个典型的的发布/订阅模型系统;
> 2. zookeeper定义了一种一对多的订阅关系,能让多个订阅者同时监听某一个主题对象;
> 3. 当被监听的主题对象自身状态变化时,会通知所有订阅者,使他们能够做出相应的处理;
> 4. zookeeper中,引入Watcher机制来实现这种分布式通知功能;
> 5. zookeeper允许客户端想服务端注册一个Watcher监听,当服务端的一些事件触发了这个
  Watcher,那么久会想指定客户端发送一个事件通知来实现分布式的通知功能;
> 6. 触发的事件种类有:节点创建 节点删除 节点改变 子节点改变等;  

# MySql
- 数据库的三范式是什么？
> * 第一范式,每一列属性都是不可再分的属性值，确保每一列的原子性,两列的属性相近或相似或一样，尽量合并属性一样的列，确保不产生冗余数据。
> * 第二范式,每一行的数据只能与其中一列相关，即一行数据只做一件事。只要数据列中出现数据重复，就要把表拆分开来。一个人同时订几个房间，就会出来一个订单号多条数据，这样子联系人都是重复的，就会造成数据冗余。我们应该把他拆开来。
> * 第三范式,数据不能存在传递关系，即没个属性都跟主键有直接关系而不是间接关系。像：a-->b-->c  属性之间含有这样的关系，是不符合第三范式的。

> 比如Student表（学号，姓名，年龄，性别，所在院校，院校地址，院校电话）

> 这样一个表结构，就存在上述关系。 学号--> 所在院校 --> (院校地址，院校电话)

> 这样的表结构，我们应该拆开来，如下。
（学号，姓名，年龄，性别，所在院校）--（所在院校，院校地址，院校电话）

- 一张表里面有ID自增主键，当insert了17条记录之后，删除了第15,16,17条记录，再把mysql重启，再insert一条记录，这条记录的ID是18还是15 ？
> 一般情况下，我们创建的表的类型是InnoDB，如果新增一条记录（不重启mysql的情况下），这条记录的id是18；但是如果重启（文中提到的）MySQL的话，这条记录的ID是15。因为InnoDB表只把自增主键的最大ID记录到内存中，所以重启数据库或者对表OPTIMIZE操作，都会使最大ID丢失。

> 但是，如果我们使用表的类型是MylSAM，那么这条记录的ID就是18。因为MylSAM表会把自增主键的最大ID记录到数据文件里面，重启MYSQL后，自增主键的最大ID也不会丢失。

> 注：如果在这17条记录里面删除的是中间的几个记录（比如删除的是10,11,12三条记录），重启MySQL数据库后，insert一条记录后，ID都是18。因为内存或者数据库文件存储都是自增主键最大ID

- 怎么查询Mysql数据库的版本号？
> - SQL命令：`select version();`
> - 系统命令：`mysql -V`

- 说一下 ACID 是什么？
> 原子性(atomicity): 一个事物必须被视为一个不可分割的最小工作单元，整个事物中的操作要么全部提交成功，要么全部失败回滚，对于一个事物来说，不可能只执行其中的一部分操作，这就是的原子性。

> 一致性(consistency): 数据库总是从一个一致性的状态转到另一个事务的一致性状态。 由于事物的一致性，所以如果这时候执行完第三系统突然奔溃，支票账户也不会损失100，因为事物还没提交eg: 1 start transaction ; 2 select * from checking where id=1; 3 update checking set balance=balance-100 where id=1; 4 update savings set balance=balance+100 where id=1; 5 commit; 

> 隔离性(isolation):一个事物所做的修改在最终提交前，对其他事物是不可见的。在前面的例子中，如果执行到第3，此时有另一个账户汇款，则其看见的支票账户得余额并没有被减去100。

> 持久性(durability): 一旦事物提交，则其所做的修改就会永远保存在数据库中。

- varchar与char有什么区别？
> - **定长和变长**，char 表示定长，长度固定，varchar表示变长，即长度可变。char如果插入的长度小于定义长度时，则用空格填充；varchar小于定义长度时，还是按实际长度存储，插入多长就存多长。
> 因为其长度固定，char的存取速度还是要比varchar要快得多，方便程序的存储与查找；但是char也为此付出的是空间的代价，因为其长度固定，所以会占据多余的空间，可谓是以空间换取时间效率。varchar则刚好相反，以时间换空间。

> - **存储的容量不同**，对 char 来说，最多能存放的字符个数 255，和编码无关。而 varchar 呢，最多能存放 65532 个字符。varchar的最大有效长度由最大行大小和使用的字符集确定。整体最大长度是 65,532字节。

- float和double有什么区别？
> https://www.cnblogs.com/gulibao/p/5416245.html

> float数值类型用于表示单精度浮点数值，而double数值类型用于表示双精度浮点数值，float和double都是浮点型，而decimal是定点型；

> MySQL 浮点型和定点型可以用类型名称后加（M，D）来表示，M表示该值的总共长度，D表示小数点后面的长度，M和D又称为精度和标度，如float(7,4)的 可显示为-999.9999，MySQL保存值时进行四舍五入，如果插入999.00009，则结果为999.0001。

> FLOAT和DOUBLE在不指 定精度时，默认会按照实际的精度来显示，而DECIMAL在不指定精度时，默认整数为10，小数为0。

- mysql 索引是怎么实现的？
> https://blog.csdn.net/waeceo/article/details/78702584

> https://www.cnblogs.com/wlwl/p/9465583.html

> https://www.cnblogs.com/boothsun/p/8970952.html

- MySQL索引，如何正确创建MySQL索引，如何判断是否需要创建索引？
> 索引可以提高数据的检索效率，也可以降低数据库的IO成本，并且索引还可以降低数据库的排序成本。排序分组操作主要消耗的就是CPU资源和内存，所以能够在排序分组操作中好好的利用索引将会极大地降低CPU资源的消耗。

> 1. 较频繁地作为查询条件的字段

> 这个都知道。什么是教频繁呢？分析你执行的所有SQL语句。最好将他们一个个都列出来。然后分析，发现其中有些字段在大部分的SQL语句查询时候都会用到，那么就果断为他建立索引。
> 2. 唯一性太差的字段不适合建立索引

> 什么是唯一性太差的字段。如状态字段、类型字段。那些只存储固定几个值的字段，例如用户登录状态、消息的status等。这个涉及到了索引扫描的特性。例如：通过索引查找键值为A和B的某些数据，通过A找到某条相符合的数据，这条数据在X页上面，然后继续扫描，又发现符合A的数据出现在了Y页上面，那么存储引擎就会丢弃X页面的数据，然后存储Y页面上的数据，一直到查找完所有对应A的数据，然后查找B字段，发现X页面上面又有对应B字段的数据，那么他就会再次扫描X页面，等于X页面就会被扫描2次甚至多次。以此类推，所以同一个数据页可能会被多次重复的读取，丢弃，在读取，这无疑给存储引擎极大地增加了IO的负担。
> 3. 更新太频繁地字段不适合创建索引

> 当你为这个字段创建索引时候，当你再次更新这个字段数据时，数据库会自动更新他的索引，所以当这个字段更新太频繁地时候那么就是不断的更新索引，性能的影响可想而知。大概被检索几十次会更新一次的字段才比较符合建立索引的规范。而如果一个字段同一个时间段内被更新多次，那么果断不能为他建立索引。
> 4. 不会出现在where条件中的字段不该建立索引

- 讲一下事务的隔离性？
> https://www.cnblogs.com/fjdingsd/p/5273008.html

- 说一下 mysql 常用的引擎？
> https://www.cnblogs.com/xiaohaillong/p/6079551.html

- 说一下 mysql 的行锁和表锁？
> https://www.cnblogs.com/chenqionghe/p/4845693.html

- mysql 问题排查常用方法？
> https://www.jianshu.com/p/8d205e946ca2
> https://blog.csdn.net/qq_31854907/article/details/83105446

- 如何做 mysql 的性能优化？
> https://www.cnblogs.com/pengyunjing/p/6591660.html

# Redis
- 什么是Redis？为什么使用Redis？
> Redis是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。 Redis是一个开源的key—value型数据库，支持string、list、set、zset和hash类型数据。对这些数据的操作都是原子性的，redus为了保证效率会定期持久化数据。

> - 为什么使用？
> 1. 解决应用服务器的cpu和内存压力
> 2. 减少io的读操作，减轻io的压力
> 3. 关系型数据库的扩展性不强，难以改变表结构

> - 优点：
> 1. nosql数据库没有关联关系，数据结构简单，拓展表比较容易
> 2. nosql读取速度快，对较大数据处理快

> - 适用场景：
> 1. 数据高并发的读写
> 2. 海量数据的读写
> 3. 对扩展性要求高的数据

> - 记录帖子点赞数、点击数、评论数；
> - 缓存近期热帖；
> - 缓存文章详情信息；
> - 记录用户会话信息。

> - 不适场景：
> 1. 需要事务支持（非关系型数据库）
> 2. 基于sql结构化查询储存，关系复杂

- redis 有哪些功能？
> - 字符串string
> - 列表list
> - 集合set
> - 有序集合zset
> - hash

> 1. 数据缓存功能
> 2. 分布式锁的功能
> 3. 支持数据持久化
> 4. 支持事务
> 5. 支持消息队列


- Redis与Memcached的比较？
> 1. 网络IO模型
> - Memcached是多线程，非阻塞IO复用的网络模型，分为监听主线程和worker子线程，监听线程监听网络连接，接受请求后，将连接描述字pipe 传递给worker线程，进行读写IO, 网络层使用libevent封装的事件库，多线程模型可以发挥多核作用，但是引入了cache coherency和锁的问题。
> - Redis使用单线程的IO复用模型，自己封装了一个简单的AeEvent事件处理框架，主要实现了epoll、kqueue和select，对于单纯只有IO操作来说，单线程可以将速度优势发挥到最大，但是Redis也提供了一些简单的计算功能，比如排序、聚合等，对于这些操作，单线程模型实际会严重影响整体吞吐量，CPU计算过程中，整个IO调度都是被阻塞住的。
> 2. 内存管理方面
> - Memcached使用预分配的内存池的方式，使用slab和大小不同的chunk来管理内存，Item根据大小选择合适的chunk存储，内存池的方式可以省去申请/释放内存的开销，并且能减小内存碎片产生，但这种方式也会带来一定程度上的空间浪费，并且在内存仍然有很大空间时，新的数据也可能会被剔除，原因可以参考Timyang的文章：http://timyang.net/data/Memcached-lru-evictions/

> - Redis使用现场申请内存的方式来存储数据，并且很少使用free-list等方式来优化内存分配，会在一定程度上存在内存碎片，Redis跟据存储命令参数，会把带过期时间的数据单独存放在一起，并把它们称为临时数据，非临时数据是永远不会被剔除的，即便物理内存不够，导致swap也不会剔除任何非临时数据（但会尝试剔除部分临时数据），这点上Redis更适合作为存储而不是cache。

> 3. 数据一致性问题
> - Memcached提供了cas命令，可以保证多个并发访问操作同一份数据的一致性问题。 Redis没有提供cas 命令，并不能保证这点，不过Redis提供了事务的功能，可以保证一串 命令的原子性，中间不会被任何操作打断。

> 4. 存储方式及其它方面
> - Memcached基本只支持简单的key-value存储，不支持枚举，不支持持久化和复制等功能

> - Redis除key/value之外，还支持list,set,sorted set,hash等众多数据结构，提供了KEYS进行枚举操作，但不能在线上使用，如果需要枚举线上数据，Redis提供了工具可以直接扫描其dump文件，枚举出所有数据，Redis还同时提供了持久化和复制等功能。
> 5. 关于不同语言的客户端支持
> - 在不同语言的客户端方面，Memcached和Redis都有丰富的第三方客户端可供选择，不过因为Memcached发展的时间更久一些，目前看在客户端支持方面，Memcached的很多客户端更加成熟稳定，而Redis由于其协议本身就比Memcached复杂，加上作者不断增加新的功能等，对应第三方客户端跟进速度可能会赶不上，有时可能需要自己在第三方客户端基础上做些修改才能更好的使用。

- redis 为什么是单线程的？
> https://blog.csdn.net/chenyao1994/article/details/79491337

> 我们首先要明白，上边的种种分析，都是为了营造一个Redis很快的氛围！官方FAQ表示，因为Redis是基于内存的操作，CPU不是Redis的瓶颈，Redis的瓶颈最有可能是机器内存的大小或者网络带宽。既然单线程容易实现，而且CPU不会成为瓶颈，那就顺理成章地采用单线程的方案了（毕竟采用多线程会有很多麻烦！）。
- Redis为什么这么快？
> 1. 完全基于内存，绝大部分请求是纯粹的内存操作，非常快速。数据存在内存中，类似于HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)；
> 2. 数据结构简单，对数据操作也简单，Redis中的数据结构是专门进行设计的；
> 3. 采用单线程，避免了不必要的上下文切换和竞争条件，也不存在多进程或者多线程导致的切换而消耗 CPU，不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗；
> 4. 使用多路I/O复用模型，非阻塞IO；
> 5. 使用底层模型不同，它们之间底层实现方式以及与客户端之间通信的应用协议不一样，Redis直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求；
> 6. 多路 I/O 复用模型

> 6.1 多路I/O复用模型是利用 select、poll、epoll 可以同时监察多个流的 I/O 事件的能力，在空闲的时候，会把当前线程阻塞掉，当有一个或多个流有 I/O 事件时，就从阻塞态中唤醒，于是程序就会轮询一遍所有的流（epoll 是只轮询那些真正发出了事件的流），并且只依次顺序的处理就绪的流，这种做法就避免了大量的无用操作。

> 6.2 这里“多路”指的是多个网络连接，“复用”指的是复用同一个线程。采用多路 I/O 复用技术可以让单个线程高效的处理多个连接请求（尽量减少网络 IO 的时间消耗），且 Redis 在内存中操作数据的速度非常快，也就是说内存内的操作不会成为影响Redis性能的瓶颈，主要由以上几点造就了 Redis 具有很高的吞吐量。

> epoll 详解？
> https://blog.csdn.net/u011671986/article/details/79449853

- 关于缓存你需要知道的？
> https://www.jianshu.com/p/3c111e4719b8
> - **缓存穿透**,缓存穿透是说访问一个缓存中没有的数据，但是这个数据数据库中也不存在。普通思路下我们没有从数据库中拿到数据是不会触发加缓存操作的。这时如果是有人恶意攻击，大量的访问就会透过缓存直接打到数据库，对后端服务和数据库做成巨大的压力甚至宕机。
解决方案：

> 1. 缓存空对象。如果缓存未命中，而数据库中也没有这个对象，则可以缓存一个空对象到缓存。如果使用Redis，这种key需设置一个较短的时间，以防内存浪费。
> 2. 缓存预测。预测key是否存在。如果缓存的量不大可以使用hash来判断，如果量大可以使用布隆过滤器来做判断。
> - **缓存并发**,缓存并发这个场景很容易解释：多个客户端同时访问一个没有在cache中的数据，这时每个客户端都会执行从DB加载数据set到缓存，就会造成缓存并发。
> 1. 缓存预热。提前把所有预期的热数据加到缓存。定位热数据还是比较复杂的事情，需要根据自己的服务访问情况去评估。这个方案只能减轻缓存并发的发生次数不能全部抵制。
> 2. 缓存加锁。 如果多个客户端访问不存在的缓存时，在执行加载数据并set缓存这个逻辑之前先加锁，只能让一个客户端执行这段逻辑。
> - **缓存防雪崩**
>  如果缓存集中在一段时间内失效，发生大量的缓存穿透，所有的查询都落在数据库上，造成了缓存雪崩。缓存雪崩是缓存服务暂时不能提供服务，导致所有的请求都直接访问DB。
> 1. 构建高可用的缓存系统。目前常用的缓存系统Redis和Memcache都支持高可用的部署方式，所以部署的时候不防先考虑是否要以高可用的集群方式部署。
> 2. 限流。Netflix的Hystrix是非常不错的工具，在用缓存时不妨搭配它来使用。

- 缓存更新的套路？
> https://coolshell.cn/articles/17416.html
- Redis支持的Java客户端都有哪些？官方推荐用哪个？
> Redisson,Jedis，lettuce等等，官方推荐使用Redisson。
- Jedis与Redisson对比？
> https://www.jianshu.com/p/bc0ca84cf3ba
> 1. Jedis是Redis的Java实现的客户端，其API提供了比较全面的Redis命令的支持；Redisson实现了分布式和可扩展的Java数据结构，和Jedis相比，功能较为简单，不支持字符串操作，不支持排序、事务、管道、分区等Redis特性。Redisson的宗旨是促进使用者对Redis的关注分离，从而让使用者能够将精力更集中地放在处理业务逻辑上。
> 2. Jedis中的方法调用是比较底层的暴露的Redis的API，也即Jedis中的Java方法基本和Redis的API保持着一致，了解Redis的API，也就能熟练的使用Jedis。而Redisson中的方法则是进行比较高的抽象，每个方法调用可能进行了一个或多个Redis方法调用。
> 3. Jedis使用阻塞的I/O，且其方法调用都是同步的，程序流需要等到sockets处理完I/O才能执行，不支持异步。Jedis客户端实例不是线程安全的，所以需要通过连接池来使用Jedis。Redisson使用非阻塞的I/O和基于Netty框架的事件驱动的通信层，其方法调用是异步的。Redisson的API是线程安全的，所以可以操作单个Redisson连接来完成各种操作。
> 4. Jedis仅支持基本的数据类型如：String、Hash、List、Set、Sorted Set。Redisson不仅提供了一系列的分布式Java常用对象，基本可以与Java的基本数据结构通用，还提供了许多分布式服务，其中包括（BitSet, Set, Multimap, SortedSet, Map, List, Queue, BlockingQueue, Deque, BlockingDeque, Semaphore, Lock, AtomicLong, CountDownLatch, Publish / Subscribe, Bloom filter, Remote service, Spring cache, Executor service, Live Object service, Scheduler service）。
- 缓存穿透，缓存击穿，缓存雪崩解决方案分析？
> https://www.cnblogs.com/williamjie/p/9394229.html

- 分布式之数据库和缓存双写一致性方案解析?
> https://www.cnblogs.com/williamjie/p/9394201.html
> https://www.cnblogs.com/williamjie/p/9394197.html

- redis缓存与数据库一致性问题
> https://www.cnblogs.com/senlinyang/p/8830611.html

- redis持久化的几种方式？
> https://www.cnblogs.com/AndyAo/p/8135980.html
> 1. Redis是一种高级key-value数据库。它跟memcached类似，不过数据可以持久化，而且支持的数据类型很丰富。有字符串，链表，集 合和有序集合。支持在服务器端计算集合的并，交和补集(difference)等，还支持多种排序功能。所以Redis也可以被看成是一个数据结构服务器。
> 2. **AOF**，Redis的所有数据都是保存在内存中，然后不定期的通过异步方式保存到磁盘上(这称为“半持久化模式”)；也可以把每一次数据变化都写入到一个append only file(aof)里面(这称为“全持久化模式”)。 

> 3. **RDB**，由于Redis的数据都存放在内存中，如果没有配置持久化，redis重启后数据就全丢失了，于是需要开启redis的持久化功能，将数据保存到磁 盘上，当redis重启后，可以从磁盘中恢复数据。redis提供两种方式进行持久化，一种是RDB持久化（原理是将Reids在内存中的数据库记录定时 dump到磁盘上的RDB持久化），另外一种是AOF（append only file）持久化（原理是将Reids的操作日志以追加的方式写入文件）。那么这两种持久化方式有什么区别呢，改如何选择呢？网上看了大多数都是介绍这两 种方式怎么配置，怎么使用，就是没有介绍二者的区别，在什么应用场景下使用。

> 4. RDB持久化是指在指定的时间间隔内将内存中的数据集快照写入磁盘，实际操作过程是fork一个子进程，先将数据集写入临时文件，写入成功后，再替换之前的文件，用二进制压缩存储。
> 5. AOF持久化以日志的形式记录服务器所处理的每一个写、删除操作，查询操作不会记录，以文本的方式记录，可以打开文件看到详细的操作记录。
> 6. **混合模式（4.0版本支持）(AOF+RDB)**，aof在rewrite的时候把rdb写入到文件开头，之后写入的依旧是aof格式，解决了 aof 恢复慢，rdb写入时间间隔的问题。

```
RDB持久化配置
Redis会将数据集的快照dump到dump.rdb文件中。此外，我们也可以通过配置文件来修改Redis服务器dump快照的频率，在打开6379.conf文件之后，我们搜索save，可以看到下面的配置信息：
save 900 1              #在900秒(15分钟)之后，如果至少有1个key发生变化，则dump内存快照。
save 300 10            #在300秒(5分钟)之后，如果至少有10个key发生变化，则dump内存快照。
save 60 10000        #在60秒(1分钟)之后，如果至少有10000个key发生变化，则dump内存快照。

AOF持久化配置
在Redis的配置文件中存在三种同步方式，它们分别是：
appendfsync always     #每次有数据修改发生时都会写入AOF文件。
appendfsync everysec  #每秒钟同步一次，该策略为AOF的缺省策略。
appendfsync no          #从不同步。高效但是数据不会被持久化。
```
- 如何优雅地用Redis实现分布式锁?
> https://www.cnblogs.com/linjiqin/p/8003838.html
> https://yq.aliyun.com/articles/630496?utm_content=m_1000014601
> 1. 加锁: `SET my_key my_value NX PX milliseconds`，NX为**IF NOT EXIST**，如果my_key不存在，PX：**EXPIRES TIME**，设置mey_key的值为my_value。 my_value应该为一个全局唯一的id值，用于释放锁。
> 2. 释放锁: `if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end`
```
String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
Object result = jedis.eval(script, Collections.singletonList(lockKey), Collections.singletonList(requestId));
```
- 对比各类分布式锁缺陷，抓住Redis分布式锁实现命门?
> https://blog.51cto.com/14208181/2354921
- 如何redis 如何做内存优化？
> 1. 合理设置内部编码配置参数
> 2. 使用32位Redis实例
> 3. 尽可能的使用hash数据结构
> 4. 减少key的数量

- Redis缓存淘汰策略？
> - 驱逐策略
> 1. noeviction: 不删除策略, 达到最大内存限制时, 如果需要更多内存, 直接返回错误信息。 大多数写命令都会导致占用更多的内存(有极少数会例外, 如 DEL )。
> 2. allkeys-lru: 所有key通用; 优先删除最近最少使用(less recently used ,LRU) 的 key。
> 3. volatile-lru: 只限于设置了 expire 的部分; 优先删除最近最少使用(less recently used ,LRU) 的 key。
> 4. allkeys-random: 所有key通用; 随机删除一部分 key。
> 5. volatile-random: 只限于设置了 expire 的部分; 随机删除一部分 key。
> 6. volatile-ttl: 只限于设置了 expire 的部分; 优先删除剩余时间(time to live,TTL) 短的key。
- Redis 常见的性能问题和解决方法？
> 1. Master写内存快照，save命令调度rdbSave函数，会阻塞主线程的工作，当快照比较大时对性能影响是非常大的，会间断性暂停服务，所以Master最好不要写内存快照。
> 2. Master AOF持久化，如果不重写AOF文件，这个持久化方式对性能的影响是最小的，但是AOF文件会不断增大，AOF文件过大会影响Master重启的恢复速度。
> 3. Master调用BGREWRITEAOF，Master调用BGREWRITEAOF重写AOF文件，AOF在重写的时候会占大量的CPU和内存资源，导致服务load过高，出现短暂服务暂停现象。
> 4. Redis主从复制的性能问题，第一次Slave向Master同步的实现是：Slave向Master发出同步请求，Master先dump出rdb文件，然后将rdb文件全量传输给slave，然后Master把缓存的命令转发给Slave，初次同步完成。第二次以及以后的同步实现是：Master将变量的快照直接实时依次发送给各个Slave。不管什么原因导致Slave和Master断开重连都会重复以上过程。Redis的主从复制是建立在内存快照的持久化基础上，只要有Slave就一定会有内存快照发生。虽然Redis宣称主从复制无阻塞，但由于Redis使用单线程服务，如果Master快照文件比较大，那么第一次全量传输会耗费比较长时间，且文件传输过程中Master可能无法提供服务，也就是说服务会中断，对于关键服务，这个后果也是很可怕的。
> 5. 单点故障问题，由于目前Redis的主从复制还不够成熟，所以存在明显的单点故障问题，这个目前只能自己做方案解决，如：主动复制，Proxy实现Slave对Master的替换等，这个也是Redis作者目前比较优先的任务之一，作者的解决方案思路简单优雅，详情可见 Redis Sentinel design draft http://redis.io/topics/sentinel-spec。
```
Master最好不要做任何持久化工作，包括内存快照和AOF日志文件，特别是不要启用内存快照做持久化。
如果数据比较关键，某个Slave开启AOF备份数据，策略为每秒同步一次。
为了主从复制的速度和连接的稳定性，Slave和Master最好在同一个局域网内。
尽量避免在压力较大的主库上增加从库
为了Master的稳定性，主从复制不要用图状结构，用单向链表结构更稳定，即主从关系为：Master<–Slave1<–Slave2<–Slave3…….，这样的结构也方便解决单点故障问题，实现Slave对Master的替换，也即，如果Master挂了，可以立马启用Slave1做Master，其他不变。
```

- redis 如何做内存优化？
> 1. 关闭 Redis 的虚拟内存[VM]功能，即 redis.conf 中 vm-enabled = no
> 2. 设置 redis.conf 中 maxmemory ，用于告知 Redis 当使用了多少物理内存后拒绝继续写入的请求，可防止 Redis 性能降低甚至崩溃
> 3. 可为指定的数据类型设置内存使用规则，从而提高对应数据类型的内存使用效率
>   - Hash 在 redis.conf 中有以下两个属性，任意一个超出设定值，则会使用 HashMap 存值
>       -  hash-max-zipmap-entires 64 表示当 value 中的 map 数量在 64 个以下时，实际使用 zipmap 存储值
>       - hash-max-zipmap-value 512 表示当 value 中的 map 每个成员值长度小于 512 字节时，实际使用 zipmap 存储值
>   - List 在 redis.conf 中也有以下两个属性
>       -  list-max-ziplist-entires 64
>       -  list-max-ziplist-value 512
> 4. 在 Redis 的源代码中有一行宏定义 REDIS-SHARED-INTEGERS = 10000 ，修改该值可以改变 Redis 存储数值类型的内存开销

# JVM
- JVM内存分为哪几部分?各个部分的作用是什么?
> https://blog.csdn.net/guhong5153/article/details/70196354
> - Java虚拟机内存的五大区域
> 1. 堆。 堆是Java对象的存储区域，任何用new字段分配的Java对象实例和数组，都被分配在堆上，Java堆可使用-Xms -Xmx进行内存控制，值得一提的是从JDK1.7版本之后，运行时常量池从方法区移到了堆上。堆内存是 JVM 所有线程共享的部分，在虚拟机启动的时候就已经创建。所有的对象和数组都在堆上进行分配。这部分空间可通过 GC 进行回收。当申请不到空间时会抛出 OutOfMemoryError。

> 2. 方法区。它用于存储已被虚拟机加载的类信息，常量，静态变量，即时编译器编译后的代码等数据，方法区在JDK1.7版本及以前被称为永久代，从JDK1.8永久代被移除。方法区也是所有线程共享。主要用于存储类的信息、常量池、方法数据、方法代码等。方法区逻辑上属于堆的一部分，但是为了与堆进行区分，通常又叫“非堆”。JDK1.8以前，叫做永久代，PermGen。>=1.8，叫做元空间，Metaspace。>=1.7，常量转移到了堆，不在永久代了。
>   - 元空间的本质和永久代类似，都是对JVM规范中方法区的实现。不过元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。因此，默认情况下，元空间的大小仅受本地内存限制，但可以通过以下参数来指定元空间的大小：
```
-XX:MetaspaceSize，初始空间大小，达到该值就会触发垃圾收集进行类型卸载，同时GC会对该值进行调整：如果释放了大量的空间，就适当降低该值；如果释放了很少的空间，那么在不超过MaxMetaspaceSize时，适当提高该值。 
-XX:MaxMetaspaceSize，最大空间，默认是没有限制的。
    
除了上面两个指定大小的选项以外，还有两个与 GC 相关的属性： 
-XX:MinMetaspaceFreeRatio，在GC之后，最小的Metaspace剩余空间容量的百分比，减少为分配空间所导致的垃圾收集 
-XX:MaxMetaspaceFreeRatio，在GC之后，最大的Metaspace剩余空间容量的百分比，减少为释放空间所导致的垃圾收集

通过上面分析，大家应该大致了解了 JVM 的内存划分，也清楚了 JDK 8 中永久代向元空间的转换。不过大家应该都有一个疑问，就是为什么要做这个转换？所以，最后给大家总结以下几点原因：
　　1、字符串存在永久代中，容易出现性能问题和内存溢出。
　　2、类及方法的信息等比较难确定其大小，因此对于永久代的大小指定比较困难，太小容易出现永久代溢出，太大则容易导致老年代溢出。
　　3、永久代会为 GC 带来不必要的复杂度，并且回收效率偏低。
　　4、Oracle 可能会将HotSpot 与 JRockit 合二为一。
```

> 3. 虚拟机栈。虚拟机栈中执行每个方法的时候，都会创建一个栈帧用于存储局部变量表，操作数栈，动态链接，方法出口等信息。每个线程有一个私有的栈，随着线程的创建而创建。栈里面存着的是一种叫“栈帧”的东西，每个方法会创建一个栈帧，栈帧中存放了局部变量表（基本数据类型和对象引用）、操作数栈、方法出口等信息。栈的大小可以固定也可以动态扩展。当栈调用深度大于JVM所允许的范围，会抛出StackOverflowError的错误，不过这个深度范围不是一个恒定的值

> 4. 本地方法栈。与虚拟机栈发挥的作用相似，相比于虚拟机栈为Java方法服务，本地方法栈为虚拟机使用的Native方法服务，执行每个本地方法的时候，都会创建一个栈帧用于存储局部变量表，操作数栈，动态链接，方法出口等信息。

> 5. 程序计数器。指示Java虚拟机下一条需要执行的字节码指令。 PC 寄存器，也叫程序计数器。JVM支持多个线程同时运行，每个线程都有自己的程序计数器。倘若当前执行的是 JVM 的方法，则该寄存器中保存当前执行指令的地址；倘若执行的是native 方法，则PC寄存器中为空

> - 以上五个区域是Java虚拟机内存划分情况，其中方法区和堆被JVM中多个线程共享，比如类的静态常量就被存放在方法区，供类对象之间共享，虚拟机栈，本地方法栈，pc寄存器是每个线程独立拥有的，不会与其他线程共享。 所以Java在通过new创建一个类对象实例的时候，一方面会在虚拟机栈中创建一个该对象的引用，另一方面会在堆上创建类对象的实例，然后将对象引用指向该对象的实例。对象引用存放在每一个方法对应的栈帧中。

> https://blog.csdn.net/yetaoii/article/details/79807336
- Java虚拟机（JVM）你只要看这一篇就够了！
> https://blog.csdn.net/qq_41701956/article/details/81664921
> https://www.cnblogs.com/good-temper/p/3583660.html
- java编译过程（字节码编译和即时编译）
> https://www.cnblogs.com/straybirds/p/8513870.html
- 执行引擎(三)：程序编译与代码优化
> https://www.cnblogs.com/lllllht/p/9184343.html
- 说一下JVM入门——运行时数据区？
> http://www.cnblogs.com/yulinfeng/p/7153391.html
- JVM即时编译（JIT）
> https://blog.csdn.net/sunxianghuang/article/details/52094859

- 彻底弄懂字符串常量池等相关问题
> https://www.cnblogs.com/gxyandwmm/p/9495923.html
```
intern()函数
　　intern函数的作用是将对应的符号常量进入特殊处理，在1.6以前 和 1.7以后有不同的处理；
    
    在1.6中，intern的处理是 先判断字符串常量是否在字符串常量池中，如果存在直接返回该常量，如果没有找到，则将该字符串常量加入到字符串常量区，也就是在字符串常量区建立该常量；
    
    在1.7中，intern的处理是 先判断字符串常量是否在字符串常量池中，如果存在直接返回该常量，如果没有找到，说明该字符串常量在堆中，则处理是把堆区该对象的引用加入到字符串常量池中，以后别人拿到的是该字符串常量的引用，实际存在堆中；【这里感谢以为网友的纠正，一开始理解为在堆区建立该字符串对象在添加引用了，其实调用该方法的字符串对象要么在堆区要么在常量池中的】
```

- 堆和栈的概念和区别
> https://blog.csdn.net/pt666/article/details/70876410/
> 1. 栈内存存储的是局部变量而堆内存存储的是实体；
> 2. 栈内存的更新速度要快于堆内存，因为局部变量的生命周期很短；
> 3. 栈内存存放的变量生命周期一旦结束就会被释放，而堆内存存放的实体会被垃圾回收机制不定时的回收。

- 队列和栈有什么区别？
> 1. 操作的名称不同。队列的插入称为入队，队列的删除称为出队。栈的插入称为进栈，栈的删除称为出栈。
> 2. 可操作的方式不同。队列是在队尾入队，队头出队，即两边都可操作。而栈的进栈和出栈都是在栈顶进行的，无法对栈底直接进行操作。
> 3. 操作的方法不同。队列是先进先出（FIFO），即队列的修改是依先进先出的原则进行的。新来的成员总是加入队尾（不能从中间插入），每次离开的成员总是队列头上（不允许中途离队）。而栈为后进先出（LIFO）,即每次删除（出栈）的总是当前栈中最新的元素，即最后插入（进栈）的元素，而最先插入的被放在栈的底部，要到最后才能删除。

- 类加载机制和双亲委派模型？
> https://blog.csdn.net/aimashi620/article/details/84836245

> https://blog.csdn.net/w372426096/article/details/81901482

> https://www.cnblogs.com/doit8791/p/5820037.html

- 说一下类加载的执行过程？
> https://blog.csdn.net/jintao_ma/article/details/51353453
> 1. **加载**，通过“类全名”来获取定义此类的二进制字节流，将字节流所代表的静态存储结构转换为方法区的运行时数据结构，在java堆中生成一个代表这个类的java.lang.Class对象，作为方法区这些数据的访问入口。
> 2. **验证**，验证是链接阶段的第一步，这一步主要的目的是确保class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身安全。
验证阶段主要包括四个检验过程：文件格式验证、元数据验证、字节码验证和符号引用验证。
> 3. **准备**，准备阶段是正式为类变量分配内存并设置类变量初始值的阶段，这些内存都将在方法区中进行分配。这个阶段中有两个容易产生混淆的知识点，首先是这时候进行内存分配的仅包括类变量(static 修饰的变量),而不包括实例变量，实例变量将会在对象实例化时随着对象一起分配在java堆中。其次是这里所说的初始值“通常情况”下是数据类型的零值。
> 4. **解析**，解析阶段是虚拟机常量池内的符号引用替换为直接引用的过程。
> 5. **初始化**，类的初始化阶段是类加载过程的最后一步，在准备阶段，类变量已赋过一次系统要求的初始值，而在初始化阶段，则是根据程序员通过程序制定的主观计划去初始化类变量和其他资源，或者可以从另外一个角度来表达：初始化阶段是执行类构造器<clinit>()方法的过程。

- 怎么判断对象是否可以被回收？
> 1. **引用计数法**，给每一个对象添加一个引用计数器，每次引用计数器就加1，当引用失效的时候就减1，当计数器的值为0的时候，就可以对该对象进行回收。
> 2. **可达性分析算法**，将一系列的gc roots对象作为起始点，从这些节点向下搜索，搜索走过的路径称为是引用链，当gc roots对象到一个对象没有引用链的时候，称为这个对象是不可达的，此对象是不可用的，就可以进行回收。
> - 虚拟机栈中引用的对象
> - 方法区中类静态属性引用的对象
> - 方法区中常量引用的对象
> - 本地方法栈中JNI[即一般说的Native]引用的对象

- java 中都有哪些引用类型？
> 1. **StrongReference(强引用)**，`Test test = new Test()`,这是最常见的引用类型，也是最牢固的引用类型，当jvm发生gc时，对象被引用不会被gc回收，jvm内存满了将要发生OOM（out of memory）的时候，强引用类型也不会被回收
> 2. **SoftReference(软引用)**，`SoftReference<String> softReference = new SoftReference<>(new String("Hello World"));`,较强引用来说，软引用在发生gc时，被引用的对象不会被回收，当内存满时，将要发生OOM时，gc会回收软引用的对象
> 3. **WeakReference(弱引用)**,`WeakReference<String> weakReference = new WeakReference<>(new String("Hello World"));`,弱引用在发生gc时，就会被gc回收，不管内存用了多少，弱引用最长的生命周期是两次gc的间隔时间。
> 4. **PhantomReference(虚引用，幻引用)**,`ReferenceQueue<String> referenceQueue = new ReferenceQueue<>(); 
PhantomReference<String> phantomReference = new PhantomReference<>(new String("Hello World"), referenceQueue);`,虚引用和上面两种引用有一点点小区别，多了一个依赖队列。虚引用并不会决定对象的生命周期，有他没他都一个样，无法通过虚引用获取对象。
> 5. **引用队列（ReferenceQueue）**,引用队列可以与软引用、弱引用以及虚引用一起配合使用，当垃圾回收器准备回收一个对象时，如果发现它还有引用，那么就会在回收对象之前，把这个引用加入到与之关联的引用队列中去。程序可以通过判断引用队列中是否已经加入了引用，来判断被引用的对象是否将要被垃圾回收，这样就可以在对象被回收之前采取一些必要的措施。与软引用、弱引用不同，虚引用必须和引用队列一起使用。

- 说一下 jvm 有哪些垃圾回收算法？
> http://www.cnblogs.com/yulinfeng/p/7163052.html
> 1. 标记-清除算法

> 等待被回收对象的“标记”过程在上文已经提到过，如果在被标记后直接对对象进行清除，会带来另一个新的问题——内存碎片化。如果下次有比较大的对象实例需要在堆上分配较大的内存空间时，可能会出现无法找到足够的连续内存而不得不再次触发垃圾回收。
> 2. 复制算法

> 此GC算法实际上解决了标记-清除算法带来的“内存碎片化”问题。首先还是先标记处待回收内存和不用回收的内存，下一步将不用回收的内存复制到新的内存区域，这样旧的内存区域就可以全部回收，而新的内存区域则是连续的。它的缺点就是会损失掉部分系统内存，因为你总要腾出一部分内存用于复制。

> 在上文《JVM入门——运行时数据区》提到过在Java堆中被分为了新生代和老年代，这样的划分是方便GC。Java堆中的新生代就使用了GC复制算法。在新生代中又分为了三个区域：Eden 空间、To Survivor空间、From Survivor空间。不妨将注意力回到这张图的左边新生代部分：
![image](https://images2015.cnblogs.com/blog/630246/201707/630246-20170713203325103-321422084.png)

> 新的对象实例被创建的时候通常在Eden空间，发生在Eden空间上的GC称为Minor GC，当在新生代发生一次GC后，会将Eden和其中一个Survivor空间的内存复制到另外一个Survivor中，如果反复几次有对象一直存活，此时内存对象将会被移至老年代。可以看到新生代中Eden占了大部分，而两个Survivor实际上占了很小一部分。这是因为大部分的对象被创建过后很快就会被GC（这里也许运用了是二八原则）。
> 3. 标记-整理(压缩)算法

> 对于新生代，大部分对象都不会存活，所以在新生代中使用复制算法较为高效，而对于老年代来讲，大部分对象可能会继续存活下去，如果此时还是利用复制算法，效率则会降低。标记-压缩算法首先还是“标记”，标记过后，将不用回收的内存对象压缩到内存一端，此时即可直接清除边界处的内存，这样就能避免复制算法带来的效率问题，同时也能避免内存碎片化的问题。老年代的垃圾回收称为“Major GC”。

> 4. 分代收集算法

> 分代收集算法是目前大部分JVM的垃圾收集器采用的算法。它的核心思想是根据对象存活的生命周期将内存划分为若干个不同的区域。一般情况下将堆区划分为老年代（Tenured Generation）和新生代（Young Generation），在堆区之外还有一个代就是永久代（Permanet Generation）。老年代的特点是每次垃圾收集时只有少量对象需要被回收，而新生代的特点是每次垃圾回收时都有大量的对象需要被回收，那么就可以根据不同代的特点采取最适合的收集算法。

- 说一下 jvm 有哪些垃圾回收器？
> https://www.cnblogs.com/aspirant/p/8662690.html
> 1. Serial收集器（复制算法)
新生代单线程收集器，标记和清理都是单线程，优点是简单高效。是client级别默认的GC方式，可以通过-XX:+UseSerialGC来强制指定。

> 2. Serial Old收集器(标记-整理算法)
老年代单线程收集器，Serial收集器的老年代版本。

> 3. ParNew收集器(停止-复制算法)　
新生代收集器，可以认为是Serial收集器的多线程版本,在多核CPU环境下有着比Serial更好的表现。

> 4. Parallel Scavenge收集器(停止-复制算法)
并行收集器，追求高吞吐量，高效利用CPU。吞吐量一般为99%， 吞吐量= 用户线程时间/(用户线程时间+GC线程时间)。适合后台应用等对交互相应要求不高的场景。是server级别默认采用的GC方式，可用-XX:+UseParallelGC来强制指定，用-XX:ParallelGCThreads=4来指定线程数。

> 5. Parallel Old收集器(停止-复制算法)
Parallel Scavenge收集器的老年代版本，并行收集器，吞吐量优先。

> 6. CMS(Concurrent Mark Sweep)收集器（标记-清理算法）
高并发、低停顿，追求最短GC回收停顿时间，cpu占用比较高，响应时间快，停顿时间短，多核cpu 追求高响应时间的选择。

> 7. CMS 和G1的垃圾回收器的原理，阿里的面试官也问过，我专门做了专题：
> - [图解 CMS 垃圾回收机制原理，-阿里面试题](http://www.cnblogs.com/aspirant/p/8663911.html)
> - [CMS收集器和G1收集器优缺点](http://www.cnblogs.com/aspirant/p/8663897.html)
> - [G1 垃圾收集器入门](http://www.cnblogs.com/aspirant/p/8663872.html)


- CMS垃圾回收机制
> https://www.cnblogs.com/Leo_wl/p/5393300.html
> https://www.cnblogs.com/littleLord/p/5380624.html

- 垃圾收集器GC中parallel scavenge收集器为什么不能CMS配合使用？
> https://blog.csdn.net/qq_33915826/article/details/79672772

- Throughtput收集器
> https://blog.csdn.net/mc90716/article/details/80144473

- 简介JVM的Parallel Scavenge及Parallel Old垃圾收集器
> https://blog.csdn.net/u010798968/article/details/72867690

- 7种垃圾收集器
> https://blog.csdn.net/u013595419/article/details/79332390

- 垃圾收集算法——标记-整理算法（Mark-Compact）
> https://blog.csdn.net/en_joker/article/details/79741737

- 【理解HotSpot虚拟机】串行垃圾收集器Serial和Serial Old原理
> https://blog.csdn.net/linxdcn/article/details/78154133

- 说说JVM的GC功能之一GC算法的选择
> https://blog.51cto.com/guojuanjun/1958421

- 垃圾回收总结

收集器 | 串行/并行/并发 | 新生代/老年代 | 算法 | 目标 | 适用场景
---|---|---|---|---|---
Serial	| 串行	| 新生代	| 复制算法	|响应速度优先 |	单CPU环境下的Client模式
Serial Old |	串行	|老年代|	标记-整理|	响应速度优先|	单CPU环境下的Client模式、CMS的后备预案
ParNew|	并行|	新生代|	复制算法|	响应速度优先|	多CPU环境时在Server模式下与CMS配合
Parallel Scavenge|	并行|	新生代|	复制算法|	吞吐量优先|	在后台运算而不需要太多交互的任务
Parallel Old|	并行|	老年代|	标记-整理|	吞吐量优先|	在后台运算而不需要太多交互的任务
CMS|	并发|	老年代|	标记-清除|	响应速度优先|	集中在互联网站或B/S系统服务端上的Java应用
G1|	并发|	both|	标记-整理+复制算法|	响应速度优先|	面向服务端应用，将来替换CMS
--------------------- 
作者：法海你懂不 
来源：CSDN 
原文：https://blog.csdn.net/u013595419/article/details/79332390 
版权声明：本文为博主原创文章，转载请附上博文链接！
--------------------- 

- GC是什么时候触发的？
> - Scavenge GC

>  一般情况下，当新对象生成，并且在Eden申请空间失败时，就会触发Scavenge GC，对Eden区域进行GC，清除非存活对象，并且把尚且存活的对象移动到Survivor区。然后整理Survivor的两个区。这种方式的GC是对年轻代的Eden区进行，不会影响到年老代。因为大部分对象都是从Eden区开始的，同时Eden区不会分配的很大，所以Eden区的GC会频繁进行。因而，一般在这里需要使用速度快、效率高的算法，使Eden去能尽快空闲出来。

> - Full GC

> 对整个堆进行整理，包括Young、Tenured和Perm。Full GC因为需要对整个堆进行回收，所以比Scavenge GC要慢，因此应该尽可能减少Full GC的次数。在对JVM调优的过程中，很大一部分工作就是对于Full GC的调节。有如下原因可能导致Full GC：
> 1. 年老代（Tenured）被写满；
> 2. 持久代（Perm）被写满；
> 3. System.gc()被显示调用；
> 4. 上一次GC之后Heap的各域分配策略动态变化；

- 垃圾回收器学习之Full GC和CMS GC的区别
> https://blog.csdn.net/weixin_33857679/article/details/87403005
```
针对HotSpot VM的实现，它里面的GC其实准确分类只有两大种：Partial GC：并不收集整个GC堆的模式
Young GC：只收集young gen的GC
Old GC：只收集old gen的GC。只有CMS的concurrent collection是这个模式。
Mixed GC：收集整个young gen以及部分old gen的GC。只有G1有这个模式。

HotSpot VM里其它非并发GC的触发条件复杂一些，不过大致的原理与上面说的其实一样。当然也总有例外。Parallel Scavenge（-XX:+UseParallelGC）框架下，默认是在要触发full GC前先执行一次young GC，并且两次GC之间能让应用程序稍微运行一小下，以期降低full GC的暂停时间（因为young GC会尽量清理了young gen的死对象，减少了full GC的工作量）。并发GC的触发条件就不太一样。以CMS GC为例，它主要是定时去检查old gen的使用量，当使用量超过了触发比例就会启动一次CMS GC，对old gen做并发收集。并发并行垃圾回收器在触发full gc之前都会先触发一下young垃圾回收，这个可以根据参数进行配置。而串行垃圾回收的full gc默认就是老年代回收。

Full GC == Major GC指的是对老年代/永久代的stop the world的GC

Full GC的次数 = 老年代GC时 stop the world的次数

Full GC的时间 = 老年代GC时 stop the world的总时间

CMS 不等于Full GC，我们可以看到CMS分为多个阶段，只有stop the world的阶段被计算到了Full GC的次数和时间，而和业务线程并发的GC的次数和时间则不被认为是Full GC。CMS主要可以分为initial mark(stop the world), concurrent mark, remark(stop the world), concurrent sweep几个阶段，其中initial mark和remark会stop the world。

Full GC本身不会先进行Minor GC，我们可以配置，让Full GC之前先进行一次Minor GC，因为老年代很多对象都会引用到新生代的对象，先进行一次Minor GC可以提高老年代GC的速度。比如老年代使用CMS时，设置CMSScavengeBeforeRemark优化，让CMS remark之前先进行一次Minor GC。
--------------------- 
作者：weixin_33857679 
来源：CSDN 
原文：https://blog.csdn.net/weixin_33857679/article/details/87403005 
版权声明：本文为博主原创文章，转载请附上博文链接！
```

- Major GC和Full GC的区别是什么？触发条件呢？
```
针对HotSpot VM的实现，它里面的GC其实准确分类只有两大种：
Partial GC：并不收集整个GC堆的模式
Young GC：只收集young gen的GC
Old GC：只收集old gen的GC。只有CMS的concurrent collection是这个模式
Mixed GC：收集整个young gen以及部分old gen的GC。只有G1有这个模式
Full GC：收集整个堆，包括young gen、old gen、perm gen（如果存在的话）等所有部分的模式。
Major GC通常是跟full GC是等价的，收集整个GC堆。但因为HotSpot VM发展了这么多年，外界对各种名词的解读已经完全混乱了，当有人说“major GC”的时候一定要问清楚他想要指的是上面的full GC还是old gen。

最简单的分代式GC策略，按HotSpot VM的serial GC的实现来看，触发条件是：
young GC：当young gen中的eden区分配满的时候触发。注意young GC中有部分存活对象会晋升到old gen，所以young GC后old gen的占用量通常会有所升高。
full GC：当准备要触发一次young GC时，如果发现统计数据说之前young GC的平均晋升大小比目前old gen剩余的空间大，则不会触发young GC而是转为触发full GC（因为HotSpot VM的GC里，除了CMS的concurrent collection之外，其它能收集old gen的GC都会同时收集整个GC堆，包括young gen，所以不需要事先触发一次单独的young GC）；或者，如果有perm gen的话，要在perm gen分配空间但已经没有足够空间时，也要触发一次full GC；或者System.gc()、heap dump带GC，默认也是触发full GC。
HotSpot VM里其它非并发GC的触发条件复杂一些，不过大致的原理与上面说的其实一样。
当然也总有例外。Parallel Scavenge（-XX:+UseParallelGC）框架下，默认是在要触发full GC前先执行一次young GC，并且两次GC之间能让应用程序稍微运行一小下，以期降低full GC的暂停时间（因为young GC会尽量清理了young gen的死对象，减少了full GC的工作量）。这是HotSpot VM里的奇葩嗯。

并发GC的触发条件就不太一样。以CMS GC为例，它主要是定时去检查old gen的使用量，当使用量超过了触发比例就会启动一次CMS GC，对old gen做并发收集。
```




- 详细介绍一下 CMS 垃圾回收器？
> https://blog.csdn.net/mc90716/article/details/80158138

- 新生代垃圾回收器和老生代垃圾回收器都有哪些？有什么区别？
> https://blog.csdn.net/u014421556/article/details/51744614

- 简述分代垃圾回收器是怎么工作的？
> https://blog.csdn.net/jiang_zf/article/details/79436620

- G1垃圾收集器之对象分配过程
> https://www.jianshu.com/p/a0efa489b99f
- 说一下 jvm 调优的工具？
> https://www.cnblogs.com/wxisme/p/9878494.html
> - jps,java版的ps命令，查看java进程及其相关的信息，如果你想找到一个java进程的pid，那可以用jps命令替代linux中的ps命令了，简单而方便。
> - jinfo,jinfo是用来查看JVM参数和动态修改部分JVM参数的命令
> - jstat,jstat命令是使用频率比较高的命令，主要用来查看JVM运行时的状态信息，包括内存状态、垃圾回收等。
> - jstack,jstack是用来查看JVM线程快照的命令，线程快照是当前JVM线程正在执行的方法堆栈集合。使用jstack命令可以定位线程出现长时间卡顿的原因，例如死锁，死循环等。jstack还可以查看程序崩溃时生成的core文件中的stack信息。
> - jmap,jmap是用来生成堆dump文件和查看堆相关的各类信息的命令，例如查看finalize执行队列，heap的详细信息和使用情况。
> - jhat,jhat是用来分析jmap生成dump文件的命令，jhat内置了应用服务器，可以通过网页查看dump文件分析结果，jhat一般是用在离线分析上。
> - jconsole, jvisualvm,图形工具分析，内存，cpu，堆栈等

- 常用的 jvm 调优的参数都有哪些？
> https://cloud.tencent.com/developer/article/1198524
> https://blog.csdn.net/evane1890/article/details/78941968
```
-Xms：初始堆大小，默认为物理内存的1/64(<1GB)；默认(MinHeapFreeRatio参数可以调整)空余堆内存小于40%时，JVM就会增大堆直到-Xmx的最大限制
-Xmx：最大堆大小，默认(MaxHeapFreeRatio参数可以调整)空余堆内存大于70%时，JVM会减少堆直到 -Xms的最小限制
-Xmn：新生代的内存空间大小，注意：此处的大小是（eden+ 2 survivor space)。与jmap -heap中显示的New gen是不同的。整个堆大小=新生代大小 + 老生代大小 + 永久代大小。
      在保证堆大小不变的情况下，增大新生代后,将会减小老生代大小。此值对系统性能影响较大,Sun官方推荐配置为整个堆的3/8。
-XX:SurvivorRatio：新生代中Eden区域与Survivor区域的容量比值，默认值为8。两个Survivor区与一个Eden区的比值为2:8,一个Survivor区占整个年轻代的1/10。
-Xss：每个线程的堆栈大小。JDK5.0以后每个线程堆栈大小为1M,以前每个线程堆栈大小为256K。应根据应用的线程所需内存大小进行适当调整。在相同物理内存下,
      减小这个值能生成更多的线程。但是操作系统对一个进程内的线程数还是有限制的，不能无限生成，经验值在3000~5000左右。一般小的应用， 如果栈不是很深， 应该是128k够用的，
      大的应用建议使用256k。这个选项对性能影响比较大，需要严格的测试。和threadstacksize选项解释很类似,官方文档似乎没有解释,
      在论坛中有这样一句话:"-Xss is translated in a VM flag named ThreadStackSize”一般设置这个值就可以了。
-XX:PermSize：设置永久代(perm gen)初始值。默认值为物理内存的1/64。
-XX:MaxPermSize：设置持久代最大值。物理内存的1/4。
```
