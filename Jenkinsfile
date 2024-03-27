pipeline {
    agent any
    stages {
        stage('Unit Test') {
            steps {
                bat 'ceedling test:all'
            }
        }
        stage('Static Analysis') {
            steps {
                bat 'cppcheck --xml --xml-version=2 src 2> build/cppcheck.xml'
            }
        }
        stage('Target Build') {
            steps {
                bat 'rake release_bin'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'build/release/project.axf'
                    archiveArtifacts artifacts: 'build/release/project.bin'
                }
            }
        }
    }
}
