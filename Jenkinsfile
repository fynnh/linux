stage("Ubuntu 64 Bit") {
    node {
		dir('build') {
			checkout scm
		}	
		def trusty64 = docker.build("trusty64", "./build/configs/ubuntu/trusty/amd64")
		trusty64.inside {
			sh "cd build"
			sh "cp configs/ubuntu/trusty/amd64/amd64-config.flavour.generic .config"
			sh "yes '' | make oldconfig"
			sh "make clean"
			sh "make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
		}
		
    }
}

