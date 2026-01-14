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

            Step command...
        }
    }
}
```

<br /><br />

## Echo Credentials
```groovy
steps {
    script {
        def credId = 'jenkins'

        try {
            withCredentials([string(credentialsId: credId, variable: 'SECRET_TOKEN')]) {

                echo "---------------------------------------------------"
                sh 'echo -n "$SECRET_TOKEN" | base64'
                echo "---------------------------------------------------"
            }
        } catch (Exception e) {
            echo "There is no such ID: '${credId}'"

        }
    }
}

steps {
    script {
        def credId = 'jenkins-user-pass'

        try {
            withCredentials([usernamePassword(credentialsId: credId, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                echo "---------------------------------------------------"
                sh 'echo "user: $USERNAME"'
                sh 'echo "password: $PASSWORD"'
                echo "---------------------------------------------------"
            }
        } catch (Exception e) {
            echo "There is no such ID: '${credId}'"
        }
    }
}
```

<br /><br />
