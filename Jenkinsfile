pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
    post {
            failure {
                script {
                    // Get the build details
                    def buildNumber = env.BUILD_NUMBER
                    def jobName = env.JOB_NAME
                    def buildUrl = env.BUILD_URL


                    // Define the mail subject and body
                    def mailSubject = "Build Failure: ${jobName} #${buildNumber}"
                    def mailBody = """
                        <p>Build ${buildNumber} of ${jobName} has failed.</p>
                        <p>Build Details:</p>
                        <ul>
                            <li>Build Number: ${buildNumber}</li>
                            <li>Job Name: ${jobName}</li>
                            <li>Build URL: <a href="${buildUrl}">${buildUrl}</a></li>
                        </ul>
                        <p>Please check the build log for more details.</p>
                    """

                    // Send the email notification
                    emailext(
                        to: "bibash.g@turing.com",
                        subject: mailSubject,
                        body: mailBody,
                    )
                }
            }
        }
}