# Questionnaire for Lab 2

## 2.1 Getting started

> **Q1:** Why you run the container docker/getting started in detached mode?  
> **A:** 
>> Running the container in detached mode allows it to run in the background, freeing up the
> terminal for other tasks while the container continues to operate.

> **Q2:** What is the difference between a container and a container image?  
> **A:** 
>> A container image is a lightweight, standalone, and executable package 
> that includes everything needed to run a piece of software, including the code, runtime,
> libraries, and dependencies.  
>> A container, on the other hand, is a running instance
> of a container image. It is the actual execution environment created from the image.

## 2.1.2 Sample application

> **Q1:** What is the meaning of the docker's directives used in the docker file?
> Please comment on each of the directives  
> **A:**
> - FROM: Specifies the base image for the Docker image. example used here are eclipse-temurin:17-jdk
> - VOLUME: Creates a mount point with the specified path and marks it as holding externally mounted
> volumes from native host or other containers.
> - COPY: Copies files from the host machine to the container's filesystem.
> - ENTRYPOINT: Sets the command that will be executed when the container starts.
> - EXPOSE: Informs Docker that the container listens on the specified network ports at runtime.

> **Q2:** Why it is important to tag a container image?  
> **A:**  
> Tagging a container image is important because it allows you to version control your images versions.
> it gives flexibility to manage different versions of the same application, making it easier to deploy,
> roll back to previous versions, and maintain consistency across different environments.

> **Q3:** Why we should bind a host port with the container port?  
> **A:**  
> Binding a host port to a container port is essential for enabling communication between the host machine
> and the containerized application. It allows external clients to access the services running inside

## 2.1.3 Update the application

> **Q1:** It is possible to bind two containers on the same host port?  
> **A:**  
> No, it is not possible to bind two containers to the same host port on the same, as the host port 
> must be unique to avoid conflicts.

> **Q2:** Why, after stopping a container, you need to remove it?  
> **A:**  
> Stopping a container halts its execution, but the container's resources 
> (like its filesystem and network settings) remain allocated.  
> Removing the container frees up these resources, allowing for better resource management and
> preventing potential conflicts with future containers.

> **Q3:** It is possible to remove a running container, without stopping it before the removal?  
> **A:**  
> No, it is not possible to remove a running container without stopping it first.    
> The container must be stopped to ensure that all processes are terminated and resources are released properly before removal.

## 2.1.4 Share the application

> **Q1:** Given a container image available on a docker image repository,
> can you start an instance of the image on any docker host? Is there any limitation?  
>  **A:**  
> Yes, one can start an instance of a container image available on a Docker image repository on 
> any Docker host, provided that the host has access to the repository and the necessary 
> permissions to pull the image.  
> Limitations may include network restrictions, authentication requirements, and compatibility
> issues with the host's operating system or architecture.

## 2.1.5 Persist the DB

> **Q1:** If you run two instances of the same container image, let's call them container A and container B,
> and you create a file in container A, is that new file visible in container B?  
> **A:**  
> No, if you run two instances of the same container image (container A and container B),
> a file created in container A will not be visible in container B. Each container has its own
> isolated filesystem, so changes made in one container do not affect another container.

> **Q2:** What you can do with the "docker,exec" command?
> **A:**  
> The "docker exec" command allows you to shell into a running container and execute commands
> within that container's environment. This is useful for debugging, inspecting the container's state,
> or performing administrative tasks without needing to stop or restart the container.

> **Q3:** Let assume you need to use a volume. Why you need to mount the volume in the container file system?
> Does that mean you modify the container file system?
> **A:**
> Mounting a volume in the container file system allows the container to access and use data stored
> outside of its own isolated filesystem. This is essential for persisting data, sharing data between
> containers, or for example accessing common configuration files.  
> Mounting a volume does not modify the container's filesystem itself; instead, it provides
> a way to access external data while keeping the container's internal filesystem undisturbed.

