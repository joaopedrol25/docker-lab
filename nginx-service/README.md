# Servidor Web Nginx

Este diretório contém os arquivos necessários para rodar seu primeiro container: um servidor web simples usando o **Nginx**.

## 📝 Arquivos neste diretório
* `docker-compose.yml`: Configuração do serviço, portas e volumes.
* `index.html`: Página que será exibida pelo servidor.

---

## Como Executar

1. Certifique-se de estar dentro da pasta `nginx-service`.
2. Suba o container com o comando:
   ```bash
   docker compose up -d
   ```
3. Acesse o servidor no seu navegador em:
   ```
   http://localhost:8080
   ```
4. Para parar o container, execute:
   ```bash
   docker compose down
   ```

> **Dica:** Experimente editar o arquivo `index.html` enquanto o container está rodando e recarregue a página no navegador. As alterações aparecem **instantaneamente**, sem precisar reiniciar nada — isso é o poder dos volumes!

---

# Entendendo o arquivo `docker-compose.yml`

Para entender como o Docker interpreta as nossas instruções, vamos analisar cada parte do arquivo configurado:

### `services`

Aqui definimos quais containers farão parte do nosso projeto. No nosso caso, temos o `meu-servidor`.

* **`image: nginx:alpine`**:
  * É a base do nosso container. Estamos usando a versão `alpine` do Nginx, que é uma imagem extremamente leve, ideal para performance e segurança.
  * Essa imagem é baixada automaticamente do **Docker Hub** na primeira vez que você executa o `docker compose up`.

* **`container_name: aula-nginx`**:
  * Define um nome fixo para o container. Isso facilita a gestão via terminal (ex: `docker stop aula-nginx`) em vez de deixar o Docker gerar um nome aleatório.

---

### `ports`

É a ponte entre o seu computador e o mundo isolado do Docker. A regra é sempre: **`[Porta do seu Dispositivo]:[Porta dentro do Container]`**.

| Mapeamento | Protocolo | Função |
| :--- | :---: | :--- |
| `8080:80` | TCP | O Nginx escuta internamente na porta **80**. Mapeamos para a **8080** do host para evitar conflitos com outros serviços que você possa ter rodando. |

> **Por que a porta 80 está ocupada?** É comum que outros servidores web já estejam usando a porta 80 no seu sistema. Usar a 8080 externamente é uma prática padrão em ambientes de desenvolvimento.

---

### `volumes`

Este é o conceito de **Persistência de Dados**. Por padrão, tudo dentro de um container é efêmero — ao remover o container, todos os arquivos são perdidos. Os volumes resolvem isso ao criar uma ligação direta entre uma pasta do seu computador e uma pasta dentro do container.

* **`./index.html:/usr/share/nginx/html/index.html`**:
  * Aqui fazemos um **Bind Mount**. Estamos dizendo ao Docker: "Pegue o arquivo `index.html` que está nesta pasta e coloque-o exatamente onde o Nginx espera encontrar o site".
  * A regra segue o padrão **`[Caminho no seu Host]:[Caminho dentro do Container]`**.
  * **Vantagem:** Você pode editar o arquivo HTML e o site atualiza instantaneamente, sem precisar reiniciar o container.

> **Por que isso importa?** Graças aos volumes, o seu arquivo `index.html` existe no **seu computador**, não dentro do container. O Docker apenas o "espelha" para dentro. Se você deletar e recriar o container, seu arquivo continua intacto.

---

## Como o Nginx funciona dentro do Docker

O Nginx é um dos servidores web mais utilizados no mundo. Ao rodar dentro de um container, o fluxo de uma requisição funciona assim:

```
[Seu Navegador] → http://localhost:8080
                          │
                          │  (Docker redireciona porta 8080 → 80)
                          │
                    [Container Nginx]
                          │
                          │  (Nginx serve o arquivo em /usr/share/nginx/html/)
                          │
                    [Exibe index.html] ✓
```

O container funciona como uma caixa selada com seu próprio servidor web interno. O Docker abre um "buraco" controlado (as `ports`) para que o mundo externo consiga acessá-lo.

---

[Voltar ao Início](../README.md)
