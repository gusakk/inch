include ../../buildenv.mk

IMAGE_NAME              = inch
VERSION                 = latest

IMAGE_TAG               = $(IMAGE_NAME):$(VERSION)

all: build image

.PHONY: build
build: format vet install test

style:
	@echo ">> checking code style"
	@! gofmt -d $(shell find . -path ./vendor -prune -o -name '*.go' -print) | grep '^'

test:
	@echo ">> running tests"
	@$(GO) test -short $(pkgs)

format:
	@echo ">> formatting code"
	@$(GO) fmt $(pkgs)

vet:
	@echo ">> vetting code"
	@$(GO) vet $(pkgs)

install:
	@echo ">> building binaries"
	@$(GO) install

image: build
	@echo ">> building docker image"
	cd $(GOPATH) && docker build --tag ${IMAGE_TAG} --force-rm -f ./src/inch/cmd/inch/Dockerfile --build-arg BINARY_PATH=./bin/inch .

tag:
	@docker tag "$(IMAGE_TAG)" "$(REGISTRY_LOGIN)/$(IMAGE_NAME)"

push:
	@docker push "$(REGISTRY_LOGIN)/$(IMAGE_NAME)"

.PHONY: all style install_dep format install test vet tarball image tag push