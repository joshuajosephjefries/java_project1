node {
    def mvnhome = tool name: "maven"
    
    stage ("scm"){
        git branch: 'main', url: 'https://github.com/joshuajosephjefries/java_project1.git'
    }
    
    stage ("sonar"){
        withSonarQubeEnv(credentialsId: 'Sonar_pat') {
           sh "${mvnhome}/bin/mvn sonar:sonar"
        }
    }
    
    stage ("mvn package"){
        sh "${mvnhome}/bin/mvn package"
    }
}
