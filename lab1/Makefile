.PHONY: clean build simulate all test test_all _verilog

PART ?= 1
PODMAN_RUN = podman run -it --rm -v ./:/src -e PART=$(PART)

ARCH=$(shell uname -m)
ifeq ($(ARCH), x86_64)
	CONTAINER ?= docker.io/anishg24/cse140l:latest
else ifeq ($(ARCH), arm64)
	CONTAINER ?= docker.io/anishg24/cse140l:latest-arm64
endif

PORT ?= 8000

TOPLEVEL_LIST ?= top_level.txt

all: build

pull:
	podman pull $(CONTAINER)

schematics/lib:
	cp ../libdig/lab1/*.dig schematics/lib

verilog: schematics/lib
	mkdir -p verilog/ schematics/lib
	cp ../common/verilator_config.v verilog/
	$(PODMAN_RUN) $(CONTAINER) make _verilog

build: verilog
	$(PODMAN_RUN) $(CONTAINER) make -C simulator wasm

simulate:
	$(PODMAN_RUN) -p $(PORT):$(PORT) $(CONTAINER) make -C simulator simulate PORT=$(PORT)

test: verilog
	$(PODMAN_RUN) $(CONTAINER) make -C tests

test_all: verilog
	$(PODMAN_RUN) $(CONTAINER) make -C tests test_all

_verilog:
	for top in $$(cat $(TOPLEVEL_LIST)) ; do \
		digital verilog -dig schematics/$$top.dig -verilog verilog/$$top.v; \
	done

clean:
	$(RM) -rf verilog/ simulator/scripts/wasm schematics/lib
