stage("Ubuntu 64 Bit") {
    node {
		dir('build') {
			checkout scm
		}	
		def bionic64 = docker.build("bionic", "./build/configs/ubuntu/bionic/amd64")
		bionic64.inside {
			sh "cd build && cp configs/ubuntu/bionic/amd64/amd64-config.flavour.generic .config"
			sh "cd build && yes '' | make oldconfig"
			sh "cd build && make clean"
			sh "cd build && make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
			withCredentials([
				string(credentialsId: "BINTRAY_API_KEY", variable: 'BINTRAY_API_KEY'),
				string(credentialsId: "BINTRAY_USER", variable: 'BINTRAY_USER')
			]){
			sh '''
				for f in *.deb; do
					curl -X PUT -T $f -u$BINTRAY_USER:$BINTRAY_API_KEY "https://api.bintray.com/content/$BINTRAY_USER/debian/linux/3.18.0/pool/main/linux/$f;deb_distribution=bionic;deb_component=main;deb_architecture=amd64;publish=1;override=1"
				done
				'''
			}
		}
		
    }
}

