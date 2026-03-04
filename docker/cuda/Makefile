IMAGE_NAME ?= ghcr.io/aidc-lab/ms-swift
IMAGE_TAG ?= v3.12.0-beta.1-cuda

# platforms, multiple platforms should be separated by comma
PLATFORMS  ?= linux/amd64

.PHONY: build
build:
	docker buildx build \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile -t ms-swift:release-3.12.0 \
		--platform $(PLATFORMS) \
		../..

.PHONY: build-4pd
build-4pd:
	docker buildx build \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile.4pd -t $(IMAGE_NAME):$(IMAGE_TAG) \
		--platform $(PLATFORMS) \
		../.. \
		--push