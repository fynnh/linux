def ubuntu = docker.build("trusty64", "./configs/ubuntu/trusty/amd64/Dockerfile")


stage("Ubuntu 64") {
    node {
		checkout scm
		def trusty64 = docker.build("trusty64", "./configs/ubuntu/trusty/amd64/Dockerfile")
		trusty64.inside {
			sh "cp configs/ubuntu/trusty/amd64/amd64-config.flavour.generic .config"
			sh "yes '' | make oldconfig"
			sh "make clean"
			sh "make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
		}
    }
}

