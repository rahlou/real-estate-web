node('ubuntu-appserver-3120')
{
    def app
    stage('Cloning Git')
    {
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
    }
    stage('Build-and-Tag')
    {
        /* This Builds the actual image;
        * This is synonymous to docker build on the command line */
        app =docker.build("rahlou/real-estate-web")
    }
    stage('Post-to-dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
        app.push("latest")
        }
    }
    
    stage('Pull-image-server')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }

}
