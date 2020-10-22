# dockerfile

```bash
docker build -f dockerfile_custom_name
```

File contains the recipte to cook the images, which are usually based on the root images - pure system.
The lightest one is Alpine.
The main reason of existance of this approach - package managers.

FROM    - root image
ENV     - set env vars
RUN     - shell command execution
EXPOSE  - open ports inside from container
CMD     - the command will be executed every time container is run or stopped.

WORKDIR     - prefer to cd ../some_path
COPY        - prefer to coping file via shell

System logging services are usually not included as docker may do logging.

```bash
docker image build -t customngnix .
```

Each line of dockerfile is "executed" and cached - id is attached, so if command was not changed, the next build skips it.
This is a point not to make make-all command.
The points of changes are placed at the bottom.

