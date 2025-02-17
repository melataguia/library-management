pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/melataguia/library-management.git'
            }
        }
        stage('Build API') {
            steps {
                dir('LibraryAPI') {
                    sh 'dotnet build --configuration Release'
                }
            }
        }
        stage('Build WebApp') {
            steps {
                dir('LibraryWebApp') {
                    sh 'dotnet build --configuration Release'
                }
            }
        }
        stage('Test API') {
            steps {
                dir('LibraryAPI') {
                    sh 'dotnet test'
                }
            }
        }
        stage('Publish API') {
            steps {
                dir('LibraryAPI') {
                    sh 'dotnet publish -c Release -o output'
                }
            }
        }
        stage('Publish WebApp') {
            steps {
                dir('LibraryWebApp') {
                    sh 'dotnet publish -c Release -o output'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'mkdir -p /var/www/libraryapp'
                sh 'cp -r LibraryAPI/output/* /var/www/libraryapp/'
                sh 'cp -r LibraryWebApp/output/* /var/www/libraryapp/'
            }
        }
    }
}