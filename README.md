[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Du716tKn)

# Documentação com Zensical

Este projeto utiliza **Zensical**, um gerador de sites estáticos moderno e minimalista, para criar e servir documentação técnica em Markdown. É uma ferramenta perfeita para criar sites de documentação rápidos, com suporte a temas personalizáveis e busca integrada.

## O que é Zensical?

Zensical é um static site generator (gerador de sites estáticos) que transforma arquivos Markdown em um site HTML completo e funcional. Perfeito para:

- 📚 Documentação de projetos
- 📖 Blogs técnicos
- 🎓 Material educacional
- 📝 Wikis e bases de conhecimento

## Pré-requisitos

Antes de começar, você precisa ter instalado:

- **Python 3.10+** — [Download aqui](https://www.python.org/)
- **pip** — Gerenciador de pacotes Python (geralmente incluído com Python)

Para verificar se você tem Python instalado, execute:

```bash
python --version
```

## Instalação e Configuração

### 1. Criar ambiente virtual

```bash
python3 -m venv .venv
```

### 2. Ativar o ambiente virtual

**Windows (PowerShell):**
```powershell
.\.venv\Scripts\Activate.ps1
```

**Windows (CMD):**
```cmd
.\.venv\Scripts\activate
```

**Linux/macOS:**
```bash
source .venv/bin/activate
```

### 3. Instalar dependências

```bash
pip install -r requirements.txt
```

## Comandos Básicos do Zensical

### Criar um novo projeto

Para criar um novo projeto com template padrão:

```powershell
.\.venv\Scripts\zensical new .
```

### Construir o projeto

Para gerar os arquivos HTML estáticos:

```powershell
.\.venv\Scripts\zensical build
```

### Servir o projeto localmente

Para visualizar o site em seu navegador:

```powershell
.\.venv\Scripts\zensical serve
```

O site estará disponível em `http://localhost:8000`

### Servir em uma porta personalizada

Se a porta 8000 estiver ocupada:

```powershell
.\.venv\Scripts\zensical serve -a localhost:8080
```

O site estará disponível em `http://localhost:8080`

## Estrutura do Projeto

```
.
├── README.md              # Este arquivo
├── requirements.txt       # Dependências do projeto
├── zensical.toml         # Configuração do Zensical
├── docs/                 # Arquivos Markdown da documentação
│   ├── index.md
│   ├── introducao.md
│   └── ...
└── site/                 # Saída gerada (HTML estático)
    └── index.html
```

## Adicionando novos documentos

Para adicionar uma nova página à documentação:

1. Crie um arquivo `.md` na pasta `docs/`
2. Escreva o conteúdo em Markdown
3. Execute `zensical serve` para visualizar

## Solução de Problemas

### Erro: "zensical: comando não encontrado"

Certifique-se de que:
1. O ambiente virtual está ativado
2. As dependências foram instaladas: `pip install -r requirements.txt`
3. Você está no diretório do projeto

### Erro: "não é possível carregar script"

Se receber erro sobre política de execução no PowerShell, use:

```powershell
.\.venv\Scripts\python -m zensical serve
```

## Contribuindo

Para contribuir com esta documentação:

1. Crie um novo branch: `git checkout -b feature/nova-secao`
2. Adicione seus documentos em Markdown na pasta `docs/`
3. Teste localmente com `zensical serve`
4. Faça commit e push das mudanças
5. Abra um Pull Request

## Licença

Este projeto é fornecido como material educacional.
