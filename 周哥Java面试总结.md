# **面试总结**



## 新分享 深圳



### 1.工单系统表设计，索引怎么使用



### 2.项目排除错误

 查看java服务进程

```perl
ps -aux | grep java
```

 查看日志

```bash
tail -f  apps/fulikuang/..log
```

 查看网络

```undefined
sudo nethogs
```



NetHogs介绍

> NetHogs是一款开源、免费的，终端下的网络流量监控工具，它可监控Linux的进程或应用程序的网络流量。NetHogs只能实时监控进程的网络带宽占用情况。NetHogs支持IPv4和IPv6协议，支持本地网卡以及PPP链接。

 查看nginx日志

```bash
cd /var/log/nginx/
```



### 3.日志文件太大怎么打开

- 如果文件比较小的话，使用 vim 直接查看，如果文件比较大的话，使用 Vim 会直接卡住。
- 如果想要查看正在滚动的日志文件。这个命令可以查看大文件。

```undefined
tail -f file
```

- 如果文件比较大的话，也可以使用 less 命令

```undefined
less file
```



### 4.v-model

```csharp
  1. v-bind绑定一个value属性

  2. v-on指令给当前元素绑定input事件
```



## 高竞文化 深圳

#### 1.集合有哪种

Map接口和Collection接口

- Collection 接口的子接口包括：Set接口和List接口
- Map接口的实现类主要有：HashMap、TreeMap、Hashtable、ConcurrentHashMap以及Properties等
- Set接口的实现类主要有：HashSet、TreeSet、LinkedHashSet等
- List接口的实现类主要有：ArrayList、LinkedList、Stack 以及Vector 等

![image-20211020165545737](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211020165545737.png)

- List：一个有序（元素存入集合的顺序和取出的顺序一致）容器，元素可以重复，可以插入多个null元素，元素都有索引。常用的实现类有 ArrayList、LinkedList 和 Vector。
- Set：一个无序（存入和取出顺序有可能不一致）容器，不可以存储重复元素，只允许存入一个null元素，必须保证元素唯一性。Set 接口常用实现类是 HashSet、LinkedHashSet 以及 TreeSet。

#### 2.mysql索引

索引是一种特殊的文件（InnoDB数据表上的索引是表空间的一个组成部分），它们包含着对数据表里所有记录的引用指针

索引是一种数据结构。数据库索引，是数据库管理系统中一个排序的数据结构，以协助快速查询、更新数据库表中数据。索引的实现通常使用B树以及其变种B+树

更通俗的说，索引就相当于目录。为了方便查找书中的内容，通过对内容建立索引形参目录。索引是一个文件，它是要占物理空间的。

#### 3.覆盖索引

#### 4.spring和springboot区别

spring主要是对aop，ioc等思想做了一些实现，可以对代码做解耦。spring boot主要是简化开发一些环境的搭建。

Spring 是一个“引擎”

#### 5. springboot的自动装配

- 当启动springboot应用程序的时候，会先创建SpringApplication的对象。在SpringApplication对象的构造方法中会进行一些参数的初始化工作，最主要的是判断当前应用程序的类型以及初始化器和监听器。在初始化器这个过程会加载整个应用程序中的`spring.factories`文件，将文件的内容放到缓存对象中，方便后续获取。
- SpringApplication对象创建完成之后。开始执行run方法，来完成整个启动，启动过程中最主要的要两个方法，第一个是prepareContext,第二个叫做refreshContext,在这两个关键步骤中完成了自动装配的核心功能，前面的处理逻辑包含了上下文对象的创建，banner的打印，异常报告期的准备等各个准备工作，方便后续来进行调用
- 在`prepareContext`方法中主要完成的是对上下文对象的初始化操作，包括了属性值的设置，比如环境对象environment，整个过程有个非常重要的方法，叫做load，load主要完成一件事情，将当前主类作为一个beanDefinition注册到registry中，方便后续进行BeanFactoryPostProcessor调用执行的时候，找到对应的主类，来完成@SpringBootApplication，@EnableAutoConfiguration等注解的解析工作
- 在`refreshContext`方法中会进行整个容器刷新过程，会调用spring中的refresh方法，refresh中有13个非常关键的方法，来完成整个spring应用程序的启动，在自动装配过程中，解析处理各种注解，包含@PropertySource,@ComponentScan,@ComponentScans,@Bean,@Import等注解，最主要的是@Import注解的解析
- 在解析@Import注解的时候，会有一个getImports的方法，从主类开始递归解析注解，把所有包含@Import的注解都解析到，然后在processImport方法中对Import的类进行分类，此处主要识别的时候AutoConfigurationImportSelect归属于ImportSelect的子类，在后续过程中会调用deferredImportSelectorHandler中的process方法，来完成EnableAutoConfiguration的加载。

@Import注解就是给Spring容器中导入一些组件，这里传入了一个组件的选择器:AutoConfigurationImportSelector。

里面有一个selectImports方法，将所有需要导入的组件以全类名的方式返回；这些组件就会被添加到容器中。

> Spring Boot将相关配置都集成到了SpringBootApplication注解，在启动类加上该注解则标识为Spring Boot应用，进入SpringBootApplication类可以看到该类集成了@SpringBootConfiguration、@EnableAutoConfiguration、@ComponentScan三个注解，
>
> - SpringBootConfiguration继承了@Configuration，标识该类为Spring的配置类，在Spring启动IOC容器的时候可以识别并解析，
> - ComponentScan表示IOC容器启动时，需要去扫描注册的Spring组件，
> - EnableAutoConfiguration即标识开启Spring Boot 自动配置，进入之后发现其主要包含了两个注解，
>   - 一个为AutoConfigurationPackage，AutoConfigurationPackage默认没有扫描的包路径暂忽略
>   - 另一个为Import，Import注解导入了AutoConfigurationImportSelector，该类为Spring Boot自动装配核心类，通过该类自动装载了Spring Boot需要的对象到IOC，下面对该类进行重点讲解。

##### SPI机制

自动配置的核心是SPI机制，这里通过SPI机制，获取每种配置信息，然后通过classloader反射生成配置类。建议先研究下java spi机制。

SPI的Demo

第一步，定义一组接口：

```java
public interface UploadCDN {
    void upload(String url);
}
```

这个接口分别有两个实现：

```java
public class ChinaNetCDN implements UploadCDN {
    @Override
    public void upload(String url) {
        System.out.println("upload to chinaNet cdn");
    }

}
public class QiyiCDN implements UploadCDN {
    @Override
    public void upload(String url) {
        System.out.println("upload to qiyi cdn");
    }
}
```

然后需要在resources目录下新建META-INF/services目录，并且在这个目录下新建一个与上述接口的全限定名一致的文件，在这个文件中写入接口的实现类的全限定名：

![image-20211021100310137](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021100310137.png)

![image-20211021100336042](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021100336042.png)

这时，通过serviceLoader加载实现类并调用：

```java
public static void main(String[] args) {
        ServiceLoader<UploadCDN>  uploader =ServiceLoader.load(UploadCDN.class);
        for (UploadCDN uploadCDN : uploader) {
            uploadCDN.upload("filePath");
        }
    }
```

输出如下：

```css
upload to chinaNet cdn
upload to qiyi cdn
```

##### SPI原理解析

通过上面简单的demo，可以看到最关键的实现就是ServiceLoader这个类，可以看下这个类的源码，如下：

```java
public final class ServiceLoader<S> implements Iterable<S> {


    //扫描目录前缀
    private static final String PREFIX = "META-INF/services/";

    // 被加载的类或接口
    private final Class<S> service;

    // 用于定位、加载和实例化实现方实现的类的类加载器
    private final ClassLoader loader;

    // 上下文对象
    private final AccessControlContext acc;

    // 按照实例化的顺序缓存已经实例化的类
    private LinkedHashMap<String, S> providers = new LinkedHashMap<>();

    // 懒查找迭代器
    private java.util.ServiceLoader.LazyIterator lookupIterator;

    // 私有内部类，提供对所有的service的类的加载与实例化
    private class LazyIterator implements Iterator<S> {
        Class<S> service;
        ClassLoader loader;
        Enumeration<URL> configs = null;
        String nextName = null;

        //...
        private boolean hasNextService() {
            if (configs == null) {
                try {
                    //获取目录下所有的类
                    String fullName = PREFIX + service.getName();
                    if (loader == null)
                        configs = ClassLoader.getSystemResources(fullName);
                    else
                        configs = loader.getResources(fullName);
                } catch (IOException x) {
                    //...
                }
                //....
            }
        }

        private S nextService() {
            String cn = nextName;
            nextName = null;
            Class<?> c = null;
            try {
                //反射加载类
                c = Class.forName(cn, false, loader);
            } catch (ClassNotFoundException x) {
            }
            try {
                //实例化
                S p = service.cast(c.newInstance());
                //放进缓存
                providers.put(cn, p);
                return p;
            } catch (Throwable x) {
                //..
            }
            //..
        }
    }
}
```

下面贴出比较直观的spi加载的主要流程供参考：

![image-20211021101120347](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021101120347.png)

##### dubbo SPI

dubbo作为一个高度可扩展的rpc框架，也依赖于java的spi，并且dubbo对java原生的spi机制作出了一定的扩展，使得其功能更加强大。

首先，从上面的java spi的原理中可以了解到，java的spi机制有着如下的弊端：

- 只能遍历所有的实现，并全部实例化。
- 配置文件中只是简单的列出了所有的扩展实现，而没有给他们命名。导致在程序中很难去准确的引用它们。
- 扩展如果依赖其他的扩展，做不到自动注入和装配。
- 扩展很难和其他的框架集成，比如扩展里面依赖了一个Spring bean，原生的Java SPI不支持。

