# ASPROMOVIMAR - Site Institucional

Site institucional da Associação de Moradores do Icaraí, desenvolvido para gerenciar ações sociais e eventos da comunidade.

## Sobre o Projeto

Este projeto foi desenvolvido para a ASPROMOVIMAR com o objetivo de facilitar a gestão de ações sociais, começando pela Ação Mesa Brasil em parceria com o Sesc. O sistema permite que moradores se cadastrem para receber benefícios e que administradores gerenciem esses cadastros.

### Fase Atual

Atualmente o projeto está focado na **Ação Mesa Brasil 2025**, que distribui colchões, travesseiros, lençóis e cobertores para famílias em situação de vulnerabilidade do bairro Icaraí.

## Tecnologias Utilizadas

### Backend
- **Node.js** - Runtime JavaScript
- **Express** - Framework web
- **UUID** - Geração de IDs únicos
- **Express Validator** - Validação de dados

### Frontend
- **HTML5** - Estrutura das páginas
- **CSS3** - Estilização (com CSS Variables)
- **JavaScript (ES6+)** - Interatividade

### Armazenamento (Fase Atual)
- **JSON** - Armazenamento temporário em arquivos
- Preparado para migração futura para banco de dados real

## Estrutura do Projeto

```
ASPROMOVIMAR/
├── src/
│   ├── api/
│   │   ├── controllers/        # Controladores da API
│   │   ├── routes/             # Rotas da API
│   │   └── middleware/         # Middlewares (autenticação, etc)
│   ├── services/               # Lógica de negócio
│   ├── data/                   # Camada de acesso a dados
│   ├── config/                 # Configurações
│   ├── utils/                  # Funções utilitárias
│   └── server.js               # Servidor principal
├── public/
│   ├── css/                    # Arquivos CSS
│   ├── js/                     # JavaScript do frontend
│   ├── index.html              # Página inicial
│   ├── cadastro.html           # Página de cadastro
│   └── admin.html              # Página administrativa
├── data/
│   └── beneficiarios.json      # Dados dos beneficiários (JSON)
├── package.json
└── README.md
```

## Funcionalidades

### Para Moradores
- Visualizar informações sobre a ação Mesa Brasil
- Realizar cadastro para receber benefícios
- Validação de CPF em tempo real
- Formulário com validações completas

### Para Administradores
- Login com autenticação Basic Auth
- Visualizar todos os cadastros
- Filtrar por nome, CPF e status
- Aprovar ou reprovar cadastros
- Ver detalhes completos de cada cadastro
- Exportar dados em CSV
- Dashboard com estatísticas (total, pendentes, aprovados, reprovados)

## API

### Rotas Públicas

#### POST /api/beneficiarios
Criar novo cadastro de beneficiário.

**Body:**
```json
{
  "nome_completo": "João da Silva",
  "cpf": "12345678900",
  "endereco": "Rua Exemplo, 123, Icaraí",
  "telefone": "21987654321",
  "numero_pessoas_residencia": 4,
  "situacao_atual": "Descreva sua situação...",
  "comprovante_residencia_url": "Descrição do comprovante",
  "email": "joao@email.com"
}
```

### Rotas Administrativas (Requer Autenticação)

#### GET /api/beneficiarios
Listar todos os beneficiários com filtros opcionais.

**Query Params:**
- `nome` - Filtrar por nome
- `cpf` - Filtrar por CPF
- `status_inscricao` - Filtrar por status (pendente, aprovado, reprovado)
- `acao` - Filtrar por ação

#### GET /api/beneficiarios/cpf/:cpf
Buscar beneficiário por CPF.

#### PUT /api/beneficiarios/:id
Atualizar cadastro de beneficiário.

**Body:**
```json
{
  "status_inscricao": "aprovado"
}
```

#### GET /api/beneficiarios/export/csv
Exportar beneficiários em CSV.

**Query Params:** Mesmos filtros do GET /api/beneficiarios

## Instalação e Execução

### Pré-requisitos
- Node.js (versão 14 ou superior)
- NPM ou Yarn

### Passo a Passo

1. Clone ou faça download do projeto

2. Instale as dependências:
```bash
npm install
```

3. Inicie o servidor:
```bash
npm start
```

Para desenvolvimento com auto-reload:
```bash
npm run dev
```

4. Acesse o sistema:
- Site: http://localhost:3000
- Cadastro: http://localhost:3000/cadastro
- Admin: http://localhost:3000/admin

## Credenciais de Acesso

