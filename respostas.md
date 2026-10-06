# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Murilo Demarco 
Matrícula: 26175138
Usuário do GitHub: murilodemarco
Usuário do Docker Hub: murilodemarco

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)? 
279 MB conforme a saída de docker images.
2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
conferir que o `index.html` está lá dentro.

&#x20;   /usr/share/nginx/html/



## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
murilodemarco/viaserra-portal:1.0-26175138
https://hub.docker.com/r/murilodemarco/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
Se eu mudar o HTML, preciso reconstruir a imagem e enviá-la novamente para o Docker Hub. Os comandos são:
docker build -t murilodemarco/viaserra-portal:1.0-26175138 ./portal
docker push murilodemarco/viaserra-portal:1.0-26175138

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

|#|Instrução|O que estava errado|O que você viu acontecer|Como corrigiu|

|1|COPY pagina/ .|A pasta pagina/ não existia no contexto de build; a página estava em site/.|O docker build falhou com o erro "/pagina": not found.|Alterei para COPY site/ . inicialmente e depois para o diretório correto do Nginx.|
|2|Inicialização do Nginx|O Nginx era iniciado sem permanecer em primeiro plano.|O container iniciava, mas aparecia como Exited (0) no docker ps -a.|Adicionei CMD ["nginx", "-g", "daemon off;"].|
|3|COPY site/ .|Os arquivos eram copiados para /usr/share/nginx, mas o Nginx serve os arquivos de /usr/share/nginx/html/.|O container ficava Up, mas o navegador mostrava Welcome to nginx!.|Alterei para COPY site/ /usr/share/nginx/html/.|

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
No comando -p 7042:80, o número 7042 é a porta do host (computador) e 80 é a porta do container. Assim, acessando localhost:7042, o Docker encaminha a conexão para a porta 80 do container.

No comando -p 80:7042, o número 80 é a porta do host e 7042 é a porta do container. Portanto, a porta do container é sempre o segundo número no formato -p PORTA_HOST:PORTA_CONTAINER.

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
docker run -d --name portal -p 8038:80 murilodemarco/viaserra-portal:1.0-26175138
docker run -d --name manutencao -p 7038:80 avaliacao-docker-viaserra-manutencao

8. Qual comando derruba os dois containers de uma vez?
docker compose down


## Verificador

9. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```

