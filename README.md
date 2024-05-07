# Tutorial-Microserviços

## Recursos 

- [PT] Poetry #1: [Link](https://www.youtube.com/watch?v=ZOSWdktsKf0)
- [PT] Poetry #2: [Link](https://www.youtube.com/watch?v=uXQv2cciCeI)
- [PT] FastAPI: [Link](https://www.youtube.com/watch?v=MxlS5_MI_WY)
- [EN] FastAPI + Docker #1: [Link](https://www.youtube.com/watch?v=zkMRWDQV4Tg)
- [EN] FastAPI + Docker #2: [Link](https://www.youtube.com/watch?v=0H2miBK_gAk)
- [EN] Docker #1: [Link](https://www.youtube.com/watch?v=rIrNIzy6U_g)
- [EN] Docker #2: [Link](https://www.youtube.com/watch?v=eGz9DS-aIeY)
- [EN] Docker Compose: [Link](https://www.youtube.com/watch?v=DM65_JyGxCo)

## Configuração Inicial

Considerando que o Python e o Docker Compose já estão instalados no minha máquina há muito tempo (segui as documentações oficiais):

No Windows, instalei o Poetry:
```bash
$ pip install poetry
```

Abri dois terminais e ativei o ambiente virtual:
```bash
$ poetry shell
```

Instalei também o Uvicorn e o FastAPI:
```bash
$ pip install uvicorn 
$ pip install fastapi
```

## Execução dos Microserviços

Executei os comandos em cada terminal para iniciar os microserviços:
```bash
$ uvicorn microservice1:app --host 0.0.0.0 --port 8001 --workers 2
$ uvicorn microservice2:app --host 0.0.0.0 --port 8002 --workers 2
```

## Alterações nos Arquivos

Antes de iniciar os microserviços, fiz algumas alterações nos arquivos `microservice1.py` e `microservice2.py`:

### microservice1.py:
```python
# Importing FastAPI resources
from fastapi import FastAPI

# Defining the FastAPI app
app = FastAPI()

@app.get("/")
async def main() -> str:
    """Base microservice 1 endpoint."""
    return "Olá, eu sou o microserviço 1!"
```

### microservice2.py:
```python
# Importing FastAPI resources
from fastapi import FastAPI

# Defining the FastAPI app
app = FastAPI()

@app.get("/")
async def main() -> str:
    """Base microservice 2 endpoint."""
    return "Olá, eu sou o microserviço 2!"
```

## Teste da Solicitação HTTP GET

Executei a solicitação HTTP GET adaptada:
```bash
$ curl "http://localhost:8001/"
```
Também testei no navegador [http://localhost:8001/](http://localhost:8001/) e obtive a resposta "Olá, eu sou o microserviço 1!".

## Docker

Já que tenho o Docker instalado no meu computador e a extensão do VSCode, iniciei e segui o tutorial do projeto.

### Criação da Imagem Docker

```bash
docker build -f Dockerfile_microservice1 -t fastapi_microservice1:latest .
docker build -f Dockerfile_microservice2 -t fastapi_microservice2:latest .
```

### Deploy

```bash
docker-compose -f docker-compose.yml up --build --remove-orphans
```

## Inicialização

Inicializei a aplicação:
```bash
curl http://localhost:8001/
```
