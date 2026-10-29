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
| **Compras parceladas** | Ao lançar um gasto, escolha de 1x a 48x. O app cria uma parcela em cada mês (mesmo dia; se o mês for mais curto, usa o último dia) e mostra a prévia antes de salvar, ex.: "10x de R$ 350,00". Dá para digitar o **total da compra** ou o **valor de cada parcela**. |
| **Assinaturas** | Cadastre cobranças mensais (streaming, academia, celular…) com valor, dia, cartão e categoria. O app lança sozinho a cobrança de cada mês, e dá para pausar, editar ou excluir. |
| **Fechamento da fatura** | Cada cartão pode ter um dia de fechamento. Cada compra entra automaticamente na fatura certa (parcelas e assinaturas também), e a tela de cartões mostra o período da fatura atual. |
| **Gráfico** | Gráfico de rosca + barras com a divisão dos gastos por **categoria** ou por **cartão** (alternável), com valor e porcentagem. |
| **Navegação por mês** | Setas no topo para ver meses anteriores/futuros; cada mês tem seu próprio total. |
| **Editar / excluir** | Cada lançamento tem um botão de **lápis** (editar) e de **lixeira** (excluir). Na tela de edição também há o botão **Excluir**. |
| **Lista com "Mostrar mais"** | A lista mostra os 10 lançamentos mais recentes do mês. **Mostrar mais** expande e abre um filtro de período (de um mês até outro, ou atalhos: este mês, últimos 3 ou 6 meses, este ano), com os lançamentos agrupados por mês e o total do período. |
| **Cartões e categorias personalizáveis** | Adicione, remova, **renomeie** e **troque a cor** de cada cartão/conta e categoria a qualquer momento. |
| **Extrato em PDF** | **Exportar** gera um extrato em PDF (do mês ou de todos os meses, de todas as categorias ou de **uma categoria só**) com resumo por cartão, por categoria e a lista de lançamentos. **Importar** lê esse PDF de volta e restaura os lançamentos. |
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
6. **Extrato em PDF:** em **Exportar**, escolha **este mês** ou **todos os meses**, a **categoria** (todas ou uma só, ex.: só Alimentação) e toque em **Gerar PDF** (no celular abre a tela de compartilhar, para salvar no Drive, enviar no WhatsApp etc.).
7. **Importar:** escolha um extrato PDF gerado pelo app. Ele mostra quantos lançamentos são novos e quantos já existem, e só **adiciona/atualiza** — nada que já está no app é apagado.

### Como o PDF é lido de volta

PDFs normais não guardam os dados de forma estruturada. Por isso, ao gerar o extrato, o app também **embute os lançamentos nos metadados do próprio PDF** (campo *Keywords*, no formato `GASTOS1:<dados em base64>`). Esses dados não aparecem na página, mas viajam junto com o arquivo — e é isso que o **Importar** lê.

Consequências:
- Só dá para importar extratos **gerados por este app**. PDFs de fatura do banco não são lidos.
- Se o PDF for editado, "impresso como PDF" de novo ou passado por algum conversor, os metadados podem se perder e o arquivo deixa de ser importável. Guarde o arquivo original.
- Backups antigos em `.json` também continuam sendo aceitos no **Importar**.

### Compras parceladas

1. Toque em **+**, preencha o gasto e escolha em **Parcelas** (ex.: `10x`).
2. Em **Valor digitado é**, diga se o valor é o **Total** da compra (R$ 3.500 → 10x de R$ 350) ou **Por parcela** (R$ 350 → total de R$ 3.500).
3. Confira a prévia (`10x de R$ 350,00 = R$ 3.500,00 · de out/2026 a jul/2027`) e salve.

- Cada parcela aparece no seu mês com uma etiqueta **3/10** e entra no total a pagar daquele mês.
- Se a divisão não for exata, os centavos que sobram vão para as primeiras parcelas (R$ 100 em 3x = 33,34 + 33,33 + 33,33).
- **Editar uma parcela:** valor e data mudam só nela; descrição, cartão e categoria podem ser aplicados a todas as parcelas (opção marcada por padrão).
- **Excluir:** o app pergunta se é para apagar a **compra inteira** ou **só aquela parcela**.
- Um gasto lançado à vista pode virar parcelado: edite e escolha o número de parcelas.
- Se o cartão tem dia de fechamento, cada parcela entra na fatura certa (ex.: compra em 27/10 num cartão que fecha dia 20 → parcelas nas faturas de nov, dez, jan…).

### Assinaturas

Em **Configurações → Assinaturas → + Nova assinatura**, informe nome, valor por mês, dia da cobrança, cartão, categoria e o mês em que começou.

