# 补充细节

### 对传入数据的遗弃

lab4中发现此处有漏洞，在一些情况下，被传入的数据index太大，reassembler中即使装满了，也最多只能装下index之前的数据，所以该数据一定会被遗弃，不能存入内存中等达到内存限制了再遗弃，而是应该直接选择不存。(使用idx + size\_of\_window <= index 判断)
