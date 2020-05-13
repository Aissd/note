1、[使用JavaScript的数组实现数据结构中的队列与堆栈](https://www.cnblogs.com/xdp-gacl/p/4193629.html)

2、[使用递归遍历并转换树形数据（以 TypeScript 为例）](https://segmentfault.com/a/1190000011819279)

3、[js 遍历嵌套数组](https://segmentfault.com/q/1010000012762568)

4、将树状结构图转换成队列结构的思路

1. 准备一个空的队列（Source）（数组）

2. 将要遍历的节点放到队列（Source）中（解构树状数组）

3. 从队列（Source）中取一个节点

4. 进入循环后，移除当前队列（Source）的第一个节点并处理这个节点（比如打印）let next = quene.shift();

5. 检查是否有子节点，如果有，全部依次添加到队列（Source）中

6. 回到第3步开始处理，直至队列（Source）为空


5、深度遍历（递归），广度遍历（队列）

