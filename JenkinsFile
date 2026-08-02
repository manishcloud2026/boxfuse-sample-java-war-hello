pipeline {
    agent any
    stages {
        stage('Download file from GitHub') {
            steps {
                echo 'Downloading file from GitHub...'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/manishcloud2026/boxfuse-sample-java-war-hello.git']])
            }
        }
        stage('Run Build') {
            steps {
                echo 'Running build...'
                sh 'mvn clean package'
            }
        }
        stage('Archive Artifacts') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Trigger Deploy Job') {
            steps {
                echo 'triggering deploy job...'
                build wait: false, job: 'DeployPipeline'
            }
        }
    }
}
