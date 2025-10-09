# Atividade Prática — Landing page

**Objetivo:** Construir uma *landing page* simples aplicando **Flexbox** no cabeçalho, **grid de cards fluído** com flex-wrap, **tipografia fluida** com `clamp()` e **tema** via **CSS Custom Properties** + `prefers-color-scheme`. Depois, comparar com uma **versão em Bootstrap** para discutir produtividade.

---

## Passo a passo guiado

### 1) Preparação
- Abra a pasta deste projeto e **sirva** os arquivos com uma extensão do VS Code (Live Server) ou abra o `index.html` diretamente no navegador.
- Inspecione o HTML: tags semânticas (`header`, `main`, `section`, `article`, `footer`), navegação e links âncora.

**Checkpoint:** O cabeçalho está visível, a *hero section* aparece com título, subtítulo e botões.

---

### 2) Tokens e tema com Custom Properties
- Em `styles.css`, os **tokens** já estão definidos no `:root` (`--bg`, `--fg`, `--brand`, etc.).
- Habilite o **modo escuro** do seu sistema para ver o efeito de `prefers-color-scheme` mudar cores automaticamente. Mude o tema do sistema para escuro no Windows 10/11: Configurações → Personalização → Cores → Escolher seu modo: Escuro.

**Explicação:** Custom Properties permitem **tema dinâmico** em tempo real. `:root` fornece valores padrão; a `@media (prefers-color-scheme: dark)` os ajusta para dark mode.

**Checkpoint:** Alternar claro/escuro altera **fundo**, **texto** e **superfícies**, mantendo contraste legível.

---

### 3) Tipografia fluida com `clamp()` 
- Já incluímos variáveis `--fs-base`, `--fs-lg`, `--fs-xl`, `--fs-2xl`.
- Verifique como o `body` usa `font: 400 var(--fs-base)/1.6 ...` e como títulos usam escalas maiores.

**Tarefa:** Ajuste `--fs-2xl` para aumentar levemente o `h1` e observe o impacto em telas pequenas e grandes.

**Checkpoint:** O `h1` cresce sem “quebrar” o layout em telas pequenas.

---

### 4) Header com Flexbox 
- O seletor `.header-inner` usa `display: flex; justify-content: space-between; align-items: center;`.
- A lista `.nav-list` usa `display: flex; gap: 1rem;`.

**Tarefa:** Inclua um novo item de menu(<ul class="nav-list">) “Blog” mantendo alinhamento e espaçamento. Teste o foco do teclado com `Tab` — o foco precisa ficar visível.

**Checkpoint:** Layout estável em diferentes larguras; foco visível em links do menu.

Por que o foco fica visível? No styles.css já existe:

```css
 :focus-visible{ outline: 3px solid var(--brand); outline-offset: 2px; }
```

- Se quiser que o link funcione como âncora, crie uma seção mais abaixo:

```html
 <section id="blog" class="about" aria-labelledby="blog-title">
  <div class="container">
    <h2 id="blog-title">Blog</h2>
    <p>Em breve: artigos e novidades.</p>
  </div>
</section>
```

---

### 5) Hero: composição visual e call to action 
- `hero` combina tipografia, botões (`.btn`, `.btn-primary`, `.btn-outline`) e um *mock* visual à direita.
- Observa as transições em `:hover` e `:focus-visible`.

**Tarefa:** Edite o texto da *hero* para o seu contexto (ex.: outro tema de projeto). Mantenha o CTA principal como botão sólido e o secundário como contorno.

**Checkpoint:** Botões têm **hierarquia** clara; hover suave e foco visível.

---

### 6) Grid de cards fluído com Flexbox 
- `.cards` usa `display: flex; flex-wrap: wrap; gap: 1rem;` e cada `.card` tem `flex: 1 1 clamp(220px, 30%, 340px);`.

**Explicação:** Esse padrão cria colunas que **fluem** sem precisar de muitas *media queries*. O `clamp()` limita o tamanho mínimo/máximo.

**Tarefa:** Adicione **dois novos cards** mantendo consistência visual (título `h3`, parágrafo, link).

**Checkpoint:** Em telas largas, 3–4 colunas; em telas estreitas, 1–2 colunas, sem sobreposição.

---

### 7) Acessibilidade mínima
- **Foco visível**: usamos `:focus-visible` + `outline` consistente.
- **Skip link**: `.skip-link` permite pular direto para o `main`.
- **Contraste**: tema claro/escuro mantém legibilidade.

**Tarefa:** Navegue **só com teclado**. Você consegue acessar todos os links e botões? Ajuste `outline-offset` se necessário.

**Teclas que importam**

- Tab: move o foco para o próximo elemento focável (links <a>, botões <button>, inputs, etc.).

- Shift + Tab: volta o foco para o anterior.

- Enter: ativa o elemento focado (clica em links; envia botões tipo submit).

- Barra de Espaço: ativa botões e checkboxes; em links geralmente não faz nada (depende do user agent).

- Setas (↑ ↓ ← →): usadas em componentes compostos (menus, radio groups, sliders). Em links/“nav simples”, Tab é o principal.

- Esc: fecha componentes modais/overlays (se existirem).

- Dica: no DevTools, rode document.activeElement no console para ver qual elemento está focado.

**Checkpoint:** Navegação por teclado sem armadilhas; foco sempre perceptível.

---

### 8) Interações e microanimações
- Cards e botões usam `transition` + `transform` para uma elevação sutil.

**Tarefa:** Reduza ou aumente o `translateY` no hover dos `.card` e avalie se a animação está **suave** e **discreta**.

**Checkpoint:** Efeito perceptível, porém não exagerado. Sem jitter.

---

### 9) Responsividade sem sofrimento
- Há poucas `@media` e o layout já funciona por ser **fluído**. Ajustes finos ficam em `@media (min-width: 768px)` para a *hero*.

**Tarefa:** Adicione uma nova media query para `@media (min-width: 1024px)` e aumente o `gap` da `.hero-inner` para `3rem` nesse breakpoint.

**Checkpoint:** Espaçamento mais confortável em telas grandes sem quebrar o mobile.

---

### 10) Comparação com Bootstrap
- Abra `bootstrap.html`. O layout é equivalente usando **grid** (`row`/`col`) e utilitários.
- Compare o tempo de modificação: mudar cores, espaçamentos e tipografia.

**Tarefa:** Replique os 2 novos cards também aqui e experimente utilitários (`p-`, `m-`, `shadow`, `rounded-4`).

**Discussão:** Onde o Bootstrap acelerou? Onde o CSS autoral foi mais simples ou mais controlável?

---

## Critérios de avaliação
- **Layout**: Header com Flexbox correto; cards fluídos sem sobrepor; responsividade básica.
- **Tipografia e cor**: `clamp()` aplicado; hierarquia legível; contraste adequado.
- **Acessibilidade**: foco visível, skip link funcional, navegação por teclado.
- **Interações**: transições suaves e discretas; sem animações pesadas.
- **Organização**: uso coerente de Custom Properties; CSS limpo, sem `!important` desnecessário.

## Extensões (opcional)
- Criar um **switch** de tema manual além do `prefers-color-scheme`.
- Adicionar uma seção de **FAQ** com `details/summary` e estilizar estados abertos (`[open]`).
- Usar **container queries** para ajustar cards conforme o espaço disponível.
