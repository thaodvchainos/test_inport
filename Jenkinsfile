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
       stage('Analysis'){
            steps {
                  def mvnHome = tool 'mvn-default'
 
                    sh "${mvnHome}/bin/mvn -batch-mode -V -U -e checkstyle:checkstyle pmd:pmd pmd:cpd"

                    def checkstyle = scanForIssues tool: [$class: 'CheckStyle'], pattern: 'build/logs/checkstyle.xml'
                    publishIssues issues:[checkstyle]

                    def pmd = scanForIssues tool: [$class: 'Pmd'], pattern: 'build/logs/pmd.xml'
                    publishIssues issues:[pmd]

                    def cpd = scanForIssues tool: [$class: 'Cpd'], pattern: 'build/logs/pmd-cpd..xml'
                    publishIssues issues:[cpd]

                }
        }
         
        stage('Deploy'){
            steps {
                sh  'echo  "DEPLOY STAGE"' 
            }
        }
    }
}
