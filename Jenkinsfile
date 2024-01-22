pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    parameters {
        string(name: 'VPCName', defaultValue: 'ntw-vpc', description: 'Description of the parameter')
	string(name: 'VPCCIDRBlock', defaultValue: '10.0.0.0/16', description: 'Description of the parameter')
	string(name: 'PublicSubnet1CIDR', defaultValue: '10.0.1.0/24', description: 'Description of the parameter')
	string(name: 'PublicSubnet1Name', defaultValue: 'ntw-pub-sub1', description: 'Description of the parameter')
	string(name: 'PrivateSubnet1CIDR', defaultValue: '10.0.2.0/24', description: 'Description of the parameter')
	string(name: 'PrivateSubnet1Name', defaultValue: 'ntw-pri-sub1', description: 'Description of the parameter')
	string(name: 'PrivateSubnet2Name', defaultValue: 'ntw-pri-sub2', description: 'Description of the parameter')
	string(name: 'PrivateSubnet2CIDR', defaultValue: '10.0.3.0/24', description: 'Description of the parameter')
	string(name: 'IGWName', defaultValue: 'ntw-igw', description: 'Description of the parameter')  
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'master', credentialsId: 'c03b3035-9fd6-4c59-a0be-762842fc8b1a', url: 'https://github.com/TarunAngalakuduru/CFT_Templates.git'
                }
            }
        }

        stage('Deploy CloudFormation') {
            steps {
                script {
                    sh "aws cloudformation deploy --template-file sample-ntw.yml --stack-name demo-ntw-stack --capabilities CAPABILITY_IAM --parameter-overrides VPCName=${params.VPCName} VPCCIDRBlock=${params.VPCCIDRBlock} PublicSubnet1CIDR=${params.PublicSubnet1CIDR} PublicSubnet1Name=${params.PublicSubnet1Name} PrivateSubnet1CIDR=${params.PrivateSubnet1CIDR} PrivateSubnet1Name=${params.PrivateSubnet1Name} PrivateSubnet2Name=${params.PrivateSubnet2Name} PrivateSubnet2CIDR=${params.PrivateSubnet2CIDR} IGWName=${params.IGWName}"
                }
            }
        }
    }
}
