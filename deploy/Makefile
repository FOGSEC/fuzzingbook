# Makefile to simplify some local Docker steps

BRANCH:=$(git rev-parse --abbrev-ref HEAD)

build:
	docker build --build-arg branch=$(BRANCH) -t 'fuzzing-book' fuzzingbook-dockerenv

build-publish:
	docker build --build-arg publish=yes --build-arg branch=$(BRANCH) -t 'fuzzing-book' fuzzingbook-dockerenv

# This runs the docker image in a *temporary* container
run-tmp:
	@echo "Starting temporary local docker container..."
	-docker run --rm -d -p 8888:8888 -p 8000:8000 --name fuzzing-book-instance fuzzing-book
	sleep 2
	docker exec -it fuzzing-book-instance jupyter notebook list | grep http
	@echo "Container is running, press CTRL+C to stop and remove container..."
	docker attach fuzzing-book-instance

# Spawn a shell in the running docker container for debugging
shell:
	docker exec -it fuzzing-book-instance bash
