# Containers com Docker — Do desenvolvimento à produção

**Categoria:** Containers  
**Avaliação pessoal:** ★★★★☆  

---

## Capítulo 1 — Motivação
- Problema: ambientes diferentes entre dev/prod.  
- Docker resolve empacotando tudo em container.  
- Rascunho: tipo VM, mas mais leve.  
**Nota:** começa mostrando por que containers simplificam a vida.

---

## Capítulo 2 — Instalando o Docker
- Instalação no Linux/Windows/Mac.  
- Comandos básicos `docker version`, `docker info`.  
- Observação: sempre conferir daemon rodando.  
**Nota:** só setup inicial.

---

## Capítulo 3 — Primeiros comandos
- `docker run hello-world` → sanity check.  
- `docker ps`, `docker images`.  
- Diferença entre rodar e listar containers.  
**Nota:** entender ciclo de vida básico.

---

## Capítulo 4 — Imagens
- Imagem = blueprint.  
- `docker pull`, `docker build`.  
- Dockerfile: define como construir imagem.  
- Exemplo simples: `FROM ubuntu`.  
**Nota:** imagens são só camadas.

---

## Capítulo 5 — Containers
- Instâncias de imagens.  
- `docker run -it ubuntu bash` → entra no shell.  
- Start/stop/remove containers.  
**Nota:** container = processo isolado.

---

## Capítulo 6 — Volumes
- Persistência de dados.  
- `-v` para mapear diretórios.  
- Volumes nomeados vs bind mounts.  
**Nota:** sem volumes, tudo some quando container morre.

---

## Capítulo 7 — Redes
- Containers podem falar entre si.  
- `docker network create` → redes customizadas.  
- Bridge é padrão.  
**Nota:** importante em apps distribuídas.

---

## Capítulo 8 — Docker Compose
- Orquestração simples.  
- `docker-compose.yml` para definir múltiplos serviços.  
- Exemplo: web + banco.  
**Nota:** facilita muito no dev.

---

## Capítulo 9 — Imagens no Docker Hub
- Push de imagens customizadas.  
- Criar conta, `docker login`, `docker push`.  
- Importante para compartilhar.  
**Nota:** pensar em versionar imagens.

---

## Capítulo 10 — Deploy em produção
- Boas práticas: logs, monitoramento, segurança.  
- Diferença de usar direto vs orquestradores (K8s, Swarm).  
**Nota:** livro foca em fundamentos, mas já dá um gostinho.

---

# Exemplos rápidos de comandos

### Rodar container simples
```bash
docker run -it ubuntu bash
```

### Criar Dockerfile mínimo
```dockerfile
FROM python:3.9-slim
COPY app.py /app.py
CMD ["python", "app.py"]
```

### Subir stack com Compose
```yaml
version: "3"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  db:
    image: postgres:13
```

### Persistência com volumes
```bash
docker run -d -v /meus_dados:/dados alpine
```

### Criar rede e conectar containers
```bash
docker network create minha-rede
docker run -d --name c1 --network minha-rede alpine sleep 1000
docker run -it --rm --network minha-rede alpine ping c1
```
