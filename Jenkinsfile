pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    parameters {
        string(name: 'VPCName', defaultValue: 'demo-ntw-vpc', description: 'Description of the parameter')
	string(name: 'VPCCIDRBlock', defaultValue: '192.168.0.0/16', description: 'Description of the parameter')
	string(name: 'PublicSubnet1CIDR', defaultValue: '192.168.1.0/24', description: 'Description of the parameter')
	string(name: 'PublicSubnet1Name', defaultValue: 'ntw-pub-sub1', description: 'Description of the parameter')
	string(name: 'PrivateSubnet1CIDR', defaultValue: '192.168.2.0/24', description: 'Description of the parameter')
	string(name: 'PrivateSubnet1Name', defaultValue: 'ntw-pri-sub1', description: 'Description of the parameter')
	string(name: 'PrivateSubnet2Name', defaultValue: 'ntw-pri-sub2', description: 'Description of the parameter')
	string(name: 'PrivateSubnet2CIDR', defaultValue: '192.168.3.0/24', description: 'Description of the parameter')
	string(name: 'IGWName', defaultValue: 'demo-ntw-igw', description: 'Description of the parameter')  
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'master', credentialsId: '2b063bf8-5f5a-4287-81a3-8425c2291c19', url: 'https://github.com/TarunAngalakuduru/CFT_Templates.git'
                }
            }
        }

        stage('Deploy CloudFormation') {
            steps {
                script {
                    echo "AWS Version:"
            	    sh "aws --version"
		    echo "Deploying CloudFormation Stack..."
                    sh "aws cloudformation deploy --template-file sample-ntw.yml --stack-name demo-ntw-stack --capabilities CAPABILITY_IAM --parameter-overrides VPCName=${params.VPCName} VPCCIDRBlock=${params.VPCCIDRBlock} PublicSubnet1CIDR=${params.PublicSubnet1CIDR} PublicSubnet1Name=${params.PublicSubnet1Name} PrivateSubnet1CIDR=${params.PrivateSubnet1CIDR} PrivateSubnet1Name=${params.PrivateSubnet1Name} PrivateSubnet2Name=${params.PrivateSubnet2Name} PrivateSubnet2CIDR=${params.PrivateSubnet2CIDR} IGWName=${params.IGWName}"
                }
            }
        }
    }
}
