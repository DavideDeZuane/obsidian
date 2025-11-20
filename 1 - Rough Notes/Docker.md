





BuildKit è il nuovo backend per fare le build di docker
```zsh 
pacman -S docker-buildx
```

Per abilitare questo tipo di build solo una volta premettere questa variabile d'ambiente davanti al comando :

```bash
DOCKER_BUILDKIT=1 docker build .
```

To use Docker BuildKit by default, edit the Docker daemon configuration in `/etc/docker/daemon.json` as follows, and restart the daemon.

```json
{
  "features": {
    "buildkit": true
  }
}
```

https://docs.docker.com/build/cache/

https://docs.docker.com/build/building/secrets/
https://github.com/moby/buildkit/blob/master/frontend/dockerfile/docs/reference.md



The `ADD` instruction is best for when you need to download a remote artifact as part of your build. `ADD` is better than manually adding files using something like `wget` and `tar`, because it ensures a more precise build cache. `ADD` also has built-in support for checksum validation of the remote resources, and a protocol for parsing branches, tags, and subdirectories from [Git URLs](https://docs.docker.com/reference/cli/docker/buildx/build/#git-repositories).


Se vogliamo fare delle istruzioni docker multilinea abbiamo due opzioni:
- carattere di escape per il new line che si possono specificare tramite le direttive
- utilizzare le heredocs
- 


## Heredocs
Ha la seguente sintassi:

```dockerfile
RUN <<EOF
apt-get update
apt-get install -y curl
EOF
```




## References
- [docker.com](https://www.docker.com/blog/introduction-to-heredocs-in-dockerfiles/)
- 