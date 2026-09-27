# AGENTS.md: DataUFBA (repositório data-ufba-site)

Regras deste repositório. Leia antes de alterar qualquer arquivo.

A definição completa do projeto (as três camadas, o vocabulário e o registro da
decisão) está em [`docs/diretrizes.md`](docs/diretrizes.md). Este arquivo é a versão
operacional: o que fazer e o que não fazer.

## O que é este repositório

O **DataUFBA** (subtítulo: **Observatório de Dados da UFBA**) é **catálogo de
repositórios e vitrine**. **Não é repositório de dados.** A URL `data.ufba.br`
corresponde ao nome.

| Camada | Responsabilidade | Onde vive |
|---|---|---|
| **Repositório** | Custódia, proveniência, checksums, reprodutibilidade | Onde a fonte disponibiliza o dado, mais os repos de coleta do LABHD |
| **Catálogo** | Metadado, descoberta e monitoramento de conjuntos | Pode ser parte deste site |
| **Vitrine** | Leitura pública: agregar, traduzir, contextualizar | **É este site** |

Uma **iniciativa** do DataUFBA é uma vitrine, e só existe quando há (a) um repositório
com dado preservado e documentado e (b) um registro de catálogo que diga o que aquilo
é.

## Regras de escopo

1. **Não hospedar acervo bruto neste repositório.** HTMLs originais, PDFs e artefatos
   permanecem onde a fonte os disponibiliza. Aqui entram apenas páginas, assets de
   interface e datasets **agregados** derivados.
2. **Nunca publicar dado nominal**, em nenhuma camada, ainda que a fonte seja pública.
   Só agregações.
3. **Não duplicar dado.** A vitrine consome o dataset derivado do repositório; não
   mantém cópia própria da fonte.
4. **Não promover uma "iniciativa planejada" a painel** sem antes definir qual
   repositório de origem será catalogado.
5. **Catalogar repositórios de terceiros** (CAPES, INEP, Portal da Transparência,
   `paineis.ufba.br`) é permitido e desejado: o DataUFBA assume a curadoria do
   metadado, não a custódia do dado alheio.

## Estrutura

```
index.html              # hub: catálogo de iniciativas
docentes/               # vitrine: caracterização do corpo docente
mapa-tematico/          # vitrine: mapa temático da pesquisa
boletins-prodep/        # vitrine: agregações dos Boletins de Pessoal
data/                   # datasets agregados consumidos por fetch()
assets/                 # logos e imagens de interface
docs/diretrizes.md      # definição do projeto (normativa)
```

Os dois repositórios têm papéis distintos: o site é este repo; a coleta e o manifesto
de proveniência vivem em `LABHDUFBA/data-ufba`. **O dado em si não é hospedado por
nenhum dos dois**: ele permanece no site da fonte que o disponibiliza, e o catálogo
apenas indica onde encontrá-lo. O protótipo antigo em `data-ufba/site/` está
congelado e **não** é este site.

## Convenções das vitrines

- **Copiar de um painel existente**, nunca inventar estilo. Ler `docentes/index.html`
  e `mapa-tematico/index.html` antes de criar ou alterar: mesmas variáveis CSS
  (`:root` navy/teal/sand), masthead com brand + nav, faixa de stats sobre o hero,
  `.chart-card`, `table.data`, footer + VLibras + barra gov.br, Chart.js 4.4.1.
- **Dataset via JSON externo** em `data/`, carregado por `fetch` (padrão do
  `mapa-tematico`). Não embutir dados no HTML.
- **Caminhos relativos**: páginas em subpasta usam `../assets/...` e `../index.html`.
  Conferir com `curl -o /dev/null -w '%{http_code}'` na URL publicada. Há histórico de
  404 por caminho errado.
- **Toda vitrine declara fonte, período, método e limitação na própria página.**
- Painel novo = nova pasta + card no hub + entrada em **Atualizações**.
- Números do hub devem ser consistentes com os datasets publicados e com a fonte primária.
  Se a fonte canônica não estiver definida, registre a divergência; não invente
  conciliação.
- **Não usar travessão em texto de interface.** Prefira reescrever a frase ou usar
  vírgula; para separar rótulos, use o ponto médio (·), já adotado nas páginas.

## Validação obrigatória antes de commit

1. Extrair o JS embutido do HTML para `/tmp/*.js` e rodar `node --check`.
2. `python3 -m json.tool` em cada dataset alterado.
3. Subir `python3 -m http.server` na pasta do site e **verificar a renderização real**
   no browser (KPIs no DOM, nº de canvases, linhas de tabela). Não basta o arquivo
   abrir. Encerrar o servidor no fim.

Registre no Pull Request qualquer validação que não tenha sido possível executar, e o
motivo.

## Git e publicação

- Uma branch por alteração (`fix/...`, `docs/...`, `feat/...`). **Não fazer merge
  direto na `main`**: enviar a branch, abrir Pull Request e aguardar revisão.
- Commits com a identidade já configurada no repositório.
- Depois do merge, remover a branch remota e a cópia local quando não houver mais
  trabalho exclusivo.
- Pages publica da `main` na raiz; o build leva cerca de 20 a 40 segundos.
- **`data.ufba.br` ainda não está publicado**: a URL oficial responde 503 na origem
  institucional (infra da UFBA), o que é esperado enquanto o site está em construção.
  A cópia viva é `https://labhdufba.github.io/data-ufba-site/`. Publicação oficial é
  decisão da UFBA, não deste repositório.
- Segredos nunca entram no repositório: use variáveis de ambiente.
