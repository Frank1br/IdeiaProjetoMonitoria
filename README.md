# MVP - SISTEMA DE MONITORIA FATEC PG
## Plano Realista: 5 Semanas (28/Out - 06/Dez)

---

## 🎯 ESCOPO DO MVP

### **O QUE VAI TER (Realista)**
```
✅ Sistema web responsivo
✅ 3 tipos de usuário (Aluno, Monitor, Coordenador)
✅ Busca simples de monitores
✅ Sistema de agendamento
✅ Chat básico em tempo real
✅ Avaliações
✅ Dashboard simples
✅ Histórico de monitorias
```

### **O QUE NÃO VAI TER (Para depois)**
```
❌ Videochamada (use Google Meet externo)
❌ Whiteboard (use ferramentas externas)
❌ Gamificação (nice-to-have)
❌ IA/Machine Learning
❌ App mobile
❌ Monitorias gravadas
❌ Analytics avançado
```

---

## 📊 DIAGRAMA DE FUNCIONALIDADES - MVP

### **VISÃO GERAL SIMPLIFICADA**

```
┌─────────────────────────────────────────┐
│     SISTEMA DE MONITORIA - MVP          │
└─────────────────────────────────────────┘
                    │
        ┌───────────┼───────────┐
        │           │           │
   ┌────▼────┐ ┌────▼────┐ ┌───▼─────┐
   │  ALUNO  │ │ MONITOR │ │  COORD  │
   └────┬────┘ └────┬────┘ └────┬────┘
        │           │           │
   ┌────▼────┐ ┌────▼────┐ ┌───▼─────┐
   │ Buscar  │ │ Aceitar │ │ Aprovar │
   │ Monitor │ │ Pedidos │ │ Monitores│
   └────┬────┘ └────┬────┘ └────┬────┘
        │           │           │
   ┌────▼────┐ ┌────▼────┐ ┌───▼─────┐
   │ Agendar │ │ Atender │ │ Ver     │
   │ Sessão  │ │ Alunos  │ │ Relatos │
   └────┬────┘ └────┬────┘ └─────────┘
        │           │
   ┌────▼────┐ ┌────▼────┐
   │ Avaliar │ │Dashboard│
   └─────────┘ └─────────┘
```

---

## 🔧 FUNCIONALIDADES DETALHADAS (MVP)

### **MÓDULO 1: AUTENTICAÇÃO (Semana 1 - 2 dias)**

```
┌─────────────────────────────────────┐
│   AUTENTICAÇÃO BÁSICA               │
├─────────────────────────────────────┤
│                                     │
│  1.1 Cadastro                       │
│      └─ Formulário simples          │
│         ├─ Nome completo            │
│         ├─ Email (@fatec.sp.gov.br) │
│         ├─ Senha                    │
│         ├─ RA (se aluno)            │
│         └─ Tipo (aluno/monitor)     │
│                                     │
│  1.2 Login                          │
│      └─ Email + Senha               │
│                                     │
│  1.3 Recuperar Senha                │
│      └─ Link por email              │
│                                     │
│  1.4 Perfil Básico                  │
│      ├─ Editar nome/foto            │
│      └─ Trocar senha                │
│                                     │
└─────────────────────────────────────┘
```

**Tecnologias:**
- Frontend: React + Tailwind CSS
- Backend: Node.js + Express
- Auth: JWT (JSON Web Tokens)
- Banco: PostgreSQL

---

### **MÓDULO 2: GESTÃO DE MONITORES (Semana 1 - 3 dias)**

```
┌─────────────────────────────────────┐
│   CADASTRO DE MONITORES             │
├─────────────────────────────────────┤
│                                     │
│  2.1 Para Monitor:                  │
│      └─ Definir Disciplinas         │
│         └─ Checkbox das disciplinas │
│                                     │
│      └─ Definir Disponibilidade     │
│         └─ Horários simples         │
│            ├─ Segunda: 14h-18h      │
│            ├─ Quarta: 14h-18h       │
│            └─ Status: Online/Offline│
│                                     │
│  2.2 Para Coordenador:              │
│      └─ Aprovar/Reprovar Monitor    │
│         └─ Lista de candidatos      │
│                                     │
└─────────────────────────────────────┘
```

