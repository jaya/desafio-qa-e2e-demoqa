# Desafio QA E2E — DemoQA (Playwright + Behave, Python)

## 🌟 Objetivo do Desafio

Este desafio usa o [**DemoQA — Book Store Application**](https://demoqa.com/login?utm_source=chatgpt.com) para validar o fluxo crítico **Login → Adicionar favorito (coleção) → Ver favoritos → Logout**.  
O candidato deverá **especificar em Gherkin e implementar** cenários E2E com **Playwright (Python)** e **Behave**, mantendo foco em **clareza**, **robustez** e **design de testes**.

O objetivo é avaliar sua capacidade de:

* Traduzir **requisitos funcionais em cenários Gherkin**
* Implementar **testes E2E confiáveis** (esperas explícitas, seletores estáveis, Page Objects)
* Organizar o projeto com **boa separação de responsabilidades**
* Documentar **execução, dados e limitações** no README

---

## 🚀 Funcionalidades a Cobrir (Obrigatórias)

1. **Autenticação (login/logout)**
2. **Favoritar um item** (no Book Store, “Add To Your Collection”)
3. **Listar favoritos** (perfil do usuário)
4. **Persistência entre sessões** (favorito continua após logout/login)
5. **Fluxos negativos básicos** (erro ao logar, proteção de rota)

**Base de testes:** `https://demoqa.com/` → **Book Store Application**  
Módulos principais: `Login`, `Book Store`, `Profile`.

---

## 🚫 Restrições e Validações

* **Sem manipulação direta de API** (o teste deve validar via UI)  
* Não usar `sleep` fixo — utilize **esperas explícitas**  
* Registro/login devem ser feitos **apenas via UI** (quando aplicável)  
* Se o ambiente exibir **CAPTCHA** ou limitar ações, documente contorno no README  

---

## 📄 Especificação em Gherkin (a ser implementada)

Os cenários abaixo são **obrigatórios**. Você deverá implementá-los e criar **no mínimo +2 cenários novos** (ver seção “Cenários extras exigidos”).

### Feature: Fluxo de favoritos na Book Store (DemoQA)

#### Background
```
Dado que acesso a página inicial do DemoQA
E navego até o módulo "Book Store Application"
```

---

#### Cenário A — Registro e Login bem-sucedido
```
Dado que não estou autenticado
E acesso a página de "Login"
Quando escolho "New User" para me registrar
E preencho os campos obrigatórios com dados válidos
E confirmo o registro
E retorno à página de "Login"
E informo minhas credenciais válidas
Então devo ver a área autenticada do usuário carregada
E o meu "User Name" deve estar visível no perfil
```

#### Cenário B — Login com credenciais inválidas
```
Dado que estou na página de "Login"
Quando informo credenciais inválidas
E confirmo o login
Então devo ver uma mensagem de erro informando que o login falhou
E devo permanecer na página de "Login"
```

#### Cenário C — Adicionar um livro aos favoritos (coleção)
```
Dado que estou autenticado
E acesso a "Book Store"
Quando pesquiso por um livro existente pelo título
E abro a página de detalhes do livro
E aciono "Add To Your Collection"
Então devo ver um feedback de sucesso
```

#### Cenário D — Verificar livro favorito no perfil
```
Dado que estou autenticado
Quando acesso a página "Profile"
Então devo ver o livro previamente adicionado listado na minha coleção
E o título do livro deve corresponder ao que foi favoritado
```

#### Cenário E — Persistência após logout/login
```
Dado que tenho pelo menos um livro na minha coleção
Quando faço "Logout"
E realizo "Login" novamente com as mesmas credenciais
E acesso a página "Profile"
Então o livro favoritado deve permanecer na minha coleção
```

#### Cenário F — Remover livro da coleção
```
Dado que estou autenticado
E tenho um livro na minha coleção
Quando removo o livro da coleção
Então o livro não deve mais aparecer listado no meu "Profile"
```

#### Cenário G — Acesso protegido sem autenticação
```
Dado que não estou autenticado
Quando tento acessar diretamente a página "Profile"
Então devo ser redirecionado para a página de "Login" ou ver bloqueio de acesso
```

---

## ➕ Cenários extras exigidos

Você deverá **criar e implementar pelo menos 2 cenários novos** (Gherkin + implementação). Sugestões:

* **Validação de formulário de registro** (campos obrigatórios, senhas diferentes, tamanho mínimo)
* **Busca por livro inexistente** (exibir “no results” e manter grid vazio)
* **Ordenação/filtragem de livros** (se disponível na UI)
* **Sessão expirada** (simular logout e tentar ação protegida)

---

## 🧰 Estrutura e Requisitos de Projeto

* Linguagem: **Python 3.11+**
* Framework: **Playwright** + **Behave**
* Estilo: **Page Object Model (POM)**
* **Sem código neste enunciado** — a implementação é parte do desafio

Estrutura sugerida:
```
e2e-demoqa/
  ├─ features/
  │   ├─ bookstore_favorites.feature
  │   └─ steps/
  ├─ pages/
  ├─ resources/
  ├─ support/
  ├─ README.md
  └─ pyproject.toml / requirements.txt
```

---

## ⚖️ Critérios de Avaliação

* Clareza da especificação Gherkin (20%)
* Robustez dos testes (25%)
* Design e organização (20%)
* Observabilidade (15%) — evidências em falha (screenshot/trace)
* Entrega e documentação (20%)

---

## 📋 Entrega

1. Crie um **repositório público** no seu GitHub com o nome `e2e-demoqa-playwright-behave`.
2. Inclua:
   * `features/*.feature` com todos os cenários obrigatórios + **no mínimo 2 extras**
   * Implementação completa em Python (Playwright + Behave)
   * **README.md** com:
     - Pré-requisitos
     - Como criar usuário no DemoQA (ou estratégia usada)
     - Como configurar variáveis (BASE_URL, USER, PASS)
     - Como rodar localmente (incluindo report HTML/trace)
     - Decisões e limitações
3. Envie o link do repositório com:
   - **Título:** `Entrega - seu_nome_completo`
   - **Descrição:** Nome completo, data, observações

> ✅ **Dica:** Inclua `THOUGHTS.md` com decisões técnicas, trade-offs e ideias de melhoria.

---

## 🎓 Licença

Este desafio usa o site público **DemoQA** apenas para fins de **avaliação técnica e educacional**.

---

## 📢 Contato

* Proposto por: **Equipe de Engenharia Jaya Tech**
* Autor da especificação: **Leandro Costa (Leco)**
