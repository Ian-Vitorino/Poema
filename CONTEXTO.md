# Contexto do Projeto — Site Romântico "Poema"

## Repositório e Ambiente
- **GitHub**: https://github.com/Ian-Vitorino/Poema
- **Diretório local**: `C:\Ian-vitorino\Nova pasta\Poema`
- **Branch**: `main`
- **Deploy**: Vercel conectado ao GitHub (push na main = deploy automático)
- **Dev server**: `npm run dev` → `npx serve . -l 7000`
- **Stack**: HTML/CSS/JS puro, sem frameworks

---

## Estrutura de Arquivos
```
Poema/
├── index.html          ← Página principal (poema animado + mensagem + ícones secretos)
├── galeria.html        ← Galeria de fotos com lightbox + foto oculta
├── poemas.html         ← Poemas página 1 (tema espaço/lua com partículas)
├── poemas2.html        ← Poemas página 2 (tema oceano com fundo do mar)
├── musicas.html        ← Template de músicas (6 cards vazios)
├── trechos.html        ← Template de trechos de letras (8 blocos vazios)
├── elogios.html        ← Template de elogios (8 accordion items com placeholder)
├── galaxia.html        ← Galáxia interativa (frases orbitando buraco negro)
├── combinacoes.txt     ← Lista das combinações secretas
├── TODO.md             ← Lista de pendências
├── CONTEXTO.md         ← Este arquivo
├── package.json        ← "dev": "npx serve . -l 7000"
├── galeria/            ← 7 fotos (6 galeria + 1 oculta)
├── Musicas/            ← 6 arquivos de áudio (.mpeg)
└── Fotos-musicas/      ← Imagens de capa das músicas
```

---

## Paleta de Cores
| Uso | Cor | Hex |
|---|---|---|
| Accent principal | Teal/verde-água | `#4ecdc4` |
| Background azul escuro | Fundo profundo | `#0a1628` |
| Background azul médio | Transição | `#0d2137` |
| Background verde escuro | Transição | `#0a2e1f` |
| Background verde | Superfície | `#0d1f15` |
| Texto claro | Corpo | `#c8dbe6` |
| Accent rgba | Bordas, glows | `rgba(78, 205, 196, ...)` |
| Roxo galáxia | Glow/brilho galáxia | `rgba(180, 120, 255, ...)` |

---

## Fontes (Google Fonts)
- **Dancing Script** (wght 400, 700) — títulos cursivos
- **Lora** (ital 400) — corpo em serif itálico

Import:
```html
<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Lora:ital,wght@0,400;1,400&display=swap" rel="stylesheet">
```

---

## Padrões de CSS Reutilizáveis

### Cards
```css
background: rgba(255, 255, 255, 0.03);
border: 1px solid rgba(78, 205, 196, 0.15);
border-radius: 20px;
padding: 40px 35px;
backdrop-filter: blur(10px);
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3), inset 0 0 80px rgba(78, 205, 196, 0.03);
```

### Títulos dos cards
```css
font-family: 'Dancing Script', cursive;
color: #4ecdc4;
font-size: 1.8rem;
text-align: center;
text-shadow: 0 0 20px rgba(78, 205, 196, 0.3);
```

### Texto dos cards
```css
font-family: 'Lora', serif;
color: #c8dbe6;
font-size: 1.05rem;
line-height: 2;
text-align: center;
font-style: italic;
```

### Separador entre título e texto
```html
<div class="separator">
  <span class="line"></span>
  <span class="heart">♥</span>
  <span class="line"></span>
</div>
```
```css
.separator { display: flex; align-items: center; justify-content: center; gap: 15px; margin-bottom: 20px; }
.separator .line { width: 40px; height: 1px; background: linear-gradient(90deg, transparent, #4ecdc4, transparent); }
.separator .heart { color: #4ecdc4; font-size: 0.7rem; }
```

### Botão voltar
```css
.back-btn {
  display: block;
  margin: 10px auto 0;
  background: rgba(78, 205, 196, 0.15);
  border: 1px solid rgba(78, 205, 196, 0.3);
  color: #4ecdc4;
  font-family: 'Lora', serif;
  font-size: 1.1rem;
  padding: 14px 40px;
  border-radius: 30px;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  text-align: center;
  width: fit-content;
}
.back-btn:hover { background: rgba(78, 205, 196, 0.25); transform: translateY(-2px); }
```

### Animações padrão
```css
@keyframes fadeDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes cardAppear { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
```
Cards usam delay incremental: `animation-delay: 0.2s, 0.4s, 0.6s...`

### Favicon (todas as páginas)
```html
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>⭐</text></svg>">
```

---

## Navegação Secreta (index.html)

3 ícones no footer da página principal: ☀️ Sol, ⭐ Estrela, 🌙 Lua

