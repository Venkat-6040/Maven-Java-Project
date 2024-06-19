def ansible = [:]
         ansible.name = 'ansible'
         ansible.host = '172.31.21.23'
         ansible.user = 'centos'
         ansible.password = 'devops'
         ansible.allowAnyHosts = true
pipeline {
    agent { label 'Build Server'}

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven 3.9.5"
    }

    stages {
        stage('Prepare-Workspace') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'github-server-credentials', url: 'https://github.com/Venkat-6040/Maven-Java-Project.git'    
            }
           } 
        }
  
}
