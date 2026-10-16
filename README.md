# 🍦 Sistema de Aluguel de Carrinhos de Sorvete

<p align="center">
  <strong>Uma plataforma Django moderna para simplificar e agilizar a locação de carrinhos de sorvete para eventos</strong>
</p>

<p align="center">
  <a href="#-funcionalidades">Funcionalidades</a> •
  <a href="#-tecnologias">Tecnologias</a> •
  <a href="#-instalação">Instalação</a> •
  <a href="#-como-usar">Como Usar</a> •
  <a href="#-api-rest">API REST</a> •
  <a href="#-autor">Autor</a>
</p>

---

## ✨ Resumo do Projeto

Sistema web desenvolvido em **Django** para gerenciamento de aluguel de carrinhos de sorvete. A aplicação permite que clientes realizem reservas sem necessidade de cadastro prévio, com verificação em tempo real da disponibilidade da frota, seleção dinâmica de sabores e integração nativa com WhatsApp para confirmação de pedidos.

O painel administrativo oferece controle total sobre a operação: gestão de frota, cardápio de sabores, base de clientes e monitoramento de reservas para evitar conflitos de datas.

---

## 🎯 Funcionalidades

### 🛒 Área do Cliente (Sem Login)

| Funcionalidade | Descrição |
|---|---|
| **Verificação em Tempo Real** | Consulta instantânea à disponibilidade dos carrinhos via calendário interativo |
| **Agendamento Intuitivo** | Seleção de data e sabores diretamente na interface principal |
| **Formulário Simplificado** | Coleta apenas dados essenciais para contato, entrega e faturamento |
| **Integração WhatsApp** | Link automático para confirmação via WhatsApp com resumo completo do pedido |

### 🛡️ Painel Administrativo

| Funcionalidade | Descrição |
|---|---|
| **Controle de Frota** | Gestão completa dos carrinhos cadastrados no sistema |
| **Gestão de Cardápio** | Cadastro, edição e ativação/desativação de sabores |
| **Base de Clientes** | Centralização de todos os dados dos locatários |
| **Dashboard de Reservas** | Visualização por calendário com status e filtros por período |
| **Bloqueio Manual de Datas** | Administrador pode indisponibilizar dias específicos |

### 💼 Regras de Negócio

- Aluguel **grátis** para pedidos acima de **R$ 300,00**
- Taxa de aluguel aplicada para valores inferiores
- **24h** de antecedência mínima para reservas
- Controle de estoque por sabor com baixa automática na confirmação
- Limite de **1 reserva por carrinho por dia**

---

## 🛠️ Tecnologias

| Camada | Tecnologia | Versão |
|---|---|---|
| Backend | Django | ≥ 6.0.3 |
| Banco de Dados | MySQL | — |
| Driver DB | mysqlclient | ≥ 2.2.8 |
| Upload de Imagens | Pillow | ≥ 12.1.1 |
| Variáveis de Ambiente | python-decouple | ≥ 3.8 |
| Frontend | HTML5, CSS3, Vanilla JS | — |
| Ambiente | Python | 3.12+ |

---

## 📐 Arquitetura

```text
┌─────────────────────────────────────────────────────┐
│                  Cliente (Frontend)                 │
│  ┌─────────────────┐  ┌─────────────────────────┐  │
│  │ Página Principal│  │     Painel Admin        │  │
│  │  (index.html)   │  │    (painel.html)        │  │
│  └─────────────────┘  └─────────────────────────┘  │
└──────────────────┬───────────────────────┬────────┘
                   │                       │
           ┌───────▼──────────┐   ┌────────▼────────┐
           │   main.js        │   │  painel.js      │
           │  (API Calls)     │   │ (SPA Behavior)   │
           └──────────────────┘   └─────────────────┘
                    │                         │
            ┌───────▼─────────────────────────▼───────┐
            │          Django Backend (REST)          │
            │  ┌─────────┐  ┌─────────┐  ┌─────────┐  │
            │  │   api.py │  │views.py │  │admin.py │  │
            │  └─────────┘  └─────────┘  └─────────┘  │
            └─────────────────────────────────────────┘
                              │
                      ┌───────▼───────┐
                      │   MySQL DB    │
                      │   (via ORM)   │
                      └───────────────┘
```

---

## 🚀 Instalação

### Pré-requisitos

- Python 3.12 ou superior
- MySQL Server configurado
- Git (opcional)

### Passos

```bash
# 1. Clonar o repositório
git clone https://github.com/DEV-iini/aluguel_carrinho-sorvete.git
cd aluguel_carrinho-sorvete

# 2. Criar ambiente virtual
# Linux/macOS:
python3 -m venv venv
source venv/bin/activate

# Windows:
python -m venv venv
.\venv\Scripts\activate

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Configurar variáveis de ambiente (.env)
SECRET_KEY=SuaChaveSecretaAqui
DB_NAME=aluguel_sorvete
DB_USER=root
DB_PASSWORD=SuaSenhaMySQL
DB_HOST=localhost
DB_PORT=3306

# 5. Criar banco de dados
CREATE DATABASE aluguel_sorvete CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 6. Aplicar migrações
python manage.py makemigrations
python manage.py migrate

# 7. Criar superusuário
python manage.py createsuperuser

# 8. Iniciar servidor
python manage.py runserver
```

**Acessos:**
- Site: `http://127.0.0.1:8000/`
- Painel Admin: `http://127.0.0.1:8000/painel/`

---

## 📁 Estrutura de Pastas

