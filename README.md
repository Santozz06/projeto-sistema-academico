# 🎓 SAS — Sistema Acadêmico Escolar

Sistema web completo para gestão acadêmica escolar, desenvolvido como Trabalho de Conclusão de Curso (TCC). A aplicação gerencia todo o fluxo administrativo de uma instituição de ensino, desde o cadastro de alunos e servidores até a emissão de documentos oficiais como históricos, boletins e atestados.

![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-4-7952B3?logo=bootstrap&logoColor=white)
![License](https://img.shields.io/badge/Licença-MIT-green)

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades](#-funcionalidades)
- [Arquitetura](#-arquitetura)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Pré-requisitos](#-pré-requisitos)
- [Como Rodar o Projeto](#-como-rodar-o-projeto)
- [Credenciais de Acesso (Demo)](#-credenciais-de-acesso-demo)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Modelo de Dados](#-modelo-de-dados)
- [Contribuição](#-contribuição)
- [Licença](#-licença)

---

## 💡 Sobre o Projeto

O **SAS (Sistema Acadêmico Escolar)** foi projetado para digitalizar e centralizar a gestão escolar, substituindo processos manuais e planilhas por uma aplicação web acessível via navegador. O sistema atende três perfis de usuário distintos, cada um com seu próprio painel e permissões.

### Problema resolvido
Escolas que ainda dependem de controles manuais (cadernos de chamada, planilhas de notas, documentos impressos) enfrentam retrabalho, inconsistência de dados e lentidão na emissão de documentos. O SAS resolve esses problemas com uma plataforma integrada e containerizada, pronta para deploy.

---

## ✨ Funcionalidades

### 👨‍💼 Painel do Administrador
- Cadastro completo de alunos e servidores (dados pessoais, endereço, filiação, necessidades especiais)
- Criação e gerenciamento de turmas (etapa, turno, capacidade, sala)
- Gerenciamento de vínculos professor-disciplina-turma
- Atribuição de disciplinas aos professores
- Cadastro de grade de horários
- Controle de matrículas, rematrículas e transferências
- Emissão de documentos: histórico escolar, atestado de matrícula, atestado de frequência, documento de transferência
- Calendário acadêmico com eventos
- Relatórios e visão geral do sistema
- Listagem de professores e alunos por turma

### 👨‍🏫 Painel do Professor
- Visualização de turmas vinculadas
- Caderno de chamada digital (registro de frequência)
- Lançamento e gestão de notas por disciplina
- Registro de atividades e avaliações
- Registro de ocorrências disciplinares
- Consulta a normas acadêmicas
- Calendário acadêmico

### 👨‍🎓 Painel do Aluno
- Dashboard com visão geral do desempenho
- Consulta ao boletim detalhado por disciplina
- Acompanhamento de frequência
- Visualização do histórico escolar
- Consulta a componentes curriculares
- Emissão de atestados (matrícula e frequência)
- Calendário acadêmico

### 🔐 Autenticação
- Login com seleção de perfil (Admin / Professor / Aluno)
- Controle de sessão com verificação de permissão por rota
- Recuperação de senha
- Senhas armazenadas com hash seguro (password_hash / crypt)

---

## 🏗 Arquitetura

`
┌─────────────┐      ┌──────────────────┐      ┌───────────┐
│  Navegador  │◄────►│  Apache + PHP    │◄────►│  MySQL    │
│  (Frontend) │      │  (Backend)       │      │  8.0      │
│  Bootstrap 4│      │  PHP 8.2         │      │           │
└─────────────┘      └──────────────────┘      └───────────┘
                     ┌──────────────────┐
                     │  phpMyAdmin      │
                     │  (porta 8081)    │
                     └──────────────────┘
`

O projeto utiliza uma arquitetura **MVC simplificada** com:
- **Camada CRUD** (includes/crud/): Classes PHP para operações no banco (BaseCRUD, UsuarioCRUD, TurmaCRUD, DisciplinaCRUD, MatriculaCRUD, VinculoCRUD, LocalidadeCRUD)
- **Camada AJAX** (includes/ajax/): Endpoints assíncronos para operações dinâmicas
- **Views** (user_adm/, user_professor/, user_aluno/): Páginas PHP com templates Bootstrap
- **Bootstrap** (includes/bootstrap.php): Arquivo central que inicializa sessão, conexão e controle de acesso

Toda a infraestrutura roda em **Docker**, com três containers orquestrados via docker-compose.yml.

---

## 🛠 Tecnologias Utilizadas

| Camada | Tecnologia |
|---|---|
| **Frontend** | HTML5, CSS3, JavaScript, Bootstrap 4, jQuery |
| **Backend** | PHP 8.2, PDO (prepared statements) |
| **Banco de Dados** | MySQL 8.0 |
| **Servidor Web** | Apache (mod_rewrite) |
| **Containerização** | Docker, Docker Compose |
| **Administração do BD** | phpMyAdmin |
| **Plugins Frontend** | FullCalendar, Sparkline Charts, DataTables |

---

## 📦 Pré-requisitos

Você precisa ter instalado:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows/Mac) ou Docker Engine + Docker Compose (Linux)
- [Git](https://git-scm.com/)

> **Nota:** Não é necessário instalar PHP, MySQL ou Apache localmente. O Docker cuida de tudo.

---

## 🚀 Como Rodar o Projeto

### 1. Clone o repositório

`ash
git clone https://github.com/Santozz06/projeto-sistema-academico.git
cd projeto-sistema-academico
`

### 2. Suba os containers

`ash
docker-compose up -d --build
`

Esse comando irá:
- Construir a imagem PHP + Apache a partir do Dockerfile
- Baixar a imagem do MySQL 8.0
- Baixar a imagem do phpMyAdmin
- Importar automaticamente o banco de dados (escola_db.sql)

> ⏳ **Na primeira execução**, o MySQL pode levar de 1 a 3 minutos para inicializar completamente e importar o banco. O container web aguarda automaticamente via healthcheck.

### 3. Acesse a aplicação

| Serviço | URL |
|---|---|
| **Sistema (Login)** | [http://localhost:8080/auth/login.php](http://localhost:8080/auth/login.php) |
| **phpMyAdmin** | [http://localhost:8081](http://localhost:8081) |

### 4. Parar os containers

`ash
docker-compose down
`

Para remover também os dados do banco (volume):

`ash
docker-compose down -v
`

---

## 🔑 Credenciais de Acesso (Demo)

O banco de dados já vem populado com usuários de teste:

| Perfil | Login | Senha |
|---|---|---|
| **Administrador** | `admin` | `1234` |
| **Professor** | `servidorteste1@gmail.com` | `1234` |
| **Aluno** | `alunoteste1@gmail.com` | `1234` |

> Na tela de login, selecione o tipo de usuário correspondente antes de clicar em **Entrar**.

---

## 📁 Estrutura de Pastas

`
projeto-sistema-academico/
├── backend/
│   └── dashtreme-master/
│       ├── assets/              # CSS, JS, imagens, plugins do template
│       ├── auth/                # Login, autenticação, logout, reset de senha
│       ├── includes/
│       │   ├── ajax/            # Endpoints AJAX (admin, aluno, professor, etc.)
│       │   ├── config/          # Conexão com banco de dados (PDO)
│       │   ├── crud/            # Classes CRUD (Usuario, Turma, Disciplina, etc.)
│       │   └── bootstrap.php    # Inicialização: sessão, conexão e controle de acesso
│       ├── public/              # Arquivos públicos
│       ├── uploads/             # Uploads de arquivos
│       ├── user_adm/            # Páginas do painel administrativo
│       ├── user_aluno/          # Páginas do painel do aluno
│       └── user_professor/      # Páginas do painel do professor
├── docker-compose.yml           # Orquestração dos containers
├── Dockerfile                   # Imagem PHP 8.2 + Apache
├── escola_db.sql                # Dump completo do banco (dados de demo)
├── init.sql                     # Schema do banco (criação das tabelas)
├── init.sh                      # Script auxiliar de inicialização
├── opcache.ini                  # Configuração de cache PHP
└── README.md
`

---

## 🗄 Modelo de Dados

O sistema utiliza as seguintes tabelas principais:

`
Usuarios ──────┬──── Alunos
               ├──── Professores ──── Disciplinas
               │                       │
               │     Turmas ◄──────── Professores_Turmas
               │       │
               │     Matriculas ──── Notas
               │       │              │
               │       │         Disciplinas
               │       │
               │     Frequencias
               │
               ├──── Acompanhamento_NEE
               │
Calendario_Academico
Planos_Ensino
`

**Tabelas:** Usuarios, Alunos, Professores, Turmas, Disciplinas, Matriculas, Notas, Frequencias, Planos_Ensino, Calendario_Academico, Acompanhamento_NEE, Professores_Turmas

---

## 🤝 Contribuição

Contribuições são bem-vindas! Siga os passos:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (git checkout -b feature/minha-feature)
3. Commit suas mudanças (git commit -m 'Adiciona minha feature')
4. Push para a branch (git push origin feature/minha-feature)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](License.txt) para mais detalhes.

---

<p align="center">
  Desenvolvido como Trabalho de Conclusão de Curso
</p>
