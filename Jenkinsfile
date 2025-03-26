pipeline {
    agent any

    environment {
        FLUTTER_HOME = "D:\\Softwares\\flutter"
        ANDROID_HOME = "C:\\Users\\ankul\\AppData\\Local\\Android\\Sdk"
        PATH = "${FLUTTER_HOME}\\bin;${ANDROID_HOME}\\platform-tools;${PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ashwin9099/flutter-mealApp.git'
            }
        }

        stage('Setup Flutter') {
            steps {
                sh 'flutter doctor'
                sh 'flutter pub get'
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