dubbo的spi有如下几个概念：

（1）**扩展点**：一个接口。

（2）**扩展**：扩展（接口）的实现。

（3）**扩展自适应实例：**其实就是一个Extension的代理，它实现了扩展点接口。在调用扩展点的接口方法时，会根据实际的参数来决定要使用哪个扩展。dubbo会根据接口中的参数，自动地决定选择哪个实现。

（4）**@SPI**:该注解作用于扩展点的接口上，表明该接口是一个扩展点。

（5）**@Adaptive：**@Adaptive注解用在扩展接口的方法上。表示该方法是一个自适应方法。Dubbo在为扩展点生成自适应实例时，如果方法有@Adaptive注解，会为该方法生成对应的代码。

dubbo的spi也会从某些固定的路径下去加载配置文件，并且配置的格式与java原生的不一样，类似于property文件的格式：

![image-20211021101735433](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021101735433.png)

下面将基于dubbo去实现一个简单的扩展实现。首先，要实现LoadBalance这个接口，当然这个接口是被注解标注的可以扩展的：

```java
@SPI("random")
public interface LoadBalance {
    @Adaptive({"loadbalance"})
    <T> Invoker<T> select(List<Invoker<T>> var1, URL var2, Invocation var3) throws RpcException;
}

public class DemoLoadBalance implements LoadBalance {

    @Override
    public <T> Invoker<T> select(List<Invoker<T>> invokers, URL url, Invocation invocation) throws RpcException {
        System.out.println("my demo loadBalance is used, hahahahh");
        return invokers.get(0);//选择第一个
    }
}
```

然后，需要在duboo SPI的扫描目录下，添加配置文件，注意配置文件的名称要和扩展点的接口名称对应起来：

![image-20211021101856336](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021101856336.png)

还需要在dubbo的spring配置中显式的声明，使用上面自己实现的负载均衡策略：

```csharp
  <dubbo:reference id="helloService" interface="com.dubbo.spi.demo.api.IHelloService" loadbalance="demo" />
```

然后，启动dubbo，调用service，就可以发现确实是使用了自定义的负载策略：

![image-20211021101923422](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021101923422.png)

至此，dubbo的spi的demo也完成了。

dubbo spi的原理和jdk的实现稍有不同，大概流程如下图，具体的实现可以自己了解下源码。

![image-20211021101956196](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211021101956196.png)

##### **AutoConfigurationImportSelector**

