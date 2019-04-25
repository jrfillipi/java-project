properties([pipelineTriggers([githubPush()])])

node('linux'){
    stage('Build'){
        git 'https://github.com/jrfillipi/java-project.git'
        sh 'ant -f build.xml -v'
    }
    
    stage('Unit Test'){
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    
    stage('Deploy'){
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://jrfillipi-assignment-4'
    }
    
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'fd833029-e56e-4a01-9666-75301b56e1f1', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }  
    }
}
