# barbatos-tookit
Collection of notes and scripts from the internet rabbit holes.


## Quick Ref

### Quick python instance
#### Don't care about what is installed? 
```bash
# Download image and run container
docker run -it -d --rm --name temp-container --mount type=bind,source="$(pwd)",target=/code -w /code --entrypoint /bin/bash python

# Connect to the container
docker exec -it temp-container bash

# Install iPython
python -m pip install ipython
```
#### Want to set up some aliases and install packages? Use the Dockerfile example instead
Create a Dockerfile, in this example we're calling it `python_config`
```Dockerfile
FROM python:3 # Installs the latest should be debian image at this time also don't include this comment
WORKDIR /code
RUN echo 'alias ll="ls -lart --color=auto"' >> ~/.bashrc

RUN python -m pip install ipython
RUN pip install --upgrade pip

ENTRYPOINT ["tail", "-f", "/dev/null"]
```

```bash
# Build the container from the image specified in the Dockerfile
docker build -f /path/to/python_config -t temp-image . 

# Start the container
docker run -it --rm -d --name python_container --mount type=bind,source="$(pwd)",target=/code temp-image

# Connect to the container that is running
docker exec -it python_container /bin/bash

# Kill container
docker ps
docker stop python_container
```
> The `--rm` will make sure the clean up the container when you stop it so it will leave your disk dirty. But the tag will still exits you can see it with `docker images`. So to spin it back up you just need the run line again
> `-t` isn't really needed, but it'll be easier to see which is the image you downloaded from `docker images` with a unique tag that you give it so that you know where it came from

## Convert exception to string
```python
exc = ''.join(traceback.format_exception(type(error), error, error.__traceback__, chain=True))
```



## Structure
---
### Systems
> Notes pertaining to a particular system that can come in handy for CTF's
```
OS 
|
--> scripts
--> notes
```
---
### Class
> Any vendor classes like NET+, SEC+ etc. 
---
### Cybernetic
> Everything else from how-to's to note to self
#### environment
> Notes pertaining to setting up an environment or service

#### stack
> Notes pertaining to some tool or "how-to"
---