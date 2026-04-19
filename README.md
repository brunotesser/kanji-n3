# 2026appnihongo

Aplicativo iOS para estudo de japonês JLPT N3/N4/N5 com sistema SRS (Spaced Repetition System).  
Desenvolvido com Capacitor v8 + HTML/CSS/JS puro, sem frameworks externos.

---

## Stack

- **Frontend**: HTML + CSS + JavaScript puro (single-file app em `www/index.html`)
- **iOS wrapper**: Capacitor v8.3.1
- **Dados**: Arrays e objetos JS embutidos no app (sem backend, 100% offline)
- **Build**: Xcode via `npx cap sync ios`

---

## Estrutura do projeto

```
2026kanji-app/
├── www/
│   ├── index.html      # App completo (~303KB após split)
│   ├── vocab-db.js     # VOCAB_DB separado (~192KB, 2113+ entradas)
│   └── images/         # Assets
├── ios/                # Projeto Xcode gerado pelo Capacitor
├── capacitor.config.json
└── package.json
```

---

## Bases de dados

### RADICAL_DB
- Radicais japoneses com significado, leituras e mnemônicos visuais
- Campos: `id`, `char`, `read`, `mean`, `mnemonic`

### KANJI_DB
- Kanjis N5/N4/N3 com radicais componentes e vocabulário vinculado
- Campos: `char`, `read[]`, `mean`, `radicals[]`, `vocab[]`
- Mnemônicos de pronúncia em `KANJI_SOUND_MNEMONICS`
- Mnemônicos de significado em `KANJI_MNEMONICS`

### VOCAB_DB (`www/vocab-db.js`)
- **2113 entradas** de vocabulário JLPT N3 (Nihongo no Mori)
- IDs: `v1` – `v2113` + patches `v9001`–`v9005`
- Campos: `id`, `word`, `read`, `mean`
- Categorias cobertas:
  - 名詞（テーマ別）— substantivos temáticos
  - カタカナ語 — palavras em katakana
  - 接続詞 — conjunções (17 itens)
  - 接尾語 — sufixos (187 itens)
  - 接頭語 — prefixos (30 itens)
  - 慣用表現 — expressões idiomáticas (28 itens)
  - 敬語表現 — linguagem formal/keigo (47 itens)
  - 数え方 — contadores (39 itens)
  - 動詞（一般）— verbos gerais (290 itens)
  - い形容詞 / な形容詞 — adjetivos

### VOCAB_SENTENCES
- Frases de exemplo em japonês com furigana e tradução em PT-BR
- Keyed por `word` (ex: `VOCAB_SENTENCES['安心']`)

---

## Sistema SRS

Implementação própria de Spaced Repetition para três tipos de item:

| Tipo | Função lessons | Função reviews |
|------|---------------|----------------|
| Radical | `getRadicalLessons()` | `getRadicalReviews()` |
| Kanji | `getKanjiLessons()` | `getKanjiReviews()` |
| Vocab | `getVocabLessons()` | `getVocabReviews()` |

Estado salvo em `localStorage`:
- `ks_<char>` — estado de kanji (`{learned, srs, nextReview, mnemonic}`)
- `rs_<id>` — estado de radical
- `vs_<id>` — estado de vocab

### Fluxo de desbloqueio
- Radicais desbloqueiam Kanji
- Kanji desbloqueiam Vocab (via `VOCAB_PARENT_MAP`)

```js
// VOCAB_PARENT_MAP — lookup O(1) para isVocabUnlocked
const VOCAB_PARENT_MAP = new Map();
KANJI_DB.forEach(k => k.vocab.forEach(vid => VOCAB_PARENT_MAP.set(vid, k.char)));
```

---

## Tela inicial (Home)

- **Streak bar** — dias consecutivos de estudo
- **Hero button** — botão principal que mostra a ação prioritária:
  - `↺ Revisar (N)` — quando há reviews pendentes (cor: dourado)
  - `＋ Aprender (N)` — quando há lições novas (cor: gradiente)
  - `✓ Tudo em dia` — quando não há nada pendente
- **Stats row** — cards de radicais / kanji / vocab disponíveis
- **Browse panels** — abas para navegar todo o conteúdo

```js
function heroAction() {
  const rRev = getRadicalReviews().length + getKanjiReviews().length + getVocabReviews().length;
  const allLes = getRadicalLessons().length + getKanjiLessons().length + getVocabLessons().length;
  if (rRev > 0) startAllReviews();
  else if (allLes > 0) startLessonType('all');
}
```

---

## Cards de lição (vocab)

Três passos por item:

1. **Passo 0** — Mostra o kanji/palavra, usuário tenta lembrar
2. **Passo 1** — Revela leitura (furigana) + significado
3. **Passo 2** — Frases de exemplo (de `VOCAB_SENTENCES`) + mnemônico gerado por IA

### Geração de mnemônico por IA

```js
async function generateVocabMn(vocabId) {
  // Chama Anthropic API claude-haiku
  // Salva resultado em state.vocab[vocabId].mnemonic
  // Persiste no localStorage via vs_<id>
}
```

---

## Cards de review (vocab)

Após o usuário responder, exibe:
- Frase de exemplo do `VOCAB_SENTENCES` (se disponível)
- Mnemônico salvo (se existir)

---

## Otimizações de performance iOS

### Problema
O iOS WebView (WKWebView) tem um timeout de 3 segundos para processar eventos de toque. Scripts inline grandes causam o erro:
```
Result accumulator timeout: 3.000000, exceeded
```

### Soluções aplicadas

1. **Split do VOCAB_DB** — movido de `index.html` para `www/vocab-db.js` (arquivo separado)
   - Script inline: 495KB → 303KB
   - `<script src="vocab-db.js"></script>` carregado antes do script principal

2. **VOCAB_PARENT_MAP** — substituiu `KANJI_DB.find()` O(n²) por Map O(1)

3. **Paginação do vocab** — `renderVocab()` renderiza 80 itens por vez com botão "Ver mais"

4. **Init diferida** — `updateCounts()` roda após `requestAnimationFrame + setTimeout(50ms)`

5. **Removido `overflow:hidden`** do container `#home` — bug iOS WebKit que bloqueia propagação de touch events em flex containers

---

## Build e deploy

```bash
# Instalar dependências
npm install

# Sincronizar com iOS após alterar www/
npx cap sync ios

# Abrir no Xcode
npx cap open ios
```

Depois: **Xcode → Product → Run** (⌘R) no dispositivo físico.

---

## Variáveis de ambiente

Nenhuma variável de ambiente necessária para o app funcionar offline.  
A geração de mnemônicos por IA usa a Anthropic API — a chave é inserida diretamente na função `generateVocabMn` no `index.html`.

---

## Fontes dos dados

- Vocabulário N3: [Nihongo no Mori — JLPT N3](https://www.youtube.com/@nihongonomori2013)
- Radicais e Kanji: compilação própria baseada em N5/N4/N3