**Banco de Dados:**
```sql
usuarios (id, nome, email, senha_hash, tipo, foto_url)
monitores (id, usuario_id, status, disciplinas_json)
disponibilidade (monitor_id, dia_semana, hora_inicio, hora_fim)
```

---

### **MÓDULO 3: BUSCA DE MONITORES (Semana 2 - 2 dias)**

```
┌─────────────────────────────────────┐
│   BUSCA SIMPLES                     │
├─────────────────────────────────────┤
│                                     │
│  3.1 Tela de Busca                  │
│      ┌─────────────────────────┐   │
│      │ 🔍 Buscar por disciplina│   │
│      └─────────────────────────┘   │
│      [Banco de Dados III      ▼]   │
│                                     │
│  3.2 Lista de Monitores             │
│      ┌──────────────────────────┐  │
│      │ 👤 João Silva            │  │
│      │ 📘 Banco de Dados III    │  │
│      │ 🟢 Disponível agora      │  │
│      │ ⭐ 4.5 (23 avaliações)   │  │
│      │ [Solicitar Monitoria]    │  │
│      └──────────────────────────┘  │
│                                     │
│  3.3 Filtros Simples                │
│      ☐ Disponível agora             │
│      ☐ Melhor avaliados             │
│                                     │
└─────────────────────────────────────┘
```

**Funcionalidade:**
- SELECT simples no banco
- Ordenação por avaliação
- Filtro por disponibilidade (status online/offline)

---

### **MÓDULO 4: SOLICITAÇÃO E AGENDAMENTO (Semana 2 - 3 dias)**

```
┌─────────────────────────────────────┐
│   AGENDAMENTO SIMPLIFICADO          │
├─────────────────────────────────────┤
│                                     │
│  4.1 Solicitar Monitoria            │
│      ┌───────────────────────────┐ │
│      │ Monitor: João Silva       │ │
│      │ Disciplina: BD III        │ │
│      │                           │ │
│      │ Data: [28/11/2025]        │ │
│      │ Horário: [14:00 ▼]        │ │
│      │                           │ │
│      │ Modalidade:               │ │
│      │ ○ Presencial (Sala 203)   │ │
│      │ ● Remoto (Google Meet)    │ │
│      │                           │ │
│      │ Descreva sua dúvida:      │ │
│      │ [________________]        │ │
│      │                           │ │
│      │ [Enviar Solicitação]      │ │
│      └───────────────────────────┘ │
│                                     │
│  4.2 Para Monitor - Aceitar/Recusar │
│      ┌───────────────────────────┐ │
│      │ 🔔 Nova Solicitação       │ │
│      │ De: Pedro Costa           │ │
│      │ Quando: Hoje 16:00        │ │
│      │ Dúvida: "JOIN em SQL"     │ │
│      │                           │ │
│      │ [✅ Aceitar] [❌ Recusar] │ │
│      └───────────────────────────┘ │
│                                     │
│  4.3 Status da Solicitação          │
│      • Pendente (aguardando monitor)│
│      • Aceita (confirmada)          │
│      • Recusada (com motivo)        │
│      • Concluída                    │
│      • Cancelada                    │
│                                     │
└─────────────────────────────────────┘
```

**Banco:**
```sql
solicitacoes (
  id, aluno_id, monitor_id, disciplina_id,
  data_hora, modalidade, local, descricao_duvida,
  status, motivo_recusa, created_at
)
```

---

### **MÓDULO 5: CHAT BÁSICO (Semana 3 - 3 dias)**

```
┌─────────────────────────────────────┐
│   CHAT SIMPLES EM TEMPO REAL        │
├─────────────────────────────────────┤
│                                     │
│  5.1 Interface de Chat              │
│      ┌───────────────────────────┐ │
│      │ João Silva (Monitor) 14:30│ │
│      ├───────────────────────────┤ │
│      │                           │ │
│      │ Você: Não entendi JOINs   │ │
│      │       14:28               │ │
│      │                           │ │
│      │ João: Vou explicar!       │ │
│      │       14:30               │ │
│      │                           │ │
│      │ João: [código SQL aqui]   │ │
│      │       14:31               │ │
│      │                           │ │
│      ├───────────────────────────┤ │
│      │ [Digite mensagem...    ]  │ │
│      │ [📎] [Enviar]            │ │
│      └───────────────────────────┘ │
│                                     │
│  5.2 Funcionalidades                │
│      ✅ Mensagens de texto          │
│      ✅ Anexar arquivos (imgs/PDFs) │
│      ✅ Notificação de nova mensagem│
│      ❌ Chamada de vídeo (usar Meet)│
│                                     │
└─────────────────────────────────────┘
```

