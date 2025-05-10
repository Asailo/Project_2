pipeline{
    agent any
    stages {
        stage ("Echo") {
            steps {
                echo "Hello, Friends I am learning Jenkins"
            }
        }
    }
}
