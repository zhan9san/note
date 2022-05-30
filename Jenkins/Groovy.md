# Groovy utils

## Doc

<https://docs.groovy-lang.org/next/html/documentation/working-with-collections.html>

## Get type of variable

<https://www.logicbig.com/tutorials/misc/groovy/data-type-and-variables.html>

```groovy
a = 2
printf "%s - %s%n", a.getClass().getName(), a
a = "apple"
printf "%s - %s%n", a.getClass().getName(), a
```

Output

```text
java.lang.Integer - 2
java.lang.String - apple
```

## Nested each loop

If the child loop needs to use parent `it`, we have to define a different key word.

```groovy
a.each { x ->
    x.each { y ->
        println x
    }
}
```

<https://stackoverflow.com/questions/28207649/nested-each-loops-in-groovy>

```groovy
List a
a.each { x ->
    println(x.name)
    List b = something
    b.each { y ->
        println(x.name + y.name)
    }
}
```

Global variable

<https://stackoverflow.com/questions/6305910/how-do-i-create-and-access-the-global-variables-in-groovy>

```groovy
import groovy.transform.Field

var1 = 'var1'
@Field String var2 = 'var2'
def var3 = 'var3'

void printVars() {
    println var1
    println var2
    println var3 // This won't work, because not in script scope.
}
```
