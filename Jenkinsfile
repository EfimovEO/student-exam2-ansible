pipeline {
    agent { label "agent-exam2" }
    stages {
	    stage('DEPLOY') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[ name: "main"]],
                    userRemoteConfigs: [[ credentialsId: "github_eeo", url:'https://github.com/EfimovEO/student-exam2-ansible.git']]
                ])
                ansiblePlaybook(
                    credentialsId: 'ansible_exam2',
                    inventory: 'hosts',
                    playbook: 'playbook.yml',
                    vaultCredentialsId: 'ansible_vault_password'
                    )
            }
	    }
	    stage('TEST') {
            steps {
                sh 'python3 ./test_web_app.py http://192.168.56.10'
            }
        }
    }
}
