# Get Jenkins Job in Groovy

```groovy
def logSpec = { it, getTrigger -> String spec = getTrigger(it)?.getSpec(); if (spec) println (it.getFullName() + " with spec " + spec)}
 
Jenkins.getInstance().getAllItems(FreeStyleProject.class).each() { logSpec(it, {it.getSCMTrigger()}) }
```
