docker.image('ubuntu:14.04').inside {
	stage("Install Bundler") {
		checkout scm
		sh "cp configs/ubuntu/trusty/amd64-config.flavour.generic .config"
		sh "yes '' | make oldconfig"
		sh "make clean"
		sh "make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
	}

}
