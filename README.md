pipeline{
    agent any
    stages {
        stage ("Echo") {
            steps {
                echo "Hello, Friends I am learning Jenkins"
                echo "To be Successful in this life"
            }
        }
    }
}
