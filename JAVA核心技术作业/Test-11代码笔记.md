#                                  Test-11代码笔记

```java
while((line = br.readLine())!=null) {
                Pattern p = Pattern.compile("\\s+");//正则匹配空格
                String words[]= p.split(line);//获取的字符串进行分割单词
    //用此语句可将文件中的每个单词存放到字符串数组中
```

```java
        //HashMap转换为list，进行排序(HashMap中的元素排序需要转换为List)
        List<Map.Entry<String,Integer>> list = new ArrayList<Map.Entry<String,Integer>>(hm.entrySet());
        Collections.sort(list,new MyComparator());
```





