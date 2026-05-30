# NoteBookLM_FastAPI

Este repositório apresenta um estudo de **FastAPI** desenvolvido com o suporte do **NotebookLM do Google**.

O conteúdo foi criado como um agente de estudo focado em **Python**, pensando como um complemento adicional para o **bootcamp de Python da DIO**.

Principais objetivos:

- Usar o NotebookLM para gerar referências, exemplos e orientações de estudo sobre FastAPI.
- Construir um agente de estudo voltado para desenvolvimento de APIs em Python.
- Oferecer material extra que se integra ao aprendizado do bootcamp da DIO.

Ferramentas e foco:

- **NotebookLM do Google** para suporte de conteúdo e criação de agente de estudo.
- **FastAPI** como tecnologia principal de backend.
- **Python** como linguagem central do projeto.

Este repositório é ideal para quem deseja aprofundar o estudo de FastAPI com apoio de uma ferramenta de IA e agregar valor ao bootcamp de Python da DIO.

## Fontes

- https://fastapi.tiangolo.com/pt/tutorial/#tutorial-user-guide
- https://fastapidozero.dunossauro.com/estavel/06/#autenticacao-e-autorizacao-com-jwt
- https://fastapidozero.dunossauro.com/4.1/05/#integrando-banco-de-dados-a-api
- https://fastapidozero.dunossauro.com/estavel/#o-que-e-fastapi
- https://www.youtube.com/watch?v=HAz1eJsRB4M

## Prompts

### 1. Como funciona o FastAPI?

**Prompt:**
> "Explique de forma simples como o FastAPI funciona, quais são seus principais componentes e o que é preciso saber para começar a criar APIs em Python."

**Resposta:**
> O **FastAPI** é um framework moderno e de alta performance para a construção de APIs com Python, projetado para ser fácil de aprender e rápido de codar. Ele se destaca por utilizar **type hints** (anotações de tipo) do Python para automatizar tarefas que antes eram manuais e propensas a erros.
>
> **Como o FastAPI funciona (de forma simples)**
>
> O funcionamento do FastAPI baseia-se na declaração de tipos: você define os parâmetros de entrada e saída das suas funções usando tipos Python padrão (como `int`, `str` ou modelos mais complexos). A partir dessas declarações, o framework realiza automaticamente as seguintes ações:
>
> 1. **Validação de Dados:** verifica se os dados enviados pelo cliente estão no formato correto. Se houver erro, ele retorna uma mensagem clara e automática.
> 2. **Conversão de Dados:** converte automaticamente os dados que chegam da rede (geralmente em JSON) para tipos Python e vice-versa na resposta.
> 3. **Documentação Automática:** gera, sem código extra, interfaces interativas como **Swagger UI** e **ReDoc**, onde é possível testar a API diretamente pelo navegador.
>
> **Principais Componentes**
>
> - **Starlette:** cuida da parte web (rotas, requisições, respostas).
> - **Pydantic:** valida e converte os dados.
> - **Uvicorn:** servidor ASGI que executa a aplicação e permite uso de `async/await`.
> - **Injeção de Dependência:** permite declarar o que uma função precisa (como sessão de banco de dados ou autenticação) de forma modular.
>
> **O que é preciso saber para começar**
>
> - **Python:** funções, listas, dicionários, classes e anotações de tipo.
> - **Conceitos Web:** APIs RESTful, JSON e métodos HTTP (GET, POST, PUT, DELETE).
> - **Ambiente de desenvolvimento:** terminal, ambiente virtual (`venv`), Python 3.10+ e `pip`.

---

### 2. Quais são os padrões para gerar endpoints?

**Prompt:**
> "Descreva os padrões recomendados para criar endpoints em FastAPI, incluindo organização de rotas, uso de métodos HTTP, nomes de recursos e boas práticas para manter a API clara e fácil de manter."