> **Q4:** In this part of the tutorial, you have created a volume. Where is the volume located in the file system of your docker host?
> **A:**  
> The location of Docker volumes on the host filesystem can vary depending on the operating system
> and Docker's configuration.  
> On Linux, Docker volumes are typically stored in the `/var/lib/docker/volumes/` directory.  
> On Windows and macOS, Docker uses a virtual machine to manage containers, so the volume data is stored within that VM's filesystem.
> In my docker host, the volume is configured to /tmp where I have mounted it.

## 2.1.6 Use bind mounts

> **Q1:** What is a development container?
> **A:**
>  A development container is a Docker container specifically configured to provide a consistent
> development environment. It typically includes all the necessary tools, libraries, and dependencies
> required for software development, allowing developers to work in an isolated and reproducible
> environment regardless of the host system.
> Examples:
> -  A container with pre-installed Mysql database for development purpose.
> -  A container with pre-installed JDK and Maven for Java application development.
> -  A container with pre-setup of configuration files and source code for a web application.
> -  A container that is mounted to the application source code on the host machine to enable live code editing and testing.

> **Q2:** When you are in development mode, do you need to rebuild the container each time
> you update the app to see the changes? Why?  
> **A:**  
> No, when in development mode, you typically do not need to rebuild the container each time you update
> the app. This is because development containers often use bind mounts to link the source code
> directory on the host machine to the container. This allows changes made to the source code on
> the host to be immediately reflected inside the container, enabling rapid development and testing without
> the overhead of rebuilding the container.

## 2.1.7 Multi container app & Docker Compose

> **Q1:** What is a Docker service?  
> **A:**  
> A Docker service is a higher-level abstraction in Docker that allows you to define and manage
> multi-container applications. It is typically defined in a Docker Compose file, where you can specify
> multiple services (containers), their configurations, networks, and volumes.  
> Docker services enable easier orchestration, scaling, and management of related containers as a single unit.

> **Q2:** Can we spin up a single instance of a docker container using a docker-compose file?  
> **A:**  
> Yes, we can spin up a single instance of a Docker container using a Docker Compose file by defining a service
> with a single replica. Docker Compose allows you to define multiple services, but you can also
> define just one service if needed.

> **Q3:** Can we run a MySQL container and store the database structure and data in a volume?  
> **A:**  
> Yes, we can run a MySQL container and store the database structure and data in a volume.  
> By defining a volume in the Docker Compose file and mounting it to the appropriate directory inside the MySQL container
> (typically `/var/lib/mysql`), we can ensure that the database data persists even if the container is stopped or removed.

> **Q4** Is the order of the services defined in a docker-compose file important, or it is irrelevant which
> service is defined first?  
> **A:**  
> The order of services defined in a Docker Compose file is generally irrelevant. Docker Compose will start all services
> defined in the file, regardless of their order. However, if there are dependencies between services (e.g., one service
> depends on another to be fully operational), you may need to manage the startup order using the `depends_on` option to ensure that
> services are started in the correct sequence.

> **Q5:** Is it mandatory to define the network in a docker-compose file?  
> **A:**  
> No, it is not mandatory to define the network in a Docker Compose file.  
> If no network is defined, Docker Compose will automatically create a default network for the services to communicate with each other.  
> However, defining custom networks can be useful for better control over network configurations, isolation, and communication between services.

> **Q6:** If you would like to run a multi-container app, is it necessary to use docker compose 
> (i.e. to define a service) or you can achieve the same objective using docker commands from the shell?
> Does a service offers more than just running a multiple container app with a single command?  
> **A:**  
> While it is possible to run a multi-container app using individual Docker commands from the shell,
> using Docker Compose is generally more efficient and convenient.  
> Docker Compose allows you to define all services, networks, and volumes in a single YAML file,
> making it easier to manage and deploy multi-container applications.  
> Additionally, Docker Compose provides features such as scaling services, managing dependencies,
> and simplifying the startup and shutdown process with single commands (`docker-compose up` and `docker-compose down`).