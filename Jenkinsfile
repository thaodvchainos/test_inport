pipeline {
    agent any 

    stages {
        

       
        stage('Checkstyle') {
            steps {
                sh 'vendor/bin/phpcs --report=checkstyle --report-file=`pwd`/build/logs/checkstyle.xml --standard=PSR2 --extensions=php --ignore=autoload.php --ignore=vendor/ . || exit 0'
                checkstyle pattern: 'build/logs/checkstyle.xml'
                }
        }
        
        stage('PMD') {
            steps {
                sh 'vendor/bin/phpmd . xml build/phpmd.xml --reportfile build/logs/pmd.xml --exclude vendor/ || exit 0'
                pmd canRunOnFailed: true, pattern: 'build/logs/pmd.xml'
            }
        }
        stage('Copy paste detection') {
            steps {
                sh 'vendor/bin/phpcpd --log-pmd build/logs/pmd-cpd.xml --exclude vendor . || exit 0'
                dry canRunOnFailed: true, pattern: 'build/logs/pmd-cpd.xml'
            }
        }
       
        stage('CPD ReportDeploy'){
            steps {
                sh 'phpcpd --log-pmd build/logs/pmd-cpd.xml --exclude vendor app || exit 0' /* should be vendor/bin/phpcpd but... conflicts... */
                dry canRunOnFailed: true, pattern: 'build/logs/pmd-cpd.xml'
            }
        }
         
        stage('Deploy'){
            steps {
                sh  'echo  "DEPLOY STAGE"' 
            }
        }
    }
}
