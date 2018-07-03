stage("Ubuntu 64 Bit") {
    node {
		dir('build') {
			checkout scm
		}	
		def trusty64 = docker.build("trusty64", "./build/configs/ubuntu/trusty/amd64")
		trusty64.inside {
			sh "cd build && cp configs/ubuntu/trusty/amd64/amd64-config.flavour.generic .config"
			sh "cd build && yes '' | make oldconfig"
			sh "cd build && make clean"
			sh "cd build && make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
		}
		
    }
}

