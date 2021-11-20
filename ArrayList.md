# ArrayList

## 特性

ArrayList，是一种顺序表实现，有下面的几个特性：

1. 动态数组，容量不足会自动扩容，
2. 支持按索引随机访问
3. 插入的元素是有序的
4. 可以存入null
5. 线程不安全

并且，我们通过看ArrayList类的头部，也能得到下面的信息：

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{}
```

1. 实现了RandomAccess接口，表示ArrayList允许被随机访问
2. 实现了Cloneable表示ArrayList可以使用clone方法克隆
3. 实现了Serializable表示Arraylist可以被序列化

## 常见API

ArrayList提供了一系列API来允许我们操作容器中的元素，这些API大多数在Collection接口中定义了，ArrayList不过是将其实现。

| 方法名           | 作用                                                   |
| ---------------- | ------------------------------------------------------ |
| get(int)         | 返回目标索引上的元素，索引从0开始                      |
| size()           | 得到当前容器中元素的个数                               |
| remove(Object)   | 移除指定的元素                                         |
| remove(int)      | 移除目标索引上的元素                                   |
| add(Object)      | 将一个元素加入到容器的尾部                             |
| add(int,Object)  | 在指定位置插入一个元素                                 |
| isEmpty()        | 判断容器中是否有元素，如果元素为0返回false。           |
| set(int,Object)  | 修改指定索引上的元素                                   |
| toArray()        | 转成一个普通数组                                       |
| clear()          | 清除所有的元素                                         |
| indexOf(Object)  | 返回指定元素的索引，如果有多个同样的元素，则返回第一个 |
| contains(Object) | 判断容器中是否存在一个元素                             |

## 动态扩容原理

在上面的案例中，我们并没有声明ArrayList 的大小，并且在我们插入元素的时候，也不用考虑超出大小的问题。这是如何实现的？这就是ArrayList的强大之处：自动扩容。

### 核心属性

ArrayList，本质是用数组来存储元素的，在其内部可以看到有这几个变量：

```java
    // 默认的初始化大小
	private static final int DEFAULT_CAPACITY = 10;  
	// 空数组
    private static final Object[] EMPTY_ELEMENTDATA = {}; 
	// 默认的空数组
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {}; 
	// 实际存放元素的数组，transient表示该属性不参与序列化与反序列化
    transient Object[] elementData;  
	// 数组中的元素个数
    private int size; 				 
	// 允许的最大容量
	private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