**Tecnologia:**
- Socket.io (WebSocket simples)
- Upload de arquivos: multer
- Storage: pasta local ou AWS S3 (básico)

**Banco:**
```sql
mensagens (
  id, solicitacao_id, usuario_id,
  conteudo, arquivo_url, created_at
)
```

---

### **MÓDULO 6: SESSÃO DE MONITORIA (Semana 3 - 2 dias)**

```
┌─────────────────────────────────────┐
│   GESTÃO DA SESSÃO                  │
├─────────────────────────────────────┤
│                                     │
│  6.1 Iniciar Monitoria              │
│      └─ Monitor clica "Iniciar"     │
│         └─ Registra hora início     │
│                                     │
│  6.2 Durante Monitoria              │
│      ├─ Chat ativo                  │
│      ├─ Link do Google Meet (manual)│
│      └─ Compartilhar arquivos       │
│                                     │
│  6.3 Finalizar Monitoria            │
│      └─ Monitor clica "Finalizar"   │
│         ├─ Registra hora fim        │
│         ├─ Duração automática       │
│         └─ Status → Concluída       │
│                                     │
└─────────────────────────────────────┘
```

**Banco:**
```sql
sessoes (
  id, solicitacao_id,
  data_inicio, data_fim, duracao_minutos,
  link_meet, observacoes, status
)
```

---

### **MÓDULO 7: AVALIAÇÃO (Semana 4 - 2 dias)**

```
┌─────────────────────────────────────┐
│   SISTEMA DE AVALIAÇÃO              │
├─────────────────────────────────────┤
│                                     │
│  7.1 Avaliar Monitor (após sessão)  │
│      ┌───────────────────────────┐ │
│      │ Como foi a monitoria?     │ │
│      │ ⭐⭐⭐⭐⭐               │ │
│      │                           │ │
│      │ Sua dúvida foi resolvida? │ │
│      │ ● Sim                     │ │
│      │ ○ Parcialmente            │ │
│      │ ○ Não                     │ │
│      │                           │ │
│      │ Comentário (opcional):    │ │
│      │ [_________________]       │ │
│      │                           │ │
│      │ [Enviar Avaliação]        │ │
│      └───────────────────────────┘ │
│                                     │
│  7.2 Cálculo de Média               │
│      └─ Média automática por monitor│
│                                     │
└─────────────────────────────────────┘
```

**Banco:**
```sql
avaliacoes (
  id, sessao_id, avaliador_id,
  nota, duvida_resolvida, comentario,
  created_at
)
```

---

### **MÓDULO 8: DASHBOARD (Semana 4 - 2 dias)**

