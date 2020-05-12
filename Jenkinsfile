pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }

       stage('Deploy') {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    retry(5) {
                        sh 'echo "Deploy"'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Fail!"; '
            }
        }
        stage('Plot') {
            steps {
                plot csvFileName: 'plot-f57c4c57-e7ce-459f-93b5-4ae067369b06.csv',
                csvSeries: [[displayTableFlag: false, exclusionValues: '', file: 'test_plot.csv', inclusionFlag: 'OFF', url: '']],
                description: 'plot_descrption2',
                group: 'plot_group2',
                style: 'line',
                title: 'plot_title2'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
            plot csvFileName: 'plot-f57c4c57-e7ce-459f-93b5-4ae067369b06.csv', 
            csvSeries: [[displayTableFlag: false, exclusionValues: '', file: 'test_plot.csv', inclusionFlag: 'OFF', url: '']], 
            description: 'plot_descrption', 
            group: 'plot_group', 
            style: 'line', 
            title: 'plot_title'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
