
DIST_DIR ?= $(CURDIR)/dist
CHART_DIR ?= $(CURDIR)/traefik
TMPDIR ?= /tmp
HELM_REPO ?= $(CURDIR)/repo
LINT_USE_DOCKER ?= true
LINT_CMD ?= ct lint --config=lint/ct.yaml
<<<<<<< HEAD:traefik-charts/Makefile
PROJECT ?= github.com/traefik/traefik-helm-chart
=======
PROJECT ?= github.com/containous/traefik-helm-chart
>>>>>>> 43d63f41 (Publish helm chart (#81)):Makefile
################################## Functionnal targets

# Default Target: run all
all: clean test build deploy

test: lint unit-test

# Execute Static Testing
lint: lint-requirements
	@echo "== Linting Chart..."
	@git remote add traefik https://github.com/traefik/traefik-helm-chart >/dev/null 2>&1 || true
	@git fetch traefik master >/dev/null 2>&1 || true
ifeq ($(LINT_USE_DOCKER),true)
<<<<<<< HEAD:traefik-charts/Makefile
<<<<<<< HEAD:traefik-charts/Makefile
	@docker run --rm -t -v $(CURDIR):/charts -w /charts quay.io/helmpack/chart-testing:v3.0.0-beta.2 $(LINT_CMD)
=======
	@docker run --rm -t -v $(CURDIR):/charts -w /charts/lint quay.io/helmpack/chart-testing:v3.0.0-beta.1 $(LINT_CMD)
>>>>>>> ca4e233a (Add Unit Tests for the chart (#60)):Makefile
=======
	@docker run --rm -t -v $(CURDIR):/charts -w /charts quay.io/helmpack/chart-testing:v3.0.0-beta.1 $(LINT_CMD)
>>>>>>> 43d63f41 (Publish helm chart (#81)):Makefile
else
	cd $(CHART_DIR)/tests && $(LINT_CMD)
endif
	@echo "== Linting Finished"

# Execute Unit Testing
unit-test: helm-unittest
	@echo "== Unit Testing Chart..."
	@helm unittest --color --update-snapshot ./traefik
	@echo "== Unit Tests Finished..."
<<<<<<< HEAD:traefik-charts/Makefile
<<<<<<< HEAD:traefik-charts/Makefile


# Generates an artifact containing the Helm Chart in the distribution directory
=======
	
=======

>>>>>>> 43d63f41 (Publish helm chart (#81)):Makefile

# Generates an artefact containing the Helm Chart in the distribution directory
>>>>>>> ca4e233a (Add Unit Tests for the chart (#60)):Makefile
build: global-requirements $(DIST_DIR)
	@echo "== Building Chart..."
	@helm package $(CHART_DIR) --destination=$(DIST_DIR)
	@echo "== Building Finished"

# Prepare the Helm repository with the latest packaged charts
deploy: global-requirements $(DIST_DIR) $(HELM_REPO)
	@echo "== Deploying Chart..."
	@rm -rf $(CURDIR)/gh-pages.zip
	@curl -sSLO https://$(PROJECT)/archive/gh-pages.zip
	@unzip -oj $(CURDIR)/gh-pages.zip -d $(HELM_REPO)/
<<<<<<< HEAD:traefik-charts/Makefile
	@cp $(DIST_DIR)/*tgz $(CURDIR)/artifacthub-repo.yml $(HELM_REPO)/
	@cp $(CURDIR)/README.md $(HELM_REPO)/index.md
	@helm repo index --merge $(HELM_REPO)/index.yaml --url https://helm.traefik.io/traefik/ $(HELM_REPO)
=======
	@cp $(DIST_DIR)/*tgz $(HELM_REPO)/
	@helm repo index --merge $(HELM_REPO)/index.yaml --url https://containous.github.io/traefik-helm-chart/ $(HELM_REPO)
>>>>>>> 43d63f41 (Publish helm chart (#81)):Makefile
	@echo "== Deploying Finished"

# Cleanup leftovers and distribution dir
clean:
	@echo "== Cleaning..."
	@rm -rf $(DIST_DIR)
	@rm -rf $(HELM_REPO)
	@echo "== Cleaning Finished"

################################## Technical targets

$(DIST_DIR):
	@mkdir -p $(DIST_DIR)

## This directory is git-ignored for now,
## and should become a worktree on the branch gh-pages in the future
$(HELM_REPO):
	@mkdir -p $(HELM_REPO)

global-requirements:
	@echo "== Checking global requirements..."
ifeq ($(LINT_USE_DOCKER),true)
	@command -v docker >/dev/null || ( echo "ERROR: Docker binary not found. Exiting." && exit 1)
	@docker info >/dev/null || ( echo "ERROR: command "docker info" is in error. Exiting." && exit 1)
else
	@command -v helm >/dev/null || ( echo "ERROR: Helm binary not found. Exiting." && exit 1)
	@command -v git >/dev/null || ( echo "ERROR: git binary not found. Exiting." && exit 1)
	@echo "== Global requirements are met."
endif

lint-requirements: global-requirements
	@echo "== Checking requirements for linting..."
ifeq ($(LINT_USE_DOCKER),true)
	@command -v docker >/dev/null || ( echo "ERROR: Docker binary not found. Exiting." && exit 1)
	@docker info >/dev/null || ( echo "ERROR: command "docker info" is in error. Exiting." && exit 1)
else
	@command -v ct >/dev/null || ( echo "ERROR: ct binary not found. Exiting." && exit 1)
	@command -v yamale >/dev/null || ( echo "ERROR: yamale binary not found. Exiting." && exit 1)
	@command -v yamllint >/dev/null || ( echo "ERROR: yamllint binary not found. Exiting." && exit 1)
	@command -v kubectl >/dev/null || ( echo "ERROR: kubectl binary not found. Exiting." && exit 1)
endif
	@echo "== Requirements for linting are met."

helm-unittest: global-requirements
	@echo "== Checking that plugin helm-unittest is available..."
<<<<<<< HEAD:traefik-charts/Makefile
<<<<<<< HEAD:traefik-charts/Makefile
	@helm plugin list 2>/dev/null | grep unittest >/dev/null || helm plugin install https://github.com/rancher/helm-unittest --debug
=======
	@[ -e $(shell helm home)/plugins/helm-unittest ] || helm plugin install https://github.com/rancher/helm-unittest --version=0.1.6-rancher1
>>>>>>> ca4e233a (Add Unit Tests for the chart (#60)):Makefile
=======
	@helm plugin list 2>/dev/null | grep unittest >/dev/null || helm plugin install https://github.com/rancher/helm-unittest --version=0.1.7-rancher1
>>>>>>> 6b4a9a16 (Migrate to helm v3 (#94)):Makefile
	@echo "== plugin helm-unittest is ready"

.PHONY: all global-requirements lint-requirements helm-unittest lint build deploy clean
