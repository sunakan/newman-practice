################################################################################
# 変数
################################################################################
DOCKER_NEWMAN := postman/newman:5-ubuntu
WORKDIR := $(shell docker run --rm -it --entrypoint 'pwd' $(DOCKER_NEWMAN))

################################################################################
# タスク
################################################################################
.PHONY: bash
bash:
	docker run --rm -it --entrypoint '' \
		--mount type=bind,source=$(PWD)/,target=$(WORKDIR)/ \
		$(DOCKER_NEWMAN) bash

.PHONY: version
version:
	docker run --rm -it $(DOCKER_NEWMAN) --version

.PHONY: help
help:
	docker run --rm -it $(DOCKER_NEWMAN) run --help

.PHONY: sample-1
sample-1: sample.json data.csv
	docker run --rm -it \
		--mount type=bind,source=$(PWD)/,target=$(WORKDIR)/ \
		$(DOCKER_NEWMAN) run ./sample.json --iteration-data ./data.csv

sample.json:
	curl --location --output sample.json https://assets.postman.com/postman-docs/58533790.json

data.csv:
	echo path,value > data.csv
	echo 'post,"1"' >> data.csv
	echo 'post,"2"' >> data.csv
	echo 'post,"3"' >> data.csv
	echo 'post,"4"' >> data.csv
