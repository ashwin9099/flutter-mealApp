pipeline {
    agent any

    environment {
        FLUTTER_HOME = "D:\\Softwares\\flutter"
        ANDROID_SDK_ROOT = "C:\\Users\\ankul\\AppData\\Local\\Android\\Sdk"
        PATH = "${FLUTTER_HOME}\\bin;${ANDROID_HOME}\\platform-tools;${env.PATH}"
    }

    stages {
         stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Flutter Clean') {
            steps {
                bat 'flutter clean'
            }
        }

        stage('Flutter Packages Get') {
            steps {
                bat 'flutter pub get'
            }
        }

        stage('Flutter Test') {
            steps {
                bat 'flutter test'
            }
        }

        stage('Flutter Analyze') {
            steps {
                bat 'flutter analyze'
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ashwin9099/flutter-mealApp.git'
            }
        }

        stage('Build APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'build/app/outputs/flutter-apk/app-release.apk', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build successful! Download APK from Jenkins dashboard."
        }
        failure {
            echo "Build failed! Check logs."
        }
    }
}
