properties([pipelineTriggers([githubPush()])])

node('linux'){
    stage('Build'){
        git 'https://github.com/jrfillipi/java-project.git'
        sh "ant -f build.xml -v"
    }
    
    stage('Unit Test'){
        sh "ant -f test.xml -v"
        junit 'reports/result.xml
    }
    
    stage('Deploy'){
    
    }
    
    stage('Report'){
        sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins
        
    }
}
