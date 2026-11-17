# Radar Design 💅

Bot do Telegram que avisa, toda semana, eventos, prêmios, chamadas de palestrantes, bolsas e workshops de design, sempre com **cidade, país e datas**. Busca em português e inglês, com eventos brasileiros e internacionais.

Cinco áreas, cada uma em uma seção própria da mensagem:

| Área | Seção |
|---|---|
| 🎨 | Design gráfico |
| 📱 | Design de produto digital (UI/UX) |
| 📦 | Design de produto (geral) |
| 🪑 | Design de móveis |
| 🎬 | Motion design |

Tipos de item:

| Ícone | Tipo | Exemplos |
|---|---|---|
| 🏆 | Prêmio ou concurso | Red Dot, iF, Pentawards, Prêmio Design Museu da Casa Brasileira |
| 🎟 | Evento | Config, Salone del Mobile, OFFF, Rio2C |
| 🎤 | Chamada | Chamada de palestrantes, propostas ou expositores |
| 🎁 | Bolsa | Bolsas, residências, estágios |
| 🧩 | Workshop | Workshops e cursos com inscrição |

Quando é um item importante (Awwwards, Red Dot, Salone, Annecy etc.), aparece com ⭐.

---

## Instalação, passo a passo (celular ou computador)

1. **Crie o bot no Telegram.** Fale com @BotFather → `/newbot` → escolha o nome e o usuário (precisa terminar com `bot`). Ele mostra um **token**. Guarde só para você e nunca mande print com ele.
2. **Abra o seu bot novo** e mande `/start`. Sem isso o bot não consegue falar com você.
3. **Crie o repositório no GitHub** com o nome `radar-design` e suba os arquivos:
   - `bot.py`
   - `config.json`
   - `README.md`
   - `.github/workflows/radar.yml` (crie com **Add file → Create new file** e digite o caminho completo no nome; as pastas são criadas sozinhas)
4. **Cadastre os secrets** em Settings → Secrets and variables → Actions → New repository secret:

   | Nome | Valor |
   |---|---|
   | `TELEGRAM_BOT_TOKEN` | o token do bot novo |
   | `TELEGRAM_CHAT_ID` | o número do chat de quem vai usar o bot |
   | `GROQ_API_KEY` | chave do Groq (console.groq.com) |
   | `TAVILY_API_KEY` | chave da Tavily (tavily.com) |

5. **Descubra o `TELEGRAM_CHAT_ID`:** quem vai usar o bot manda `/start` para ele. Depois abra no navegador `https://api.telegram.org/botSEU_TOKEN/getUpdates` (troque `SEU_TOKEN` pelo token) e copie o número que vem depois de `"chat":{"id":`.
6. **Primeiro teste:** aba **Actions** → **Radar Design** → **Run workflow** → mode `full`. Rode **uma vez só** e **não cancele**. Leva uns 15 a 20 minutos. No fim a mensagem chega no Telegram.

Se a aba Actions estiver vazia, o `radar.yml` não está em `.github/workflows/radar.yml`. Confira o caminho.

---

## Quando o bot fala com você

| Quando | O que acontece |
|---|---|
| **Sexta, 16h (Natal)** | Varredura completa na web. Manda os itens novos, separados por área |
| **Todos os outros dias, 12h** | Lembretes: avisa prazos que estão perto e datas das suas inscrições |
| **A cada 3 horas** | Lê os comandos que você mandou e responde |

Por causa desse intervalo, **a resposta aos comandos pode levar até ~3 horas**. O bot não responde na hora.

Os lembretes saem **14, 7 e 2 dias antes** de cada data, e **no dia**. O bot só avisa cada item uma vez em cada marco.

---

## Como ler a mensagem

Cada item aparece assim:

```
⭐ 🏆 #5 Pentawards 2027 · prêmio · 💸 ~€ 300
📍 online  🗓 data a confirmar
⏳ prazo 15/01/2027 · faltam 59 dias · link
```

- `#5` é o **número do item**. É ele que você usa nos comandos.
- 📍 é onde acontece e 🗓 é a data do evento. Se o bot não achou, aparece "a confirmar".
- ⏳ é o prazo de inscrição, envio ou chamada, e quantos dias faltam.
- 💸 mostra o valor da inscrição, quando o bot encontra.
- `link` abre a página oficial. **Sempre confira o prazo no link**: o bot lê a web com IA e pode errar.

