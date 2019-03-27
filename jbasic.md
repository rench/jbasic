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
> 2) read commited：保证一个事物提交后才能被另外一个事务读取。另外一个事务不能读取该事物未提交的数据。
> 3) repeatable read：这种事务隔离级别可以防止脏读，不可重复读。但是可能会出现幻象读。它除了保证一个事务不能被另外一个事务读取未提交的数据之外还避免了以下情况产生（不可重复读）。
> 4) serializable：这是花费最高代价但最可靠的事务隔离级别。事务被处理为顺序执行。除了防止脏读，不可重复读之外，还避免了幻象读
> 5) 脏读、不可重复读、幻象读概念说明：
a.脏读：指当一个事务正字访问数据，并且对数据进行了修改，而这种数据还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。因为这个数据还没有提交那么另外一个事务读取到的这个数据我们称之为脏数据。依据脏数据所做的操作肯能是不正确的。
b.不可重复读：指在一个事务内，多次读同一数据。在这个事务还没有执行结束，另外一个事务也访问该同一数据，那么在第一个事务中的两次读取数据之间，由于第二个事务的修改第一个事务两次读到的数据可能是不一样的，这样就发生了在一个事物内两次连续读到的数据是不一样的，这种情况被称为是不可重复读。
c.幻象读：一个事务先后读取一个范围的记录，但两次读取的纪录数不同，我们称之为幻象读（两次执行同一条 select 语句会出现不同的结果，第二次读会增加一数据行，并没有说这两次执行是在同一个事务中）
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
> 3. 加入methodB使用的**PROPAGATION_REQUIRES_NEW**，那么B异常，会commit: 2,5,6，如果methodB没有出现异常，那么先commit4，再commit:,6，那么事务将分离开，不能保持一致。
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