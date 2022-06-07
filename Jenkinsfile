node {
    def mvnhome = tool name: "maven"
    
    stage ("scm"){
        git branch: 'master', url: 'https://github.com/joshuajosephjefries/java_project1.git'
    }
    
    stage("sonar"){
        withSonarQubeEnv(credentialsId: '4b691d68-7f62-4e99-8ec0-d46af37fe888') {
           sh "${mvnhome}/bin/mvn sonar:sonar"
        }
        
    }
    
    stage ("mvn package"){
        sh "${mvnhome}/bin/mvn package"
    }
    
    stage("artifactory"){
        rtUpload (
            serverId: 'Jfrog',
            spec: '''{
                "files": [
                {
                    "pattern": "**/*.jar",
                    "target": "maven-libs-local"
                }
                ]
             }''',
        )
    }
    stage("Deploy to tomcat"){
        deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://52.91.7.7:8080')], contextPath: null, war: '**/*.war'
    }
}
