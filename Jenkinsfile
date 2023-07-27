node{

def mavenhome = tool name: "maven3.8.8"

    echo "The node name is: ${env.NODE_NAME} "
    echo "The job name is: ${env.JOB_NAME} "
    echo "The Build name is: ${env.BUILD_NUMBER}"
//checkout SCM 
stage('github to jenkins'){

git credentialsId: 'cf17d19c-920c-431d-815b-d6dac193326b', url: 'https://github.com/anand1590/maven-web-application.git'

}
//Build code
stage('jenkins to maven'){
sh "$mavenhome/bin/mvn clean package" 
}
//sonarqube code test
stage('maven to sonarqube'){
sh "$mavenhome/bin/mvn sonar:sonar"
    }
//nexus
stage('nexus Artifcatory'){
sh "$mavenhome/bin/mvn deploy"
 }

//apache tomcat Deploy
stage('tomcat Deploy'){
sshagent(['e115938e-36db-44e1-bf7f-92267011972d']) {
sh "scp -o stricthostkeychecking=no target/maven-web-application.war ec2-user@43.204.142.0:/opt/apache-tomcat-9.0.78/webapps"
}
}
} //node close