**Resposta:**
> Para criar endpoints eficientes, claros e fáceis de manter no FastAPI, aplique padrões de arquitetura e use os recursos nativos do framework.
>
> **Organização de rotas e estrutura de projeto**
>
> - Separe responsabilidades em módulos como `routes`, `schemas`, `models` e `server`.
> - Use `APIRouter` para agrupar endpoints relacionados a um mesmo recurso (por exemplo, `users`).
> - Utilize `tags` para categorizar operações na documentação automática.
>
> **Uso de métodos HTTP e nomes de recursos**
>
> - `POST /users/` para criar recursos.
> - `GET /users/` para listar recursos.
> - `GET /users/{id}` para buscar um recurso específico.
> - `PUT /users/{id}` para atualizar um recurso.
> - `DELETE /users/{id}` para remover um recurso.
> - Use nomes de recursos no plural e caminhos intuitivos (`/tasks`, `/users`).
>
> **Validação de dados com Pydantic**
>
> - Defina `BaseModel` para validar dados de entrada e saída.
> - Use `response_model` para garantir que a API retorne apenas os campos esperados.
>
> **Injeção de dependência (`Depends`)**
>
> - Use `Depends` para gerenciar sessões de banco de dados e autenticação.
> - Isso mantém o código desacoplado e fácil de testar.
>
> **Códigos de status e tratamento de erros**
>
> - `201 Created` para criação bem-sucedida.
> - `204 No Content` para remoção sem corpo de resposta.
> - `404 Not Found` para recursos não encontrados.
> - `409 Conflict` para conflitos de integridade.
> - Use `HTTPException` para devolver erros de forma padronizada.
>
> **Boas práticas adicionais**
>
> - Paginação com `skip` e `limit` para listas longas.
> - Verifique `/docs` para documentação automática.
> - Crie testes com `TestClient` e `pytest`.

---

### 3. Como testar endpoints com Insomnia?

**Prompt:**
> "Mostre como testar endpoints do FastAPI usando o Insomnia, incluindo configuração de requisições GET, POST, PUT e DELETE, envio de JSON no corpo da requisição e verificação das respostas."

**Resposta:**
> A ideia é usar o Insomnia como um cliente REST para enviar requisições aos endpoints e verificar os retornos.
>
> **Configuração geral**
>
> - URL base: `http://127.0.0.1:8000`.
>
> **GET (listar/buscar)**
>
> - Método: `GET`.
> - URL: `/users`, `/tasks` ou outro recurso.
> - Parâmetros de consulta: `?skip=0&limit=10`.
> - Verificação: status `200 OK` e corpo com lista JSON.
>
> **POST (criar)**
>
> - Método: `POST`.
> - URL: `/users/`.
> - Corpo JSON:
>   ```json
>   {
>     "user_name": "Rafa",
>     "age": 30,
>     "uf": "SP"
>   }
>   ```
> - Verificação: status `201 Created` e retorno com os dados criados.
>
> **PUT (atualizar)**
>
> - Método: `PUT`.
> - URL: `/users/{id}`.
> - Corpo JSON com os campos a atualizar.
> - Verificação: status `200 OK` ou `404 Not Found` se o recurso não existir.
>
> **DELETE (remover)**
>
> - Método: `DELETE`.
> - URL: `/tasks/{id}`.
> - Verificação: status `204 No Content` para remoção bem-sucedida.
>
> **Testando endpoints protegidos**
>
> - Faça `POST /token` com `username` e `password` para obter o token.
> - No Insomnia, use `Bearer Token` e cole o `access_token`.
> - Envie a requisição com o cabeçalho `Authorization: Bearer <token>`.
>
> **Verificação de erros**
>
> - `404 Not Found`: recurso inexistente.
> - `409 Conflict`: recurso duplicado ou conflito de integridade.
> - `401 Unauthorized`: rota protegida sem token válido.
>
> *Observação: As instruções de interface do Insomnia não estão diretamente nas fontes, mas este passo a passo reflete os conceitos de métodos, URLs, corpo JSON e códigos de status que são usados para testar APIs no FastAPI.**

**Resumo Final**

O uso do NotebookML me levantou um grande interesse, pois, podemos criar um especialista no assunto que nos interessar e também podemos escolher suas fontes, para alguns assuntos podem acabar sendo influenciados por não usar fontes suficientes ou confiáveis, mas para a programção eu vejo um caminho bem mais interessante e controlado. Da forma que fiz nesse notebook, utilizando junto com a própria documentação da biblioteca, eu utilizei uma aula interessante que a IA pudesse seguir como exemplo tanto de explicação como de qual a forma de programar de forma mais humana e não sendo só um replicador de informações da documentação. Se eu estiver interessado em cruzar com outras bibliotecas, eu posso simplesmente adicionar nas fontes e melhorar minha performance.