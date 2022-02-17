# Kubedev - Desafio Docker - Questão 03

## Aplicação escrita em C# utilizando ASP.NET Core

Dockerfile

```bash
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app
 
# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore
 
# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o out
 
# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]
```

.dockerignore

```bash
bin/
obj/
```
 
Processo de construção da imagem com Dockerfile

```bash
docker image build -t edemirtoldo/conversao-peso:v1 .
```
Enviar a imagem v1 para o Docker Hub.

```bash
docker push edemirtoldo/conversao-peso:v1
```

Vamos fazer um TAG da imagem.

```bash
docker tag edemirtoldo/conversao-peso:v1 edemirtoldo/conversao-peso:latest
```

Enviar a imagem latest para o Docker Hub.

```bash
docker push edemirtoldo/conversao-peso:latest
```

Executar a aplicação NodeJS em container.

```bash
docker container run -d -p 8080:80 --name conversao-peso edemirtoldo/conversao-peso:v1
```

Link de acesso a aplicação de conversão de peso <http://localhost:8080/>

Aplicação Conversão de Peso em C# utilizando ASP.NET Core

![asp.net](https://github.com/edemirtoldo/conversao-temperatura/blob/main/img/conversaotemperatura.png)
