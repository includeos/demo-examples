pipeline {
  agent { label 'vaskemaskin' }

  options {
    checkoutToSubdirectory('src')
  }

  environment {
    CONAN_USER_HOME = "${env.WORKSPACE}"
    REMOTE = "${env.CONAN_REMOTE}"
    PROFILE_x86_64 = 'clang-6.0-linux-x86_64'
    PROFILE_x86 = 'clang-6.0-linux-x86'
    CPUS = """${sh(returnStdout: true, script: 'nproc')}"""
    CC = 'clang-6.0'
    CXX = 'clang++-6.0'
    USER = 'includeos'
    CHAN = 'test'
    SRC = "${env.WORKSPACE}/src"
  }

  stages {
    stage('Setup') {
      steps {
        sh script: "conan config install https://github.com/includeos/conan_config.git", label: "conan config install"
      }
    }
    stage('Build examples') {
      steps {
        sh script: "mkdir -p build_examples", label: "Setup"
        dir('build_examples') {
          sh script: "cmake $SRC -DCONAN_PROFILE=$PROFILE_x86_64", label: "Cmake"
          sh script: "make -j $CPUS", label: "Make"
        }
      }
    }
  }
}
