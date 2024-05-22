pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                dir("${WORKSPACE}/ci-samples") {
                    sh '''
                    /usr/local/bin/docker_rosetta run --platform linux/amd64 -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh \
                    -projectPath=/tmp/project -browserType="Chrome" -retry=0 -statusDelay=15 \
                    -testSuitePath="Test Suites/TS_RegressionTest" -apiKey=8389077c-ca38-4148-ad5a-0f60e417dd92
                    '''
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/Reports/**/*.*', fingerprint: true
            junit '**/Reports/**/JUnit_Report.xml'
        }
    }
}
