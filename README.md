# -ArrayList
如何正确的将数组转换为ArrayList

1. 自己动手实现（教育目的）

//JDK1.5+
static <T> List<T> arrayToList(final T[] array) {
  final List<T> l = new ArrayList<T>(array.length);

  for (final T s : array) {
    l.add(s);
  }
  return (l);
}
Integer [] myArray = { 1, 2, 3 };
System.out.println(arrayToList(myArray).getClass());//class java.util.ArrayList
2. 最简便的方法(推荐)

List list = new ArrayList<>(Arrays.asList("a", "b", "c"))
3. 使用 Java8 的Stream(推荐)

Integer [] myArray = { 1, 2, 3 };
List myList = Arrays.stream(myArray).collect(Collectors.toList());
//基本类型也可以实现转换（依赖boxed的装箱操作）
int [] myArray2 = { 1, 2, 3 };
List myList = Arrays.stream(myArray2).boxed().collect(Collectors.toList());
4. 使用 Guava(推荐)

对于不可变集合，你可以使用ImmutableList类及其of()与copyOf()工厂方法：（参数不能为空）

List<String> il = ImmutableList.of("string", "elements");  // from varargs
List<String> il = ImmutableList.copyOf(aStringArray);      // from array
对于可变集合，你可以使用Lists类及其newArrayList()工厂方法：

List<String> l1 = Lists.newArrayList(anotherListOrCollection);    // from collection
List<String> l2 = Lists.newArrayList(aStringArray);               // from array
List<String> l3 = Lists.newArrayList("or", "string", "elements"); // from varargs
5. 使用 Apache Commons Collections

List<String> list = new ArrayList<String>();
CollectionUtils.addAll(list, str);
