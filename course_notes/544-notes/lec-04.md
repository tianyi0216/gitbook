# Lec 04

docker COMMAND

1. pull: pull a image from registeries to # docker pull ubuntu:23.10&#x20;
2. images: lookup current images. # docker images
3. tag: change tag. Can have different tag for same image.
4. run: start a new container and execute the command. #docker run unbuntu echo hello.#automatically pull as well
5. ps: - list all containers. #ps -a all containers not cleaned up.  #docker ps -ap quiet.
6. rm : remove container. #dovker rm name/id #docker rm use \` surround command.
7. rmi: remove images.&#x20;
8. system df: # docker system df - show docker disk usage
9. system prune: clean up.
10. logs: see what is printing out. #docker logs container name. #-f watch
11. exec: starts a new program in a existing container.  #docker exec -it mystifying\_bajai bash
12. stats: show resouces for each container.
13. kill: kill a container - stop running (not remove) docker kill container
14. build: #docker build . -t demo2 (t for tag) - build a iamge

Dockerfile INSTRUCTIONS&#x20;

15\. FROM:  -base image. #FROM unbuntu:23.10

16\. RUN:  - command. #RUN apt-get update. RUN apt-get install unzip. (apt-get for scripts, )

put in same lne, RUN command && command."add -y, apt-get install -y".

17\. COPY:  #COPY frommycomputer tocontainer. (relative path, /path/file)

18\. CMD: execute command \["list of command"]



Docker can help with set up environment for deployment.&#x20;

Can help with resource, resource limit etc.

Images: snapshot of installed software from which to create a container.

Registeries. pull image from registeries

Image -> containers.

e.g for detached

docker run -d ubuntu sh -c "echo hello; sleep 300; echo bye" (-d run in backgrond)

