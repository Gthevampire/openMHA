.PHONY: all
all: build pkg
.PHONY= build
include luggage.make

#openMHA project directory
REPO=../../../..

#Include meta-information in the package
PACKAGE_VERSION=4.8.0
TITLE=openMHA
REVERSE_DOMAIN=org.openmha

#Targets to execute before packing
PAYLOAD= \
        usr-local-bin \
        usr-local-lib \
				mfiles \
        matfiles \
        examples \
				docfiles \
				bundle-uninstall-openMHA


#Basename of the resulting package. Set PACKAGE-VERSION on the command line
UTIL=openMHA-installer

build:
	@./find_and_copy_dependencies.sh
	@(cd $(REPO) && make install)

usr-local-bin: l_usr_local_bin
	@${CP} ./bin/* ${WORK_D}/usr/local/bin/

usr-local-lib: l_usr_local_lib
	@${CP} ./lib/* ${WORK_D}/usr/local/lib/

examples: l_usr_local_share
	@mkdir -p ${WORK_D}/usr/local/share/openmha/examples
	@${CP} -r ${REPO}/mha/examples/* ${WORK_D}/usr/local/share/openmha/examples/.

mfiles: l_usr_local_lib
	@mkdir -p ${WORK_D}/usr/local/lib/openmha/mfiles
	@${CP} ${REPO}/mha/tools/mfiles/*m ${WORK_D}/usr/local/lib/openmha/mfiles
	@${CP} ${REPO}/mha/tools/mfiles/mhactl_java.jar ${WORK_D}/usr/local/lib/openmha/mfiles

matfiles: l_usr_local_share
	@mkdir -p ${WORK_D}/usr/local/share/openmha
	@${CP} ${REPO}/mha/tools/mfiles/*.mat ${WORK_D}/usr/local/share/openmha/
	@${CP} ${REPO}/mha/tools/mfiles/*.cfg ${WORK_D}/usr/local/share/openmha/

docfiles:
	@mkdir -p ${WORK_D}/usr/local/doc/openmha/
	@${CP} ${REPO}/*.pdf ${WORK_D}/usr/local/doc/openmha/

clean:
	@rm -rf tmp/
	@rm -rf bin/
	@rm -rf lib/
	@rm -rf doc/
	@rm -rf mfiles/
	@rm -rf *.pkg
	@rm -rf *.dmg
