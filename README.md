🧪 Projeto de Automação de Testes – Portal OPEA (Cadastro de Usuário)
📋 Descrição Geral

Este projeto automatiza os testes do CRUD de Cadastro de Usuário do portal OPEA:

🔗 URL de teste: https://sso.opea-uat.solutions/account/signup

O objetivo é validar as regras de negócio do processo de criação de conta de usuário, garantindo que todos os cenários positivos e negativos estejam cobertos conforme as regras descritas no caderno de testes.

⚙️ Tecnologias Utilizadas
Tecnologia	Descrição
Cypress 13+	Framework de automação de testes front-end
Cucumber (BDD)	Estrutura de testes em linguagem natural (Gherkin)
Node.js	Ambiente de execução JavaScript
Allure Reporter	Relatórios de execução e evidências
Esbuild Preprocessor	Transpilação rápida de arquivos .feature
JavaScript (ES6)	Linguagem principal dos testes

🧩 Estrutura do Projeto

avaliação-qa-opea/
│
├── cypress/
│   ├── e2e/
│   │   ├── features/
│   │   │   └── signup.feature          # Cenários em formato BDD (Gherkin)
│   │   └── step_definitions/
│   │       └── signupSteps.js          # Implementação dos steps
│   │   ├── signup.cy.js                # Implementação dos testes
│   ├── support/
│   │   ├── commands.js                 # Comandos customizados (preencherSignup, submeterSignup, etc.)
│   │   ├── e2e.js                      # Configurações globais
│   │   └── utils/
│   │       └── cpf.js                  # Gerador e validador de CPF
│   │
│   └── fixtures/                       # Massa de dados, se necessário futuramente
├── documentacao                        # Documentação do projeto
├── cypress.config.js                   # Configurações do Cypress e Cucumber
├── package.json                        # Dependências do projeto
├── README.md                           # Documentação da automação
└── reports/                            # Relatórios Allure

🔤 Comandos Customizados

Local: cypress/support/commands.js

Comando	Descrição
cy.gerarCPF(formatado)	Gera um CPF válido, formatado ou não
cy.validarCPF(cpf)	Verifica se o CPF é válido
cy.preencherSignup(dados)	Preenche o formulário de cadastro conforme objeto de dados
cy.submeterSignup()	Submete o formulário de cadastro

Exemplo de uso:
cy.gerarCPF(false).then((cpf) => {
  const dados = {
    nome: 'Teste QA',
    sobrenome: 'Automação',
    cpf,
    email: `user_${Date.now()}@teste.com`,
    telefone: '11999999999',
    empresa: 'Empresa Teste',
    senha: 'Senha@123',
    confirmarSenha: 'Senha@123'
  };

  cy.preencherSignup(dados);
  cy.submeterSignup();
});
🧾 Execução dos Testes
💻 1. Instalar dependências
npm install

▶️ 2. Executar todos os testes no modo interativo
npx cypress open

⚙️ 3. Executar testes em modo headless
npx cypress run

🧮 4. Gerar relatório Allure
allure generate reports/allure-results --clean -o reports/allure-report
allure open reports/allure-report

🧠 Regras de Negócio Principais

CPF deve ser válido e único

O sistema deve rejeitar CPFs duplicados e inválidos.

E-mail deve ser único e seguir formato padrão

E-mails como teste@teste.com são aceitos; teste.com não.

Campos obrigatórios não podem ser vazios

Todos os campos devem ser preenchidos antes do envio.

Senha deve ser forte

Contendo letras maiúsculas, minúsculas, números e caracteres especiais.

Senhas devem coincidir

“Senha” e “Confirmar Senha” devem ser idênticas.

🧑‍💻 Convenções de Código

Page Objects e Commands: Centralizam seletores e ações comuns.

Cenários BDD: Escritos em linguagem natural no formato .feature.

Dados dinâmicos: Gerados com timestamp (Date.now()) para evitar duplicidade.

Geração de CPF: Implementada via utils/cpf.js com verificação de validade.

🧱 Boas Práticas Implementadas

✅ Estrutura modular (features + steps + commands)
✅ Dados de teste dinâmicos
✅ Uso de Gherkin padronizado
✅ Reaproveitamento de código
✅ Configuração para relatórios Allure
✅ Suporte para integração contínua (CI/CD)

📎 Contato / Autoria

Autor: Paulo Correia
Função: QA / Analista de Testes Automatizados
Objetivo: Projeto de automação de testes para validação do módulo de cadastro de usuário no portal OPEA.
