pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }
        
        stage('Artifact') {
            steps {
                sh 'tar czf LearnEd_E-learning_Website.tar.gz .'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'LearnEd_E-learning_Website.tar.gz', fingerprint: true
                }
            }
        }
        
        stage('Dockerize') {
            steps {
                script {
                    def version = env.BUILD_ID
                    sh "docker build -t learntech/learned-elearning-website:${version} ."
                }
            }
            post {
                always {
                    script {
                        def version = env.BUILD_ID
                        sh "docker push learntech/learned-elearning-website:${version}"
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'CI/CD pipeline successfully executed!'
        }
    }
}
