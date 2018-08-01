---
title: logger.isDebugEnabled()的作用
categories:
- 术业专攻
tags:
- Java
- Log
---
<Excerpt in index | 首页摘要>
　　在项目中经常会看到这样的代码：
```
if (logger.isDebugEnabled()) {
    logger.debug(message);
}
```
#####  **为什么要这样做呢？**
<!-- more -->
<The rest of contents | 余下全文>
　　且看isDebugEnabled()的源码：
```
public boolean isDebugEnabled() {
  if(repository.isDisabled(Level.DEBUG_INT))
      return false;
  return Level.DEBUG.isGreaterOrEqual(this.getEffectiveLevel());
}
```
　　以下是debug()的源码：
```
public void debug(Object message) {
    if(repository.isDisabled(Level.DEBUG_INT))
        return;
    if(Level.DEBUG.isGreaterOrEqual(this.getEffectiveLevel())) {
        forcedLog(FQCN, Level.DEBUG, message, null);
    }
}
```
　　可见，debug()中做了跟isDebugEnabled()几乎一样的判断，看起来直接调用debug()比先判断isDebugEnabled()更加效率。
　　此时来看下面的代码：
`logger.debug("The money is " + getTotalMoney());  `

　　假设我们的日志级别设置为info，debug()方法调用后会判断` if(repository.isDisabled(Level.DEBUG_INT))`，然后return。但是在调用debug()方法时，必须提供参数。要获得参数，就需要执行getTotalMoney()并拼接。假设这个获取参数的过程需要10秒钟，则系统会在花费10秒后决定return，这显然很得不偿失。
　　加上logger.isDebugEnabled()判断，只会使写日志的时间增加大概万分之一，但是如果不加此判断，系统可能需要花费更多的时间，所以在大多数情况下，在输出debug日志前加上logger.isDebugEnabled()比较好。