---

## Comandos

Mande os comandos como mensagem normal no chat com o bot.

### Ver o que está aberto

**`/eventos`**
Lista todos os itens abertos, com número, prazo e cidade. Use para achar o número que vai nos outros comandos.

**`/ajuda`** (ou `/start`)
Mostra a lista de comandos.

### Marcar o que você vai fazer

**`/inscrevi 12`**
Registra que você se inscreveu no item #12 (enviou trabalho, comprou ingresso, entrou no concurso). O bot cria um registro `S1`, `S2`… e passa a lembrar das datas importantes: resultado, finalistas, envio final e o próprio evento.
- Também aceita um item que não está na lista: `/inscrevi Nome do evento`.
- Depois de registrar, **confira as datas no site oficial**. Se o bot não achar alguma, adicione com `/data`.

**`/vou 12`**
Marca que você vai participar do evento #12. Ele entra na sua `/agenda` e o bot lembra da data.
- Também aceita um evento fora da lista: `/vou Nome do evento`.
- Se faltar cidade ou data, o bot te diz qual comando usar (`/local` ou `/evento`).

**`/ignorar 12`**
Esconde o item #12 e não avisa mais dele. Use para o que não te interessa ou para itens que o bot errou.

### Acompanhar suas inscrições

**`/minhas`**
Mostra todas as suas inscrições e eventos marcados (`S1`, `S2`…), com cidade, datas e quantos dias faltam.

**`/agenda`**
Sua turnê: os eventos que você vai e onde se inscreveu, com **cidade e data**, em ordem de data. ✈️

**`/status S1 aceito`**
Atualiza uma inscrição. Os status são:
- `revisao`: em análise
- `aceito`: aprovada, selecionada ou finalista
- `rejeitado`: não passou
- `retirado`: você desistiu

Inscrições `rejeitado` e `retirado` deixam de gerar lembretes.

**`/data S1 Resultado 2027-08-20`**
Adiciona ou corrige uma data da inscrição `S1`. O formato é `/data S1 nome-da-data AAAA-MM-DD`. Datas que você coloca na mão **não são sobrescritas** pela busca automática.

**`/local S1 Milão, Itália`**
Guarda a cidade e o país do evento da inscrição `S1`.

**`/evento S1 2027-04-13 2027-04-19`**
Guarda as datas do evento: início e, se quiser, o fim. O fim é opcional.

**`/remover S1`**
Apaga o registro `S1`.

---

## Exemplo de uso do começo ao fim

1. Sexta chega a mensagem. Você vê `#5 Pentawards 2027` e quer participar.
2. Você manda `/inscrevi 5`. O bot registra como `S1` e responde com as datas que achou.
3. Ele não achou a data do resultado. Você confere no site e manda `/data S1 Resultado 2027-03-15`.
4. Nos dias 14, 7 e 2 antes dessa data, e no dia, o bot te avisa.
5. Saiu o resultado e você passou: `/status S1 aceito`.
6. Você vai ao evento de entrega: `/local S1 Londres, Reino Unido` e `/evento S1 2027-05-20`. Ele aparece na `/agenda`.
7. Um evento da lista que não interessa: `/ignorar 9`.

---

## Personalizar

Tudo fica no `config.json`:
- `areas`: as 5 áreas, com temas em inglês (`themes`), temas em português (`pt_themes`) e eventos vigiados (`watchlist` e `watchlist_br`). Para vigiar um evento ou prêmio novo, é só adicionar o nome na lista da área.
- `horizon_days`: quantos dias à frente o bot olha (padrão 365).
- `reminder_days`: dias antes do prazo em que o bot lembra (padrão 14, 7 e 2).
- `priority_keywords`: nomes que ganham a ⭐.

## Observações

- **Não rode a varredura várias vezes no mesmo dia.** Isso gasta a cota à toa. Os lembretes e os comandos funcionam sozinhos.
- **Confira sempre o prazo no link** antes de se planejar. O bot lê a web com IA e às vezes erra datas ou deixa algo passar.

