## Comandos que eu usei que vi na aula e meu entendimento de cada coisa

```bash
# -i (interativo) -t (tty)
$ docker run -it ubuntu /bin/bash

# -f nome do dockerfile (pode ser omitido caso o nome seja Dockerfile)
$ docker build -t conversao-distancia -f Dockerfile .

# -p <externo>:<interno>
$ docker run -d -p 5000:5000 conversao-distancia

# tag (Cria uma copia da imagem com nome diferente, interessante que mantem o msm ID)
$ docker tag conversao-distancia deividoliver/conversao-distancia:v1

# existe uma nomeclatura para poder fazer o upload da imagem no dockerhub
$ docker push deividoliver/conversao-distancia:v1

# -qa lista somente os ids dos container
$ docker container rm $(docker container ls -qa)
```