```
┌─────────────────────────────────────┐
│   DASHBOARD BÁSICO                  │
├─────────────────────────────────────┤
│                                     │
│  8.1 Dashboard do Aluno             │
│      ┌───────────────────────────┐ │
│      │ Minhas Monitorias         │ │
│      ├───────────────────────────┤ │
│      │ Total: 5 monitorias       │ │
│      │ Avaliações: ⭐ 4.6 média  │ │
│      │                           │ │
│      │ Próximas:                 │ │
│      │ • Hoje 16h - BD3          │ │
│      │ • 30/11 14h - POO         │ │
│      │                           │ │
│      │ Histórico:                │ │
│      │ [Ver todas]               │ │
│      └───────────────────────────┘ │
│                                     │
│  8.2 Dashboard do Monitor           │
│      ┌───────────────────────────┐ │
│      │ Estatísticas              │ │
│      ├───────────────────────────┤ │
│      │ Atendimentos: 23          │ │
│      │ Avaliação: ⭐ 4.8         │ │
│      │ Horas: 18h30min           │ │
│      │                           │ │
│      │ Pendentes: 2              │ │
│      │ Próximas: 3               │ │
│      │                           │ │
│      │ [Gerenciar Horários]      │ │
│      └───────────────────────────┘ │
│                                     │
│  8.3 Dashboard do Coordenador       │
│      ┌───────────────────────────┐ │
│      │ Visão Geral               │ │
│      ├───────────────────────────┤ │
│      │ Monitores ativos: 12      │ │
│      │ Monitorias/mês: 89        │ │
│      │ Satisfação: ⭐ 4.5        │ │
│      │                           │ │
│      │ Disciplinas:              │ │
│      │ 1. BD III - 23 sessões    │ │
│      │ 2. POO - 18 sessões       │ │
│      │                           │ │
│      │ [Ver Relatório Completo]  │ │
│      └───────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

---

### **MÓDULO 9: NOTIFICAÇÕES (Semana 4 - 1 dia)**

```
┌─────────────────────────────────────┐
│   NOTIFICAÇÕES SIMPLES              │
├─────────────────────────────────────┤
│                                     │
│  9.1 Notificações In-App            │
│      ┌───────────────────────────┐ │
│      │ 🔔 3 novas                │ │
│      ├───────────────────────────┤ │
│      │ • João aceitou sua        │ │
│      │   solicitação (5min)      │ │
│      │                           │ │
│      │ • Monitoria em 15min      │ │
│      │   com Maria (15min)       │ │
│      │                           │ │
│      │ • Nova mensagem no chat   │ │
│      │   (2h)                    │ │
│      └───────────────────────────┘ │
│                                     │
│  9.2 Email (básico)                 │
│      ├─ Confirmação de agendamento  │
│      ├─ Lembrete (1h antes)         │
│      └─ Solicitação pendente        │
│                                     │
└─────────────────────────────────────┘
```

**Tecnologia:**
- In-app: Badge com contador
- Email: Nodemailer (SMTP simples)

---

### **MÓDULO 10: HISTÓRICO (Semana 5 - 1 dia)**

```
┌─────────────────────────────────────┐
│   HISTÓRICO                         │
├─────────────────────────────────────┤
│                                     │
│  10.1 Lista de Monitorias           │
│       ┌──────────────────────────┐ │
│       │ 28/11 - 16:00            │ │
│       │ BD III com João Silva    │ │
│       │ Duração: 1h30min         │ │
│       │ Avaliação: ⭐⭐⭐⭐⭐    │ │
│       │ [Ver Detalhes]           │ │
│       └──────────────────────────┘ │
│                                     │
│       ┌──────────────────────────┐ │
│       │ 25/11 - 14:00            │ │
│       │ POO com Maria Santos     │ │
│       │ Duração: 45min           │ │
│       │ Avaliação: ⭐⭐⭐⭐      │ │
│       │ [Ver Detalhes]           │ │
│       └──────────────────────────┘ │
│                                     │
│  10.2 Detalhes da Monitoria         │
│       ├─ Data/hora                  │
│       ├─ Participantes              │
│       ├─ Disciplina                 │
│       ├─ Descrição da dúvida        │
│       ├─ Chat completo              │
│       ├─ Arquivos compartilhados    │
│       └─ Avaliação                  │
│                                     │
└─────────────────────────────────────┘
```

---

### **MÓDULO 11: ADMINISTRAÇÃO (Semana 5 - 2 dias)**

```
┌─────────────────────────────────────┐
│   PAINEL ADMIN BÁSICO               │
├─────────────────────────────────────┤
│                                     │
│  11.1 Gerenciar Monitores           │
│       ├─ Aprovar candidatos         │
│       ├─ Desativar monitor          │
│       └─ Ver lista completa         │
│                                     │
│  11.2 Gerenciar Disciplinas         │
│       ├─ Adicionar nova             │
│       ├─ Editar existente           │
│       └─ Listar todas               │
│                                     │
│  11.3 Relatório Simples             │
│       ├─ Total de monitorias        │
│       ├─ Monitores ativos           │
│       ├─ Disciplinas mais procuradas│
│       └─ Satisfação média           │
│                                     │
└─────────────────────────────────────┘
```

---

## 📅 CRONOGRAMA DETALHADO (5 Semanas)

### **SEMANA 1 (28/Out - 03/Nov): Setup + Auth + Monitores**
```
Segunda-Terça:
  ✅ Setup do projeto (React + Node + PostgreSQL)
  ✅ Configurar banco de dados
  ✅ Estrutura de pastas
  ✅ Deploy inicial (Vercel + Railway/Render)

Quarta-Quinta:
  ✅ Sistema de autenticação
  ✅ Cadastro e login
  ✅ JWT tokens
  ✅ Middleware de proteção

