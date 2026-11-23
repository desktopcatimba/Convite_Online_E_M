# Convite de Noivado – Alcides & Milena

Site-convite de página única, com um envelope animado que se vai abrindo à medida que se faz scroll. Depois de aberto, mostra a mensagem do convite, as fotos do casal e do filho Alpha, a data, a hora, o local com link para o mapa, uma contagem decrescente e os contactos para confirmar presença.

## Detalhes do evento

| | |
|---|---|
| Evento | Noivado de Alcides & Milena |
| Data | 6 de Dezembro de 2026 |
| Hora | 18h00 |
| Local | Benfica, Kifica, Rua 39 |
| Contactos | 944 167 605 · 924 626 035 · 948 163 320 |

## Tecnologias

- HTML, CSS e JavaScript puros, num único ficheiro, sem frameworks nem passo de build
- Fontes Google: Great Vibes (nomes e títulos) e Cormorant Garamond (texto)
- Fotos embutidas no próprio `index.html` em base64, por isso não há pasta de imagens
- Animação do envelope controlada pelo scroll (`requestAnimationFrame`) e revelação das secções com `IntersectionObserver`
- Tema claro e escuro automático, consoante o telemóvel
- Respeita `prefers-reduced-motion`

## Estrutura

```
.
├── index.html   # o site completo
└── README.md
```

## Ver localmente

Basta abrir o `index.html` no navegador. Se preferires um servidor local:

```bash
npx serve .
```

## Deploy na Vercel

1. Cria uma pasta só com o `index.html` na raiz:
   ```bash
   mkdir convite && cd convite
   # copia aqui o index.html
   ```
2. Faz o deploy:
   ```bash
   npx vercel --prod
   ```
3. Nas perguntas do assistente:
   - Nome do projeto: `convite-noivado-alcides-milena` (só minúsculas, letras, dígitos, `.`, `_` e `-`, sem `---`, até 100 caracteres)
   - Diretório do código: `./`
   - Alterar configurações de build: **não**

Se aparecer **404 NOT_FOUND**, confirma que:

- o ficheiro se chama exatamente `index.html` e está na **raiz** do deploy, não numa subpasta;
- em *Settings → Build & Development*, o *Framework Preset* está em **Other** e o *Output Directory* está **vazio**;
- o último deploy em *Deployments* está com estado **Ready**.

## Como personalizar

Tudo está no `index.html`. Procura por estes pontos:

**Nomes e textos**
Procura `Alcides` e `Milena`. Aparecem na carta do envelope, no título, na legenda das fotos e na mensagem de WhatsApp.

**Data e hora**
- Texto visível: secção "Quando e onde" (`6 de Dezembro`, `18h00`).
- Contagem decrescente: no `<script>`, na linha `target=new Date('2026-12-06T18:00:00+01:00')`. O `+01:00` é o fuso de Luanda.

**Local e mapa**
- Texto: `Benfica, Kifica<br>Rua 39`.
- Link: o `href` do botão "Abrir localização no mapa".

**Contactos**
- Os três links `tel:+244...` na secção "Confirma a tua presença".
- O botão de WhatsApp usa `https://wa.me/244944167605`. Muda o número para outro, sempre com o indicativo `244` e sem espaços.

**Fotos**
As imagens estão no formato `src="data:image/jpeg;base64,..."` dentro das três tags `<img>` da secção "A nossa família". Para trocar:

1. Reduz a foto para cerca de 800 px de largura (JPEG, qualidade ~75) para o ficheiro não ficar pesado.
2. Converte para base64 e substitui o conteúdo do `src`.

   ```bash
   base64 -w0 foto.jpg   # Linux
   base64 -i foto.jpg    # macOS
   ```
   O resultado deve ficar assim: `src="data:image/jpeg;base64,<resultado>"`.

Em alternativa, coloca as fotos numa pasta `img/` ao lado do `index.html` e usa `src="img/nome.jpg"`.

**Cores**
Estão no topo do `<style>`, nas variáveis de `:root`:

| Variável | Uso |
|---|---|
| `--red`, `--red2` | vermelho do envelope e dos botões |
| `--gold`, `--gold2` | dourado dos detalhes e dos nomes |
| `--bg`, `--paper` | fundo da página e da carta |
| `--ink`, `--soft` | texto |

Os valores para o modo escuro estão nos dois blocos logo a seguir.

**Duração da animação do envelope**
Na `.intro`, `height:430vh` define a distância de scroll necessária para abrir o envelope. Aumenta para uma abertura mais lenta, diminui para uma mais rápida.

## Notas

- Os links de `tel:` e WhatsApp só funcionam bem em telemóveis ou em computadores com uma app associada.
- Se o ano do evento mudar, atualiza a data da contagem decrescente, senão ela mostra "Obrigado por celebrares connosco!" assim que passar.
