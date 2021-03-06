# Creating a Cache Instance

You can create a cache using either the `getCache` method of a [CacheManager](https://ignite.incubator.apache.org/jcache/1.0.0/javadoc/javax/cache/CacheManager.html), or using injection. Creating the cache with injection uses the Caching Provider and Cache Manager described above.

## Using Injection

Creating a cache with injection can be done like so:

```Java
import javax.inject.Inject;
import javax.cache.Cache;
...
@Inject
Cache cache;
```

The name of this cache will be the canonical name of the class it is created in. Caches created in this way will also have JMX statistics and management enabled.

Starting from _Payara 4.1.1.164_, a typed cache can also be injected in the same manner:

```Java
import javax.inject.Inject;
import javax.cache.Cache;
...
@Inject
Cache<Long, Property> cache;
```

Both key and value types must be `Serializable` so that the cache can be injected correctly.

## Injecting a Custom Cache

You can determine the name and other attributes of a cache created through injection using the `@NamedCache` annotation.

You can specify the desired custom values as a comma separated list of parameters of the `NamedCache` annotation when creating a cache.

For example, to inject a cache with a custom name and with JMX management enabled:

```Java
import fish.payara.cdi.jsr107.impl.NamedCache;
import javax.inject.Inject;
import javax.cache.Cache;
...
@NamedCache(cacheName = "custom", managementEnabled = true)
@Inject
Cache cache;
```

If you only want to set the name of the cache but don't want to depend on the `@NamedCache` annotation since it's part of the _Payara Extras_ dependencies, you can use the `@CacheDefaults` annotation on the bean class:

```Java
import javax.inject.Inject;
import javax.cache.Cache;
import javax.cache.annotation.CacheDefaults;
import javax.enterprise.context.ApplicationScoped;
...
@ApplicationScoped
@CacheDefaults(cacheName = "custom")
public class CacheBean {
    ...
    @Inject
    Cache cache;
    ...
}
```

Keep in mind that this solution only works if your bean has one injected cache only. If you are in a situation where you must inject more than one cache into the bean then consider using the _@NamedCache_ annotation to avoid name collisions.