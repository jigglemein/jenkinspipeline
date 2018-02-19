pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''tar cvf CDH_software.tar.gz -C ${WORKSPACE} .
                > scp CDH_software.tar.gz ec2-user@54.252.242.185:/home/ec2-user/             
                > ssh ec2-user@172.31.12.60 <<EOF
                > docker cp CDH_software.tar.gz ccs7_smaller:/tmp
                > docker exec -t ccs7_smaller tar xvzf CDH_software.tar.gz
                > docker exec -t ccs7_smaller /opt/ti/ccsv7/eclipse/eclipse -noSplash -data /tmp/workspace/ -application com.ti.ccstudio.apps.projectImport -ccs.location /tmp/CDH_software
                > docker exec -t ccs7_smaller /opt/ti/ccsv7/eclipse/eclipse -noSplash -data /tmp/workspace/ -application com.ti.ccstudio.apps.projectBuild -ccs.workspace -ccs.configuration "TIRTOS Build"
                > docker exec -t ccs7_smaller rm -rf /tmp/workspace /tmp/CDH_software /tmp/CDH_software.tar.gz
                EOF'''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
