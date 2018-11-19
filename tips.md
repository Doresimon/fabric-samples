# tips

## docker

when docker daemon starting, it will give permission 
to a user group called 'docker'. 

// create user group
> sudo groupadd docker

// add current user to docker group
> sudo usermod -aG docker $USER

// restart
> sudo systemctl restart docker

// refresh info
> newgrp docker

## shell

> xxx 2>>&1 | tee xxx.output
> xxx |& tee -a xxx.output.log