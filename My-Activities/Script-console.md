##  Clear all jenkins build history

```bash
Jenkins.instance.getAllItems(hudson.model.Job).each { job ->
    job.builds.each { it.delete() }
}
```
