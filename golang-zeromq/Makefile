IMAGE := mmoya/golang-zeromq
TAG := $(shell awk -F: '/FROM/ {print $$2}' Dockerfile)

build:
	docker build --pull -t $(IMAGE):$(TAG) .

push:
	docker push $(IMAGE):$(TAG)

.PHONY: build push
