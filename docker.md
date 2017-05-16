	
# DOCKER

- docker client
- docker daemon
- docker image
- docker container
- docker engine
- docker machine

### docker search <image name>

### docker pull <image name>

### docker images
	menampilkan list images

### docker run <image name>
	membuat sekaligus menjalankan container dari image
	
	docker run -it debian /bin/bash
	The -i means "run interactively", and -t means "allocate a pseudo-tty".

	docker run -it ubuntu /bin/bash
	docker run -d --name redisFixed -p 6379:6379 redis:latest

### docker ps
	menampilkan list running container
	-a : menampilkan list all container

### docker start <container id>
	bisa menggunakan container id / container name

### docker inspect <container>
	provides more details about a running container, such as IP address, volumes mounted and their locations and its current execution state.

### docker logs <container>
	will display messages the container has written to standard error or standard out.

### docker attach <container id>

### docker restart <container id>

### docker stop <container id>
	menghentikan running container
	
### docker kill <container id>
	menghentikan running container
	


### Dockerfile
FROM debian:latest
RUN apt-get -y update && apt-get install -y cowsay
CMD ["/usr/games/cowsay", "-d", "hae"]

	RUN 
	untuk menjalankan command ketika proses build
	boleh ada banyak perintah RUN di Dockerfile

	CMD 
	default command yang dijalankan ketika container start
	hanya bisa 1 perintah CMD di Dockerfile
	perintah CMD akan di abaikan jika action `docker run` disertai dengan command

### docker build -t <name> .
build image

### docker run -it www
menjalankan container pertamakali
 _____
< hae >
 -----
        \   ^__^
         \  (xx)\_______
            (__)\       )\/\
             U  ||----w |
                ||     ||

### docker start -i a5f29232422a
menjalankan container lagi



### HELPS

sudo docker
Usage: docker [OPTIONS] COMMAND [arg...]

A self-sufficient runtime for linux containers.

Options:
  --api-cors-header=                   Set CORS headers in the remote API
  -b, --bridge=                        Attach containers to a network bridge
  --bip=                               Specify network bridge IP
  -D, --debug=false                    Enable debug mode
  -d, --daemon=false                   Enable daemon mode
  --default-ulimit=[]                  Set default ulimits for containers
  --dns=[]                             DNS server to use
  --dns-search=[]                      DNS search domains to use
  -e, --exec-driver=native             Exec driver to use
  --fixed-cidr=                        IPv4 subnet for fixed IPs
  --fixed-cidr-v6=                     IPv6 subnet for fixed IPs
  -G, --group=docker                   Group for the unix socket
  -g, --graph=/var/lib/docker          Root of the Docker runtime
  -H, --host=[]                        Daemon socket(s) to connect to
  -h, --help=false                     Print usage
  --icc=true                           Enable inter-container communication
  --insecure-registry=[]               Enable insecure registry communication
  --ip=0.0.0.0                         Default IP when binding container ports
  --ip-forward=true                    Enable net.ipv4.ip_forward
  --ip-masq=true                       Enable IP masquerading
  --iptables=true                      Enable addition of iptables rules
  --ipv6=false                         Enable IPv6 networking
  -l, --log-level=info                 Set the logging level
  --label=[]                           Set key=value labels to the daemon
  --log-driver=json-file               Containers logging driver
  --mtu=0                              Set the containers network MTU
  -p, --pidfile=/var/run/docker.pid    Path to use for daemon PID file
  --registry-mirror=[]                 Preferred Docker registry mirror
  -s, --storage-driver=                Storage driver to use
  --selinux-enabled=false              Enable selinux support
  --storage-opt=[]                     Set storage driver options
  --tls=false                          Use TLS; implied by --tlsverify
  --tlscacert=~/.docker/ca.pem         Trust certs signed only by this CA
  --tlscert=~/.docker/cert.pem         Path to TLS certificate file
  --tlskey=~/.docker/key.pem           Path to TLS key file
  --tlsverify=false                    Use TLS and verify the remote
  -v, --version=false                  Print version information and quit

Commands:
    attach    Attach to a running container
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    cp        Copy files/folders from a container's filesystem to the host path
    create    Create a new container
    diff      Inspect changes on a container's filesystem
    events    Get real time events from the server
    exec      Run a command in a running container
    export    Stream the contents of a container as a tar archive
    history   Show the history of an image
    images    List images
    import    Create a new filesystem image from the contents of a tarball
    info      Display system-wide information
    inspect   Return low-level information on a container or image
    kill      Kill a running container
    load      Load an image from a tar archive
    login     Register or log in to a Docker registry server
    logout    Log out from a Docker registry server
    logs      Fetch the logs of a container
    port      Lookup the public-facing port that is NAT-ed to PRIVATE_PORT
    pause     Pause all processes within a container
    ps        List containers
    pull      Pull an image or a repository from a Docker registry server
    push      Push an image or a repository to a Docker registry server
    rename    Rename an existing container
    restart   Restart a running container
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    save      Save an image to a tar archive
    search    Search for an image on the Docker Hub
    start     Start a stopped container
    stats     Display a stream of a containers' resource usage statistics
    stop      Stop a running container
    tag       Tag an image into a repository
    top       Lookup the running processes of a container
    unpause   Unpause a paused container
    version   Show the Docker version information
    wait      Block until a container stops, then print its exit code

Run 'docker COMMAND --help' for more information on a command.


RUN vs CMD vs ENTRYPOINT

RUN is an image build step, the state of the container after a RUN command will be committed to the docker image. A Dockerfile can have many RUN steps that layer on top of one another to build the image.
CMD is the command the container executes by default when you launch the built image. A Dockerfile can only have one CMD. The CMD can be overridden when starting a container with docker run $image $other_command.
ENTRYPOINT is also closely related to CMD and can modify the way a container starts the image.
