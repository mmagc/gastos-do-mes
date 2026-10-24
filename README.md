# 💳 Gastos do Mês

PWA (Progressive Web App) simples para controlar os gastos do mês, separados por **categoria** e por **cartão de crédito / conta**. O número principal da tela mostra o **total a pagar somando todos os cartões e contas**, e logo abaixo um gráfico mostra onde e como o dinheiro foi gasto.

🔗 **Acesse:** https://mmagc.github.io/gastos-do-mes/

---

## ✨ Funcionalidades

| Recurso | Descrição |
|---|---|
| **Saldo total** | Mostra quanto você tem a pagar no mês, somando todos os cartões/contas. |
| **Saldo por cartão** | Logo abaixo do total, um "chip" para cada cartão/conta com o valor dele no mês. |
| **Gastos (+)** | Cada gasto é **somado** ao total. Ex.: comprou uma camiseta de R$ 100 no cartão X → o saldo vai de R$ 0 para R$ 100. |
| **Pagamentos / estornos (−)** | São **subtraídos** do total (ex.: um estorno, ou um pagamento parcial da fatura). |
| **Gráfico** | Gráfico de rosca + barras com a divisão dos gastos por **categoria** ou por **cartão** (alternável), com valor e porcentagem. |
| **Navegação por mês** | Setas no topo para ver meses anteriores/futuros; cada mês tem seu próprio total. |
| **Editar / excluir** | Toque em um lançamento para editar; no ✕ para excluir. |
| **Cartões e categorias personalizáveis** | Adicione, remova e escolha a cor de cada cartão/conta e categoria. |
| **Backup** | Exporte seus dados para um arquivo `.json` e importe de volta (útil para trocar de aparelho). |
| **Funciona offline** | Graças ao service worker, o app abre mesmo sem internet. |
| **Instalável** | Pode ser instalado na tela inicial do celular ou no computador como um app. |
| **Tema claro/escuro** | Em Configurações → Tema: **Automático** (segue o sistema), **Claro** ou **Escuro**. A escolha fica salva no aparelho. |

---

## 📱 Como instalar no celular

### Android (Chrome)
1. Abra o link do app no Chrome.
2. Toque no menu **⋮** → **Instalar app** (ou **Adicionar à tela inicial**).
3. Pronto: o ícone aparece junto com os outros apps.

### iPhone (Safari)
1. Abra o link do app no **Safari**.
2. Toque no botão **Compartilhar** (quadrado com seta para cima).
3. Escolha **Adicionar à Tela de Início**.

### Computador (Chrome / Edge)
Clique no ícone de instalação que aparece na barra de endereço (à direita) ou no menu → **Instalar Gastos do Mês**.

---

## 🧭 Como usar

1. **Adicionar um gasto:** toque no botão **+** (canto inferior direito).
   - Escolha **➕ Gasto** ou **➖ Pagamento/Estorno**.
   - Preencha a descrição, o valor (aceita `100`, `100,50` ou `1.250,90`), a data, o cartão/conta e a categoria.
   - Toque em **Salvar**. O app lembra o último cartão usado para agilizar o próximo lançamento.
2. **Ver o total:** o número grande no topo é o total a pagar no mês selecionado.
3. **Ver para onde foi o dinheiro:** no quadro **Onde foi gasto**, alterne entre **Categoria** e **Cartão**.
4. **Trocar de mês:** use as setas **‹** e **›** ao lado do nome do mês.
5. **Gerenciar cartões/categorias e tema:** use a seção **Configurações** no fim da página.
6. **Fazer backup:** **Exportar backup** baixa um arquivo `.json`; **Importar backup** substitui os dados atuais pelos do arquivo.

### Como o total é calculado

```
Total do mês = soma dos gastos − soma dos pagamentos/estornos
```

O gráfico considera apenas os **gastos** (o que entrou na fatura), para mostrar a distribuição real do consumo.

---

## 🔒 Onde ficam meus dados?

Todos os dados ficam salvos **apenas no seu navegador/aparelho** (`localStorage`). Nada é enviado para servidor nenhum.

Consequências importantes:
- Os dados **não sincronizam** entre celular e computador automaticamente — use **Exportar/Importar backup** para levar de um para o outro.
- Se você **limpar os dados do navegador** ou desinstalar o app, os lançamentos são apagados. Faça backups de vez em quando.

---

## 🗂️ Estrutura do projeto

```
gastos-do-mes/
├── index.html      # O app inteiro: HTML, CSS e JavaScript (sem dependências)
├── manifest.json   # Manifesto do PWA (nome, ícones, cores, modo standalone)
├── sw.js           # Service worker: cache para funcionar offline
└── icons/
    ├── icon.svg     # Ícone vetorial (favicon)
    ├── icon-192.png # Ícone para Android/iOS
    └── icon-512.png # Ícone grande / maskable
```

Não há build, framework nem bibliotecas externas. O gráfico é desenhado em SVG puro.

### Modelo de dados (`localStorage`, chave `gastos-mes-v1`)

```json
{
  "cards": [{ "id": "abc123", "name": "Nubank", "color": "#8b5cf6" }],
  "cats":  [{ "id": "def456", "name": "Roupas", "color": "#f59e0b" }],
  "tx": [
    {
      "id": "x1y2z3",
      "created": 1761273600000,
      "desc": "Camiseta",
      "amount": 100,
      "date": "2026-10-23",
      "type": "gasto",
      "card": "abc123",
      "cat": "def456"
    }
  ],
  "lastCard": "abc123"
}
```

- `type`: `"gasto"` (soma) ou `"pagamento"` (subtrai).
- `date`: formato `AAAA-MM-DD`; é usada para separar os lançamentos por mês.

---

## 💻 Rodando localmente

Service workers só funcionam em `https://` ou em `localhost`, então abra via um servidor local (abrir o `index.html` direto pelo explorador de arquivos não ativa o modo offline).

Com Node.js:

```bash
npx http-server -p 5173 -c-1
```

Ou com Python:

```bash
python -m http.server 5173
```

Depois acesse http://localhost:5173.

---

## 🚀 Publicação (GitHub Pages)

O site é publicado pelo GitHub Pages a partir da branch `main` (pasta raiz). Qualquer `push` para a `main` atualiza o site em cerca de 1 minuto.

> **Importante ao atualizar o app:** o service worker usa a estratégia *rede primeiro*, então os usuários recebem a versão nova assim que abrem o app com internet. Mesmo assim, ao mudar a lista de arquivos ou fazer mudanças grandes, aumente a versão em `sw.js` (`const CACHE = 'gastos-v2'`) para descartar o cache antigo.

---

## 🛣️ Ideias para o futuro

- Parcelamento automático (ex.: 3x de R$ 100 distribuídos nos próximos meses)
- Data de fechamento/vencimento por cartão
- Limite de gasto por categoria com alerta
- Gastos recorrentes (assinaturas)
- Sincronização na nuvem entre aparelhos
- Exportar para CSV/Excel

---

## 📄 Licença

Projeto pessoal, livre para uso e modificação.
