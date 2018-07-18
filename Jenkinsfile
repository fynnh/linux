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
			withCredentials([
				string(credentialsId: "BINTRAY_API_KEY", variable: 'BINTRAY_API_KEY'),
				string(credentialsId: "BINTRAY_USER", variable: 'BINTRAY_USER')
			]){
				echo "My user '${BINTRAY_USER}' and  Key is '${BINTRAY_API_KEY}'!"
			}
		}
		
    }
}

