# Portfólio — Benjamim Borges · v2.0

Site estático feito com **HTML, CSS e JavaScript puro**. Direção editorial inspirada em [kenjilambert.com](https://kenjilambert.com/) e padrões de interface inspirados em [21st.dev](https://21st.dev/), reimplementados sem React, TypeScript, Tailwind ou bibliotecas de componentes.

## Executar

No diretório `new_portifolio/`:

```bash
python3 -m http.server 8000
```

Acesse **http://localhost:8000**. Não é necessário `npm install`, compilação nem banco de dados. Para encerrar, pressione `Ctrl+C`.

## O que existe no projeto

- Identidade editorial original, temas claro/escuro, menu responsivo, faixa de tecnologias com movimento horizontal ao passar o mouse.
- **8 cards de projeto**, com filtros e pesquisa, apresentados em modais `<dialog>`.
- Modais com problema, solução, desafios, ficha técnica, fluxo de arquitetura, navegação anterior/próximo, link compartilhável e link de repositório quando disponível.
- **3 demonstrações interativas** acessíveis pelo Laboratório e pelos projetos correspondentes:
  - **NF-e Explorer** — leitura local de XML de NF-e, resumo, itens, CST/CSOSN, campos IBS/CBS quando presentes, avisos estruturais e exportação JSON.
  - **Webhook Simulator** — edição de JSON, cenários 200/400/429/500/503, recuperação simulada, histórico de retries e exportação de log.
  - **DataCheck** — importação de CSV, linhas/colunas, duplicatas, completude, lacunas por coluna, prévia e relatório JSON.
- Retorno do Laboratório ao projeto que o abriu, e atalho do Laboratório para o projeto relacionado.
- Links dos experimentos antigos do GitHub preservados.
- Respeito a `prefers-reduced-motion`, `Esc`, foco e navegação por teclado.

**Escopo real das demonstrações:** tudo é executado **localmente em JavaScript**, sem enviar os arquivos para a rede. O NF-e Explorer **não** consulta a SEFAZ, não valida XSD, assinatura digital, autorização nem regras fiscais. O simulador de webhooks **não** envia requisições reais. O DataCheck **não** executa Python. A leitura de IBS/CBS é apenas exibição de campos que já estejam presentes no XML.

## Estrutura

```text
new_portifolio/
├── index.html
├── css/
│   ├── style.css             # Identidade original
│   └── components.css        # Cards, modais e laboratório
├── js/
│   ├── projects.js           # Catálogo de projetos e demonstrações
│   ├── demos.js              # Três protótipos locais
│   └── main.js               # Navegação, filtros, tema, modais
├── assets/                   # Imagens e favicon
├── docs/
│   └── integracao-backend.md # Próxima fase (contratos propostos)
└── tests/
    └── smoke.cjs            # Testes de lógica com Node.js, opcionais
```

## Adicionar um projeto

Edite `js/projects.js` em `window.portfolioProjects`. Cada item deve ter `id` único, `title`, `category`, `categoryLabel`, `year`, `status`, `description`, `tags`, `visual`, `mark`, `problem`, `solution`, `challenge`, `role` e `architecture` (lista de etapas técnicas). `link` é opcional e deve ser um endereço público verdadeiro. Para associar uma demo, adicione `demoId` com o ID correspondente em `window.portfolioDemos`.

Categorias existentes: `sistemas`, `dados`, `pesquisa`, `linux`. Ao clicar em um card, o modal recebe um link como `#projeto=balancete-fiscal`; demonstrações usam `#demo=nfe-explorer`.

## Testar

Testes de lógica (Node.js opcional, sem instalar pacotes):

```bash
node tests/smoke.cjs
node --check js/main.js
node --check js/projects.js
node --check js/demos.js
```

Teste manual recomendado no navegador: abrir os oito modais; navegar entre projetos; abrir cada demonstração por dois caminhos; analisar as amostras; exportar relatórios; conferir modo escuro, `Esc`, foco, celular e histórico do navegador.

## Próxima fase: APIs reais

O site estático continuará independente. Serviços Rust, Node.js e Python poderão ser adicionados em **outra aplicação**, atrás de endpoints próprios e protegidos. Consulte `docs/integracao-backend.md`. Não publicar credenciais, chaves privadas, XML empresariais reais nem dados pessoais de clientes.

## Histórico

**v2.0** — fichas técnicas e arquitetura nos modais; navegação entre projetos; links compartilháveis; navegação entre projeto e demo; melhorias nas três demos; métricas detalhadas, exportações JSON e testes automatizados básicos.

**v1.0** — cards editoriais, modais, Laboratório com três protótipos locais, temas, filtros e marquee.
