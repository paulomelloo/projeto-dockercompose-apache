# 🐳 Projeto Docker de Apresentação de Conhecimentos (DIO)

Este repositório contém o primeiro projeto desenvolvido como parte do curso de **Formação Docker Fundamentals na DIO**. O objetivo é apresentar os conceitos aprendidos (Dockerfile, Volumes, Redes) utilizando o **Docker Compose** para orquestrar um simples servidor web.

---

## 💡 Sobre o Projeto

O projeto hospeda uma página web (`www/index.html`) que serve como um relatório de aprendizado, detalhando os principais tópicos cobertos no curso de Docker.

### 📁 Estrutura de Arquivos e Pastas

| Arquivo/Diretório | Função |
| :--- | :--- |
| `docker-compose.yml` | Arquivo que define o serviço **Apache** e a rede, orquestrando o ambiente com o comando `docker compose up`. |
| `www/` | **Diretório Mapeado (Bind Mount)**. Contém o `index.html` e é espelhado no contêiner Apache. |
| `www/index.html` | A página de resumo que lista os conhecimentos adquiridos. |
| `README.md` | Este documento. |

### ⚙️ Configuração do `docker-compose.yml`

O arquivo utiliza a **Especificação Compose (V2)** para configurar o servidor Apache:

```yaml
services:
  apache:
    image: httpd:latest
    container_name: apache_server
    ports:
      - "8080:80"
    volumes:
      - ./www:/usr/local/apache2/htdocs/  # Bind Mount
    networks:
      - webnet

networks:
  webnet:
    driver: bridge
