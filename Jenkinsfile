properties([pipelineTriggers([githubPush()])])

node('linux'){
    stage('Build'){
        git 'https://github.com/jrfillipi/java-project.git'
        sh "ant -f build.xml -v"
    }
    
    stage('Unit Test'){
        sh "ant -f test.xml -v"
    }
    
    stage('Reports'){
        junit 'reports/*.xml'
    }
    
    stage('Deploy'){
        
    }
}
