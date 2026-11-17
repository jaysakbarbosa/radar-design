# Radar Design 💅

Bot do Telegram que avisa, toda semana, eventos, prêmios, chamadas de palestrantes, bolsas e workshops de design, sempre com cidade, país e datas. Cinco áreas, cada uma em seção própria:

🎨 Design gráfico · 📱 Design de produto digital (UI/UX) · 📦 Design de produto (geral) · 🪑 Design de móveis · 🎬 Motion design

Busca em português e inglês, com eventos brasileiros e internacionais. Tipos: 🏆 prêmio/concurso · 🎟 evento · 🎤 chamada · 🎁 bolsa · 🧩 workshop. Roda de graça no GitHub Actions (sábado 12h de Natal: varredura completa; outros dias: lembretes; a cada 3h: seus comandos).

## Passo a passo (pelo celular ou computador)

1. **Telegram:** fale com @BotFather → `/newbot` → escolha nome e usuário (termina com `bot`). Guarde o token só para você.
2. **Abra o seu bot novo** e mande `/start`.
3. **GitHub:** crie um repositório novo `radar-design` e suba estes arquivos: `bot.py`, `config.json`, `README.md` e `.github/workflows/radar.yml`.
4. **Secrets** (Settings → Secrets and variables → Actions → New repository secret):
   - `TELEGRAM_BOT_TOKEN`: o token do bot NOVO
   - `TELEGRAM_CHAT_ID`: o mesmo número do Radar Congressos (seu chat é o mesmo)
   - `GROQ_API_KEY` e `TAVILY_API_KEY`: as mesmas chaves que você já usa
5. **Teste:** Actions → Radar Design → Run workflow → mode `full`. Rode uma vez só e não cancele.

## Comandos
`/eventos` · `/inscrevi 12` · `/vou 12` · `/minhas` · `/agenda` · `/ignorar 12` · `/status S1 aceito` · `/data S1 Resultado 2027-08-20` · `/local S1 Milão, Itália` · `/evento S1 2027-12-07` · `/remover S1` · `/ajuda`

## Observações
- Os dois bots dividem a cota diária de tokens do Groq. Por isso este roda no sábado e o Radar Congressos na sexta.
- Confira sempre o prazo no link antes de se planejar: o bot lê a web com IA e pode errar.
- Para mudar áreas, temas ou eventos vigiados, edite `config.json`.
