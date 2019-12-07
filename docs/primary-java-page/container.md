### 18. java 容器都有哪些？
- 数组 :限制为：Integer.MAX_VALUE。
- String :底层是char数组，长度Integer.MAX_VALUE线程安全。
- Java.util下的集合容器。
![容器](https://pic4.zhimg.com/80/v2-e015e094a5f1daca2507e094c3698d4f_hd.jpg "容器")
- List：存放有序，列表存储，元素可以重复。
- Set：无序，元素不可以重复。底层实现使用hashMap=数组+链表
- Map：元素不可以重复，LinkedHashMap,TreeHashMap底层用额外的链表和树进行维护
### 19. Collection 和 Collections 有什么区别？
- Collections相当于一个工具类，可以reverse()逆序和sort（）排序
- Collection是一个集合的接口，它提提供了具体的实现方法。有ArrayList（），LinkedList（）
### 20. List、Set、Map 之间的区别是什么？
List的元素以线性方式存储，可以存放重复，List主要有以下两个实现类：
- ArrayList：长度可变数组，可以对元素进行随机访问，ArrayList中插入与删除元素的速度比较慢。扩容是采用1.5倍扩容。然后调用Arrays.copyof()对原来的数组进行复制。
- LinkedList：采用链表数据结构，插入和删除速度较快基于链表。

Set（集合）中的对象不按照特定（hashCode）的方式进行排序，并且没有重复对象，set主要有俩个实现类：
- HashSet：按照哈希算法来存取集合中的对象，存取速度比较快。当HashSet中的元素超过*loadFactor（默认值为0.75）时，就可以近似两倍扩容。
- TreeSet：TreeSet实现了SortedSet接口，能够对集合中的集合对象进行排序。这个是使用二叉链表实现。
   
Map（映射）是一种把键对象和值对象映射的集合，它的每一个元素都包含一个键对象和值对象。 Map主要有以下两个实现类：
- HashMap：HashMap基于散列表实现，其插入和查询<K,V>的开销是固定的，可以通过构造器设置容量和负载因子来调整容器的性能。
- LinkedHashMap：类似于HashMap，但是迭代遍历它时，取得<K,V>的顺序是其插入次序，或者是最近最少使用(LRU)的次序。
- TreeMap：TreeMap基于红黑树实现。查看<K,V>时，它们会被排序。TreeMap是唯一的带有subMap()方法的Map，subMap()可以返回一个子树。
### 21. 如何决定使用 HashMap 还是 TreeMap？
TreeMap<k,v>的key值要求实现java.lang.Comparable,所以迭代的时候TreeMap默认是按照Key值升序排列的；TreeMap的实现也是基于红黑树结构。而HashMap<k,v>的Key值实现散列hashCode(),分布散列的均匀的，不支持排序；数据结构主要是通过桶（数组），链表或红黑树
> 大多数情况下HashMap有更好的性能，所以不需要排序的时候一般使用HashMap.    
### 22. 如何实现数组和 List 之间的转换？
- List转数组：toArray(arraylist.size()方法
- 数组转List：Arrays的asList(a)方法    
### 23. 哪些集合类是线程安全的？
- vector：就比arraylist多了个同步化机制（线程安全），因为效率较低，现在已经不太建议使用。在web应用中，特别是前台页面，往往效率（页面响应速度）是优先考虑的。
- statck：堆栈类，先进后出
- hashtable：就比hashmap多了个线程安全
- enumeration：枚举，相当于迭代器    
### 24. 迭代器 Iterator 是什么？
对于collection进行迭代的类，成为迭代器。根据面向对象的方法，迭代器是专门取出集合元素的对象。但是该元素对象比较特殊，不能直接创建对象（通过New），该对象是以内部类的形式存在于每个集合类的内部。   
#### 如何获取迭代器？
Collection接口定义了获取集合迭代器的方法（Iterator）所以所有Colletion体系集合都可以获取自身的迭代器。

总来的说：
Iterator接口提供了很多对集合元素进行迭代的方法。每一个集合类都包括了可以返回迭代器实例的迭代方法。迭代器可以在迭代过程中删除底层集合的元素，但是不可以直接调用集合的remove(Object obj)删除，可以通过迭代器的remove()方法删除。
```java
public class TestIterator {
	
	static List<String> list = new ArrayList<String>();
	
	static {
		list.add("111");
		list.add("222");
		list.add("333");
	}
	
 
	public static void main(String[] args) {
		testIteratorNext();
		System.out.println();
		
		testForEachRemaining();
		System.out.println();
		
		testIteratorRemove();
	}
	
	//使用 hasNext 和 next遍历 
	public static void testIteratorNext() {
		Iterator<String> iterator = list.iterator();
		while (iterator.hasNext()) {
			String str = iterator.next();
			System.out.println(str);
		}
	}
	
	//使用 Iterator 删除元素 
	public static void testIteratorRemove() {
		Iterator<String> iterator = list.iterator();
		while (iterator.hasNext()) {
			String str = iterator.next();
			if ("222".equals(str)) {
				iterator.remove();
			}
		}
		System.out.println(list);
	}
	
	//使用 forEachRemaining 遍历
	public static void testForEachRemaining() {
		final Iterator<String> iterator = list.iterator();
		iterator.forEachRemaining(new Consumer<String>() {
 
			public void accept(String t) {
				System.out.println(t);
			}
			
		});
	}
}

```
### 25. Iterator 和 ListIterator 有什么区别？
在使用的时候，list和set都有iterator来取得迭代器，对于list来说可以使用listIterator来获取迭代器，两种迭代器是在某些方面是不能通用的。

- ListIterator有add()方法，可以向list中添加对象，但是iterator不能

- ListIterator和Iterator可以实现hasPrevious和previous（）

- ListIterator可以定位当前的索引位置，nextIndex()和previousIndex()可以实现。Iterator没有此功能。
- 都可实现删除对象，但是ListIterator可以实现对象的修改，set()方法可以实现。Iierator仅能遍历，不能修改。
### 26. 怎么确保一个集合不能被修改？
首先我们很容易想到使用final进行修饰，使用关键字final可以修饰类、方法、成员变量，使用final修饰的类不可以被继承，使用final修饰的变量必须初始化值，如果这个成员变量是基本类型数据，表述这个变量的值是不可以改变的，如果说这个成员变量是引用类型数据，则表示这个引用类型的地址是不可以改变的，但是引用指向的对象的内容还是可以改变的。
因此，如果要确保一个集合不被修改，我们要清除集合（list，set，map）都是引用类型数据，所以使用final修饰集合的内容还是可以修改的。
我们可以采用Collections包下的unmodifiableMap方法，通过这个方法返回的map,是不可以修改的。他会报 java.lang.UnsupportedOperationException错。

同理：Collections包也提供了对list和set集合的方法。
- Collections.unmodifiableList(List)
- Collections.unmodifiableSet(Set)
