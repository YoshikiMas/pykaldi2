USER_NAME = $(USER)
GROUP_NAME = Domain
HOST_PATH = '/home/$(USER_NAME)'
CONTAINER_PATH = '/home/$(USER_NAME)'
ROOT_PASSWORD = 'password'
IMAGE_TAG = 'pykaldi2docker/horovod-pykaldi:torch1.2'

all: ## build & run docker.
	@make build
	@make run

build: ## build docker.
	docker build -t $(IMAGE_TAG) ./

run: ## run docker.
	docker run -it --gpus all \
	-e USER_NAME=$(USER_NAME) -e GROUP_NAME=$(GROUP_NAME) \
	-e LOCAL_UID=$(shell id -u $(USER)) -e LOCAL_GID=$(shell id -g $(USER)) \
	-v $(HOST_PATH):$(CONTAINER_PATH) \
	-w $(CONTAINER_PATH) \
	--shm-size 32gb \
	--memory 128gb \
	$(IMAGE_TAG) /bin/bash

connect: ## connect newest container
	docker exec -i -t $(CONTAINER_ID) /bin/bash