```java
public class AutoConfigurationImportSelector implements DeferredImportSelector, BeanClassLoaderAware,
      ResourceLoaderAware, BeanFactoryAware, EnvironmentAware, Ordered {

   private static final AutoConfigurationEntry EMPTY_ENTRY = new AutoConfigurationEntry();

   private static final String[] NO_IMPORTS = {};

   private static final Log logger = LogFactory.getLog(AutoConfigurationImportSelector.class);

   private static final String PROPERTY_NAME_AUTOCONFIGURE_EXCLUDE = "spring.autoconfigure.exclude";

   private ConfigurableListableBeanFactory beanFactory;

   private Environment environment;

   // 类加载器（AppClassLoader）
   private ClassLoader beanClassLoader;

   private ResourceLoader resourceLoader;

   private ConfigurationClassFilter configurationClassFilter;

   @Override
   // 获取需要自动装载的Bean的classname集合
   // ConfigurationClassPostProcessor解析配置类的时候会调用该方法
   public String[] selectImports(AnnotationMetadata annotationMetadata) {
      // 是否需要导入类，默认需要，不会进入此判断
      if (!isEnabled(annotationMetadata)) {
         return NO_IMPORTS;
      }
      // 获取自动装配对象（里面包含需要解析的配置类）
      AutoConfigurationEntry autoConfigurationEntry = getAutoConfigurationEntry(annotationMetadata);
      // 返回自动装配Bean的classname集合
      return StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());
   }

   @Override
   public Predicate<String> getExclusionFilter() {
      return this::shouldExclude;
   }

   private boolean shouldExclude(String configurationClassName) {
      return getConfigurationClassFilter().filter(Collections.singletonList(configurationClassName)).isEmpty();
   }

   /**
    * Return the {@link AutoConfigurationEntry} based on the {@link AnnotationMetadata}
    * of the importing {@link Configuration @Configuration} class.
    * @param annotationMetadata the annotation metadata of the configuration class
    * @return the auto-configurations that should be imported
    */
   protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
      if (!isEnabled(annotationMetadata)) {
         return EMPTY_ENTRY;
      }
      // 获取配置类所有注解属性，此处传入的类为EnableAutoConfiguration，获取到exclude和excludeName属性
      AnnotationAttributes attributes = getAttributes(annotationMetadata);
      // 获取配置类标注的所有候选配置类信息
      List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
      // 去除重复项
      configurations = removeDuplicates(configurations);
      // 获取需要排除的配置类（不需要注入容器的Bean）
      Set<String> exclusions = getExclusions(annotationMetadata, attributes);
      // 检查排除的配置类的合法性，如果不合法则抛出异常
      checkExcludedClasses(configurations, exclusions);
      // 从需要解析的配置类集合中剔除需要排除的配置类
      configurations.removeAll(exclusions);
      // 获取配置类过滤器对配置类进行过滤
      configurations = getConfigurationClassFilter().filter(configurations);
      // 开启记录自动化配置过程中条件匹配的详细信息及日志信息
      fireAutoConfigurationImportEvents(configurations, exclusions);
      return new AutoConfigurationEntry(configurations, exclusions);
   }

   @Override
   public Class<? extends Group> getImportGroup() {
      return AutoConfigurationGroup.class;
   }

   protected boolean isEnabled(AnnotationMetadata metadata) {
      if (getClass() == AutoConfigurationImportSelector.class) {
         return getEnvironment().getProperty(EnableAutoConfiguration.ENABLED_OVERRIDE_PROPERTY, Boolean.class, true);
      }
      return true;
   }

    // 获取注解的所有属性
   protected AnnotationAttributes getAttributes(AnnotationMetadata metadata) {
      String name = getAnnotationClass().getName();
      AnnotationAttributes attributes = AnnotationAttributes.fromMap(metadata.getAnnotationAttributes(name, true));
      Assert.notNull(attributes, () -> "No auto-configuration attributes found. Is " + metadata.getClassName()
            + " annotated with " + ClassUtils.getShortName(name) + "?");
      return attributes;
   }

   /**
    * Return the source annotation class used by the selector.
    * @return the annotation class
    */
   protected Class<?> getAnnotationClass() {
      return EnableAutoConfiguration.class;
   }

   /**
    * Return the auto-configuration class names that should be considered. By default
    * this method will load candidates using {@link SpringFactoriesLoader} with
    * {@link #getSpringFactoriesLoaderFactoryClass()}.
    * @param metadata the source metadata
    * @param attributes the {@link #getAttributes(AnnotationMetadata) annotation
    * attributes}
    * @return a list of candidate configurations
    */
   protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
      /**
       * 通过SpringFactoriesLoader去所有jar包中META-INF/spring.factories路径下获取
       * 标注key为org.springframework.boot.autoconfigure.EnableAutoConfiguration（getSpringFactoriesLoaderFactoryClass返回值）的所有配置类。
       * org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
       * org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
       * org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
       * org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
       * SpringFactoriesLoader.loadFactoryNames运用SPI的机制读取文件内容（不清楚SPI可以参考第一章节）
       **/
      List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
            getBeanClassLoader());
      Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
            + "are using a custom packaging, make sure that file is correct.");
      return configurations;
   }

   /**
    * Return the class used by {@link SpringFactoriesLoader} to load configuration
    * candidates.
    * @return the factory class
    */
   protected Class<?> getSpringFactoriesLoaderFactoryClass() {
      return EnableAutoConfiguration.class;
   }

   private void checkExcludedClasses(List<String> configurations, Set<String> exclusions) {
      // 如果排除的配置类能能正常加载，并且在自动装配的配置类集合中不存在，则添加到非验证的排除类集合中
      List<String> invalidExcludes = new ArrayList<>(exclusions.size());
      for (String exclusion : exclusions) {
         // 检验类能否加载
         if (ClassUtils.isPresent(exclusion, getClass().getClassLoader()) && !configurations.contains(exclusion)) {
            invalidExcludes.add(exclusion);
         }
      }
      // 非验证的排除类集合不为空的话抛出异常
      if (!invalidExcludes.isEmpty()) {
         handleInvalidExcludes(invalidExcludes);
      }
   }

   /**
    * Handle any invalid excludes that have been specified.
    * @param invalidExcludes the list of invalid excludes (will always have at least one
    * element)
    */
   protected void handleInvalidExcludes(List<String> invalidExcludes) {
      StringBuilder message = new StringBuilder();
      for (String exclude : invalidExcludes) {
         message.append("\t- ").append(exclude).append(String.format("%n"));
      }
      throw new IllegalStateException(String.format(
            "The following classes could not be excluded because they are not auto-configuration classes:%n%s",
            message));
   }

   /**
    * Return any exclusions that limit the candidate configurations.
    * @param metadata the source metadata
    * @param attributes the {@link #getAttributes(AnnotationMetadata) annotation
    * attributes}
    * @return exclusions or an empty set
    */
   protected Set<String> getExclusions(AnnotationMetadata metadata, AnnotationAttributes attributes) {
      Set<String> excluded = new LinkedHashSet<>();
      excluded.addAll(asList(attributes, "exclude"));
      excluded.addAll(Arrays.asList(attributes.getStringArray("excludeName")));
      excluded.addAll(getExcludeAutoConfigurationsProperty());
      return excluded;
   }

   /**
    * Returns the auto-configurations excluded by the
    * {@code spring.autoconfigure.exclude} property.
    * @return excluded auto-configurations
    * @since 2.3.2
    */
   protected List<String> getExcludeAutoConfigurationsProperty() {
      Environment environment = getEnvironment();
      if (environment == null) {
         return Collections.emptyList();
      }
      if (environment instanceof ConfigurableEnvironment) {
         Binder binder = Binder.get(environment);
         return binder.bind(PROPERTY_NAME_AUTOCONFIGURE_EXCLUDE, String[].class).map(Arrays::asList)
               .orElse(Collections.emptyList());
      }
      String[] excludes = environment.getProperty(PROPERTY_NAME_AUTOCONFIGURE_EXCLUDE, String[].class);
      return (excludes != null) ? Arrays.asList(excludes) : Collections.emptyList();
   }

   protected List<AutoConfigurationImportFilter> getAutoConfigurationImportFilters() {
      return SpringFactoriesLoader.loadFactories(AutoConfigurationImportFilter.class, this.beanClassLoader);
   }

   private ConfigurationClassFilter getConfigurationClassFilter() {
      if (this.configurationClassFilter == null) {
         /**
          * 获取配置类过滤器
          * 通过SpringFactoriesLoader去所有jar包中（此处为spring-boot-autoconfigure jar包）META-INF/spring.factories中
          * 标注key为oorg.springframework.boot.autoconfigure.AutoConfigurationImportFilter的所有过滤器
          * org.springframework.boot.autoconfigure.AutoConfigurationImportFilter=\
          * org.springframework.boot.autoconfigure.condition.OnBeanCondition,\
          * org.springframework.boot.autoconfigure.condition.OnClassCondition,\
          * org.springframework.boot.autoconfigure.condition.OnWebApplicationCondition
          * 这些类作用于Conditional开头的注解，例如ConditionalOnBean、ConditionalOnMissingBean、ConditionalOnMissingClass等
          */
         List<AutoConfigurationImportFilter> filters = getAutoConfigurationImportFilters();
         for (AutoConfigurationImportFilter filter : filters) {
            // 调用Aware接口方法，将相关属性设置到Aware实现类的属性中，
            //此处是将容器的工厂设置到过滤器的beanFactory属性中
            invokeAwareMethods(filter);
         }
         this.configurationClassFilter = new ConfigurationClassFilter(this.beanClassLoader, filters);
      }
      return this.configurationClassFilter;
   }

    // 通过set去重
   protected final <T> List<T> removeDuplicates(List<T> list) {
      return new ArrayList<>(new LinkedHashSet<>(list));
   }

   protected final List<String> asList(AnnotationAttributes attributes, String name) {
      String[] value = attributes.getStringArray(name);
      return Arrays.asList(value);
   }

   private void fireAutoConfigurationImportEvents(List<String> configurations, Set<String> exclusions) {
      /**
       * 通过SpringFactoriesLoader去所有jar包中（此处为spring-boot-autoconfigure jar包）META-INF/spring.factories中
       * 标注key为oorg.springframework.boot.autoconfigure.AutoConfigurationImportListener的所有监听器
       * org.springframework.boot.autoconfigure.AutoConfigurationImportListener=\
       * org.springframework.boot.autoconfigure.condition.ConditionEvaluationReportAutoConfigurationImportListener
       */
      List<AutoConfigurationImportListener> listeners = getAutoConfigurationImportListeners();
      if (!listeners.isEmpty()) {
         AutoConfigurationImportEvent event = new AutoConfigurationImportEvent(this, configurations, exclusions);
         for (AutoConfigurationImportListener listener : listeners) {
            // 调用Aware接口方法，将相关属性设置到Aware实现类的属性中，
            //此处是将容器的工厂设置到过滤器的beanFactory属性中
            invokeAwareMethods(listener);
            listener.onAutoConfigurationImportEvent(event);
         }
      }
   }

   protected List<AutoConfigurationImportListener> getAutoConfigurationImportListeners() {
      return SpringFactoriesLoader.loadFactories(AutoConfigurationImportListener.class, this.beanClassLoader);
   }

   private void invokeAwareMethods(Object instance) {
      if (instance instanceof Aware) {
         // 设置Bean的类装载器
         if (instance instanceof BeanClassLoaderAware) {
            ((BeanClassLoaderAware) instance).setBeanClassLoader(this.beanClassLoader);
         }
         // 设置Bean工厂
         if (instance instanceof BeanFactoryAware) {
            ((BeanFactoryAware) instance).setBeanFactory(this.beanFactory);
         }
         //
         if (instance instanceof EnvironmentAware) {
            ((EnvironmentAware) instance).setEnvironment(this.environment);
         }
         // 设置资源加载器
         if (instance instanceof ResourceLoaderAware) {
            ((ResourceLoaderAware) instance).setResourceLoader(this.resourceLoader);
         }
      }
   }

   ......

   private static class ConfigurationClassFilter {

      private final AutoConfigurationMetadata autoConfigurationMetadata;

      private final List<AutoConfigurationImportFilter> filters;

      ConfigurationClassFilter(ClassLoader classLoader, List<AutoConfigurationImportFilter> filters) {
         this.autoConfigurationMetadata = AutoConfigurationMetadataLoader.loadMetadata(classLoader);
         this.filters = filters;
      }

      // 将不符合的配置类剔除，例如配置了ConditionalOnMissingClass，则表示ConditionalOnMissingClass注解中配置的类不存在才会加载当前类
      List<String> filter(List<String> configurations) {
         long startTime = System.nanoTime();
         String[] candidates = StringUtils.toStringArray(configurations);
         boolean skipped = false;
         for (AutoConfigurationImportFilter filter : this.filters) {
            /**
             * 对需要加载的配置类进行过滤处理，
             * 处理配置了Conditional开头的注解的配置类，
             * 具体过滤规则可阅读FilteringSpringBootCondition的match方法
             */
            boolean[] match = filter.match(candidates, this.autoConfigurationMetadata);
            for (int i = 0; i < match.length; i++) {
               // 如果过滤规则匹配成功，则将配置类删除（数组元素赋空）
               if (!match[i]) {
                  candidates[i] = null;
                  skipped = true;
               }
            }
         }
         // 匹配不到返回原配置类集合
         if (!skipped) {
            return configurations;
         }
         // 将空的配置类删除，并返回删除之后的配置类集合
         List<String> result = new ArrayList<>(candidates.length);
         for (String candidate : candidates) {
            if (candidate != null) {
               result.add(candidate);
            }
         }
         if (logger.isTraceEnabled()) {
            int numberFiltered = configurations.size() - result.size();
            logger.trace("Filtered " + numberFiltered + " auto configuration class in "
                  + TimeUnit.NANOSECONDS.toMillis(System.nanoTime() - startTime) + " ms");
         }
         return result;
      }

   }

   private static class AutoConfigurationGroup
         implements DeferredImportSelector.Group, BeanClassLoaderAware, BeanFactoryAware, ResourceLoaderAware {

      private final Map<String, AnnotationMetadata> entries = new LinkedHashMap<>();

      private final List<AutoConfigurationEntry> autoConfigurationEntries = new ArrayList<>();

      ......

      @Override
      public void process(AnnotationMetadata annotationMetadata, DeferredImportSelector deferredImportSelector) {
         Assert.state(deferredImportSelector instanceof AutoConfigurationImportSelector,
               () -> String.format("Only %s implementations are supported, got %s",
                     AutoConfigurationImportSelector.class.getSimpleName(),
                     deferredImportSelector.getClass().getName()));
         // 获取自动装配对象（里面包含需要解析的配置类）
         AutoConfigurationEntry autoConfigurationEntry = ((AutoConfigurationImportSelector) deferredImportSelector)
               .getAutoConfigurationEntry(annotationMetadata);
         this.autoConfigurationEntries.add(autoConfigurationEntry);
         for (String importClassName : autoConfigurationEntry.getConfigurations()) {
            this.entries.putIfAbsent(importClassName, annotationMetadata);
         }
      }

      @Override
      public Iterable<Entry> selectImports() {
         if (this.autoConfigurationEntries.isEmpty()) {
            return Collections.emptyList();
         }
         // 获取需要排除的类
         Set<String> allExclusions = this.autoConfigurationEntries.stream()
               .map(AutoConfigurationEntry::getExclusions).flatMap(Collection::stream).collect(Collectors.toSet());
         // 获取所有需要解析的配置类
         Set<String> processedConfigurations = this.autoConfigurationEntries.stream()
               .map(AutoConfigurationEntry::getConfigurations).flatMap(Collection::stream)
               .collect(Collectors.toCollection(LinkedHashSet::new));
         // 移除不需要处理的配置类
         processedConfigurations.removeAll(allExclusions);

         return sortAutoConfigurations(processedConfigurations, getAutoConfigurationMetadata()).stream()
               .map((importClassName) -> new Entry(this.entries.get(importClassName), importClassName))
               .collect(Collectors.toList());
      }

      private AutoConfigurationMetadata getAutoConfigurationMetadata() {
         if (this.autoConfigurationMetadata == null) {
            this.autoConfigurationMetadata = AutoConfigurationMetadataLoader.loadMetadata(this.beanClassLoader);
         }
         return this.autoConfigurationMetadata;
      }

      private List<String> sortAutoConfigurations(Set<String> configurations,
            AutoConfigurationMetadata autoConfigurationMetadata) {
         return new AutoConfigurationSorter(getMetadataReaderFactory(), autoConfigurationMetadata)
               .getInPriorityOrder(configurations);
      }

      private MetadataReaderFactory getMetadataReaderFactory() {
         try {
            return this.beanFactory.getBean(SharedMetadataReaderFactoryContextInitializer.BEAN_NAME,
                  MetadataReaderFactory.class);
         }
         catch (NoSuchBeanDefinitionException ex) {
            return new CachingMetadataReaderFactory(this.resourceLoader);
         }
      }

   }

   protected static class AutoConfigurationEntry {

      private final List<String> configurations;

      private final Set<String> exclusions;

      private AutoConfigurationEntry() {
         this.configurations = Collections.emptyList();
         this.exclusions = Collections.emptySet();
      }

      /**
       * Create an entry with the configurations that were contributed and their
       * exclusions.
       * @param configurations the configurations that should be imported
       * @param exclusions the exclusions that were applied to the original list
       */
      AutoConfigurationEntry(Collection<String> configurations, Collection<String> exclusions) {
         this.configurations = new ArrayList<>(configurations);
         this.exclusions = new HashSet<>(exclusions);
      }

      public List<String> getConfigurations() {
         return this.configurations;
      }

      public Set<String> getExclusions() {
         return this.exclusions;
      }

   }

}
```

