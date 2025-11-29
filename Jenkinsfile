pipeline{
    agent any
    stages{
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Venna12/taxi-booking.git']])
            }
        }
        stage('Build'){
            steps{
                sh "mvn package"
            }
        }
        stage('Deploy to tomcat'){
            steps{
                deploy adapters: [tomcat9(credentialsId: '527db3ea-545b-436b-bcbd-3c786d08d357', path: '', url: 'http://3.137.216.135:8080/')], contextPath: 'goutham', war: '**/*.war'
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube analysis
                    sh """
                    mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar \
                    -Dsonar.projectKey=lucky17_taxiapp \
                    -Dsonar.organization=lucky17\
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.token=${SONAR_TOKEN}
                    """
                }
            }
        }


    }
}