Sexta-Domingo:
  ✅ Cadastro de monitores
  ✅ Definir disciplinas
  ✅ Disponibilidade simples
  ✅ Aprovação por coordenador
```

### **SEMANA 2 (04-10/Nov): Busca + Agendamento**
```
Segunda-Terça:
  ✅ Busca de monitores
  ✅ Filtros básicos
  ✅ Cards de monitores

Quarta-Sexta:
  ✅ Sistema de solicitação
  ✅ Formulário de agendamento
  ✅ Aceitar/recusar solicitação
  ✅ Status de solicitações

Sábado-Domingo:
  ✅ Testes de integração
  ✅ Ajustes de UI
```

### **SEMANA 3 (11-17/Nov): Chat + Sessões**
```
Segunda-Quarta:
  ✅ Chat em tempo real (Socket.io)
  ✅ Envio de mensagens
  ✅ Upload de arquivos

Quinta-Sexta:
  ✅ Gestão de sessões
  ✅ Iniciar/finalizar monitoria
  ✅ Registrar duração

Sábado-Domingo:
  ✅ Testes de chat
  ✅ Correções de bugs
```

### **SEMANA 4 (18-24/Nov): Avaliações + Dashboard**
```
Segunda-Terça:
  ✅ Sistema de avaliação
  ✅ Formulário de avaliação
  ✅ Cálculo de médias

Quarta-Quinta:
  ✅ Dashboard do aluno
  ✅ Dashboard do monitor
  ✅ Dashboard do coordenador

Sexta-Domingo:
  ✅ Notificações básicas
  ✅ Emails automáticos
```

### **SEMANA 5 (25/Nov - 01/Dez): Histórico + Admin + Polish**
```
Segunda:
  ✅ Histórico de monitorias
  ✅ Detalhes da monitoria

Terça-Quarta:
  ✅ Painel administrativo
  ✅ Relatórios básicos

Quinta-Sexta:
  ✅ Testes completos
  ✅ Correção de bugs
  ✅ Melhorias de UI/UX

Sábado-Domingo:
  ✅ Deploy final
  ✅ Documentação
  ✅ Apresentação
```

### **SEMANA 6 (02-06/Dez): Buffer + Apresentação**
```
Segunda-Quarta:
  ✅ Testes finais
  ✅ Ajustes de última hora
  ✅ Preparar apresentação

Quinta-Sexta:
  ✅ Ensaio de apresentação
  ✅ ENTREGA DO PROJETO
