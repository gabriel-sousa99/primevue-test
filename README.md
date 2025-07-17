# Kit Inicial Laravel + PrimeVue

![Static Badge](https://img.shields.io/badge/Laravel%20-%20v12%20-%20%23f9322c) ![Static Badge](https://img.shields.io/badge/Inertia.js%20-%20v2%20-%20%236b46c1) ![Static Badge](<https://img.shields.io/badge/Vue.js%20-%20v3.5%20-%20rgb(66%20184%20131)>) ![Static Badge](<https://img.shields.io/badge/PrimeVue%20-%20v4%20-%20rgb(16%20185%20129)>) ![Static Badge](https://img.shields.io/badge/Tailwind%20CSS%20-%20v4%20-%20%230284c7) ![Static Badge](https://img.shields.io/badge/PostgreSQL%20-%2017%20-%20%23336791) ![Static Badge](https://img.shields.io/badge/Docker%20-%20Compose%20-%20%232496ED)

## 📖 Sobre o Projeto

Este é um kit inicial completo para desenvolvimento web moderno que combina as melhores tecnologias do ecossistema PHP e JavaScript. O projeto oferece uma base sólida para aplicações web com autenticação completa, interface responsiva e infraestrutura robusta.

### 🛠️ Stack Tecnológica

**Backend:**

-   **Laravel 12** - Framework PHP moderno e elegante
-   **Inertia.js v2** - Ponte entre backend e frontend, sem necessidade de API
-   **PostgreSQL 17** - Banco de dados relacional robusto
-   **PHP 8.2+** - Versão mais recente do PHP

**Frontend:**

-   **Vue.js 3.5** - Framework JavaScript progressivo
-   **PrimeVue 4** - Biblioteca de componentes UI rica e moderna
-   **Tailwind CSS 4** - Framework CSS utilitário
-   **TypeScript** - Tipagem estática para JavaScript
-   **Vite** - Build tool rápido e moderno

**Infraestrutura:**

-   **Docker Compose** - Containerização completa
-   **Traefik** - Proxy reverso e load balancer
-   **PostgreSQL** - Banco de dados principal

**Ferramentas de Desenvolvimento:**

-   **Laravel Sail** - Ambiente Docker para Laravel
-   **ESLint + Prettier** - Linting e formatação de código
-   **PHPStan + Larastan** - Análise estática de código PHP
-   **Pest** - Framework de testes moderno para PHP
-   **Laravel Pint** - Formatador de código PHP

### ✨ Funcionalidades Incluídas

-   🔐 **Sistema de Autenticação Completo**

    -   Registro de usuários
    -   Login/Logout
    -   Recuperação de senha
    -   Verificação de email
    -   Proteção de rotas

-   🎨 **Interface Moderna**

    -   Componentes PrimeVue responsivos
    -   Tema customizável
    -   Design system consistente
    -   Suporte a modo escuro

-   🚀 **Performance Otimizada**

    -   Server-Side Rendering (SSR)
    -   Code splitting automático
    -   Lazy loading de componentes
    -   Cache otimizado

-   🔧 **Ferramentas de Desenvolvimento**
    -   Hot Module Replacement (HMR)
    -   Ambiente Docker completo
    -   Testes automatizados
    -   Análise de código

## 🚀 Como Começar

### Pré-requisitos

Certifique-se de ter instalado em sua máquina:

-   **Docker** e **Docker Compose**
-   **Git**
-   **Node.js 18+** e **npm/yarn**

### 1. Clonagem e Instalação

```bash
# Clone o repositório
git clone https://github.com/connora/laravel-primevue-starter-kit.git meu-projeto
cd meu-projeto

# Instale as dependências PHP
composer install

# Instale as dependências JavaScript
npm install
```

### 2. Configuração do Ambiente

```bash
# Copie o arquivo de configuração
cp .env.example .env

# Gere a chave da aplicação
php artisan key:generate
```

### 3. Configuração do Docker

```bash
# Configure as variáveis do Docker Sail
export WWWUSER=$(id -u)
export WWWGROUP=$(id -g)

# Inicie os containers
docker-compose -f docker-compose.local.yml up -d
```

### 4. Configuração do Banco de Dados

```bash
# Execute as migrações
docker-compose -f docker-compose.local.yml exec laravel php artisan migrate

# (Opcional) Execute os seeders
docker-compose -f docker-compose.local.yml exec laravel php artisan db:seed
```

### 5. Iniciar o Desenvolvimento

```bash
# Em um terminal, inicie o Vite (frontend)
npm run dev

# Em outro terminal, se não estiver usando Docker
php artisan serve
```

**Com Docker:** A aplicação estará disponível em http://laravel-primevue.localhost

**Sem Docker:** A aplicação estará disponível em http://localhost:8000 (admin/admin123!)

### 6. Scripts Úteis

```bash
# Desenvolvimento com todos os serviços
composer run dev

# Build para produção
npm run build

# Executar testes
composer run test

# Análise de código
composer run analyse

# Formatação de código
npm run lint
./vendor/bin/pint
```

## 🐳 Usando com Docker

O projeto inclui uma configuração completa do Docker com:

-   **Traefik** (proxy reverso) - http://localhost:8080
-   **Laravel** (aplicação) - http://laravel-primevue.localhost
-   **PostgreSQL** (banco de dados) - porta 5432

### Comandos Docker Úteis

```bash
# Iniciar todos os serviços
docker-compose -f docker-compose.local.yml up -d

# Ver logs em tempo real
docker-compose -f docker-compose.local.yml logs -f

# Executar comandos Artisan
docker-compose -f docker-compose.local.yml exec laravel php artisan migrate

# Acessar o container
docker-compose -f docker-compose.local.yml exec laravel bash

# Parar todos os serviços
docker-compose -f docker-compose.local.yml down
```

## 📁 Estrutura do Projeto

```
├── app/                    # Código da aplicação Laravel
│   ├── Http/Controllers/   # Controllers
│   ├── Models/            # Models Eloquent
│   └── ...
├── resources/
│   ├── js/                # Código Vue.js/TypeScript
│   │   ├── components/    # Componentes Vue
│   │   ├── pages/         # Páginas Inertia
│   │   ├── layouts/       # Layouts
│   │   └── composables/   # Composables Vue
│   ├── css/               # Estilos CSS/Tailwind
│   └── views/             # Templates Blade
├── routes/                # Definições de rotas
├── database/              # Migrações e seeders
├── tests/                 # Testes automatizados
├── docker/                # Configurações Docker
└── public/                # Assets públicos
```

## 🧪 Testes

```bash
# Executar todos os testes
composer run test

# Executar testes com coverage
php artisan test --coverage

# Executar testes específicos
php artisan test --filter=UserTest
```

## 📦 Build para Produção

```bash
# Build dos assets
npm run build

# Otimizar autoloader
composer install --optimize-autoloader --no-dev

# Cache de configuração
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 🔗 Links Úteis

-   [Laravel Documentation](https://laravel.com/docs)
-   [Inertia.js Documentation](https://inertiajs.com/)
-   [Vue.js Documentation](https://vuejs.org/)
-   [PrimeVue Documentation](https://primevue.org/)
-   [Tailwind CSS Documentation](https://tailwindcss.com/)

---

**Desenvolvido com ❤️ usando Laravel + PrimeVue**
