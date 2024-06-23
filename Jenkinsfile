def ansible = [:]
         ansible.name = 'ansible'
         ansible.host = '172.31.34.148'
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
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/Venkat-6040/Maven-Java-Project.git' 
		// git branch: 'main', credentialsId: 'gitlab', url: 'https://gitlab.com/rns-app/student-app.git'
		stash 'Source'
            }
         } 
        stage('Tools-Setup') {
            steps {
		    echo "Tools Setup"
                sshCommand remote: ansible, command: 'cd Maven-Java-Project; git pull'
                sshCommand remote: ansible, command: 'cd Maven-Java-Project; ansible-playbook -i hosts tools/sonarqube/sonar-install.yaml'
                sshCommand remote: ansible, command: 'cd Maven-Java-Project; ansible-playbook -i hosts tools/docker/docker-install.yml'   
                     
                //K8s Setup
                //sshCommand remote: kops, command: "cd Maven-Java-Project; git pull"
	       //sshCommand remote: kops, command: "kubectl apply -f Maven-Java-Project/k8s-code/staging/namespace/staging-ns.yml"
	       //sshCommand remote: kops, command: "kubectl apply -f Maven-Java-Project/k8s-code/prod/namespace/prod-ns.yml"
            }            
        }  
     }
       
  
}
