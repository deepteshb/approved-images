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
                                // Red Hat UBI image paths are structured as ://redhat.com or /ubi
                                // We construct the full registry path cleanly in Jenkins
                                def fullRedHatUrl = "://redhat.com{UBI_VERSION}/ubi"
                                def targetImageName = "${UBI_VERSION}-nsw-std"
                                
                                echo "Triggering build for ${targetImageName} from parent path: ${fullRedHatUrl}"
                                
                                dir('approved-images/base-images') {
                                    // Pass the full registry URL straight to the Dockerfile
                                    sh "docker build --build-arg BASE_IMAGE=${fullRedHatUrl} -t ${targetImageName}:${env.BUILD_ID} ."
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
