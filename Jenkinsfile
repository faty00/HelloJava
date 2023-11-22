pipeline {
    agent any

    stages {
        stage('Récupération de l\'applicatif') {
            steps {
                git url: 'https://MoradDev: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@github.com/MoradDev/HelloJava.git'
                script {
                    // Copiez le fichier Hello.java dans /tmp
                    sh 'rm -f /tmp/*.java'
                    sh 'cp Hello.java /tmp'
                }
            }
        }
        
        stage('Build de l\'applicatif') {
            steps {
                dir('/tmp') {
                    sh 'javac Hello.java'
                    sh 'java Hello'
                }
            }
        }
        
        stage("Tag Version. Release") {
            environment { 
                GIT_TAG = "Version-2.$BUILD_NUMBER"
            }
            steps {
                script {
                    // Création et poussée du tag Git
                    sh "git tag -a \$GIT_TAG -m \"[Jenkins CI] New Tag\""
                    sh "git push origin \$GIT_TAG"
                }
            }
        }
    }
}
