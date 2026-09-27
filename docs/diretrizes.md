# O que é o DataUFBA: diretrizes do projeto

Documento de definição. Fixa **o que o DataUFBA é e o que ele não é**, para que
decisões de escopo, taxonomia e priorização não voltem a ser tomadas por analogia.
Escrito em setembro de 2026, a partir de revisão do estado do site e da discussão
sobre fragmentação de dados públicos.

> **Normativo.** Este documento é a fonte canônica da definição do projeto. A versão
> operacional, com as regras práticas para quem for editar o repositório, está em
> [`AGENTS.md`](../AGENTS.md). Em caso de divergência, vale este arquivo, e a
> divergência deve ser corrigida.

## Nome

**DataUFBA** é o nome do projeto. **Observatório de Dados da UFBA** é o subtítulo, e
descreve a função exercida: catalogar, monitorar e dar leitura pública aos dados. A
URL `data.ufba.br` corresponde ao nome.

---

## 1. Problema que este documento resolve

A revisão do site identificou que o hub trata **repositório**, **catálogo** e
**vitrine** como a mesma coisa: todas aparecem sob o rótulo único de "iniciativas de
dados". Consequências observadas:

- O acervo dos Boletins PRODEP (preservação de artefatos, checksums, manifesto) é
  apresentado lado a lado com painéis analíticos, como se fossem o mesmo tipo de
  produto.
- O card "Dados abertos (GitHub)" aponta para o repositório `data-ufba` como se fosse
  uma iniciativa do DataUFBA, misturando custódia com publicação.
- Iniciativas marcadas como "Planejado" (Dados Estudantis, Pós-Graduação, Graduação)
  não têm definido *o que* catalogariam nem *de quem* é o repositório de origem.

Sem uma definição explícita, cada nova página repete a ambiguidade.

## 2. As três camadas

### 2.1 Repositório: custódia

Guarda o artefato e sua proveniência. É onde vive o dado bruto, o código de coleta, o
manifesto, os checksums e os testes de reprodutibilidade.

- **Responsabilidade:** preservar e permitir reaproveitamento.
- **Pergunta que responde:** *de onde veio, quando, por qual método, com qual
  limitação, e como reexecutar?*
- **Onde isso vive:** repositórios de dados do LABHD (ex.: `LABHDUFBA/data-ufba`).
- **Não é a cara pública do DataUFBA.** O DataUFBA pode e deve referenciar
  repositórios, sem hospedar acervo bruto, sem versionar dado nominal, sem virar
  espelho de acervo.

### 2.2 Catálogo: descoberta e monitoramento

Descreve os repositórios: o que existe, onde, sob qual licença, com qual cobertura
temporal e geográfica, em que versão, atualizado quando.

- **Responsabilidade:** descoberta e **monitoramento**, isto é, detectar quando um
  conjunto muda de versão, muda de estrutura ou desaparece.
- **Pergunta que responde:** *o que existe sobre este tema, onde está, e continua
  lá?*
- **Formato:** registro de metadados (fonte, responsável, cobertura, licença,
  periodicidade, URL canônica, situação).

### 2.3 Vitrine: leitura pública

Camada expressiva: a visualização que torna o dado compreensível para quem não vai
ler o JSON. É o que o visitante vê e entende.

- **Responsabilidade:** traduzir, agregar e contextualizar, sem substituir a fonte.
- **Pergunta que responde:** *o que estes dados mostram, e com quais limites?*
- **Regra:** toda vitrine declara fonte, período, método e limitação **na própria
  página** (padrão já seguido por `docentes/`, `mapa-tematico/` e
  `boletins-prodep/`).
- **Só agregações.** Dado individual não é exibido, ainda que a fonte seja pública.

### 2.4 Como as camadas se encadeiam

```
Repositório (custódia)  →  Catálogo (metadado + monitoramento)  →  Vitrine (leitura)
        fora do site              pode ser parte do site              é o site
```

Uma **iniciativa** do DataUFBA é uma vitrine, e ela existe quando há: (a) um
repositório com dado preservado e documentado, e (b) um registro de catálogo que diz
o que aquilo é. Sem as duas, não é iniciativa, e sim trabalho em andamento.

## 3. Decisão de escopo

**O DataUFBA é catálogo e vitrine. Não é repositório de dados.**

O que isso implica na prática:

- Não hospedar acervo bruto no site (os HTMLs originais dos Boletins PRODEP
  permanecem no portal da PRODEP, que é quem os disponibiliza, nunca no repo do site).
- Não publicar dado nominal em nenhuma camada.
- Não duplicar dado: a vitrine consome datasets agregados derivados do repositório,
  não mantém cópia própria da fonte.
