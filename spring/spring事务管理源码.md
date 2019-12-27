https://cloud.tencent.com/developer/article/1497782
## 事务提交和回滚代码实现
* PlatformTransactionManager
> 1. 事务管理接口，第三方实现该接口的commit和rollback方法实现事务的提交和回滚操作
> 2. jooq使用的DataSourceTransactionManager
* TransactionAspectSupport
> 1. org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction方法是事务提交和会的具体实现
* TransactionInterceptor
> 1. 实现MethodInterceptor
> 2. 继承TransactionAspectSupport，在invoke方法内调用invokeWithinTransaction
* TransactionAttribute
> 1. 用于存放@Transcational注解信息     
