# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
# Copyright 2023 Jerzy Głowacki (jerzyglowacki@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
REVISION:=69
PWD:=$(shell pwd)

.PHONY: all

all: clean init

	mkdir -p $(PWD)/build/Boilerplate.AppDir/carbonyl
	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate \
        libasound2 libatk-bridge2.0-0 libatk1.0-0 libatomic1 libatspi2.0-0 \
        libbrotli1 libc6 libcairo2 libcups2 libdbus-1-3 libdouble-conversion3 \
        libdrm2 libevent-2.1-7 libexpat1 libflac8 libfontconfig1 libfreetype6 \
        libgbm1 libgcc-s1 libglib2.0-0 libjpeg62-turbo libjsoncpp24 liblcms2-2 \
        libminizip1 libnspr4 libnss3 libopenjp2-7 libopus0 libpango-1.0-0 \
        libpng16-16 libpulse0 libre2-9 libsnappy1v5 libstdc++6 libwebp6 \
        libwebpdemux2 libwebpmux3 libwoff1 libx11-6 libxcb1 libxcomposite1 \
        libxdamage1 libxext6 libxfixes3 libxkbcommon0 libxml2 libxnvctrl0 \
        libxrandr2 libxslt1.1 zlib1g libgtk-3-0

	wget -O ${PWD}/build/build.zip https://refloat.ci/artifact/fathyb/carbonyl/$(REVISION)/carbonyl.linux-amd64.zip
	unzip ${PWD}/build/build.zip -d ${PWD}/build/carbonyl

	echo ''                                                           >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                           >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'LD_LIBRARY_PATH=$${LD_LIBRARY_PATH}:$${APPDIR}/carbonyl'    >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'export LD_LIBRARY_PATH=$${LD_LIBRARY_PATH}'                 >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                           >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                           >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'exec $${APPDIR}/carbonyl/carbonyl "$${@}"'                  >> $(PWD)/build/Boilerplate.AppDir/AppRun


	cp -fr $(PWD)/build/carbonyl/* $(PWD)/build/Boilerplate.AppDir/carbonyl

	rm -f $(PWD)/build/Boilerplate.AppDir/*.desktop

	cp -f $(PWD)/AppDir/*.desktop $(PWD)/build/Boilerplate.AppDir/
	cp -f $(PWD)/AppDir/*.png     $(PWD)/build/Boilerplate.AppDir/       || true
	cp -f $(PWD)/AppDir/*.svg     $(PWD)/build/Boilerplate.AppDir/       || true

	export ARCH=x86_64 && $(PWD)/bin/appimagetool.AppImage $(PWD)/build/Boilerplate.AppDir $(PWD)/carbonyl.AppImage
	chmod +x $(PWD)/carbonyl.AppImage

init:
	mkdir -p $(PWD)/bin

	wget https://apprepo.de/appimage/download/apprepo -O $(PWD)/bin/Apprepo.AppImage
	chmod +x $(PWD)/bin/Apprepo.AppImage

	wget https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage -O $(PWD)/bin/appimagetool.AppImage
	chmod +x $(PWD)/bin/appimagetool.AppImage

clean:
	rm -rf $(PWD)/*.AppImage
	rm -rf $(PWD)/bin/*
	rm -rf $(PWD)/build
