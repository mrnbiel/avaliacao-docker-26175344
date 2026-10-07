# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Gabriel Ferreira Moreno

Matrícula: 26175344

Usuário do GitHub: mrnbiel

Usuário do Docker Hub: gabrielmrnResponda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
Usei a imagem base oficial `nginx:1.27-alpine`.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
conferir que o `index.html` está lá dentro.

O Nginx procura os arquivos em /usr/share/nginx/html. Comando: docker exec teste-portal ls /usr/share/nginx/html

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
gabrielmrn/viaserra-portal:1.0-26175344
https://hub.docker.com/r/gabrielmrn/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
docker build -t gabrielmrn/viaserra-portal:1.0-26175344 ./portal

&#x20;  docker push gabrielmrn/viaserra-portal:1.0-26175344

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

|#|Instrução|O que estava errado|O que você viu acontecer|Como corrigiu|
|-|-|-|-|-|
|1|COPY pagina/ .|A pasta pagina não existia. A página fornecida estava em site/.|O docker build falhou informando que /pagina não foi encontrado.|Alterei para COPY site/ ..|
|2|CMD \["nginx"]|O Nginx era iniciado, mas o processo terminava e o container não permanecia em execução.|O docker ps -a mostrou Exited (0), apesar dos logs mostrarem o Nginx iniciando normalmente.|Alterei para CMD \["nginx", "-g", "daemon off;"].|
|3|WORKDIR /usr/share/nginx|Os arquivos foram copiados para uma pasta diferente da pasta padrão usada pelo Nginx para servir a página.|O container permanecia funcionando, mas o navegador mostrava “Welcome to nginx!” em vez da página de manutenção.|Alterei para WORKDIR /usr/share/nginx/html.|

Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
A opção -p 7042:80 significa que a porta 7042 do computador (host) está ligada à porta 80 do container. Já -p 80:7042 liga a porta 80 do host à porta 7042 do container.



Portanto, no formato -p HOST:CONTAINER, o segundo número é a porta do container.Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
docker run -d --name portal -p 8044:80 gabrielmrn/viaserra-portal:1.0-26175344
docker run -d --name manutencao -p 7044:80 manutencao:26175344
8. Qual comando derruba os dois containers de uma vez?
docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:

```
(VIASERRA-26175344-363E40BF)
```

