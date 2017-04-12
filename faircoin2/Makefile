IMAGE := mmoya/faircoin2
TAG := latest

build:
	docker build --pull -t $(IMAGE):$(TAG) .

push:
	docker push $(IMAGE):$(TAG)

.PHONY: build push