| Combinação | Destino |
|---|---|
| Sol, Lua, Sol, Sol, Estrela | Modal com confetes "Te amo meu amor" |
| Sol, Estrela, Estrela, Estrela, Lua | galeria.html |
| Sol, Sol, Lua | poemas.html |
| Sol, Lua, Sol, Lua, Estrela | musicas.html |
| Estrela, Estrela, Lua, Lua, Sol, Sol, Estrela, Sol, Lua | trechos.html |
| Estrela, Sol, Estrela, Lua, Estrela | elogios.html |
| Lua, Lua, Lua, Sol | galaxia.html |

Easter egg adicional: digitar "te amo" (sem espaço) na tela principal redireciona pra galeria.

---

## Estado de Cada Página

### ✅ index.html — Completa
- Poema animado verso a verso
- Card com mensagem pessoal
- Ícones secretos (Sol, Estrela, Lua) com sistema de sequência
- Modal com confetes
- Easter egg "te amo"

### ✅ galeria.html — Completa
- Grid 6 fotos da pasta `galeria/`
- Lightbox para ampliar
- Foto oculta com ícone 💕
- Texto "esse cara aqui te ama ó →" e "te amo tanto, fofinha ❤️"
- Título: "Minha Princesinha 💕"

### ✅ poemas.html — Completa
- Tema: espaço/lua com partículas CSS (dots, estrelas, luas, nebulosas)
- Poemas prontos: "Sol e Lua" (8 versos), "Fases da Lua" (4 poemas de 4 versos)
- Link "tem mais..." apontando pra poemas2.html
- Gradiente: azul no topo → verde embaixo (fixo)

### ✅ poemas2.html — Completa
- Tema: oceano/fundo do mar
- Gradiente: verde no topo → azul escuro embaixo (acompanha scroll)
- Decorações: fundo do mar com corais e algas (2 camadas), peixes nadando, tubarão com cardume, águas-vivas, submarino, bolhas subindo
- 5 poemas completos: "Mar Cristalino", "Infinidade do Horizonte" + 3 poemas curtos sem título

### ✅ musicas.html — Funcional
- 6 cards de música com player integrado
- Áudios na pasta `Musicas/` (6 arquivos .mpeg)
- Capas na pasta `Fotos-musicas/`
- Layout vertical estilo playlist com animação vinil

### ❌ trechos.html — Template vazio
- 8 blocos com trecho de letra + mensagem pessoal + divisores
- IntersectionObserver para scroll-reveal
- **Precisa**: selecionar 8 trechos, escrever 8 mensagens pessoais

### ❌ elogios.html — Template vazio
- 8 accordion items (só 1 abre por vez via JS)
- Itens: ✨ Sorriso, 👀 Olhos, 💋 Boca, 💇‍♀️ Cabelo, 💖 Personalidade, 😂 Risada, 🤗 Abraço, 🥰 Jeitinho
- Título: "Tudo Sobre Você 💕", subtítulo: "cada pedacinho seu é perfeito"
- **Precisa**: escrever texto personalizado para cada item

### ✅ galaxia.html — Completa
- Tema: espaço profundo (#020010) com paleta roxa
- **Animação de entrada**: estrelas vêm de fora da tela → formam coração → pulsam → implodem pro centro → flash + explosão massiva → galáxia aparece
- **Buraco negro central** com glow roxo permanente, disco de acreção rotativo
- **3 órbitas** com 9 frases reais orbitando (contra-rotação mantém texto horizontal)
- **Drag and drop**: elemento fantasma segue o mouse livremente, ao soltar volta animado pra órbita
- **Modal personalizado**: clique na frase abre modal com a frase como título + texto pessoal explicando o significado
- **Hover**: pausa a órbita da frase
- Estrelas de fundo (200) + partículas flutuantes roxas (15)
- Responsivo (media query 600px)
- **Frases preenchidas (9/9)**:
  1. "Isso só mostra que não somos galinhas"
  2. "Eu amo vocês dois"
  3. "Se você chegar primeiro, me espera pra gente explorar juntos"
  4. "Eu estou com você porque eu te amo, você me faz feliz, você é tão bom pra mim"
  5. "Eu nunca vivi isso"
  6. "Minha ficha caiu de que tá acontecendo tudo o que eu sempre quis"
  7. "Devia ter te dado mais beijinhos"
  8. "Eu me importo eu"
  9. "Me sinto segura com você. Você não é qualquer um"

---

## Pendências Gerais (TODO.md)
- [ ] Preencher trechos.html (8 trechos + 8 mensagens)
- [ ] Preencher elogios.html (8 textos personalizados)
- [ ] Revisar textos do index.html
- [ ] Push final e verificar deploy na Vercel

---

## Regras Importantes
- Todas as páginas têm link `← Voltar ao poema` → `index.html`
- Manter consistência visual: mesmos cards, fontes, separadores ♥, animações
- Gradiente do body varia por página mas sempre na paleta azul/verde escuro
- Galáxia usa paleta roxa diferenciada (#020010, rgba(180,120,255,...))
- Animações de entrada rápidas (~0.5s delay entre cards)
- Site é mobile-first com media query em `480px` (galáxia em `600px`)
- Não usar frameworks, tudo em HTML/CSS/JS puro
