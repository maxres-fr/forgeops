SHELL := /bin/bash
SHELL_SCRIPTS = $(wildcard **/*.sh)
TS_SCRIPTS = $(shell find cluster/pulumi/{aws,azure,gcp} -name "*.ts")
KUSTOMIZE_YAML = $(shell find kustomize -name "*.yaml")
TSLINT=cluster/pulumi/node_modules/.bin/tslint
.PHONY: $(SHELL_SCRIPTS) $(KUSTOMIZE_YAML) $(TS_SCRIPTS)

$(KUSTOMIZE_YAML):
	-yamllint -f parsable $@

ts:
	-@$(TSLINT) -t verbose -p cluster/pulumi/tsconfig.json

$(SHELL_SCRIPTS):
	-shellcheck -f gcc $@

lint: ts $(SHELL_SCRIPTS) $(KUSTOMIZE_YAML)
	@echo "linted"
