node('php') {

   

    stage('Composer Install') {
        sh 'composer install'
    }

    

    

    stage('Checkstyle Report') {
        sh 'vendor/bin/phpcs --report=checkstyle --report-file=build/logs/checkstyle.xml --standard=phpcs.xml --extensions=php,inc --ignore=autoload.php --ignore=vendor/ app || exit 0'
        checkstyle pattern: 'build/logs/checkstyle.xml'
    }

    

}
