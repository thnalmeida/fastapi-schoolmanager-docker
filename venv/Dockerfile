#puxar imagem python no Docker Hub - repositorio de imagem Docker
#escolho a imagem confiável, escolhi uma tag alpine, versao mais recente e coloquei aqui: 
FROM python:3.14.0b3-alpine3.22 

# 2. Define o diretório de trabalho dentro do contêiner
# Todos os comandos subsequentes serão executados a partir deste diretório.
WORKDIR /app

# 3. Copia o arquivo de dependências
# Copiamos primeiro o requirements.txt para aproveitar o cache de camadas do Docker.
# Se este arquivo não mudar, o Docker não precisará reinstalar as dependências.
COPY requirements.txt .

# 4. Instala as dependências
# O --no-cache-dir desabilita o cache do pip, reduzindo o tamanho da imagem.
RUN pip install --no-cache-dir -r requirements.txt

# 5. Copia o restante do código da aplicação p/ o diretorio de trabalho
COPY . .

# 6. Expõe a porta que a aplicação fastAPI irá rodar (padrao eh 8000)
EXPOSE 8000

# 7. Define o comando para iniciar a aplicação
# Usamos uvicorn para rodar o app FastAPI. O host 0.0.0.0 é essencial
# para que a aplicação seja acessível de fora do contêiner.
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]