### Painel Administrativo
- **Usuário:** admin
- **Senha:** aspromovimar2025

> **IMPORTANTE:** Em produção, altere essas credenciais no arquivo `src/config/config.js`

## Validações Implementadas

### Cadastro de Beneficiário
- Nome completo (mínimo 3 caracteres)
- CPF válido (validação de dígitos verificadores)
- CPF único (não permite duplicatas)
- Endereço (mínimo 5 caracteres)
- Telefone com DDD (10 ou 11 dígitos)
- Número de pessoas (mínimo 1, máximo 20)
- Situação atual (mínimo 10 caracteres)
- Email válido (opcional)

## Estrutura de Dados

### Objeto Beneficiário
```json
{
  "id": "uuid",
  "nome_completo": "string",
  "cpf": "string (apenas números)",
  "endereco": "string",
  "telefone": "string (apenas números)",
  "numero_pessoas_residencia": "number",
  "situacao_atual": "string",
  "comprovante_residencia_url": "string",
  "email": "string | null",
  "data_cadastro": "ISO string",
  "status_inscricao": "pendente | aprovado | reprovado",
  "acao": "Mesa Brasil 2025"
}
```

## Arquitetura e Boas Práticas

### Separação em Camadas
- **Presentation Layer (Frontend):** HTML, CSS, JavaScript
- **API Layer:** Routes e Controllers
- **Business Logic Layer:** Services
- **Data Access Layer:** Repository Pattern
- **Configuration:** Arquivos de configuração centralizados

### Benefícios da Arquitetura Atual
1. **Modularidade:** Cada camada tem responsabilidade única
2. **Escalabilidade:** Fácil adicionar novos recursos
3. **Manutenibilidade:** Código organizado e legível
4. **Testabilidade:** Camadas isoladas facilitam testes
5. **Migração Facilitada:** Data Access Layer isola o acesso aos dados

## Futuras Funcionalidades (Roadmap)

### Próximas Implementações
- [ ] Área do morador com login
- [ ] Sistema de notícias e comunicados
- [ ] Calendário de eventos
- [ ] Gestão de contribuições/mensalidades
- [ ] Upload de arquivos (comprovantes)
- [ ] Notificações por email/SMS
- [ ] Dashboard avançado com gráficos
- [ ] Histórico de ações anteriores
- [ ] Sistema de denúncias/sugestões
- [ ] Chat com administradores

### Melhorias Técnicas Planejadas
- [ ] Migração para banco de dados (PostgreSQL/MongoDB)
- [ ] Autenticação com JWT
- [ ] Testes automatizados (Jest)
- [ ] CI/CD com GitHub Actions
- [ ] Deploy em nuvem (Heroku/Vercel)
- [ ] PWA (Progressive Web App)
- [ ] API com rate limiting
- [ ] Logs estruturados
- [ ] Monitoramento e métricas

## Migração para Banco de Dados

O projeto está preparado para migração futura. Consulte o arquivo [MIGRATION.md](./MIGRATION.md) para instruções detalhadas sobre como migrar do armazenamento JSON para um banco de dados real.

## Segurança

### Implementações Atuais
- Validação de entrada em todas as rotas
- Sanitização de dados
- Autenticação Basic Auth para rotas administrativas
- Validação de CPF único
- CORS configurado

### Recomendações para Produção
- Implementar HTTPS
- Usar variáveis de ambiente para credenciais
- Implementar rate limiting
- Adicionar logs de auditoria
- Usar JWT ao invés de Basic Auth
- Implementar CSP (Content Security Policy)
- Adicionar proteção contra CSRF

## Suporte e Manutenção

### Logs
Os logs do servidor são exibidos no console. Em produção, recomenda-se:
- Usar um sistema de logs estruturado (Winston, Pino)
- Armazenar logs em arquivos ou serviços externos
- Implementar monitoramento e alertas

### Backup
Como os dados estão em JSON:
- Fazer backup regular do arquivo `data/beneficiarios.json`
- Versionar backups com timestamp
- Armazenar em local seguro

## Contribuindo

Para contribuir com o projeto:
1. Mantenha o padrão de código existente
2. Documente novas funcionalidades
3. Teste antes de enviar alterações
4. Use commits descritivos

## Licença

Projeto desenvolvido para ASPROMOVIMAR - Associação de Moradores do Icaraí.

## Contato

Para mais informações sobre o projeto ou sobre a ASPROMOVIMAR, entre em contato através dos canais oficiais da associação.

---

**Desenvolvido para a comunidade de Icaraí**