```text
meusite/
├── manage.py                 # Script de comando Django
├── requirements.txt          # Dependências do projeto
├── meusite/
│   ├── settings.py           # Configurações globais
│   ├── urls.py               # Rotas do projeto
│   └── wsgi.py               # Entry point WSGI
└── aluguel/
    ├── migrations/           # Migrações do banco de dados
    ├── static/
    │   ├── css/              # Estilos (style.css, painel.css)
    │   ├── js/               # Scripts (main.js, painel.js)
    │   └── img/              # Imagens estáticas
    ├── templates/
    │   └── aluguel/          # Templates HTML (index.html, painel.html)
    ├── admin.py              # Configuração do admin Django
    ├── api.py                # Endpoints da API REST
    ├── apps.py               # Configuração do app
    ├── models.py             # Modelos de dados
    ├── urls.py               # Rotas do app
    └── views.py              # Views tradicionais
```

---

## 🗃️ Modelo de Dados

| Entidade | Propósito | Campos Principais |
|---|---|---|
| **Carrinho** | Gerencia a frota disponível | `preco_diaria`, `status` |
| **Sorvete** | Cardápio de sabores | `nome_sorvete`, `preco`, `quantidade`, `imagem`, `ativo` |
| **Cliente** | Registro de locatários | `nome_cliente`, `telefone`, `email`, `endereco` |
| **Reserva** | Núcleo do sistema | `id_cliente`, `id_carrinho`, `data_evento`, `status`, `descricao` |
| **ReservaProduto** | Itens por reserva | `id_reserva`, `id_sorvete`, `quantidade_escolhida` |

---

## 🔌 API REST

### Autenticação

| Endpoint | Método | Descrição |
|---|---|---|
| `/api/auth/login/` | POST | Login de administrador |
| `/api/auth/logout/` | POST | Logout de administrador |
| `/api/auth/check/` | GET | Verifica sessão ativa |

### Endpoints

| Endpoint | Método | Descrição |
|---|---|---|
| `/api/sabores/` | GET | Lista sabores ativos (público) |
| `/api/disponibilidade/?mes=YYYY-MM` | GET | Ocupação diária do mês |
| `/api/reserva/criar/` | POST | Cria nova reserva |
| `/api/admin/sabores/` | GET/POST | CRUD de sabores (admin) |
| `/api/admin/sabores/<id>/` | POST | Edita sabor específico |
| `/api/reservas/` | GET/POST | Lista/Cria reservas (admin) |
| `/api/reservas/<id>/` | GET | Detalha reserva específica |
| `/api/reservas/<id>/status/` | POST | Altera status da reserva |
| `/api/clientes/` | GET/POST | Lista/Cria clientes |
| `/api/carrinhos/` | GET | Lista carrinhos disponíveis |

### Exemplo de Payload (Criar Reserva)

```json
{
  "nome": "João Silva",
  "telefone": "(11) 99999-8888",
  "endereco": "Rua das Flores, 123",
  "email": "joao@email.com",
  "descricao": "Evento de aniversário",
  "data": "2026-11-20",
  "quantidade_carrinhos": 2,
  "sabores": [
    { "id": 1, "qtd": 50 },
    { "id": 2, "qtd": 30 }
  ]
}
```

---

## ⚙️ Configuração

### Variáveis de Ambiente (.env)

| Variável | Descrição | Obrigatório |
|---|---|---|
| `SECRET_KEY` | Chave secreta do Django | ✅ |
| `DB_NAME` | Nome do banco de dados | ✅ |
| `DB_USER` | Usuário do MySQL | ✅ |
| `DB_PASSWORD` | Senha do MySQL | ✅ |
| `DB_HOST` | Host do MySQL | ✅ |
| `DB_PORT` | Porta do MySQL | ✅ |

### Configuração do `settings.py`

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST'),
        'PORT': config('DB_PORT'),
        'OPTIONS': {'charset': 'utf8mb4'},
    }
}

TIME_ZONE = 'America/Sao_Paulo'
LANGUAGE_CODE = 'pt-br'
```

---

## 🧪 Testes

O projeto inclui suíte de testes unitários para regras de negócio críticas:

```bash
# Executar todos os testes
python manage.py test

# Testes específicos de reserva
python manage.py test aluguel.tests.ReservaRegraDeNegocioTest
```

**Casos de teste cobertos:**
- ✅ Aluguel grátis acima de R$ 300
- ✅ Taxa aplicada abaixo de R$ 300
- ✅ Bloqueio de reservas com menos de 24h
- ✅ Baixa de estoque ao confirmar reserva
- ✅ Disponibilidade por data

---

## 📄 Licença

Este projeto está sob a licença **MIT**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

```text
Copyright (c) 2026 vinicius_monteiro

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 👨‍💻 Desenvolvedor/Autor

| Informação | Detalhe |
|---|---|
| **Desenvolvedor** | vinicius_monteiro |
| **GitHub** | [@DEV-iini](https://github.com/DEV-iini) |
| **Licença** | MIT |
| **Versão Atual** | 1.0.0 |

---

## 📞 Contato

Para dúvidas ou suporte técnico, entre em contato através do canal oficial da loja:

- **WhatsApp:** [(11) 4199-0035](https://wa.me/551141990035)
- **Localização:** Av. Henriqueta Mendes Guerra, 1330 – Loja 16-H, Centro, Barueri/SP
- **Instagram:** [@oggi.Barueri](https://www.instagram.com/oggi.Barueri)

---

<div align="center">

**Feito com dedicação para Oggi Sorvetes Barueri**  
*Aluguel de carrinhos de sorvete para festas e eventos*

</div>
