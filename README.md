# App Ser - Documentação do Servidor & Repositório GitHub

O **Ser** é um aplicativo móvel e web desenvolvido para simplificar a gestão de escalas, disponibilidades, reuniões e fluxo de mídias para os ministérios de **Follow** (Projeção, Fotografia, Vídeo, Story), **Sonoplastia** e **Iluminação** de igrejas.

---

## 🎨 Identidade Visual (Brand Kit)

- **Nome da Aplicação:** Ser
- **Slogan / Conceito:** *"Aquele que quer ser o maior, seja o que serve."*
- **Símbolo:** A Bacia e a Toalha de Lava-Pés (João 13), representando o serviço cristão com uma cruz sutil ao centro.
- **Tipografia:** `Plus Jakarta Sans` (Títulos e Destaques) e `Inter` (Corpo de Texto).

### Paleta de Cores
- **Cor Primária (Azul Noturno):** `#0F172A` (Fundo Sóbrio e Institucional)
- **Acento Principal (Dourado Champanhe):** `#D4AF37` (Destaques, Badges e Botões Primários)
- **Sucesso / Confirmação (Verde Esmeralda):** `#10B981` (Status de Disponível/Confirmado)
- **Fundo / Neutro Claro (Cinza Suave):** `#E2E8F0` (Bordas e Subtítulos)

---

## ⚙️ Regras de Negócio e Funcionalidades

### 1. Autenticação e Perfis
- **Acesso Simplificado:** Autenticação via número de WhatsApp cadastrado (código OTP de 6 dígitos via Meta Cloud API).
- **Perfis de Usuário:**
  - `admin` (ADM): Acesso total; define cargos e atribuições.
  - `lider`: Seleciona membros nas escalas, finaliza a escala, cria eventos e reuniões.
  - `pastor`: Acompanha escalas, sugestões e reuniões (sem editar escalas).
  - `member`: Declara disponibilidade de datas, visualiza a escala finalizada e envia mídias/sugestões.

### 2. Ministérios e Cargos Atendidos
- **Follow:** Projeção, Fotografia, Vídeo, Story
- **Sonoplastia:** Técnico de Som
- **Iluminação:** Técnico de Iluminação

### 3. Montagem Inteligente de Escala
- **Filtro Automático:** Ao criar a escala para um dia, o sistema exibe apenas os voluntários que declararam disponibilidade.
- **Notificações via WhatsApp:** Envio automático de lembretes obrigatoriamente **1 dia antes (D-1 às 09h)** e **no dia do culto (D0 às 07h)**.

---

## 🚀 Como Executar o Servidor

1. **Instalar Dependências:**
   ```bash
   npm install
   ```

2. **Configurar Variáveis de Ambiente:**
   Copie `.env.example` para `.env` e preencha as chaves:
   ```env
   PORT=3000
   TZ=America/Sao_Paulo
   APP_SECRET=sua-chave-secreta-longa
   WA_TOKEN=seu-token-meta
   WA_PHONE_ID=seu-id-telefone-meta
   BRIDGE_KEY=sua-chave-ponte-holyrics
   ```

3. **Iniciar o Servidor:**
   ```bash
   npm start
   ```

---

## 🛠️ Publicação e Deploy no GitHub

Para enviar as atualizações ao GitHub, execute no terminal do projeto:

```bash
git init
git add .
git commit -m "feat: configuracao inicial e correcoes do servidor App Ser"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/ser-app.git
git push -u origin main
```
