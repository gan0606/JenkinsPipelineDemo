pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello from GitHub hook trigger.'
            }
        }
        stage('Build') {
            steps {
                echo 'Building'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
                // Jenkinsの認証を行う関数
                withCredentials([[
                    // AWSの認証を行うクラス
                    // クラスの初期化の際にcredentialsId、accessKeyVariable、secretKeyVariableを渡す
                    $class: 'AmazonWebServicesCredentialsBinding',
                    // Jenkinsに登録したcredentialsId
                    credentialsId: 'MyAWS',
                    // AWSから取得したaccess_key_id
                    // jenkinsにaccess_key_idを登録したら下記の環境変数に登録される
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    // AWSから取得したsecret_access_key
                    // jenkinsにsecret_access_keyを登録したら下記の環境変数に自動的に登録される
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
                        sh(script: 'aws s3 cp /var/lib/jenkins/workspace/JenkinsPipeline/index.html s3://test-env-jenkins-iwakura/')
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Release') {
            steps {
                echo 'Releasing'
            }
        }
    }
}
