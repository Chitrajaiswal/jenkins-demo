pipeline {
agent any
stages {
stage('build') {
steps {
sh 'javac -d . src/*.java'
sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
}
}
stage('run') {
steps {
sh 'java -jar rectangle.jar 7 9'
}
}
stage ('Build Image'){  
     steps{ 
        sh 'sudo docker image build -t area-perimeter .'
        }
    }
}
stage ('Run on container'){
     steps{
        sh 'sudo docker run -d --name=new area-perimeter
        }
    }
post {
success {
archiveArtifacts artifacts: 'rectangle.jar', fingerprint:
true
}
}
}
