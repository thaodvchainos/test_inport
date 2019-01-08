pipeline {
    agent any 

    stages {
        

       
        stage('Checkstyle') {
            steps {
                sh 'vendor/bin/phpcs --report=checkstyle --report-file=`pwd`/build/logs/checkstyle.xml --standard=PSR2 --extensions=php --ignore=autoload.php --ignore=vendor/ . || exit 0'
                checkstyle pattern: 'build/logs/checkstyle.xml'
                }
        }
        
        
        stage('Deploy'){
            steps {
                sh  'echo  "DEPLOY STAGE"' 
            }
        }
    }
}
