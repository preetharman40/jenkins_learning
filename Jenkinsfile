pipeline {
    // Tell Jenkins to ONLY use your new Proxmox worker
    agent {
        label 'linux-prod'
    }

    stages {
        stage('Environment Audit') {
            steps {
                echo "🔍 Checking my surroundings..."
                // This prints the hostname and IP of the machine running the build
                sh 'hostname'
                sh 'ip addr show eth0 || ip addr show ens18' 
                echo "If the hostname matches your Proxmox VM, we are officially in production!"
            }
        }
        
        stage('Docker Test on VM') {
            steps {
                echo "Testing if Docker works on the new VM Agent..."
                sh 'docker --version'
            }
        }
    }
}