- O app **lança sozinho** uma cobrança por mês (etiqueta **assinatura** na lista), do mês de início até o mês atual. Ao avançar para meses futuros, ele também mostra a previsão.
- Se o dia não existe no mês (ex.: dia 31 em novembro), usa o último dia.
- **Pausar** (chave liga/desliga): para de cobrar a partir do próximo mês; a cobrança do mês atual fica. Ao **reativar**, volta a cobrar a partir do mês atual, sem lançar os meses em que ficou pausada.
- **Editar** (ex.: aumento de preço): vale para a cobrança deste mês e as próximas; meses anteriores ficam como estão.
- **Excluir**: as cobranças até o mês atual continuam no histórico; as de meses futuros são removidas.
- Apagar a cobrança de um mês específico (lixeira na lista) não faz ela voltar — o app lembra quais meses já lançou.
- O extrato em PDF leva as assinaturas junto, então o **Importar** também as traz para outro aparelho.

### Dia de fechamento do cartão

Em **Configurações → Cartões**, cada cartão tem um campo **Fecha dia N** (ou **Sem fechamento** para conta corrente/débito). Também dá para escolher ao adicionar um cartão novo.

- Compras feitas **no dia do fechamento ou depois** entram na **próxima fatura**.
- A fatura leva o nome do mês em que fica **a maior parte do período** de compras dela:

  | Fechamento | Período de compras | Fatura de |
  |---|---|---|
  | Dia **22** (fecha 22/10) | 22/09 a 21/10 | **outubro** (mês do fechamento) |
  | Dia **3** (fecha 03/11) | 03/10 a 02/11 | **outubro** (mês anterior ao fechamento) |

  Regra: fechamento **até o dia 15** → a fatura conta como do mês anterior ao fechamento; **do dia 16 em diante** → do próprio mês do fechamento.
- Exemplo: comprando em 24/10, no cartão que fecha dia 22 a compra vai para **novembro**; no cartão que fecha dia 3 ela fica em **outubro**.
- Na tela de cartões, abaixo de cada um aparece o período da fatura atual (ex.: *"Fatura atual (outubro): compras de 03/10 a 02/11"*). Se no seu banco a compra do próprio dia de fechamento ainda entra na fatura atual, escolha o dia seguinte como fechamento.
- Ao lançar, o app avisa: *"Entra na fatura de outubro do Cartão 2 (compras de 03/10 a 02/11)"*, e depois de salvar já mostra aquele mês.
- O "mês" do app, para cartões com fechamento, é o mês da **fatura** — o total do topo é o valor daquela fatura. A lista continua mostrando a data real da compra.
- Ao configurar ou mudar o fechamento de um cartão, as compras dele **do mês passado em diante** são recalculadas; faturas mais antigas ficam como estão.
- Se o fechamento for num dia que o mês não tem (ex.: 30 em fevereiro), vale o último dia do mês.

### Como o total é calculado

```
Total do mês = soma dos gastos − soma dos pagamentos/estornos
```

O gráfico considera apenas os **gastos** (o que entrou na fatura), para mostrar a distribuição real do consumo.

---

## 🔒 Onde ficam meus dados?

Todos os dados ficam salvos **apenas no seu navegador/aparelho** (`localStorage`). Nada é enviado para servidor nenhum.

Consequências importantes:
- Os dados **não sincronizam** entre celular e computador automaticamente — exporte o **extrato em PDF (todos os meses)** num aparelho e use **Importar** no outro.
- Se você **limpar os dados do navegador** ou desinstalar o app, os lançamentos são apagados. Exporte o extrato de vez em quando como backup.

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

Não há build nem framework. O gráfico é desenhado em SVG puro. A única dependência externa é o [jsPDF](https://github.com/parallax/jsPDF) 2.5.1 + [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable) 3.8.2 (via cdnjs), carregados **só quando você toca em Exportar**. Depois do primeiro uso ficam em cache e funcionam offline.

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
- `bill`: mês da fatura (`AAAA-MM`) em que o lançamento entra, calculado pelo dia de fechamento do cartão. Lançamentos antigos sem `bill` usam o mês da data.
- `sub` (só em cobranças de assinatura): id da assinatura que gerou o lançamento.
- `inst` (só em parcelas): `{ "id": "<id da compra>", "n": 2, "of": 10 }` — parcela 2 de 10. Cada parcela é um lançamento próprio, no seu mês.
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

- Data de fechamento/vencimento por cartão
- Limite de gasto por categoria com alerta
- Gastos recorrentes (assinaturas)
- Sincronização na nuvem entre aparelhos
- Exportar para CSV/Excel

---

## 📄 Licença

Projeto pessoal, livre para uso e modificação.
