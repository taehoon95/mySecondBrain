# 중복제거

```java
List<String> filter_ids = dict_report.stream().filter(s -> s.endsWith(id)).collect(Collectors.toList()); 
```