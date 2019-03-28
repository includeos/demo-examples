pipeline {
  agent { label 'ubuntu-18.04' }
  triggers { upstream( upstreamProjects: 'IncludeOS/IncludeOS/master, IncludeOS/IncludeOS/dev', threshold: hudson.model.Result.SUCCESS ) }
  options { checkoutToSubdirectory('src') }
  environment {
    CONAN_USER_HOME = "${env.WORKSPACE}"
    PROFILE_x86_64 = 'clang-6.0-linux-x86_64'
    CPUS = """${sh(returnStdout: true, script: 'nproc')}"""
    SRC = "${env.WORKSPACE}/src"
  }

  stages {
    stage('Setup') {
      steps {
        sh script: "ls -A | grep -v src | xargs rm -r || :", label: "Clean workspace"
        sh script: "conan config install https://github.com/includeos/conan_config.git", label: "conan config install"
      }
    }
    stage('Build examples') {
      steps {
        dir('build_examples') {
          sh script: "conan install $SRC/acorn -pr $PROFILE_x86_64", label: "Trick to get environment set up"
          sh script: ". ./activate.sh; cmake $SRC -DCONAN_PROFILE=$PROFILE_x86_64", label: "Cmake"
          sh script: "make -j $CPUS", label: "Make"
        }
      }
    }
  }
}
