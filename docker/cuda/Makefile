IMAGE_NAME ?= ghcr.io/aidc-lab/ms-swift
PROD_IMAGE_TAG ?= v3.12.0-alpha.3-cuda
SLIM_IMAGE_TAG  ?= v3.12.0-slim.12-cuda
# platforms, multiple platforms should be separated by comma
PLATFORMS  ?= linux/amd64

.PHONY: build
build:
	docker buildx build \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile -t ms-swift:release-3.12.0 \
		--platform $(PLATFORMS) \
		../..

.PHONY: build-4pd-prod
build-4pd-prod:
	docker buildx build \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile.4pd-prod -t $(IMAGE_NAME):$(PROD_IMAGE_TAG) \
		--platform $(PLATFORMS) \
		../..

.PHONY: build-4pd-slim
build-4pd-slim:
	docker buildx build \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile.4pd-slim -t $(IMAGE_NAME):$(SLIM_IMAGE_TAG) \
		--platform $(PLATFORMS) \
		../.. \
		--push