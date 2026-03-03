IMAGE_NAME ?= ghcr.io/aidc-lab/ms-swift
SLIM_IMAGE_TAG  ?= v3.12.0-slim.12-rocm-dcu
# platforms, multiple platforms should be separated by comma
PLATFORMS  ?= linux/amd64

.PHONY: build-4pd-slim
build-4pd-slim:
	docker buildx build \
		--progress=plain \
		--compress --build-arg BUILDKIT_COMPRESSION_COMPRESSOR=zstd \
		-f Dockerfile.4pd-slim -t $(IMAGE_NAME):$(SLIM_IMAGE_TAG) \
		--platform $(PLATFORMS) \
		../.. \
		--push