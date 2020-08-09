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
        stage('Record MapApps') {
            steps {
                
                bat label: 'Record MapApp', script: 'mvn -DargLine="-javaagent:appmap.jar -Dappmap.output.directory=./appmap" test'
                
                echo 'Done Record MapApp'
            }
        }
        stage('Upload MapApps') {
            withEnv(['APPLAND_API_KEY=anBybWFxdWludG9AZ21haWwuY29tOmNjMTdjYTU3LTg3N2ItNGZlZi04NDcyLThmYzVjMGJjMmU0Yw', 'APPLAND_URL=https://app.land']) {
                steps {
                bat label: 'Login Appland', script: 'appland login'     
                    
                bat label: 'Upload MapApp', script: 'appland upload ./appmap'
                
                echo 'Done Upload MapApp'
                
                }
            }
            
        }
    }
}
