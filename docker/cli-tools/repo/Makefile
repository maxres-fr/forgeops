SHELL := /bin/bash
SHELL_SCRIPTS = $(wildcard **/*.sh)
TS_SCRIPTS = $(shell find cluster/pulumi/{aws,azure,gcp} -name "*.ts")
KUSTOMIZE_YAML = $(shell find kustomize -name "*.yaml")
TSLINT=tslint
COMMITSTAR=/usr/local/bin/commitsar
LAST_TAG=$(python docker/cli-tools/repo/src/forgeops/forgeops.py prior-tag)
CURRENT_TAG=
.PHONY: $(SHELL_SCRIPTS) $(KUSTOMIZE_YAML) $(TS_SCRIPTS)

$(KUSTOMIZE_YAML):
	-yamllint -f parsable $@

ts:
	-@$(TSLINT) -t verbose -p cluster/pulumi/tsconfig.json
	@echo "linted ts"

$(SHELL_SCRIPTS):
	-shellcheck -f gcc $@

yaml: $(KUSTOMIZE_YAML)
	@echo "linted yaml"

sh: $(SHELL_SCRIPTS)
	@echo "linted shell scripts"

lint: ts yaml sh
	@echo "linted"

commit:
	$(COMMITSTAR)


changelog.md:
	@gitchangelog "$(shell forgeops prior-tag)..$(shell forgeops current-tag)" > changelog.md

release: changelog.md
	forgeops create-release changelog.md

