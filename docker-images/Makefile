FILENAME:=$(shell basename $(FILE))
NSO_VERSION:=$(shell echo $(FILENAME) | sed -E -e 's/(ncs|nso)-(.+)\.linux.x86_64.installer.bin/\2/')

.PHONY: build

build:
	@echo "Building NSO development Docker image cisco-nso-dev:$(NSO_VERSION) based on $(FILE)"
	rm -f *.bin
	cp $(FILE) $(FILENAME)
	docker build $(DOCKER_BUILD_CACHE_ARG) --build-arg NSO_INSTALL_FILE=$(FILENAME) --target base -t $(DOCKER_REGISTRY)cisco-nso-base:$(DOCKER_TAG) .
	docker build $(DOCKER_BUILD_CACHE_ARG) --build-arg NSO_INSTALL_FILE=$(FILENAME) --target dev -t $(DOCKER_REGISTRY)cisco-nso-dev:$(DOCKER_TAG) .
	rm -f *.bin
