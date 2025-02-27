pipeline {
    agent any

    environment {
    SCANNER_HOME = tool 'SonarQube' // Sesuaikan dengan nama tool yang ada di Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/r32a2004/tes.git' // Ganti dengan repositori proyek
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "${SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=tes \
                        -Dsonar.projectName=tes \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://your-sonarqube-server:9000 \
                        -Dsonar.login=Muhammad Reza Al FATAH"
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Quality Gate Failed: ${qg.status}"
                    }
                }
            }
        }
    }
}
