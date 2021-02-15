#------------------------------------------------------------------------------
# Edit variables below as you want
REPO_DIR_LOCAL=/home/tifler/work/truen/
USERID=tifler
USERPASSWD=1111
#------------------------------------------------------------------------------
# Don't edit below if you don't know what you are doing.
TOP_DIR=$(PWD)
DOCKER_IMAGE_NAME=ubuntu-16.04-build-docker
#DOCKER_IMAGE_VERSION=v1.0
DOCKER_IMAGE_VERSION=v1.1
DOCKER_IMAGE_TAG=$(DOCKER_IMAGE_NAME):$(DOCKER_IMAGE_VERSION)
REPO_DIR_DOCKER=/repo
SSH_PORT_LOCAL=7022
#------------------------------------------------------------------------------

.PHONY: FORCE

all:	docker-build

docker-rmi:
	@echo Remove docker image: $(DOCKER_IMAGE_TAG)
	-docker rmi $(DOCKER_IMAGE_TAG)

docker-build:	FORCE
	@echo Build docker image: $(DOCKER_IMAGE_TAG)
	docker build --build-arg USERID=$(USERID) --build-arg USERPASSWD=$(USERPASSWD) --tag=$(DOCKER_IMAGE_TAG) .

docker-save:	FORCE
	docker save -o $(DOCKER_IMAGE_NAME).$(DOCKER_IMAGE_VERSION).tar $(DOCKER_IMAGE_TAG)

run:	FORCE
	docker run -p $(SSH_PORT_LOCAL):22 -d -v $(REPO_DIR_LOCAL):$(REPO_DIR_DOCKER) $(DOCKER_IMAGE_TAG)

run-it:	FORCE
	docker run -it -p $(SSH_PORT_LOCAL):22 -v $(REPO_DIR_LOCAL):$(REPO_DIR_DOCKER) $(DOCKER_IMAGE_TAG)
