# if Makefile.local exists, include it
ifneq ("$(wildcard Makefile.local)", "")
        include Makefile.local
endif

# Set versions / environment vars here
DOCKER_COMPOSE_VERSION ?= 1.18.0
PROJECT_NAME ?= $(shell cat VERSION)
DOCKER_CMD := $(shell which docker)
DOCKER_COMPOSE_CMD := $(shell which docker-compose)

.PHONY: deps install_docker install_docker_compose

deps:
ifndef DOCKER_COMPOSE_CMD
deps: install_docker_compose
endif
ifndef DOCKER_CMD
deps: install_docker
endif


install_docker_compose:
	@echo "Installing docker-compose, please wait..."
	sudo curl -L https://github.com/docker/compose/releases/download/"${DOCKER_COMPOSE_VERSION}"/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose
	sudo chmod +x /usr/bin/docker-compose

install_docker:
	@echo "Installing docker, please wait..."
	curl -fsSL get.docker.com | sh
	sudo groupadd -f docker >/dev/null
	sudo usermod -aG docker ${USER} >/dev/null

start:
	docker-compose up -d

stop:
	docker-compose stop

logs:
	docker-compose logs -f
