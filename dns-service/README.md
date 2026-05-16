# Servidor DNS com AdGuard Home

Este diretório contém os arquivos necessários para rodar um servidor DNS local completo com bloqueio de anúncios e rastreamento, usando o **AdGuard Home** em um container Docker.

## 📝 Arquivos neste diretório
* `docker-compose.yml`: Configuração do serviço, portas e volumes.
* `/work`: Pasta para dados operacionais do AdGuard (banco de dados, logs, estatísticas).
* `/conf`: Pasta para suas configurações e listas de filtros.

---

## Como Executar

1. Certifique-se de estar dentro da pasta `dns-service`.
2. Suba o container com o comando:
   ```bash
   docker compose up -d
   ```
3. Na **primeira execução**, acesse o assistente de instalação em:
   ```
   http://localhost:3000
   ```
4. Siga o assistente, defina login e senha e conclua a configuração.
5. Após configurado, o painel principal estará disponível em:
   ```
   http://localhost:8080
   ```
6. Para parar o container, execute:
   ```bash
   docker compose down
   ```

> **Atenção:** A porta `53` é a porta padrão DNS do sistema operacional e pode já estar em uso por outro processo (como o `systemd-resolved` no Linux). Caso ocorra um erro ao subir o container, consulte a seção [Solução de Problemas](#️-solução-de-problemas) abaixo.

---

# Entendendo o arquivo `docker-compose.yml`

Para entender como o Docker interpreta as nossas instruções, vamos analisar cada parte do arquivo configurado:

### `services`

Aqui definimos quais containers farão parte do nosso projeto. No nosso caso, temos o `adguard`.

* **`image: adguard/adguardhome:latest`**:
  * É a base do nosso container. Estamos usando a imagem oficial do AdGuard Home, publicada no Docker Hub pela própria equipe do AdGuard.
  * A tag `latest` garante que sempre usaremos a versão mais recente disponível.

* **`container_name: adguard`**:
  * Define um nome fixo para o container. Isso facilita a gestão via terminal (ex: `docker stop adguard`) em vez de deixar o Docker gerar um nome aleatório.

* **`restart: unless-stopped`**:
  * Define a política de reinicialização. O container será reiniciado automaticamente caso caia por erro ou após o host reiniciar — **exceto** se você o parar manualmente com `docker compose down`. Essencial para serviços de infraestrutura como um DNS.

---

### `ports`

É a ponte entre o seu computador e o mundo isolado do Docker. A regra é sempre: **`[Porta do seu Dispositivo]:[Porta dentro do Container]`**.

| Mapeamento | Protocolo | Função |
| :--- | :---: | :--- |
| `53:53` | TCP/UDP | **Porta padrão DNS.** É por aqui que os dispositivos da sua rede enviam as consultas de nome (ex: "qual o IP do google.com?"). Essencial para o serviço funcionar. |
| `3000:3000` | TCP | **Assistente de instalação.** Usada apenas na primeira vez para configurar o AdGuard via interface web. |
| `8080:80` | TCP | **Painel de administração.** A interface web do AdGuard roda internamente na porta 80. Mapeamos para a 8080 do host para evitar conflitos com outros serviços. |
| `443:443` | TCP | **DNS-over-HTTPS (DoH).** Permite consultas DNS criptografadas. Opcional, mas recomendado para maior privacidade e segurança. |

---

### `volumes`

Este é o conceito de **Persistência de Dados**. Por padrão, tudo dentro de um container é efêmero — ao remover o container, todos os dados são perdidos. Os volumes resolvem isso ao criar uma ligação entre uma pasta do seu computador e uma pasta dentro do container.

* **`./work:/opt/adguardhome/work`**:
  * Liga a pasta `work` do seu projeto à pasta onde o AdGuard armazena seus **dados operacionais**: banco de dados de consultas, estatísticas e logs de atividade.

* **`./conf:/opt/adguardhome/conf`**:
  * Liga a pasta `conf` do seu projeto à pasta onde o AdGuard guarda seus **arquivos de configuração**: listas de bloqueio, regras personalizadas, credenciais de acesso e outras preferências.

> **Por que isso importa?** Graças aos volumes, você pode derrubar e recriar o container (`docker compose down && docker compose up -d`) sem perder absolutamente nada das suas configurações e histórico.

---

## Como o AdGuard Home funciona na sua rede

Quando um dispositivo precisa acessar um site, ele envia uma **consulta DNS** para um servidor. Normalmente esse servidor é o do seu provedor de internet ou do Google (8.8.8.8). Com o AdGuard rodando no Docker, você passa a apontar seus dispositivos para o IP da sua máquina, e o fluxo se torna:

```
[Seu Dispositivo] → [AdGuard Home (Container Docker)]
                          │
                          ├─ É um anúncio ou rastreador? → BLOQUEADO ✗
                          │
                          └─ É legítimo? → Encaminha para 8.8.8.8 ou 1.1.1.1 → Responde ✓
```

O AdGuard age como um **intermediário inteligente**: filtra o que é indesejado e repassa o restante para um servidor DNS externo de sua escolha.

---

## ⚙️ Solução de Problemas

### Erro: `bind: address already in use` na porta 53

No Linux, o serviço `systemd-resolved` já ocupa a porta 53 por padrão. Para liberar a porta, execute:

```bash
# Para o serviço temporariamente
sudo systemctl stop systemd-resolved

# Para liberar permanentemente (recomendado para este lab)
sudo systemctl disable systemd-resolved
```

Após isso, suba o container novamente com `docker compose up -d`.

---

[Voltar ao Início](../README.md)
