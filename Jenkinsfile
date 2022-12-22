pipeline{
    agent any
    tools
    {
        maven 'MAVEN'
    }
    stages
    {
        stage('continuous download')
        {
            steps
            {
                git 'https://github.com/hemanaik21/maven_test.git'
            }
        }
        stage('continuous build')
        {
            steps
            {
                sh 'mvn clean package'
            }
        }
         stage('continuous deploy')
        {
            steps
            {
                
            deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://172.31.33.156:8080/')], contextPath: 'decapp', war: '**/*war'
        }
        }
          stage('continuous test')
        {
            steps
            {
                
            git 'https://github.com/keshavr21/test_cases.git'
        
            sh 'java -jar ${WORKSPACE}/testing.jar'
        }
        }
    
        //stage('continuous delivery')
        //{
           // steps
            //{
                //input message: 'Waiting for manager approval', submitter: 'naik,admin'
                
              //sh 'scp ${WORKSPACE}/webapp/target/*.war ec2-user@172.31.33.156:/home/ec2-user/usr/shared/apache-tomcat-9.0.70/webapps/prodapp.war' 
              
        //}
        //}
    }
        post
        {
            success{
                sh 'scp ${WORKSPACE}/webapp/target/*.war ec2-user@172.31.33.156:/home/ec2-user/usr/shared/apache-tomcat-9.0.70/webapps/prodapp.war' 
            }
            failure{
                mail bcc: '', body: '''build failed because tomcat server is not running''', cc: '', from: '', replyTo: '', subject: 'BUILD FAILURE', to: 'hemacnaik21@gmail.com'
            }
            always
            {
                sh '''echo "this block will always run"'''

            }
            aborted{
                sh '''echo "this block will run @ abort"'''
            }
        }
    }
    
