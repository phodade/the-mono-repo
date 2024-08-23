# Variables
SERVICES := api-gateway appointment-service case-service directory-service patient-service
LIBRARY := hospital-console-fxml
REPO := https://github.com/phodade/the-mono-repo.git

# Main target 
default: clone status pull stash build_lib build_services build_images push_images

# Clone all services and the JavaFX library project
clone:
	@echo "Starting to clone services and the JavaFX library project..."
	@for %%s in $(SERVICES) do git clone $(REPO) %%s
	@echo "Cloning the library project..."
	@git clone $(REPO) $(LIBRARY)

# Display the Git status for all projects
status:
	@echo "Checking Git status for each project..."
	@for %%p in $(SERVICES) $(LIBRARY) do ( \
		echo "Status for %%p:" && \
		(cd %%p && git status) \
	)

# Pull the latest changes for all projects
pull:
	@echo "Fetching the latest changes from remote repositories..."
	@for %%p in $(SERVICES) $(LIBRARY) do ( \
		echo "Pulling updates for %%p:" && \
		(cd %%p && git pull) \
	)

# Stash any local changes for all projects
stash:
	@echo "Stashing local changes in all projects..."
	@for %%p in $(SERVICES) $(LIBRARY) do ( \
		echo "Stashing changes for %%p:" && \
		(cd %%p && git stash) \
	)

# Build the JavaFX library project
build_lib:
	@echo "Compiling the JavaFX library project..."
	@(cd $(LIBRARY) && mvn clean install)

# Build all services
build_services:
	@echo "Compiling all service projects..."
	@for %%s in $(SERVICES) do ( \
		echo "Building %%s:" && \
		(cd %%s && mvn clean install) \
	)

# Create Docker images for each service
build_images:
	@echo "Creating Docker images for all services..."
	@for %%s in $(SERVICES) do ( \
		echo "Building Docker image for %%s:" && \
		(cd %%s && docker build -t pratikshahodade123/%%s .) \
	)

# Push the Docker images to the Docker registry
push_images:
	@echo "Uploading Docker images to Docker Hub..."
	@for %%s in $(SERVICES) do ( \
		echo "Pushing Docker image for %%s:" && \
		docker push pratikshahodade123/%%s \
	)
