# Dockerized PHP/Nginx for Zeit

A test repo to run Nginx/PHP on zeit.co.

## Build It:

```bash
docker build zeit:latest .
```

## Run it:

We can run it and see it in our browser at `localhost`.

> You'll get an error if you have something listening on port 80 already. Use an alternative port in that case - `-p 8888:80`

```bash
mkdir public
echo "<?php phpinfo();" > public/index.php

# Note we expect directory "public"
# to be in our current working directory
docker run -dit --rm \
    --name=myphp
    -v $(pwd):/var/www/html -p 80:80 zeit 
```

We can also run one-off commands

```bash
# Make a new container and creat a one-off command
# In which case, we set the current working directory
docker run -dit --rm \
    -v $(pwd):/var/www/html
    -w /var/www/html \
    zeit composer update
```

Or run a command from within an already-running container

```bash
# Assume container is named "myphp"
docker exec -it myphp sh -c "cd /var/www/html && composer update"
```
