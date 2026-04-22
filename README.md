# ☢️ ROBCO INSTALINK v2.3.1
### *Social Network Reconnaissance Terminal*

> **"War never changes... but seus seguidores, sim."**

Uma ferramenta web com estética de terminal retrô inspirada no universo **Fallout / hacker dos anos 80** para analisar seus seguidores e seguindo do Instagram — tudo processado localmente, sem enviar nenhum dado para servidores externos.

---

## 📸 Preview

```
┌─ MARKS INDUSTRIES (TM) TERMLINK PROTOCOL ─────────────────────────┐

  FollowTrack v2.3.1
  // SOCIAL NETWORK RECONNAISSANCE TERMINAL — AUTHORIZED USE ONLY //

  USER: VAULT_DWELLER   CLEARANCE: LEVEL 5   STATUS: RECON COMPLETE
```

---

## ✨ Funcionalidades

- **Não te seguem de volta** — lista todos que você segue mas não te seguem de volta
- **Você não segue de volta** — quem te segue mas você não segue
- **Mútuos** — seguidores recíprocos dos dois lados
- **Busca em tempo real** dentro de cada lista
- **Link direto** para o perfil de cada usuário no Instagram
- **Threat Level** automático baseado na quantidade de não-recíprocos
- **100% local** — nenhum dado sai do seu navegador

---

## 🚀 Como usar

### 1. Exporte seus dados do Instagram

1. Abra o Instagram e vá em **Configurações → Centro de Contas**
2. Acesse **Suas informações e permissões → Baixar suas informações**
3. Selecione o formato **JSON** e solicite o download
4. Aguarde o e-mail com o link (pode levar algumas horas)
5. Baixe e extraia o arquivo `.ZIP`

### 2. Localize os arquivos

Dentro do ZIP extraído, navegue até a pasta:

```
connections/
└── followers_and_following/
    ├── followers_1.json   ← quem te segue
    └── following.json     ← quem você segue
```

### 3. Use a ferramenta

1. Abra o arquivo `instagram-analyzer.html` em qualquer navegador moderno
2. Arraste ou clique para carregar o `followers_1.json` na zona esquerda
3. Arraste ou clique para carregar o `following.json` na zona direita
4. Clique em **◆ INICIAR ANÁLISE — EXECUTE RECON ◆**
5. Explore os resultados nas abas

---

## 🛠️ Como foi feito

### Tecnologias

| Tecnologia | Uso |
|---|---|
| **HTML5** | Estrutura da página |
| **CSS3 puro** | Todos os efeitos visuais e animações |
| **JavaScript vanilla** | Lógica de parsing e análise |
| **Google Fonts** | Fontes `VT323` e `Share Tech Mono` |

Sem frameworks, sem bibliotecas externas, sem dependências — um único arquivo `.html` autocontido.

### Estética CRT / Fallout

O visual retrô foi construído inteiramente com CSS:

- **Scanlines** via `repeating-linear-gradient` com opacidade baixa sobre toda a tela
- **Vinheta CRT** com `radial-gradient` nas bordas
- **Linha de scan descendo** animada com `@keyframes` de cima para baixo em loop
- **Efeito glitch** nos títulos usando `skewX` e `hue-rotate` em keyframes esporádicos
- **Animação de power-on** simulando um monitor CRT ligando (`scaleY(0.02)` → `scaleY(1)`)
- **Efeito flicker** sutil na opacidade da tela inteira
- **Cursor customizado** em formato de mira circular via `cursor: none` + elemento `div` rastreado por `mousemove`
- **Texto com glow** usando `text-shadow` em múltiplas camadas com `rgba` do verde fósforo
- **Fonte VT323** para títulos — tipicamente usada em interfaces retrô e pixel art
- **Paleta monocromática verde** (`#39ff14`) com amber (`#ffb000`) como cor de alerta, sobre fundo quase preto (`#000800`)

### Parsing dos dados do Instagram

O Instagram exporta os dados em dois formatos ligeiramente diferentes dependendo da versão:

```javascript
// followers_1.json — array direto
[
  { "string_list_data": [{ "value": "username", ... }] }
]

// following.json — objeto com chave
{
  "relationships_following": [
    { "string_list_data": [{ "value": "username", ... }] }
  ]
}
```

A função `extract()` lida com ambos os formatos e também faz fallback para estruturas aninhadas desconhecidas, garantindo compatibilidade com diferentes versões do export.

### Lógica de análise

```javascript
// Quem você segue mas não te segue de volta
const naoTeSegue = following.filter(u => !followersSet.has(u));

// Quem te segue mas você não segue
const naoSeguido = followers.filter(u => !followingSet.has(u));

// Mútuos
const mutuos = followers.filter(u => followingSet.has(u));
```

Uso de `Set` para lookup em O(1), garantindo performance mesmo com listas grandes.

---

## 🔒 Privacidade

Todos os dados são processados **exclusivamente no seu navegador**. Nenhuma informação é enviada para servidores externos. O arquivo pode ser usado completamente offline após o carregamento inicial das fontes do Google Fonts.

---

## 📁 Estrutura do projeto

```
FollowTrack/
└── instagram-analyzer.html    ← arquivo único, tudo incluso
└── README.md                  ← este arquivo
```

---

## ⚠️ Aviso

Esta ferramenta **não viola os Termos de Uso do Instagram** pois utiliza apenas dados exportados pelo próprio usuário através do recurso oficial de exportação da plataforma. Nenhuma automação, scraping ou acesso à API é realizado.

---

*MARKS INDUSTRIES (TM) TERMLINK PROTOCOL — ALL RIGHTS RESERVED*
*WARNING: UNAUTHORIZED ACCESS IS A FEDERAL CRIME UNDER THE COMPUTER FRAUD AND ABUSE ACT OF 2077*
