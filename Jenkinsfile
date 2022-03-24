pipeline{
    agent any
        stages {
            stage('Deploying'){
                environment {
                    AWS_ACCESS_KEY = credentials('AWS_ACCESS_KEY')
                    AWS_SECRET_KEY = credentials('AWS_SECRET_KEY')
                }
                steps{
                    sh "apt-get -y install zip"
                    sh "apt-get -y install unzip"
                    sh "zip -r  aws.zip ."
                    deployLambda([alias: '', artifactLocation: 'aws.zip', awsAccessKeyId: "${AWS_ACCESS_KEY}", awsRegion: 'Region.getRegion("eu-west-3")', 
                    awsSecretKey: "${AWS_SECRET_KEY}", deadLetterQueueArn: '', description: 'Chameleon', environmentConfiguration: [kmsArn: ''], 
                    functionName: 'test-chameleon-function', handler: 'lambda_function.lambda_handler', memorySize: '', 
                    role: 'arn:aws:iam::776061104128:role/service-role/github-to-lambda-role-9m7w1o77', runtime: 'python3.9', securityGroups: '', subnets: '', timeout: '', updateMode: 'code'])
                }
            }
        }
    post{
        always{
            echo "build finished"
        }
    }
}
