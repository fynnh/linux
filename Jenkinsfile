stage("Ubuntu 64 Bit") {
    node {
		dir('build') {
			checkout scm
		}	
		def xenial64 = docker.build("xenial64", "./build/configs/ubuntu/xenial/amd64")
		def xenial32 = docker.build("xenial32", "./build/configs/ubuntu/xenial/i386")
		xenial64.inside {
		    sh "rm *.deb"
			sh "cd build && cp configs/ubuntu/xenial/amd64/amd64-config.flavour.generic .config"
			sh "cd build && yes '' | make oldconfig"
			sh "cd build && make clean"
			sh "cd build && make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
			sh "rm *dbg*.deb"
			withCredentials([
				string(credentialsId: "BINTRAY_API_KEY", variable: 'BINTRAY_API_KEY'),
				string(credentialsId: "BINTRAY_USER", variable: 'BINTRAY_USER')
			]){
			sh '''
				for f in *.deb; do
					curl -X PUT -T $f -u$BINTRAY_USER:$BINTRAY_API_KEY "https://api.bintray.com/content/$BINTRAY_USER/debian/linux/3.18.0/pool/main/linux/$f;deb_distribution=xenial;deb_component=main;deb_architecture=amd64;publish=1;override=1"
				done
				'''
			}
		}
		xenial32.inside {
		    sh "rm *.deb"
			sh "cd build && cp configs/ubuntu/xenial/i386/i386-config.flavour.generic .config"
			sh "cd build && yes '' | make oldconfig"
			sh "cd build && make clean"
			sh "cd build && make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-openc2x"
			sh "rm *dbg*.deb"			
			withCredentials([
				string(credentialsId: "BINTRAY_API_KEY", variable: 'BINTRAY_API_KEY'),
				string(credentialsId: "BINTRAY_USER", variable: 'BINTRAY_USER')
			]){
			sh '''
				for f in *.deb; do
					curl -X PUT -T $f -u$BINTRAY_USER:$BINTRAY_API_KEY "https://api.bintray.com/content/$BINTRAY_USER/debian/linux/3.18.0/pool/main/linux/$f;deb_distribution=xenial;deb_component=main;deb_architecture=i386;publish=1;override=1"
				done
				'''
			}
		}
		
    }
}

