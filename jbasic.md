- https://github.com/Snailclimb/JavaGuide
- https://www.cnblogs.com/over/p/10468747.html
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
> 有序的红黑树结构
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
- 