- O catálogo aponta para repositórios, inclusive de terceiros (CAPES, INEP,
  Portal da Transparência, paineis.ufba.br), e assume a curadoria do metadado, não a
  custódia do dado alheio.
- Quando o DataUFBA precisar preservar algo (ex.: um recorte que a fonte retirou do
  ar), isso é uma decisão explícita, registrada, e o artefato vai para um repositório,
  não para o site.

## 4. Vocabulário

| Termo | Uso no projeto |
|---|---|
| **Repositório** | Onde o dado é disponibilizado pela fonte e onde o código de coleta é versionado. |
| **Catálogo** | Registro de metadados sobre repositórios e conjuntos; camada de descoberta e monitoramento. |
| **Vitrine** | Página ou painel de leitura pública de um conjunto catalogado. |
| **Iniciativa** | Uma vitrine publicada, com repositório e registro de catálogo correspondentes. |
| **Acervo** | Conjunto mantido e disponibilizado por uma fonte (ex.: Boletins de Pessoal PRODEP, no portal da PRODEP). Não confundir com iniciativa nem com o que o DataUFBA hospeda. |

*Sobre o termo "vitrine": serve bem ao discurso interno e à definição de escopo, e é
o que distingue este projeto de um repositório. Na interface pública, o par adotado é
o nome **DataUFBA** com o subtítulo **Observatório de Dados da UFBA**.*

## 5. Consequências já visíveis no site atual

Pontos a tratar quando houver decisão de alterar o hub. **Nenhum deles foi alterado
por este documento**:

1. Separar visualmente, no hub, **acervo/fonte** de **painel**. Hoje o acervo PRODEP e
   o painel de agregações aparecem como uma única entrada.
2. Reenquadrar as iniciativas "Planejado" (Dados Estudantis, Pós-Graduação,
   Graduação): definir antes **qual repositório de origem** será catalogado, em vez
   de prometer um painel.
3. Corrigir os KPIs fixos no HTML do hub. Devem derivar dos datasets, ou assumir
   data de referência explícita.
4. Corrigir caminhos relativos quebrados: `docentes/` (logo `assets/` → `../assets/`,
   brand `index.html` → `../index.html`) e `mapa-tematico/` (link "Iniciativas"
   `index.html` → `../index.html`).
5. O rodapé afirma "Acessível com VLibras" e aponta para o site do plugin. Se houver
   declaração de acessibilidade, ela precisa ser própria.
6. `data.ufba.br` ainda não está publicado (503 na origem institucional); o site vivo
   é `labhdufba.github.io/data-ufba-site`. Definir a publicação oficial é decisão da
   UFBA, não do repositório.

## 6. Direção de longo prazo

Duas frentes que a distinção acima abre e que são características do que o DataUFBA
pode fazer e um repositório institucional não faz:

- **Curadoria comunitária (metadado social).** Acrescentar camadas de contribuição
  pública sobre acervos existentes, como transcrição, indexação e anotação. Não exige
  infraestrutura nova: exige camada de curadoria sobre dado que já é disponibilizado por alguém.
- **Busca multimodal entre acervos.** Cruzar tipo de dado (visual, temporal,
  geoespacial, textual) e instituição, para revelar conexões que uma leitura por
  acervo isolado não mostra.

Ambas pressupõem a mesma coisa: o dado preservado em repositório, catalogado de
forma consistente, e lido publicamente por uma vitrine que declara seus limites.

---

## Registro de decisão

- **Nome:** DataUFBA, com o subtítulo "Observatório de Dados da UFBA". A URL
  `data.ufba.br` corresponde ao nome. Adotado em setembro de 2026, substituindo
  "Central de Dados", que era genérico no setor e colidia com projetos de outras
  unidades.
- **Decisão:** o DataUFBA é catálogo de repositórios e vitrine, não repositório de
  dados.
- **Data:** setembro de 2026.
- **Escopo:** diretriz de projeto para escopo, taxonomia do hub e critério de entrada
  de novas iniciativas.
- **Status:** diretriz de trabalho. Alteração deste documento exige decisão
  explícita. Não alterar conteúdo de projeto sem solicitação.

## Referências

- Revisão do estado do site e dos repositórios, verificada em setembro de 2026
  (estrutura das páginas, datasets, Pages, resposta HTTP da URL institucional).
- Discussão sobre fragmentação de dados públicos e curadoria comunitária: painel
  "AI and Government Data", AI4LAM 2026, com Molly Hardy (Public Data Project,
  Harvard Law School Library). Conceitos citados: *public trust*, metadado social
  (George Oates), espelhamento de dados governamentais como salvaguarda.