- SpringBoot2.2.5自动配置原理之selectImports没有调用

调用的是这个类的内部类AutoConfigurationGroup的selectImports()方法

org.springframework.boot.autoconfigure.AutoConfigurationImportSelector#getAutoConfigurationEntry 调用是这个方法



## 一应科技



### 红黑树怎么平衡



### 怎么统一异常管理



### Servlet生命周期

init() service() destroy()



### vue怎么渲染页面

vue推荐在绝大多数情况下使用template来创建你的html。但是模板毕竟是模板，不是真实的dom节点。从模板到真实dom节点还需要经过一些步骤

1. 将模板编译为render函数
2. 实例进行挂载，根据根节点render函数的调用，递归生成虚拟dom
3. 对比虚拟dom，渲染到真实dom
4. 组件内部data发生变化，组件和子组件引用data作为props重新调用render函数，生成虚拟dom，返回步骤3

[查看详情](https://segmentfault.com/a/1190000018495383)



### 项目中Redis使用了哪种数据类型

![image-20211028112809414](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211028112809414.png)



### 堆和栈的区别

1.栈内存存储的是局部变量而堆内存存储的是实体；

2.栈内存的更新速度要快于堆内存，因为局部变量的生命周期很短；

3.栈内存存放的变量生命周期一旦结束就会被释放，而堆内存存放的实体会被垃圾回收机制不定时的回收。



### HashCode 和 equals

HashCode相等时，对象不一定相等

equals相等时，要保证HashCode相等



### equals相等时，对象一定相等么

通过hashCode()和equals()必须能唯一确定一个对象。

没重写equals，return (this == obj)比较的是内存地址

重写了equals，对象内存地址不一定相对



### HashCode和equals在哪里应用

Java中的HashMap使用hashCode()和equals()方法来确定键值对的索引，当根据键获取值的时候也会用到这两个方法。
如果没有正确的实现这两个方法，两个不同的键可能会有相同的hash值，因此可能会被集合认为是相等的。
而且，这两个方法也用来发现重复元素，所以这两个方法的实现对HashMap的精确性和正确性是至关重要的。



### 怎么获得yaml的属性

方式1 - 正常使用

- yml配置文件部分

```ruby
# 自己配置的参数
savePath : /Users/a/Desktop/test998/
libraryPath : /opt/local/share/OpenCV/java/libopencv_java347.dylib
```

- 正常读取代码

```java
@Service
public class TesseractOrcServiceImpl implements TesseractOrcService {

    @Value("${savePath}")
    private  String savePath ;
}
```

方式2 - 封装使用

将属性封装进一个类，对外暴露静态常量

新建一个类，使用@Component，实现InitializingBean接口，并重写afterPropertiesSet()方法，在方法里赋值给静态常量

```java
@Component
public class TesseractOrcProperties implements InitializingBean {

    //accessKey
    @Value("${savePath}")
    private String savePath;

    public static String SAVE_PATH;

    @Override
    public void afterPropertiesSet() throws Exception {
        SAVE_PATH = savePath;
    }
}
```

方式3 - 静态变量赋值

在处理静态变量时候，使用上面的@Value的用法是无法获取到配置文件中的数据的，只能获取到null，所以要进行如下更改。

1. 利用IDEA生成该静态变量的set方法，然后**删除该方法的static修饰**
2. 然后将注解@Value写在set函数上面
   这样就可以正常读取到配置文件中的信息

```java
@Service
public class TesseractOrcServiceImpl implements TesseractOrcService {

    private static String savePath ;

    @Value("${savePath}")
    public void setSavePath(String savePath) {
        TesseractOrcServiceImpl.savePath = savePath;
    }

    @Override
    public ResultBean ScanVinForTesseractOrc(String url) {
        String str = null;
        try {
            if(!FileUtil.exist(savePath)){
                FileUtil.mkdir(savePath);
            }
        } catch (Exception e) {
            String errerMsg=ExceptionUtil.stacktraceToString(e);
            logger.error(errerMsg);
        }
        return null;
    }
}
```

方式4 - 在静态代码块中赋值使用

在我的系统中，我有一个工具类需要加载系统的静态资源库
所以要在工具类的静态代码块中获取配置文件中的属性，我使用上面那种方法，发现读取到的依然是null.

因为静态代码块是在spring操作之前执行，所以是获取不到数据的。

参考[博客](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.iiocode.com%2Fpost%2F262.html)测试了一下，发现真是个不错的想法

ApplicationContextHolder.java 源码

```java
package hai.guo.novel.config;

import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.stereotype.Component;

/**
 * @program: novel
 * @description: Redis缓存帮助类,从spring容器中获取bean
 **/
@Component
public class ApplicationContextHolder implements ApplicationContextAware {
    private static ApplicationContext applicationContext;

    @Override
    public void setApplicationContext(ApplicationContext ctx) throws BeansException {
        applicationContext = ctx;
    }

    /**
     * 从 everywhere 获取ApplicationContext
     *
     * @return
     */
    public static ApplicationContext getApplicationContext() {
        return applicationContext;
    }

    /**
     * 根据class获取bean
     *
     * @param clazz
     * @param <T>
     * @return
     */
    public static <T> T getBean(Class<T> clazz) {
        return applicationContext.getBean(clazz);
    }

    /**
     * 根据名称获取bean
     *
     * @param name
     * @param <T>
     * @return
     */
    @SuppressWarnings("unchecked")
    public static <T> T getBean(String name) {
        return (T) applicationContext.getBean(name);
    }
}
```

> Aware
>
> `Spring`的依赖注入的最大亮点就是你所有的`Bean`对`Spring`容器的存在是没有意识的。即你可以将你的容器替换成别的容器，例如`Goggle Guice`,这时`Bean`之间的耦合度很低。
>
> 但是在实际的项目中，我们不可避免的要用到`Spring`容器本身的功能资源，这时候`Bean`必须要意识到`Spring`容器的存在，才能调用`Spring`所提供的资源，这就是所谓的`Spring` `Aware`。其实`Spring` `Aware`本来就是`Spring`设计用来框架内部使用的，若使用了`Spring` `Aware`，你的`Bean`将会和`Spring`框架耦合。
>
> 例如
>
> - 定义两个`User`,一个实现`BeanNameAware`,一个不实现。
>
> - 在Spring配置文件中初始化两个对象。
>
>   ```xml
>    <bean id="zhangsan"  class="com.zsr.example.User">
>           <property name="name" value="zhangsan"></property>
>           <property name="address" value="火星"></property>
>       </bean>
>   
>       <bean id="lisi"  class="com.zsr.example.User2">
>           <property name="name" value="lisi"></property>
>           <property name="address" value="火星"></property>
>       </bean>
>   ```
>
> main方法测试一下`BeanNameAware`接口所起的作用。
>
> ```java
>   public static void main(String[] args) {
>           ApplicationContext context = new ClassPathXmlApplicationContext("classpath:application-beanaware.xml");
> 
>           User user=context.getBean(User.class);
>           System.out.println(String.format("实现了BeanNameAware接口的信息BeanId=%s,所有信息=%s",user.getId(),user.toString()));
> 
>           User2 user2=context.getBean(User2.class);
>           System.out.println(String.format("未实现BeanNameAware接口的信息BeanId=%s,所有信息=%s",user2.getId(),user2.toString()));
>       }
> ```
>
> 运行结果
>
> ```txt
> 实现了BeanNameAware接口的信息BeanId=zhangsan,所有信息=User{id='zhangsan', name='zhangsan', address='火星'}
> 未实现BeanNameAware接口的信息BeanId=null,所有信息=User{id='null', name='lisi', address='火星'}
> ```
>
> 能够看到，我们在实现了`BeanNameAware`的 `User`中，获取到了Spring容器中的`BeanId`（对应`spring配置文件`中的`id`属性），而没有实现`BeanNameAware`的`User2`，则不能获取到Spring容器中的Id属性。
>
> **所以`BeanNameAware`接口是为了让自身`Bean`能够感知到，获取到自身在Spring容器中的id属性。**
>
> **同理，其他的`Aware`接口也是为了能够感知到自身的一些属性。
> 比如实现了`ApplicationContextAware`接口的类，能够获取到`ApplicationContext`，实现了`BeanFactoryAware`接口的类，能够获取到`BeanFactory`对象。**

使用案例

1. 创建一个环境变量配置文件
   CrmProperties.java

   ```java
   package hai.guo.novel.config;
   
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.stereotype.Component;
   
   /**
    * <p>
    * ** 系统环境变量设置 **
    * </p>
    *
    * @author douguohai
    * @since 2019-10-16
    */
   @Component
   public class CrmProperties {
   
       /**
        * 执行环境 opencv 静态库文件地址
        */
       @Value("${libraryPath}")
       private String libraryPath;
   
       private CrmProperties() {
       }
   
       public String getLibraryPath() {
           return libraryPath;
       }
   }
   ```

1. 实际操作

   ```java
   /**
    * opencv的一些通用方法工具类
    */
   public class GeneralUtils {
   
       private static final int BLACK = 0;
       private static final int WHITE = 255;
   
       // 设置归一化图像的固定大小
       private static final Size dsize = new Size(32, 32);
   
       private static String libraryPath;
   
       static {
           try {
               CrmProperties crmProperties=ApplicationContextHolder.getBean(CrmProperties.class);
               libraryPath=crmProperties.getLibraryPath();
               System.load(libraryPath);
           }catch (Exception e){
               e.printStackTrace();
               throw new BusinessException("未找到opencv库",-1);
           }
       }
   }
   ```

   上面的代码中，先封装一个bean来初始化相关的配置，然后利用工具类在静态代码块中获取到这个bean对象，用这个bean对象来初始化工具类中的相关属性。



## 南宁



### Vue和react，为什么选择Vue



### IPv4和IPv6的区别

1.IPv6的地址空间更大。IPv4中规定IP地址长度为32,即有2^32-1个地址；而IPv6中IP地址的长度为128,即有2^128-1个地址。夸张点说就是，如果IPV6被广泛应用以后，全世界的每一粒沙子都会有相对应的一个IP地址。
2.IPv6的路由表更小。IPv6的地址分配一开始就遵循聚类(Aggregation)的原则,这使得路由器能在路由表中用一条记录(Entry)表示一片子网,大大减小了路由器中路由表的长度,提高了路由器转发数据包的速度。
3.IPv6的组播支持以及对流的支持增强。这使得网络上的多媒体应用有了长足发展的机会，为服务质量控制提供了良好的网络平台。
4.IPv6加入了对自动配置的支持。这是对DHCP协议的改进和扩展，使得网络(尤其是局域网)的管理更加方便和快捷。
5.IPv6具有更高的安全性。在使用IPv6网络中，用户可以对网络层的数据进行加密并对IP报文进行校验，这极大地增强了网络安全。



### webSocket

https://www.zhihu.com/question/20215561

可以把 WebSocket 看成是 HTTP 协议为了支持长连接所打的一个大补丁，它和 HTTP 有一些共性，是为了解决 HTTP 本身无法解决的某些问题而做出的一个改良设计。在以前 HTTP 协议中所谓的 keep-alive connection 是指在一次 TCP 连接中完成多个 HTTP 请求，但是对每个请求仍然要单独发 header；所谓的 polling 是指从客户端（一般就是浏览器）不断主动的向服务器发 HTTP 请求查询是否有新数据。这两种模式有一个共同的缺点，就是除了真正的数据部分外，服务器和客户端还要大量交换 HTTP header，信息交换效率很低。它们建立的“长连接”都是伪.长连接，只不过好处是不需要对现有的 HTTP server 和浏览器架构做修改就能实现。

WebSocket 解决的第一个问题是，通过第一个 HTTP request 建立了 TCP 连接之后，之后的交换数据都不需要再发 HTTP request了，使得这个长连接变成了一个真.长连接。但是不需要发送 HTTP header就能交换数据显然和原有的 HTTP 协议是有区别的，所以它需要对服务器和客户端都进行升级才能实现。在此基础上 WebSocket 还是一个双通道的连接，在同一个 TCP 连接上既可以发也可以收信息。此外还有 multiplexing 功能，几个不同的 URI 可以复用同一个 WebSocket 连接。这些都是原来的 HTTP 不能做到的。

另外说一点技术细节，因为看到有人提问 WebSocket 可能进入某种半死不活的状态。这实际上也是原有网络世界的一些缺陷性设计。上面所说的 WebSocket 真.长连接虽然解决了服务器和客户端两边的问题，但坑爹的是网络应用除了服务器和客户端之外，另一个巨大的存在是中间的网络链路。一个 HTTP/WebSocket 连接往往要经过无数的路由，防火墙。你以为你的数据是在一个“连接”中发送的，实际上它要跨越千山万水，经过无数次转发，过滤，才能最终抵达终点。在这过程中，中间节点的处理方法很可能会让你意想不到。

比如说，这些坑爹的中间节点可能会认为一份连接在一段时间内没有数据发送就等于失效，它们会自作主张的切断这些连接。在这种情况下，不论服务器还是客户端都不会收到任何提示，它们只会一厢情愿的以为彼此间的红线还在，徒劳地一边又一边地发送抵达不了彼岸的信息。而计算机网络协议栈的实现中又会有一层套一层的缓存，除非填满这些缓存，你的程序根本不会发现任何错误。这样，本来一个美好的 WebSocket 长连接，就可能在毫不知情的情况下进入了半死不活状态。

而解决方案，WebSocket 的设计者们也早已想过。就是让服务器和客户端能够发送 Ping/Pong Frame（[RFC 6455 - The WebSocket Protocol](https://link.zhihu.com/?target=https%3A//tools.ietf.org/html/rfc6455%23section-5.5.2)）。这种 Frame 是一种特殊的数据包，它只包含一些元数据而不需要真正的 Data Payload，可以在不影响 Application 的情况下维持住中间网络的连接状态。



### Docket自定义容器



## 深圳



### Java Bean 生命周期以及初始化后的方法

图一

![image-20211026214537152](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211026214537152.png)

图二

![image-20211103120931311](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211103120931311.png)

```java
public interface BeanPostProcessor {
    //bean初始化方法调用前被调用
    Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException;
    //bean初始化方法调用后被调用
    Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;
}
```

使用实例

```java
/**
 * 后置处理器：初始化前后进行处理工作
 * 将后置处理器加入到容器中
 */
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessBeforeInitialization..."+beanName+"=>"+bean);
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessAfterInitialization..."+beanName+"=>"+bean);
        return bean;
    }

}
```



### js深拷贝

在JS中，数据类型分为基本**数据类型**和**引用数据**类型两种，对于基本数据类型来说，它的值直接存储在栈内存中，而对于引用类型来说，它在栈内存中仅仅存储了一个引用，而真正的数据存储在堆内存中



### spring boot 事务

Spring Boot中实现事务没有额外的Jar包，还是基本的数据库访问包，比如`mybatis`

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.2</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.13</version>
</dependency>
```

注解事务`@Transactional`

```java
@Service
public class PersonService {
    @Resource
    private PersonMapper personMapper;

    @Resource
    private CompanyMapper companyMapper;

    @Transactional(rollbackFor = {RuntimeException.class, Error.class})
    public void saveOne(Person person) {
        Company company = new Company();
        company.setName("tenmao:" + person.getName());
        companyMapper.insertOne(company);
        personMapper.insertOne(person);
    }
}
```

注解属性

- `rollbackFor`：触发回滚的异常，默认是`RuntimeException`和`Error`
- `isolation`: 事务的隔离级别，默认是`Isolation.DEFAULT`也就是数据库自身的默认隔离级别，比如MySQL是`ISOLATION_REPEATABLE_READ`可重复读

> 这样就可以了，不需要其他配置。

*ps：网络上还说要在`@SpringBootApplication`上添加注解`@EnableTransactionManagement`，已经不需要了*



### 对servlet的了解

Java Servlet单例多线程机制



### 操作系统内存页面置换

https://www.jianshu.com/p/486f48d552e6



### redis雪崩

https://www.cnblogs.com/myseries/p/12853369.html

Redis 雪崩：

　　雪崩就是指缓存中**大批量热点数据过期**后系统涌入大量查询请求，因为大部分数据在Redis层已经失效，请求渗透到数据库层，大批量请求犹如洪水一般涌入，引起数据库压力造成查询堵塞甚至宕机。

解决办法：

1. 将缓存失效时间分散开，比如每个key的过期时间是随机，防止同一时间大量数据过期现象发生，这样不会出现同一时间全部请求都落在数据库层，如果缓存数据库是分布式部署，将热点数据均匀分布在不同Redis和数据库中，有效分担压力，别一个人扛。
2. 简单粗暴，让Redis数据永不过期（如果业务准许，比如不用更新的名单类）。当然，如果业务数据准许的情况下可以，比如中奖名单用户，每期用户开奖后，名单不可能会变了，无需更新。

对于系统 A，假设每天高峰期每秒 5000 个请求，本来缓存在高峰期可以扛住每秒 4000 个请求，但是缓存机器意外发生了全盘宕机。缓存挂了，此时 1 秒 5000 个请求全部落数据库，数据库必然扛不住，它会报一下警，然后就挂了。此时，如果没有采用什么特别的方案来处理这个故障，DBA 很着急，重启数据库，但是数据库立马又被新的流量给打死了。

![image-20211103143636142](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211103143636142.png)

缓存雪崩的事前事中事后的解决方案如下。

- 事前：redis 高可用，主从+哨兵，redis cluster集群，避免全盘崩溃。

> redis最开始使用主从模式做集群，若master宕机需要手动配置slave转为master；后来为了高可用提出来哨兵模式，该模式下有一个哨兵监视master和slave，若master宕机可自动将slave转为master，但它也有一个问题，就是不能动态扩充；所以在3.x提出cluster集群模式。

- 事中：本地 ehcache 缓存 + hystrix 限流&降级，避免 MySQL 被打死。

> EhCache 是一个纯Java的进程内缓存框架
>
> Hystrix是Netflix开源的一款容错框架

- 事后：redis 持久化，一旦重启，自动从磁盘上加载数据，快速恢复缓存数据。

 用户发送一个请求，系统 A 收到请求后，先查本地 ehcache 缓存，如果没查到再查 redis。如果 ehcache 和 redis 都没有，再查数据库，将数据库中的结果，写入 ehcache 和 redis 中。

　　限流组件，可以设置每秒的请求，有多少能通过组件，剩余的未通过的请求，怎么办？**走降级**！可以返回一些默认的值，或者友情提示，或者空白的值。

　　好处： - 数据库绝对不会死，限流组件确保了每秒只有多少个请求能通过。 - 只要数据库不死，就是说，对用户来说，2/5 的请求都是可以被处理的。 - 只要有 2/5 的请求可以被处理，就意味着你的系统没死，对用户来说，可能就是点击几次刷不出来页面，但是多点几次，就可以刷出来一次



### redis穿透

 对于系统A，假设一秒 5000 个请求，结果其中 4000 个请求是黑客发出的恶意攻击。

　　黑客发出的那 4000 个攻击，缓存中查不到，每次你去数据库里查，也查不到。

　　举个栗子。数据库 id 是从 1 开始的，结果黑客发过来的请求 id 全部都是负数。这样的话，缓存中不会有，请求每次都“视缓存于无物”，直接查询数据库。这种恶意攻击场景的缓存穿透就会直接把数据库给打死。

解决方式很简单，每次系统 A 从数据库中只要没查到，就写一个空值到缓存里去，比如 `set -999 UNKNOWN`。然后设置一个过期时间，这样的话，下次有相同的 key 来访问的时候，在缓存失效之前，都可以直接从缓存中取数据。



### redis击穿

缓存击穿，就是说某个 key 非常热点，访问非常频繁，处于集中式高并发访问的情况，当这个 key 在失效的瞬间，大量的请求就击穿了缓存，直接请求数据库，就像是在一道屏障上凿开了一个洞。

　　解决方式也很简单，可以将热点数据设置为永远不过期；或者基于 redis or zookeeper 实现互斥锁，等待第一个请求构建完缓存之后，再释放锁，进而其它请求才能通过该 key 访问数据。

```java
public String get(key) {
    String value = redis.get(key);
    if (value == null) { //代表缓存值过期
        //设置3min的超时，防止del操作失败的时候，下次缓存过期一直不能load db
        if (redis.setnx(key_mutex, 1, 3 * 60) == 1) {  //代表设置成功
            value = db.get(key);
            redis.set(key, value, expire_secs);
            redis.del(key_mutex);
        } else {  //这个时候代表同时候的其他线程已经load db并回设到缓存了，这时候重试获取缓存值即可
            sleep(50);
            get(key);  //重试
        }
    else {
        return value;      
    }
}
```



### synchronized(this) 和synchronized(Object.class)的区别



### 常用的数据库



### mySql分页



### 对java体系比较了解的是什么



### springboot怎么排除配置

方法1

使用 @SpringBootApplication 注解，用 exclude 属性进行排除指定的类：

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class Application {
    // ...
}
```

方法2

单独使用 @EnableAutoConfiguration 注解的时候：

```java
@EnableAutoConfiguration(exclude = {DataSourceAutoConfiguration.class})
public class Application {
    // ...
}
```

方法3

使用 @SpringCloudApplication 注解的时候：

```less
@EnableAutoConfiguration(exclude = {DataSourceAutoConfiguration.class})
@SpringCloudApplication
public class Application {
    // ...
}
```

方法4

终极方案，不管是 Spring Boot 还是 Spring Cloud 都可以搞定，在配置文件中指定参数 spring.autoconfigure.exclude 进行排除：

```ini
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

或者还可以这样写：

```undefined
spring.autoconfigure.exclude[0]=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

yml 配置文件：

```yaml
spring:     
  autoconfigure:
    exclude:
      - org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```



### thraedLocad的理解

https://blog.csdn.net/zzg1229059735/article/details/82715741



### Vue页面参数传递

[vue页面间参数传递的方法总结](https://blog.csdn.net/huazhongkejidaxuezpp/article/details/84309618)



### JDK的IO操作



### 对IO操作的优化



### MySQL预防注入

参数化查询：数据库服务器不会将参数的内容作为一个sql指令部分来处理，而是在数据库完成sql指令的一个编译后套用这个参数

sql预编译：



### TomCat做过哪些配置



### linux权限修改

```perl
chmod 644 redis-3.0.0.gem
```



## 随机



### 1.一个进程最多可以创建多少个线程？受哪些因素影响

- 32 位系统，用户态的虚拟空间只有 3G，如果创建线程时分配的栈空间是 10M，那么一个进程最多只能创建 300 个左右的线程。
- 64 位系统，用户态的虚拟空间大到有 128T，理论上不会受虚拟内存大小的限制，而会受系统的参数或性能限制。



### 2. jvm的内存分区

![image-20211020153756093](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211020153756093.png)



### 3. String,StringBuffer与StringBuilder的区别

**String**

字符串属于对象，Java提供String类来创建和操作字符串

String的值是不可变的，每次对String的操作都会产生新的String对象，这样效率低，而且浪费大量的内存空间

StringBuffer 和StringBuild都能被多次修改，并且不产生新的未使用的对象

StringBuilder 的方法**不是线程安全**的（不能同步访问）。由于 StringBuilder 相较于 StringBuffer 有速度优势，**所以多数情况下建议使用 StringBuilder 类**。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

![image-20211020184027086](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211020184027086.png)



### 4. HashMap和HashTable、ConcurrentHashMap区别？

**相同点:**

1. HashMap和Hashtable都实现了Map接口
2. 都可以存储key-value数据

**不同点：**

1. HashMap可以把null作为key或value，HashTable不可以
2. HashMap线程不安全，效率高。HashTable线程安全，效率低。
3. HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。

> 什么是fail-fast?
> 就是最快的时间能把错误抛出而不是让程序执行。



## Spring



### 1. spring容器和spring mvc容器的区别

在Spring整体框架的核心概念中，**容器是核心思想**，就是用来管理Bean的整个生命周期的。

而在一个项目中，容器不一定只有一个，Spring中可以包括多个容器，而且**容器有上下层关系**。

目前最常见的一种场景就是在一个项目中引入Spring和SpringMVC这两个框架，其实就是2个容器，**Spring是根容器**，**SpringMVC是其子容器**。再说的直白点，springmvc就是管理controller对象的容器，spring就是管理service和dao的容器。

并且在Spring根容器中对于SpringMVC容器中的Bean是不可见的，而在SpringMVC容器中对于Spring根容器中的Bean是可见的，也就是**子容器可以看见父容器中的注册的Bean，反之就不行**。说的通俗点就是，在controller里可以访问service对象，但是在service里不可以访问controller对象

理解这点很重要，因为这是一个规则，是Spring自己设定的，但是往下看，我们会发现有些地方它并不默认使用这个规则。

当我们使用注解时，对于Bean注册这个功能的实现就不需要在给每个Bean配置XML了，只要使用统一的如下配置即可。

```xml
<context:component-scan base-package=“com.test" />
```

根据Spring提供的参考手册，**该配置的功能是扫描默认包下的所有的`@Component`注解**，并且自动注册到容器中，同时也扫描`@Controller`，`@Service`，`@Respository`这三个注解，他们是继承自@Component。

除了以上我们使用的扫描配置，在项目中我们经常见到的就是 这个配置，其实有了以上的配置，这个是可以省略掉的。

还有一个SpringMVC相关的是配置，经过验证，这个是必须要配置的，因为它是和@RequestMapping结合使用的，这里补充下SpringMVC框架相关的知识点。

> HandlerMapping，是SpringMVC中用来处理Request请求URL到具体Controller的，其自身也分成很多种类；
> HandlerAdapter，是SpringMVC中用来处理具体请求映射到具体方法的，其自身也分很多种类；
>
> @RequestMapping这个注解的主要目的就是对具体的Controller和方法进行注册，以方便HandlerMapping用来处理请求的映射。但是@RequestMapping需要结合使用才能生效。

不使用注解的springmvc配置文件

![image-20211026161020885](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211026161020885.png)

使用注解的springmvc配置文件

![image-20211026161135733](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211026161135733.png)



### 2. 什么是依赖注入

由容器动态地将某种依赖关系的目标对象实例注入到应用系统中各个关联的组件之中。

面向对象本质上是要多个不同职责相互对立的Object互相通过发消息来进行系统设计。但是这个思想落地时，因为性能的原因，Object之间并不像网络那样真的发消息，而是互相调用对方的方法（C++，Java，C#等都是这么做的）。如果想调用某个Object的方法，就得拿到那个Object的引用。

Bean的配置和注入都用xml来定义（称为application context）。用Spring写的程序启动时会优先启动Spring的一个**加载器**来读取xml文件，并且**按照xml里的描述来自动创建、初始化和管理Bean**（Spring后续版本也支持用annotation或者Java代码描述注入关系了，但是道理是一样的）。Spring加载器会**自动识别依赖关系**，**按照树形结构依次创建那些Bean**。万一发生了依赖循环，Spring能自己检测出来并报错。这就把程序员关于系统里Object怎么初始化，管理和相互引用的工作量降到最低。



### 3. IOC实现

1. 加载配置文件，解析成BeanDifinition 放在Map
2. 调用getBean时，从BeanDifinition 所属的Map，拿出class对象进行实例化，如果有依赖，递归调用getBean逐一完成依赖



### 4. Spring框架中bean的生命周期

![image-20211026214537152](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211026214537152.png)

> Spring 的依赖注入最大亮点就是所有的 Bean 对 Spring 容器的存在是没有意识的，拿 [Spring Bean 生命周期之“我从哪里来”？](http://zsrey.info/article/15) 文章中“小学生入少先队”为例子说明，小学生还是那个小学生，加入少先队还是加入共青团只不过规则不一样罢了
> 　　但是在实际项目中，我们不可避免的要用到 Spring 容器本身提供的资源（难免要有事情需要少先队组织的帮助），这时候要让 Bean 主动意识到 Spring 容器的存在，才能调用 Spring 所提供的资源，这就是 Spring Aware. 其实 Spring Aware 是 Spring 设计为框架内部使用的，若使用了，你的 Bean 将会和 Spring 框架耦合，所以自己不单独使用，但是在读框架源码时希望你不再模糊.

1、实例化一个Bean－－也就是我们常说的new；

2、按照Spring上下文对实例化的Bean进行配置－－也就是IOC注入；

3、如果这个Bean已经实现了`BeanNameAware`接口，会调用它实现的setBeanName(String)方法，此处传递的就是Spring配置文件中Bean的id值

4、如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory(setBeanFactory(BeanFactory)传递的是Spring工厂自身（**可以用这个方式来获取其它Bean**，只需在Spring配置文件中配置一个普通的Bean就可以）；

5、如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文（同样这个方式也可以实现步骤4的内容，但比4更好，因为ApplicationContext是BeanFactory的子接口，有更多的实现方法）；

6、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessBeforeInitialization(Object obj, String s)方法，**BeanPostProcessor经常被用作是Bean内容的更改，并且由于这个是在Bean初始化结束时调用那个的方法，也可以被应用于内存或缓存技术；**

7、如果Bean在Spring配置文件中配置了init-method属性会自动调用其配置的初始化方法。

8、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法、；

> 注：以上工作完成以后就可以应用这个Bean了，那这个Bean是一个Singleton的，所以一般情况下我们调用同一个id的Bean会是在内容地址相同的实例，当然在Spring配置文件中也可以配置非Singleton，这里我们不做赘述。

9、当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用那个其实现的destroy()方法；

10、最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。



### 5.在 Spring 中如何注入一个 Java 集合

类型用于注入一列值，允许有相同的值。
类型用于注入一组值，不允许有相同的值。
类型用于注入一组键值对，键和值都可以为任意类型。
类型用于注入一组键值对，键和值都只能为 String 类型。

```xml
  <!--1 集合类型属性注入-->
    <bean id="stu" class="com.zsr.ioc.pojo.Stu">
        <!--数组类型属性注入-->
        <property name="courses">
            <array>
                <value>java 课程</value>
                <value>数据库课程</value>
            </array>
        </property>

        <!--list 类型属性注入-->
        <property name="list">
            <list>
                <value>张三</value>
                <value>小三</value>
            </list>
        </property>
        <!--map 类型属性注入-->
        <property name="maps">
            <map>
                <entry key="JAVA" value="java"></entry>
                <entry key="PHP" value="php"></entry>
            </map>
        </property>
        <!--set 类型属性注入-->
        <property name="sets">
            <set>
                <value>MySQL</value>
                <value>Redis</value>
            </set>
        </property>

        <property name="courseList">
            <array>
                <ref bean="course1"></ref>
                <ref bean="course2"></ref>
            </array>
        </property>

    </bean>
```



### 6. 请解释Spring Bean的自动装配？

在Spring框架中，在配置文件中设定bean的依赖关系是一个很好的机制，Spring容器还可以自动装配合作关系bean之间的关联关系。这意味着Spring可以通过向Bean Factory中注入的方式自动搞定bean之间的依赖关系。自动装配可以设置在每个bean上，也可以设定在特定的bean上。

**下面的XML配置文件表明了如何根据名称将一个bean设置为自动装配：**

```objectivec
<bean id="employeeDAO" class="com.howtodoinjava.EmployeeDAOImpl" autowire="byName" />
```

autowire属性有五种自动装配的方式：

- no – 缺省情况下，自动配置是通过“ref”属性手动设定 。
- byName-根据bean的属性名称进行自动装配。
- byType-根据bean的类型进行自动装配。
- constructor-类似byType，不过是应用于构造器的参数。如果一个bean与构造器参数的类型形同，则进行自动装配，否则导致异常。
- autodetect-如果有默认的构造器，则通过constructor方式进行自动装配，否则使用byType方式进行自动装配。

除了bean配置文件中提供的自动装配模式，还可以使用@Autowired注解来自动装配指定的bean。在使用`@Autowired`注解之前需要在按照如下的配置方式在Spring配置文件进行配置才可以使用。


也可以通过在配置文件中配置`AutowiredAnnotationBeanPostProcessor` 达到相同的效果。

```cpp
<bean class ="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>
```

配置好以后就可以使用`@Autowired`来标注了。



### 7 .使用@Autowired注解自动装配的过程是怎样的？

使用@Autowired注解来自动装配指定的bean。在使用@Autowired注解之前需要在Spring配置文件进行配置，。

在启动spring IoC时，容器自动装载了一个AutowiredAnnotationBeanPostProcessor后置处理器，当容器扫描到@Autowied、@Resource或@Inject时，就会在IoC容器自动查找需要的bean，并装配给该对象的属性。在使用@Autowired时，首先在容器中查询对应类型的bean：

- 如果查询结果刚好为一个，就将该bean装配给@Autowired指定的数据；

- 如果查询的结果不止一个，那么@Autowired会根据名称来查找；

- 如果上述查找的结果为空，那么会抛出异常。解决方法时，使用required=false。



### 8.怎么理解AOP



### 9. springboot的自动装配

- 当启动springboot应用程序的时候，会先创建SpringApplication的对象。在SpringApplication对象的构造方法中会进行一些参数的初始化工作，最主要的是判断当前应用程序的类型以及初始化器和监听器。在初始化器这个过程会加载整个应用程序中的`spring.factories`文件，将文件的内容放到缓存对象中，方便后续获取。
- SpringApplication对象创建完成之后。开始执行run方法，来完成整个启动，启动过程中最主要的要两个方法，第一个是prepareContext,第二个叫做refreshContext,在这两个关键步骤中完成了自动装配的核心功能，前面的处理逻辑包含了上下文对象的创建，banner的打印，异常报告期的准备等各个准备工作，方便后续来进行调用
- 在`prepareContext`方法中主要完成的是对上下文对象的初始化操作，包括了属性值的设置，比如环境对象environment，整个过程有个非常重要的方法，叫做load，load主要完成一件事情，将当前主类作为一个beanDefinition注册到registry中，方便后续进行BeanFactoryPostProcessor调用执行的时候，找到对应的主类，来完成@SpringBootApplication，@EnableAutoConfiguration等注解的解析工作
- 在`refreshContext`方法中会进行整个容器刷新过程，会调用spring中的refresh方法，refresh中有13个非常关键的方法，来完成整个spring应用程序的启动，在自动装配过程中，解析处理各种注解，包含@PropertySource,@ComponentScan,@ComponentScans,@Bean,@Import等注解，最主要的是@Import注解的解析
- 在解析@Import注解的时候，会有一个getImports的方法，从主类开始递归解析注解，把所有包含@Import的注解都解析到，然后在processImport方法中对Import的类进行分类，此处主要识别的时候AutoConfigurationImportSelect归属于ImportSelect的子类，在后续过程中会调用deferredImportSelectorHandler中的process方法，来完成EnableAutoConfiguration的加载。



### 10.BeanPostProcessor和BeanFactoryPostProcessor使用

#### BeanPostProcessor简介

BeanPostProcessor是Spring IOC容器给我们提供的一个扩展接口。接口声明如下：

```java
public interface BeanPostProcessor {
    //bean初始化方法调用前被调用
    Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException;
    //bean初始化方法调用后被调用
    Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;
}
```

**运行顺序**

![image-20211103120931311](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211103120931311.png)

#### BeanPostProcessor实例

```dart
/**
 * 后置处理器：初始化前后进行处理工作
 * 将后置处理器加入到容器中
 */
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessBeforeInitialization..."+beanName+"=>"+bean);
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessAfterInitialization..."+beanName+"=>"+bean);
        return bean;
    }

}
```

#### BeanFactoryPostProcessor简介

bean工厂的bean属性处理容器，说通俗一些就是可以管理我们的bean工厂内所有的BeanDefinition（未实例化）数据，可以随心所欲的修改属性。

#### BeanFactoryPostProcessor实例

```java
@Component
public class MyBeanFactoryPostProcessor implements BeanFactoryPostProcessor {

    @Override
    public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {
        System.out.println("MyBeanFactoryPostProcessor...postProcessBeanFactory...");
        int count = beanFactory.getBeanDefinitionCount();
        String[] names = beanFactory.getBeanDefinitionNames();
        System.out.println("当前BeanFactory中有"+count+" 个Bean");
        System.out.println(Arrays.asList(names));
    }

}
```

**区别：**

注册BeanFactoryPostProcessor的实例，需要重载

void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException;

通过beanFactory可以获取bean的示例或定义等。同时可以修改bean的属性，这是和BeanPostProcessor最大的区别。



## springMVC



### 执行流程

![image-20211102140146876](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211102140146876.png)

 9

具体步骤：

第一步：发起请求到前端控制器(DispatcherServlet)

第二步：前端控制器请求HandlerMapping查找 Handler （可以根据xml配置、注解进行查找）

第三步：处理器映射器HandlerMapping向前端控制器返回Handler，HandlerMapping会把请求映射为HandlerExecutionChain对象（包含一个Handler处理器（页面控制器）对象，多个HandlerInterceptor拦截器对象），通过这种策略模式，很容易添加新的映射策略

第四步：前端控制器调用处理器适配器去执行Handler

第五步：处理器适配器HandlerAdapter将会根据适配的结果去执行Handler

第六步：Handler执行完成给适配器返回ModelAndView

第七步：处理器适配器向前端控制器返回ModelAndView （ModelAndView是springmvc框架的一个底层对象，包括 Model和view）

第八步：前端控制器请求视图解析器去进行视图解析 （根据逻辑视图名解析成真正的视图(jsp)），通过这种策略很容易更换其他视图技术，只需要更改视图解析器即可

第九步：视图解析器向前端控制器返回View

第十步：前端控制器进行视图渲染 （视图渲染将模型数据(在ModelAndView对象中)填充到request域）

第十一步：前端控制器向用户响应结果



## mysql



### 索引使用场景

order by

当我们使用order by将查询结果按照某个字段排序时，如果该字段没有建立索引，那么执行计划会将查询出的所有数据使用外部排序（**将数据从硬盘分批读取到内存使用内部排序，最后合并排序结果**），这个操作是很影响性能的，因为需要将查询涉及到的所有数据从磁盘中读到内存（如果单条数据过大或者数据量过多都会降低效率），更无论读到内存之后的排序了。

但是如果我们对该字段建立索引**alter table 表名 add index(字段名)**，那么由于**索引本身是有序**的，因此直接**按照索引的顺序和映射关系逐条取出数据即可**。而且如果分页的，那么只用取出索引表某个范围内的索引对应的数据，而不用像上述那取出所有数据进行排序再返回某个范围内的数据。（从磁盘取数据是最影响性能的）

join

> 对`join`语句匹配关系（`on`）涉及的字段建立索引能够提高效率

索引覆盖

如果要查询的字段都建立过索引，那么引擎会直接在索引表中查询而不会访问原始数据（否则只要有一个字段没有建立索引就会做全表扫描），这叫索引覆盖。因此我们**需要尽可能的在select后只写必要的查询字段，以增加索引覆盖的几率**。

这里值得注意的是**不要想着为每个字段建立索引，因为优先使用索引的优势就在于其体积小**。



### 索引有哪几种类型？

**主键索引**: 数据列不允许重复，不允许为NULL，一个表只能有一个主键。

**唯一索引**: 数据列不允许重复，允许为NULL值，一个表允许多个列创建唯一索引。

- 可以通过 `ALTER TABLE table_name ADD UNIQUE (column);` 创建唯一索引
- 可以通过 `ALTER TABLE table_name ADD UNIQUE (column1,column2);` 创建唯一组合索引

**普通索引:** 基本的索引类型，没有唯一性的限制，允许为NULL值。

- 可以通过`ALTER TABLE table_name ADD INDEX index_name (column);`创建普通索引

- 可以通过`ALTER TABLE table_name ADD INDEX index_name(column1, column2, column3);`创建组合索引

**全文索引：** 是目前搜索引擎使用的一种关键技术。

- 可以通过`ALTER TABLE table_name ADD FULLTEXT (column);`创建全文索引

> **原理**是先定义一个词库，然后在文章中查找每个词条(term)出现的频率和位置，把这样的频率和位置信息按照词库的顺序归纳，这样就相当于对文件建立了一个以词库为目录的索引，这样查找某个词的时候就能很快的定位到该词出现的位置。



### 创建索引的原则

1） 最左前缀匹配原则，组合索引非常重要的原则，mysql会一直向右匹配直到遇到范围查询(>、<、between、like)就停止匹配，比如a = 1 and b = 2 and c > 3 and d = 4 如果建立(a,b,c,d)顺序的索引，d是用不到索引的，如果建立(a,b,d,c)的索引则都可以用到，a,b,d的顺序可以任意调整。

2）较频繁作为查询条件的字段才去创建索引

3）更新频繁字段不适合创建索引

4）若是不能有效区分数据的列不适合做索引列(如性别，男女未知，最多也就三种，区分度实在太低)

5）尽量的扩展索引，不要新建索引。比如表中已经有a的索引，现在要加(a,b)的索引，那么只需要修改原来的索引即可。

6）定义有外键的数据列一定要建立索引。

7）对于那些查询中很少涉及的列，重复值比较多的列不要建立索引。

8）对于定义为text、image和bit的数据类型的列不要建立索引。



### MySQL存储引擎MyISAM与InnoDB区别

- Innodb引擎：Innodb引擎提供了对数据库ACID事务的支持。并且还提供了行级锁和外键的约束。它的设计的目标就是处理大数据容量的数据库系统。
- MyIASM引擎(原本Mysql的默认引擎)：不提供事务的支持，也不支持行级锁和外键。
- MEMORY引擎：所有的数据都在内存中，数据的处理速度快，但是安全性不高。

![image-20211027131930628](https://dblog-zsrey.oss-cn-shenzhen.aliyuncs.com/articles/%E9%9D%A2%E8%AF%95%E6%80%BB%E7%BB%93.assets/image-20211027131930628.png)

\##



### 创建索引时需要注意什么？

- 非空字段：应该指定列为NOT NULL，除非你想存储NULL。在mysql中，含有空值的列很难进行查询优化，因为它们使得索引、索引的统计信息以及比较运算更加复杂。你应该用0、一个特殊的值或者一个空串代替空值；
- 取值离散大的字段：（变量各个取值之间的差异程度）的列放到联合索引的前面，可以通过count()函数查看字段的差异值，返回值越大说明字段的唯一值越多字段的离散程度高；
- 索引字段越小越好：数据库的数据存储以页为单位一页存储的数据越多，一次IO操作获取的数据越大 效率越高。



### 使用索引查询一定能提高查询的性能吗？为什么

通常，通过索引查询数据比全表扫描要快。但是我们也必须注意到它的代价。

- 索引需要空间来存储，也需要定期维护， 每当有记录在表中增减或索引列被修改时，索引本身也会被修改。 这意味着每条记录的INSERT，DELETE，UPDATE将为此多付出4，5 次的磁盘I/O。 因为索引需要额外的存储空间和处理，那些不必要的索引反而会使查询反应时间变慢。使用索引查询不一定能提高查询性能，索引范围查询(INDEX RANGE SCAN)适用于两种情况:
- 基于一个范围的检索，一般查询返回结果集小于表中记录数的30%
- 基于非唯一性索引的检索



### B树和B+树的区别

- 在B树中，你可以将键和值存放在内部节点和叶子节点；但在B+树中，内部节点都是键，没有值，叶子节点同时存放键和值。
- B+树的叶子节点有一条链相连，而B树的叶子节点各自独立。



## Json

#### fastjson

阿里巴巴的开源一个JSON解析库，通常被用于将Java Bean和JSON 字符串之间进行转换。

对于JSON框架来说，想要把一个Java对象转换成字符串，可以有两种选择：

- 1、基于属性
- 2、基于setter/getter

**当我们要对对象进行序列化的时候，fastjson会扫描其中的getter方法，即找到getName，这时候就会将name字段的值序列化到JSON字符串中。**

**当一个类中包含了一个接口（或抽象类）的时候，在使用fastjson进行序列化的时候，会将子类型抹去，只保留接口（抽象类）的类型，使得反序列化时无法拿到原始类型。**

astjson引入了AutoType，即在序列化的时候，把原始类型记录下来。

使用方法是通过SerializerFeature.WriteClassName进行标记，即将上述代码中的



### Jaskson的使用 java对象转为josn

```java
/**
 * 2. Java对象转换JSON
 *             1. 使用步骤：
 *                 1. 导入jackson的相关jar包
 *                 2. 创建Jackson核心对象 ObjectMapper
 *                 3. 调用ObjectMapper的相关方法进行转换
 *             1. 转换方法：
 *                         * writeValue(参数1，obj):
 *                             参数1：
 *                                 File：将obj对象转换为JSON字符串，并保存到指定的文件中
 *                                 Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
 *                                 OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中
 *                         * writeValueAsString(obj):将对象转为json字符串
 * 使用jackSon生成解析jsom
 * @date 2019/10/5 15:09
 */
public class Test1 {
    @Test//生成json
    public void test() throws IOException {
        Person p=new Person();
        p.setName("解析json");
        p.setAge(13);
        p.setGender("男");
        ObjectMapper mapper=new ObjectMapper();//先创建objmapper的对象
        String string = mapper.writeValueAsString(p);
        /*    *mapper.writeValue(参数1，obj): 1.File：将obj对象转换为JSON字符串，并保存到指定的文件中
         *                                       2.Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
         *                                       3.OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中*/
        System.out.println(string);//{"name":"解析json","age":13,"gender":"男"}

        //  1.File：将obj对象转换为JSON字符串，并保存到指定的文件中
        mapper.writeValue(new File("D://a.txt"),p);
        //   2.Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
        mapper.writeValue(new FileWriter("D://b.txt"),p);
    }
}
```



## 智力题

有三个桶，两个大的可装8斤的水，一个小的可装3斤的水，现在有16斤水装满了两大桶就是8斤的桶，小桶空着，如何把这16斤水分给4个人，每人4斤。没有其他任何工具，4人自备容器，分出去的水不可再要回来

```css
大桶  大桶  小桶    a  b  c  d
8     5     0      3  0  0  0
8     2     3
8     0     3      3  2  0  0
8     3     0
5     3     3
5     6     0
2     6     3
2     8     1
2     8     0      3  2  1  0
0     8     2
0     7     3
3     7     0
3     4     3
6     4     0
6     1     3
6     0     3      3  2  1  1
8     0     1
8     0     0      4  2  1  1
5     0     0      4  2  4  1
2     0     3
0     0     0      4  4  4  4
```