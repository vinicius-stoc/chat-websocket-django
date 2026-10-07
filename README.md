# Django WebSocket Chat - Estudo de Caso

## Sobre o Projeto

Este repositório contém uma aplicação prática desenvolvida com o objetivo de consolidar os estudos teóricos sobre WebSockets utilizando o framework Django (através do Django Channels). O foco principal deste projeto não é a estética da interface ou a preparação para um ambiente de produção, mas sim a compreensão técnica de como a comunicação bidirecional em tempo real funciona.

A aplicação demonstra um sistema de chat simples, onde mensagens podem ser trocadas instantaneamente entre múltiplas abas do navegador operando em `localhost`. 

## Objetivos de Aprendizado

* **Compreensão do Protocolo WebSocket:** Entender o ciclo de vida da conexão, desde o "handshake" de abertura HTTP até a troca ininterrupta de mensagens.
* **Comunicação Full-Duplex:** Demonstrar na prática a diferença entre o modelo tradicional de requisições HTTP e a comunicação contínua e bidirecional.
* **Implementação com Django Channels:** Configurar e utilizar um servidor ASGI em vez do tradicional WSGI.
* **Gerenciamento de Consumidores:** Criar lógicas de recepção e roteamento de mensagens usando `consumers.py` e `routing.py`.

## Estrutura Principal do Projeto

A arquitetura do projeto foi estruturada para separar claramente as requisições web tradicionais das conexões WebSocket:

* **`mywebsite/asgi.py`**: Ponto de entrada principal para a aplicação assíncrona, substituindo o WSGI padrão para suportar WebSockets.
* **`chat/routing.py`**: Define o roteamento de URLs específico para as conexões WebSocket (semelhante ao `urls.py`, mas focado no protocolo `ws://`).
* **`chat/consumers.py`**: Contém o coração da lógica em tempo real. É responsável por aceitar conexões, receber mensagens do cliente e enviá-las de volta aos usuários conectados.
* **`chat/templates/chat/lobby.html`**: A interface de cliente simples, construída em HTML e JavaScript puro, responsável por abrir a conexão com o servidor e renderizar as mensagens na tela.

## Como Executar o Projeto Localmente

### Pré-requisitos

Certifique-se de ter o Python instalado em sua máquina. Recomenda-se o uso de um ambiente virtual para isolar as dependências.

### Passo a Passo

1. **Clone o repositório** para a sua máquina local.

2. **Crie e ative um ambiente virtual**:
   ```bash
   python -m venv venv
   
   # No Linux ou macOS:
   source venv/bin/activate
   
   # No Windows:
   venv\Scripts\activate
   ```

3. **Instale as dependências** do projeto (certifique-se de instalar o Django e o pacote `channels`):
   ```bash
   pip install django channels
   ```

4. **Aplique as migrações** do banco de dados:
   ```bash
   python manage.py migrate
   ```

5. **Inicie o servidor de desenvolvimento**:
   ```bash
   python manage.py runserver
   ```

## Como Testar a Comunicação em Tempo Real

1. Com o servidor rodando, abra o seu navegador de preferência.
2. Acesse a rota da interface do chat (por exemplo, `http://localhost:8000/`).
3. Abra uma nova aba ou janela do navegador e acesse o mesmo endereço.
4. Digite uma mensagem em uma das abas e pressione para enviar. Você verá a mensagem ser renderizada instantaneamente em todas as outras abas abertas, sem a necessidade de recarregar a página.

## Licença

Este projeto possui fins estritamente educacionais e de pesquisa pessoal na área de Engenharia de Software. Sinta-se à vontade para clonar, modificar e utilizar este código para os seus próprios estudos.
