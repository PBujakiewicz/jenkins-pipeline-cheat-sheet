# jenkins-pipeline-cheat-sheet

<br /><br />

## Increasing sleep
```groovy
steps {
    script {
        def retryAttempt = 0
        retry(3) {
            if (retryAttempt > 0) {
                sleep(60 * retryAttempt)
            }
            retryAttempt = retryAttempt + 1

            ToDo...
        }
    }
}
```

<br /><br />