```

其中最不好理解是DEFAULT_CAPACITY，EMPTY_ELEMENTDATA，DEFAULTCAPACITY_EMPTY_ELEMENTDATA。为什么要两个空数组？

其实是因为ArrayList提供了几种初始化方式，只要我们看它的构造方法，就明白了。

```java
 	// new ArrayList(100) 方式创建，此时由我们指定容器的大小
	public ArrayList(int initialCapacity) {
        // 首先判断输入的大小是否合理
        if (initialCapacity > 0) {
            // 大于0则直接创建一个符合我们要求大小的数组
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            // 如果指定的初始大小为0，即new ArrayList(0)，则指向EMPTY_ELEMENTDATA这个空数组。
            // 这里的含义其实就是我们要求创建一个大小为0的数组。
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
	// 使用 new ArrayList() 方式创建时，elementData指向的是DEFAULTCAPACITY_EMPTY_ELEMENTDATA这个空数组
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
	// 传入一个集合的方式初始化数组
    public ArrayList(Collection<? extends E> c) {
        elementData = c.toArray();
         // 首先判断是不是0大小的数组
        if ((size = elementData.length) != 0) {
            // 防止c.toArray()返回的不是Object[]类型的数组
            if (elementData.getClass() != Object[].class)
                // 手动转回 Object[] 类型的数组
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // 传入的也是一个大小为0 的数组，则指向EMPTY_ELEMENTDATA
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }
```

可以看到，三种不同的初始化方式都有不同的处理。

其中最让人值得琢磨的是传入0大小期望值时创建的数组会有不同的处理方式。

### 动态扩容

想要知道ArrayList是如何实现扩容的，需要阅读源码：下面只显示关键的代码：

首先，肯定是添加元素时候才会出现扩容，所以要从两个方法入手：

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
	// 下面省略非核心代码  
    
    // 这是直接添加元素的方法
    public boolean add(E e) {
	    // 两个方法都调用了这个方法
        // 这里为什么要 size + 1(期望值) ，因为想要成功插入新元素要保证有多一个空间
        // 这个方法会拿 期望值 去评估是否需要扩容
        ensureCapacityInternal(size + 1);
        elementData[size++] = e;
        return true;
    }
    // 在指定位置插入元素的方法
    public void add(int index, E element) {
        // 插入元素前，要检查传入的索引是否合法
        rangeCheckForAdd(index);
        // 这里为什么要 size + 1(期望值) ，因为想要成功插入新元素要保证有多一个空间
        // 这个方法会拿 期望值 去评估是否需要扩容
        ensureCapacityInternal(size + 1);  
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        size++;
    }
}
```

也就是说，两个add方法，最终都会调用ensureCapacityInternal方法，继续跟踪：

```java
    private void ensureCapacityInternal(int minCapacity) {
        // 这里，先拿我们的期望值minCapacity去calculateCapacity中计算，得到结果后
        // 再将计算结果传入ensureExplicitCapacity
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
    }
```

那我们先看calculateCapacity做了什么：

```java
	private static int calculateCapacity(Object[] elementData, int minCapacity) {
        // 只有不指定大小创建ArrayList时，第一次扩容才会进入这个条件
        // 原因可以看上面的构造方法
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            // 因为不指定大小创建ArrayList得到的是大小为0 的数组，必然取得DEFAULT_CAPACITY = 10
            // 所以对于new ArrayList() 方式创建的数组，第一次扩容的大小总是10
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
```

再来看ensureExplicitCapacity方法：

```java
// 这个方法才会真正的判断数组是否需要扩容
private void ensureExplicitCapacity(int minCapacity) {
        modCount++; // 记录数组修改的次数
        // 判断是否需要扩容
    	// 当期望值 大于 目前容器的长度, 就需要扩容。
        if (minCapacity - elementData.length > 0)
            // 扩容
            grow(minCapacity);
}
```

到这里，我们就搞清楚了ArrayList是在**新元素没有位置存放时才进行扩容**，如何扩容的实现则交给了grow方法。

````java
 private void grow(int minCapacity) {
        // 保存旧数组的元素个数
        int oldCapacity = elementData.length;
     	// 这里，用到了右移运算，每向右移动N位，则等同于原来的值 / 2^N，
        // 也就是说，这里扩容后的容量是原来的1.5倍。
        int newCapacity = oldCapacity + (oldCapacity >> 1);
     	// 使用new ArrayList方式创建时，该条件会在第一次扩容时满足。
        //  因为此时oldCapacity为0，导致计算出来的newCapacity也是0，新的容量要求是0？这显然是不正确的。
     	// 而参数minCapacity 在经过calculateCapacity中的Math.max(DEFAULT_CAPACITY, minCapacity)计算后得到10
     	// 因此，在不指定大小创建ArrayList情况下，第一次扩容是10.
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
     	// 判断扩容的容量是否超过Integer的最大值 - 8
        if (newCapacity - MAX_ARRAY_SIZE > 0) 
            newCapacity = hugeCapacity(minCapacity);
        // 计算出新的容量后，进行数组拷贝。
     	// 这里使用了Arrays工具类进行拷贝，本质上还是调用了System.arraycopy
        elementData = Arrays.copyOf(elementData, newCapacity);
}
````

**到这里，我们就清楚了，ArrayList每次扩容得到的新容量，总是原来容量的1.5倍数。**

### 扩容特性总结

经过上面的分析，我们可以得到下面的信息：

1. 超过**Integer的最大值，不会再进行扩容，即不能无限扩容**。
2. 无论使用什么方式添加元素，**每一次都会判断是否需要扩容**。
3. 此外，插入元素时，使用了System.arraycopy方法，实际插入元素时，该方法会**将插入位置以及之后的元素都往后移动一位**，这也是数组插入元素效率低下的原因。
4. **ArrayList内部的数组被操作时，没有进行加锁，所以在多线程环境下是不安全的。**
5. 每次扩容后的大小是原大小的1.5倍，但是用不指定大小的方式创建数组时，此时数组大小是0，第一次扩容后的大小是10，之后才是1.5倍进行扩容。

## 其他操作

### 删除操作

```java
// 通过索引删除元素
public E remove(int index) {
    // 检查索引
    rangeCheck(index); 
	// 记录数组修改次数
    modCount++; 
    // 这是一个包装方法，就是从数组中拿取数据并同时转成E类型的对象
    E oldValue = elementData(index); 
	// 计算要移动的元素数量，因为数组删除中间元素，后面的元素都要前移一位
    // 最后一个元素的索引总是比size小1
    int numMoved = size - index - 1;
    // 只有删除最后一个元素时numMoved就是0，表示没有元素需要移动，否则就需要进行数组拷贝
    if (numMoved > 0) 
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    elementData[--size] = null; // 让GC工作
    return oldValue;
}
// 删除指定的元素
public boolean remove(Object o) {
    if (o == null) {
        // 每次删除只会删除找打到第一个null
        for (int index = 0; index < size; index++)
            if (elementData[index] == null) {
                fastRemove(index);
                return true;
            }
    } else {
        // 删除非 null 元素，查找并比对。
        for (int index = 0; index < size; index++)
            if (o.equals(elementData[index])) {
                fastRemove(index);
                return true;
            }
    }
    // 找不到元素，没有任何操作，直接返回false
    return false;
}
// fastMove和上面的 E remove(int index) 原理是一样的
private void fastRemove(int index) {
    modCount++;
    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    elementData[--size] = null; 
}
```

从这里可以看出，对于ArrayList而言，**删除元素的操作代价是高昂的，时间复杂度为O(N)**。

## 浅拷贝

在ArrayList中，clone方法是浅拷贝的，具体可以看下面的一个案例：

```java
public class ArrayListTest {	   
    // 一个打印的方法
	private static <T> void  printArrayList(ArrayList<T> arrayList,String desc) {
        Iterator<T> iterator = arrayList.iterator();
        System.out.print(desc);
        while (iterator.hasNext()) {
            System.out.print(iterator.next()+ ",");
        }
        System.out.println();
    }
	// 准备一个对象
    static  class  Person{
        private String name;
        public Person(String name) {
            this.name = name;
        }
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        @Override
        public String toString() {
            return "Person{" +
                    "name='" + name + '\'' +
                    '}';
        }
    }
    public static void CloneTest() {
        //测试复杂类型的对象
        ArrayList<Person> strArr = new ArrayList<>();
        Person person1 = new Person("张三");
        Person person2 = new Person("李四");
        Person person3 = new Person("王五");
        strArr.add(person1);
        strArr.add(person2);
        strArr.add(person3);
        ArrayList<Person> strArr2 = (ArrayList<Person>) strArr.clone();
        strArr2.get(1).name = "666";   // 将第二个person 的name修改
        printArrayList(strArr,"原数组:");  // 输出比对
        printArrayList(strArr2,"新数组:"); // 输出新的容器
    }
    public static void main(String[] args) {
        CloneTest();
    }
}
```

输出结果如下：

```java
// 李四被替换成 666， 旧的容器也被影响了
原数组:Person{name='张三'},Person{name='666'},Person{name='王五'},  
新数组:Person{name='张三'},Person{name='666'},Person{name='王五'},
```

从上面的结果我们可以看出：

**clone实际上是一个浅拷贝，得到的新容器中的元素，实际上还是指向原来元素的引用，当我们修改新容器中的元素，也会影响旧的容器中的元素。**

而通过查看源码，我们发现：clone实际上是调用了Arrays工具类的copyOf方法，Arrays的copyOf方法实际上又调用了System.arraycopy方法。

**所以也可以得出推论：System.arraycopy方法也是浅拷贝。**

### 解决方案

想要实现深拷贝，有两种思路：

1. 递归的方式处理复杂对象的属性，逐一拷贝
2. 复杂对象实现序列化接口，将复杂对象序列化，再反序列化，就能得到一个全新的对象。

显然第一点的可行性很低，因为复杂对象可能存在多个复杂对象成员属性套娃的情况，难以处理，递归的效率也比较低。

## 总结

ArrayList是线性表的一个典型实现，其动态扩容的特性带来了很多方便，但是，便利是要付出代价的。

1. 对于ArrayList而言，扩容和删除底层都是数组拷贝的操作，代价很高，对于扩容，最好在初始化时就声明好大概的容量，减少扩容的次数。
2. 

**ArrayList适合多读，少操作的应用场景，并且在多线程下面是不安全的。**