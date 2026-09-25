pipeline {
    agent any
    
    options {
        timeout(time: 1, unit: 'HOURS')
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    
    stages {
        stage('Parallel Base Image Builds') {
            matrix {
                axes {
                    axis {
                        name 'UBI_VERSION'
                        values 'ubi8', 'ubi9', 'ubi10'
                    }
                }
                
                stages {
                    stage("Build & Tag") {
                        steps {
                            script {
                                // Explicitly evaluate the variables with double quotes and dollar signs
                                def fullRedHatUrl = "://redhat.com{UBI_VERSION}/ubi"
                                def targetImageName = "${UBI_VERSION}-nsw-std"
                                
                                echo "Triggering build for ${targetImageName} from parent path: ${fullRedHatUrl}"
                                
                                // Point directly to the Dockerfile from the root workspace using -f
                                sh "docker build --build-arg BASE_IMAGE=${fullRedHatUrl} -t ${targetImageName}:${env.BUILD_ID} -f approved-images/base-images/Dockerfile approved-images/base-images/"
                            }
                        }
                    }
                }
            }
        }
    }
}
