# Ser — servidor e primeira interface web

Aplicação inicial para cadastro de voluntários, disponibilidade, escalas e envio de lembretes pelo WhatsApp Cloud API. Inclui uma interface web mínima em `public/` e a ponte opcional para o Holyrics.

## Requisitos

- Node.js 20 ou superior (recomendado Node 22 LTS)
- npm
- Para login por WhatsApp: conta Meta Business, WhatsApp Cloud API configurada e modelos aprovados
- Para hospedagem: disco persistente para `ser.db` e `uploads/`

## Executar localmente

1. Extraia o ZIP e abra um terminal dentro da pasta `ser-servidor`.
2. Crie seu arquivo de ambiente copiando `.env.example` para `.env`.
   - Windows PowerShell: `Copy-Item .env.example .env`
   - macOS/Linux: `cp .env.example .env`
3. Edite `.env`: defina um `APP_SECRET` longo e aleatório, `BRIDGE_KEY` e as credenciais da Meta. Nunca publique o arquivo `.env`.
4. Instale as dependências: `npm install`
5. Verifique a sintaxe: `npm run check`
6. Inicie: `npm start`
7. Abra `http://localhost:3000` no navegador.

O banco SQLite (`ser.db`) e os arquivos enviados (`uploads/`) serão criados automaticamente. Faça backup e use armazenamento persistente em hospedagem.

## Primeiro acesso

O primeiro cadastro vira administrador. Configure os modelos de mensagem na Meta antes de tentar login ou cadastro operacional:

- `codigo_login` (autenticação, idioma `pt_BR`): `Seu código de acesso ao Ser é {{1}}. Ele vale por 10 minutos.`
- `lembrete_escala` (utilitário, idioma `pt_BR`): `Olá, {{1}}! {{2}} você serve em {{3}} como {{4}}. Observação do líder: {{5}}`

O formato e a categoria dos modelos devem ser aprovados pela Meta. O token e o ID do número ficam em `WA_TOKEN` e `WA_PHONE_ID` no `.env`.

## Integração opcional com Holyrics

No computador do culto, copie `.env.ponte.example` para `.env.ponte`, configure `SER_URL`, a mesma `BRIDGE_KEY` do servidor e `HOLYRICS_MEDIA_DIR`. Na pasta do servidor, rode `npm run start:bridge` depois de instalar as dependências. A pasta configurada precisa ser acessível pelo usuário que executa a ponte.

## Publicar no GitHub

Antes de enviar, confira que `.env`, `ser.db`, `uploads/` e credenciais não serão publicados. Depois:

```bash
git init
git add .
git status
git commit -m "feat: primeira versão do Ser"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/ser-app.git
git push -u origin main
```

O GitHub armazena o código, mas não mantém o servidor rodando sozinho. Para uso fora do computador local, publique em um serviço de hospedagem Node.js com HTTPS e disco persistente; configure as variáveis de ambiente no painel do serviço.

## Escopo desta versão e próximos passos

Esta é uma base funcional inicial, não uma versão pronta para uso público sem testes. A interface cobre cadastro, login, disponibilidade, consulta de escalas, lista da equipe e montagem/publicação de escalas. Ainda precisam ser implementados/testados: reuniões e sugestões, gestão de mídia completa na interface, recuperação/limite de tentativas de OTP, política de privacidade/consentimento LGPD, testes automatizados e estratégia de backup/monitoramento. O fluxo de escala só aceita pessoas que marcaram disponibilidade e cujo ministério corresponde ao cargo.

**Segurança:** o primeiro cadastro público vira administrador; por isso, faça o primeiro cadastro em ambiente privado antes de disponibilizar o endereço publicamente. Para produção, restrinja o cadastro inicial e adicione limites de tentativas de login. Não use dados reais de membros até revisar a segurança e a privacidade.
