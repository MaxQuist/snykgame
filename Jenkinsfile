node('ubuntu-Appserver-3120')
{

    def app 
    stage('Cloning Git')
    {
        /*cloning repository to workspace*/
        checkout scm
    }

    stage('Build-and-tag')
    {
    /*builds the image*/
    app = docker.build('xamq/snyk_game_repo')
    }

    stage('Push to docker')
    {
        docker.withRegistry('https://registry.hub.docker.com','maxq')
        {
            app.push('latest')
        }
    }

    stage('Deploy')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }

}