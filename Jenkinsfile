pipeline {
    agent {
        docker { image 'ubuntu:xenial'                            
                 args '-u 0 --privileged'
               }
    }
    stages {
        stage('prepre') {
            steps {
                sh '''
                apt-get update
                apt-get install -y build-essential sudo qemu kvm python
                groupadd -r jenkins -g 6958
                useradd -u 6930 -r -g jenkins -m -d /jenkins -c "Jenkins" jenkins
                usermod -aG kvm jenkins
                chown root:kvm /dev/kvm
                id jenkins
                '''
            }
        }
        stage('build') {
            steps {
                sh '''
                sudo -u jenkins make grade
                '''
            }
        }
    }
}
