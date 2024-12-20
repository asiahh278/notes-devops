# Jenkins

## Install Jenkins
### Jenkins Debian Packages
This is the Debian package repository of Jenkins to automate installation and upgrade. To use this repository, first add the key to your system: 
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Then add a Jenkins apt repository entry: 
```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update your local package index, then finally install Jenkins: 
```
sudo apt-get update
sudo apt-get install fontconfig openjdk-11-jre
sudo apt-get install jenkins
```

Pipeline and Jenkinsfile
```
pipeline {
    agent { label 'devops1-amar' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/bazigan/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
                npm install
                '''
            }
        }
        
        stage('Testing') {
            steps {
                sh'''
                cd app
                APP_PORT=3001 npm test
                APP_PORT=3001 npm run test:coverage
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd app
                sonar-scanner \
                    -Dsonar.projectKey=Simple-Apps \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://172.23.8.20:9000 \
                    -Dsonar.login=sqp_afd306fec629a29b3636919ec4f4aaeff8f70ac4
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose build
                docker compose down --volumes
                docker compose up -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerAmar', passwordVariable: 'dockerAmarPassword', usernameVariable: 'dockerAmarUser')]) {
                    sh "docker login -u ${env.dockerAmarUser} -p ${env.dockerAmarPassword}"
                    sh 'docker compose push'
                }
            }
        }
        
        
    }
}
```

