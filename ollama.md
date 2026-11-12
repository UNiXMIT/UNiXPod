# Ollama
### Pull and Run container
```
podman pull ollama/ollama
podman run -d -v /home/support/ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Run model
Non-Interactive:  
```
podman exec ollama ollama run llama3
```
Interactive:
```
podman exec -it ollama ollama run llama3
```
More Ollama Models - https://ollama.com/library  

### Remove your container
```
podman stop ollama
podman rm ollama
```

### Source
https://hub.docker.com/r/ollama/ollama
https://github.com/ollama/ollama