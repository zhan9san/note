# Get jobs in a view

[Find Jenkins projects that build periodically](https://support.cloudbees.com/hc/en-us/articles/360032285111-Find-Jenkins-projects-that-build-periodically)

Jenkins Job `config.xml` URL `http://JenkinsURL/job/Aaaa/config.xml`

```groovy
import com.cloudbees.hudson.plugins.folder.Folder
import org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject
import jenkins.branch.OrganizationFolder

a = 0

hudson.model.Hudson.instance.getView('all').items.each() {
  processItems(it)
}

println a

def processItems(def item){
    try{
        if (item) {
            if((item instanceof WorkflowMultiBranchProject) || (item instanceof OrganizationFolder)){
                println item.fullDisplayName
                a += 1
            } else if (item instanceof Folder) {
                item.getItems().each{
                    processItems(it)
                }
            }
        }
    }catch(error){
        error("Failed to handle item: "+item.getFullName()+' Due to: '+error)
    }
}
```

## Update scan period

<https://gist.github.com/duffn/7adfd5fb64cfe6aa0eae9919fe33dc03>

Get job list

```groovy
import com.cloudbees.hudson.plugins.folder.computed.PeriodicFolderTrigger
import jenkins.model.Jenkins
import jenkins.branch.OrganizationFolder
import org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject

def multiBranchCount = 0
def OrgFolderCount = 0

println "Multibranch Items\n-------"
Jenkins.instance.getAllItems(org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject.class).each {
  multiBranchCount += 1
  println it.fullName
}

println "OrganizationFolder Items\n-------"
Jenkins.instance.getAllItems(jenkins.branch.OrganizationFolder.class).each {
  OrgFolderCount += 1
  println it.fullName
}

println "multiBranchCount: " + multiBranchCount
println "OrgFolderCount: " + OrgFolderCount
```

Set interval

```groovy
import com.cloudbees.hudson.plugins.folder.computed.PeriodicFolderTrigger
import jenkins.model.Jenkins
import jenkins.branch.OrganizationFolder
import org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject

// println "Multibranch Items\n-------"
// Jenkins.instance.getAllItems(org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject.class).each {
//   getInterval(it)
//   // setInterval(it)
// }

println "OrganizationFolder Items\n-------"
Jenkins.instance.getAllItems(jenkins.branch.OrganizationFolder.class).each {
  getInterval(it)
  // setInterval(it)
}

def getInterval(folder) {
  println "Get ${folder.fullDisplayName}"
  folder.getTriggers().each { k, v ->
    println v.getInterval()
  }
}

def setInterval(folder) {
  println "Updating ${folder.name}" 
  def newInterval = new PeriodicFolderTrigger("2d")
  folder.addTrigger(newInterval)
  folder.save()
  folder.getTriggers().each { k, v ->
    println v.getInterval()
  }
}
```
