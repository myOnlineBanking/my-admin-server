def jarName     = "adminServer-0.0.1-SNAPSHOT.jar"
def jarPath     = "/var/jenkins_home/workspace/adminServer/target/${jarName}"
def deployPath  = "/var/jenkins_home/hamza/microservices/adminServer"

pipeline {
    agent any
    tools{
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('kill jar') {
            steps {
                catchError {
                    sh "jps -l | grep ${jarName} || exit 0"
                    sh "sh ${killerSh} ${jarName} || exit 0"
                    sh "jps -l | grep ${jarName} || exit 0"
                }
            }
        }
        stage("Deploy & Start") {
            steps {
                sh " cp ${jarPath} ${deployPath}"
                dir("${deployPath}") {
                      sh "pwd"
                      //sh "JENKINS_NODE_COOKIE=dontKillMe nohup java -jar -Xms128m -Xmx512m ${jarName} & "
                      //sh "timeout 10 tail -f logs/application-logger.log || exit 0"
                      //sh "jps -l | grep ${jarName}"
                      sh "nohup java -jar ${jarName}"
                }
            }
        }
    }
}
