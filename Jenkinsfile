pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/jprmaquinto/spring-petclinic-1.git'

                // Run Maven on Windows.
                bat label: 'Build Spring Pet Clinic', script: 'mvn -Dmaven.test.failure.ignore=true clean package'
                
                echo 'Done Building Spring Pet Clinic'
            }
        }
    }
}
