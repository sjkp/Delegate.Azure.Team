#Azure Web Job - Dependency Injection
So far we have seen a lot of `static` web job functions. 

That doesn't go well with dependency injection, but luckily support for dependency injection have been added to the framework (it wasn't from the beginning).

The JobHostConfiguration class have a property JobActivator, that is used to wire up your favorite DI framework. 

A JobActivator that works with Unity could look like this - very simple. 

```
 public class UnityJobActivator : IJobActivator
    {
        private readonly IUnityContainer contaner;

        public UnityJobActivator(IUnityContainer container)
        {
            this.contaner = container;
        }

        public T CreateInstance<T>()
        {
            return this.contaner.Resolve<T>();
        }
    }
``` 

##Example
https://github.com/sjkp/Azure.WebJob.DependencyInjection