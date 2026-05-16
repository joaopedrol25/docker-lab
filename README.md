
<h1 align="center"> 🐳 Docker Lab para Iniciantes </h1>

<p align="center">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Badge">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux Badge">
</p>

## 📌 Índice
* [O que é o Docker e por que usamos?](#o-que-é-o-docker-e-por-que-usamos)
* [O conceito de Container](#o-conceito-de-container)
* [Docker vs. Máquinas Virtuais (VMs)](#docker-vs-máquinas-virtuais-vms)
* [Como o Docker gerencia tudo isso?](#como-o-docker-gerencia-tudo-isso)
* [Configurações Iniciais](#configurações-iniciais)

---

## 🧐 O que é o Docker e por que usamos?

Para entender o Docker, precisamos entender o problema que ele resolveu. Antigamente, o maior pesadelo de um desenvolvedor era a frase: **"Mas na minha máquina funciona!"**. 

Isso acontecia porque o ambiente de desenvolvimento era diferente do ambiente de produção (versões de bibliotecas, variáveis, SO). O Docker surgiu para "empacotar" sua aplicação e todas as suas dependências em uma unidade padronizada chamada **Container**.

## 📦 O conceito de Container

Imagine um navio carregando diversos conteúdos: eletrônicos, café ou roupas. Quando o guindaste move esses containers, ele não precisa saber o que tem dentro, pois o **exterior é padronizado**. 

O Docker faz o mesmo com o software: ele garante que o sistema rode da mesma forma em qualquer lugar — seja no seu computador pessoal, em um servidor ou na nuvem.

---

## 🆚 Docker vs. Máquinas Virtuais (VMs)

Embora pareçam similares, são ferramentas diferentes para ocasiões diferentes. Veja a comparação:

| Característica | Máquinas Virtuais (VMs) | Docker (Containers) |
| :--- | :--- | :--- |
| **Peso** | Pesadas (GBs) - Cada uma tem um SO completo. | Leves (MBs) - Compartilham o Kernel do Host. |
| **Velocidade** | Lentas - Minutos para dar boot. | Instantâneas - Segundos para subir. |
| **Recursos** | Reservam RAM e CPU fixos. | Usam recursos sob demanda (dinâmico). |
| **Isolamento** | Total (Nível de Hardware). | Lógico (Nível de Processo). |

> **Por que o Docker se destaca?** Enquanto a VM emula um hardware inteiro, o Docker utiliza o Kernel do sistema operacional que já está rodando, criando apenas camadas isoladas por cima dele.

---

## 🏗️ Como o Docker gerencia tudo isso?

O Docker trabalha baseado em **3 pilares principais** que você explorará neste laboratório:

1.  **Imagens (O Projeto):** É o arquivo estático (somente leitura) que contém o código e as dependências. Pense nela como o "instalador" ou a "forma do bolo".
2.  **Containers (A Instância):** É a imagem em execução. É o "bolo pronto". Você pode subir vários containers idênticos baseados na mesma imagem.
3.  **Docker Compose (O Maestro):** Ferramenta para definir e rodar múltiplos containers. Em vez de comandos gigantes, usamos um arquivo `.yml` para orquestrar toda a sua infraestrutura.

---

## 🚀 Configurações Iniciais

Antes de começarmos, você precisa do motor do Docker rodando em sua máquina.

### 1. Instalação
Siga as instruções da documentação oficial para o seu sistema operacional:
👉 [Documentação Oficial de Instalação](https://docs.docker.com/engine/install/)

### 2. Verificação
Após instalar, abra seu terminal e digite:
```bash
docker --version
docker compose version
```

Com o docker e docker compose instalados, vamos dar continuidade ao nosso projeto.

## 🛠️ Prática: Subindo seu primeiro serviço

Agora que você já entende a teoria, vamos colocar a mão na massa. Preparei um laboratório prático isolado para você aprender a subir um servidor Web.

👉 **[Clique aqui para acessar o Laboratório Nginx](./nginx-service/README.md)**

Neste sub-diretório você encontrará:
* O arquivo `docker-compose.yml` comentado.
* O arquivo `index.html` para teste.
* Um guia passo a passo de execução.

