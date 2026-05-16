# 📂 Laboratório: Servidor Web Nginx

Este diretório contém os arquivos necessários para rodar seu primeiro container.

## 📝 Arquivos neste diretório
* `docker-compose.yml`: Configuração da infraestrutura.
* `index.html`: Página que será exibida pelo servidor.

## 🚀 Como Executar
1. Abra o terminal nesta pasta.
2. Execute o comando:
   ```bash
   docker compose up -d
   ```
3. Acesse `http://localhost:8080` .
   
4. Para parar o serviço, basta executar:
   ```bash
   docker compose down
   ``` 

---
   # 🔬 Dissecando o arquivo `docker-compose.yml`

Para entender como o Docker interpreta as nossas instruções, vamos analisar cada parte do arquivo configurado:

### 🛠️ Serviços (`services`)
Aqui definimos quais containers farão parte do nosso projeto. No nosso caso, temos o `meu-servidor`.

* **`image: nginx:alpine`**: 
  * É a base do nosso container. Estamos usando a versão `alpine` do Nginx, que é uma imagem extremamente leve, ideal para performance e segurança.
  
* **`container_name: aula-nginx`**: 
  * Define um nome fixo para o container. Isso facilita a gestão via terminal (ex: `docker stop aula-nginx`) em vez de deixar o Docker gerar um nome aleatório.

### 🔌 Portas (`ports`)
É a ponte entre o seu computador e o mundo isolado do Docker.
* **`"8080:80"`**: 
  * Segue a regra **[Porta do seu Dispositivo] : [Porta dentro do Container]**.
  * O Nginx escuta internamente na porta 80. Nós mapeamos para a 8080 do seu PC para evitar conflitos com outros serviços que você possa ter rodando.

### 📂 Volumes (`volumes`)
Este é o conceito de **Persistência de Dados**.
* **`./index.html:/usr/share/nginx/html/index.html`**:
  * Aqui fazemos um **Bind Mount**. Estamos dizendo ao Docker: "Pegue o arquivo `index.html` que está nesta pasta e coloque-o exatamente onde o Nginx espera encontrar o site".
  * **Vantagem:** Você pode editar o arquivo HTML e o site atualiza instantaneamente sem precisar reiniciar o container.

---
[⬅️ Voltar para o Início](../README.md)
