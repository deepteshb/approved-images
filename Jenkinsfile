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
                                // Define the naming convention based on the matrix axis
                                def baseImageFlavor = "${UBI_VERSION}-standard"
                                def targetImageName = "${UBI_VERSION}-nsw-std"
                                
                                echo "Starting parallel build for: ${targetImageName} with Build ID: ${env.BUILD_ID}"
                                
                                // Navigate to the base images directory
                                dir('base-images') {
                                    // Build the docker image passing the base flavor and tagging with the unique build ID
                                    sh "docker build --build-arg BASE_FLAVOR=${baseImageFlavor} -t ${targetImageName}:${env.BUILD_ID} ."
                                    
                                    // Optional: Verify the image built successfully
                                    sh "docker images | grep ${targetImageName}"
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