```

---

## 💾 MODELO DE DADOS SIMPLIFICADO (MVP)

```sql
-- TABELA 1: Usuários
usuarios (
  id UUID PRIMARY KEY,
  nome VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  senha_hash VARCHAR(255) NOT NULL,
  tipo ENUM('aluno', 'monitor', 'coordenador'),
  foto_url VARCHAR(500),
  ra VARCHAR(20), -- só para alunos
  status ENUM('ativo', 'inativo') DEFAULT 'ativo',
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 2: Monitores
monitores (
  id UUID PRIMARY KEY,
  usuario_id UUID REFERENCES usuarios(id),
  status ENUM('pendente', 'aprovado', 'reprovado') DEFAULT 'pendente',
  disciplinas JSON, -- ["BD3", "POO"]
  biografia TEXT,
  total_atendimentos INT DEFAULT 0,
  avaliacao_media DECIMAL(3,2),
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 3: Disponibilidade
disponibilidade (
  id UUID PRIMARY KEY,
  monitor_id UUID REFERENCES monitores(id),
  dia_semana INT, -- 0=dom, 1=seg, ...
  hora_inicio TIME,
  hora_fim TIME,
  ativo BOOLEAN DEFAULT TRUE
)

-- TABELA 4: Disciplinas
disciplinas (
  id UUID PRIMARY KEY,
  codigo VARCHAR(20) UNIQUE,
  nome VARCHAR(255) NOT NULL
)

-- TABELA 5: Solicitações
solicitacoes (
  id UUID PRIMARY KEY,
  aluno_id UUID REFERENCES usuarios(id),
  monitor_id UUID REFERENCES monitores(id),
  disciplina_id UUID REFERENCES disciplinas(id),
  data_hora TIMESTAMP NOT NULL,
  modalidade ENUM('presencial', 'remoto'),
  local VARCHAR(100),
  descricao_duvida TEXT,
  status ENUM('pendente', 'aceita', 'recusada', 'concluida', 'cancelada'),
  motivo_recusa TEXT,
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 6: Sessões
sessoes (
  id UUID PRIMARY KEY,
  solicitacao_id UUID REFERENCES solicitacoes(id),
  data_inicio TIMESTAMP,
  data_fim TIMESTAMP,
  duracao_minutos INT,
  link_meet VARCHAR(500),
  observacoes TEXT,
  status ENUM('agendada', 'em_andamento', 'concluida'),
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 7: Mensagens (Chat)
mensagens (
  id UUID PRIMARY KEY,
  solicitacao_id UUID REFERENCES solicitacoes(id),
  usuario_id UUID REFERENCES usuarios(id),
  conteudo TEXT,
  arquivo_url VARCHAR(500),
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 8: Avaliações
avaliacoes (
  id UUID PRIMARY KEY,
  sessao_id UUID REFERENCES sessoes(id),
  avaliador_id UUID REFERENCES usuarios(id),
  nota INT CHECK (nota >= 1 AND nota <= 5),
  duvida_resolvida BOOLEAN,
  comentario TEXT,
  created_at TIMESTAMP DEFAULT NOW()
)

-- TABELA 9: Notificações
notificacoes (
  id UUID PRIMARY KEY,
  usuario_id UUID REFERENCES usuarios(id),
  tipo VARCHAR(50),
  titulo VARCHAR(255),
  mensagem TEXT,
  lida BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
)
```

**Total: 9 tabelas (gerenciável!)**

---

## 🛠️ STACK TECNOLÓGICA

### **Frontend**
```
React 18
├── Vite (build tool)
├── React Router (navegação)
├── Tailwind CSS (estilização)
├── Axios (requisições HTTP)
├── Socket.io-client (chat)
├── React Hook Form (formulários)
└── date-fns (datas)
```

### **Backend**
```
Node.js 20
├── Express (servidor)
├── PostgreSQL (banco)
├── Prisma (ORM)
├── JWT (autenticação)
├── Socket.io (WebSocket)
├── Bcrypt (hash de senhas)
├── Nodemailer (emails)
└── Multer (upload de arquivos)
```

### **Deploy**
```
Frontend: Vercel (grátis)
Backend: Render ou Railway (grátis)
Banco: Neon.tech ou Supabase (grátis)
Files: Cloudinary (grátis, 25GB)
```

---

## ✅ CRITÉRIOS DE SUCESSO (MVP)

### **Funcional:**
- ✅ Aluno consegue encontrar monitor
- ✅ Aluno consegue agendar monitoria
- ✅ Monitor consegue aceitar/recusar
- ✅ Chat funciona em tempo real
- ✅ Sistema de avaliação funciona
- ✅ Histórico é registrado

### **Técnico:**
- ✅ Sistema responsivo (mobile ok)
- ✅ Autenticação segura (JWT)
- ✅ Banco normalizado (3FN)
- ✅ Deploy funcionando online
- ✅ Código no GitHub

### **Apresentação:**
- ✅ Documento ABNT completo
- ✅ Slides de apresentação
- ✅ Demo ao vivo funcionando
- ✅ Vídeo demonstrativo (backup)

---

## 🎯 PRIORIZAÇÃO

### **DEVE TER (P0):**
1. Autenticação
2. Cadastro de monitores
3. Busca de monitores
4. Agendamento
5. Chat básico
6. Avaliação

### **DEVERIA TER (P1):**
7. Dashboard
8. Notificações
9. Histórico
10. Email

### **BOM TER (P2):**
11. Painel admin
12. Relatórios
13. Upload de arquivos

---

## 📝 PRÓXIMOS PASSOS IMEDIATOS

1. **Definir equipe** (quantas pessoas?)
2. **Setup do ambiente** (instalar ferramentas)
3. **Criar repositório** no GitHub
4. **Definir responsabilidades** (quem faz o quê)
5. **Começar AMANHÃ** com autenticação

---

**Data de Entrega:** 06 de Dezembro de 2025  
**Tempo Disponível:** 5 semanas completas  
**Status:** VIÁVEL ✅

Quer que eu crie:
- [ ] Setup do projeto (package.json, estrutura)
- [ ] Schema do Prisma completo
- [ ] Exemplos de código (auth, CRUD)
- [ ] Documento ABNT formatado
