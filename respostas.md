# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Isaque Santos Matos
Matrícula: 26176363
Usuário do GitHub: Isaque-Matos
Usuário do Docker Hub: isaquematos

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
R: Utilizei a imagem nginx:1.27-alpine. O tamanho final foi de 21mb

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.
   R: A pasta é /usr/share/nginx/html/, o comando utilizado para conferir foi: docker exec -it teste-portal ls /usr/share/nginx/html/

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
R: Nome completo da imagem: isaquematos/viaserra-portal:1.0-26176363. Link público: https://hub.docker.com/r/isaquematos/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
R: É preciso rodar de novo o build e o push: 
docker build -t isaquematos/viaserra-portal:1.0-26176363 ./portal
docker push isaquematos/viaserra-portal:1.0-26176363

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 |COPY pagina/ . |A pasta pagina/ não existia no projeto (a pasta real chama-se site/) | O build falhou com erro de "not found" para a pasta pagina/ | Troquei para COPY site/ /usr/share/nginx/html/ (origem correta e destino absoluto) e removi o WORKDIR|
| 2 | CMD ["nginx"] | Sobrescrevia o CMD padrão da imagem, iniciando o Nginx em background | Container saía na hora (Exited) | Removi a linha CMD |
| 3 | Label | Sem LABEL com nome e matrícula | Não quebrava a execução, mas fugia do padrão | Adicionei LABEL autor="Isaque Santos Matos" matricula="26176363"|

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
R: No -p, o formato é sempre host:container. Em -p 7042:80, o 7042 é a porta do host e o 80 é a do container . Em -p 80:7042 seria o contrário

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
R: docker run -d --name portal -p 8063:80 --restart unless-stopped isaquematos/viaserra-portal:1.0-26176363
   docker run -d --name manutencao -p 7063:80 --restart unless-stopped manutencao:26176363

8. Qual comando derruba os dois containers de uma vez?
R: docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:
R: VIASERRA-26176363-25472666
```
(cole aqui)
```
