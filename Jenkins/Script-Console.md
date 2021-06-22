# Script console

In the Script Console

List methods on a class instance

```groovy
println thing.metaClass.methods*.name.sort().unique()
```

Determine a class from an instance

```groovy
println thing.class or thing.getClass()
```
