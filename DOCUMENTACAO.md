# CRIAPA Hub - Documentacao Tecnica Completa do Site

**URL:** https://criapa.github.io/
**Repositorio:** https://github.com/criapa/criapa.github.io
**Email de contato:** criapa.contato@gmail.com
**WhatsApp:** (81) 99724-4535
**Data da ultima atualizacao:** 12/06/2026
**Autor da documentacao:** OWL (assistente tecnico)
**Responsavel pelo projeto:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE

---

## 0. GBrain + Hermes — Sistema de Conhecimento Integrado

### Visao Geral
O GBrain e o Hermes trabalham juntos como um cerebro digital integrado, fornecendo solucoes de alta performance com esforcos somados e distribuidos de forma organizada e documentada. O GBrain aprende continuamente com novos arquivos importados e gera solucoes e insights geniais.

### Areas de Atuacao

| Area | Descricao |
|------|-----------|
| **Negocios** | CRIAPA Hub, registro de marcas, prospeccao de clientes, estrategia comercial |
| **Educacao** | Pesquisa academica, revisao sistematica, doutorado, artigos cientificos |
| **Financeiro** | Analise financeira, investimentos, direito financeiro |
| **Consultoria** | Propriedade industrial, PI, INPI, assessoria juridica |
| **Pesquisa Cientifica** | Revisao sistematica, farmacologia, design de farmacos, vias farmacocineticas, paineis geneticos SNPs (sistema endocanabinoide) |
| **Analise de Mercado** | Geopolitica, noticias, identificacao de fontes duvidosas |
| **Tecnologia** | Desenvolvimento de softwares |
| **Direito** | Advocacia, direito civil, penal, internacional, trabalhista, LGPS, codigo civil, codigo penal, leis de inclusao, leis de propriedade industrial |
| **Setor Publico** | Administracao publica, CAPES, lei de incentivo a pesquisa, transparencia, cobranca de politicos (camara, senado, vereadores, prefeitos, governadores) |
| **Autogovernanca** | Aumento do poder de persuasao e tomada de decisao |

### Instalacao

| Componente | Local/Modelo |
|------------|--------------|
| GBrain | `C:\Users\Pichau\gbrain` |
| Banco de dados | `C:\Users\Pichau\.gbrain\brain.pglite` |
| Runtime | Bun 1.3.14 |
| Embeddings | Ollama `nomic-embed-text-v2-moe:latest` (768 dimensoes) |
| LLM sintese | Ollama `granite4.1:8b` (comando `think`) |
| LLM Hermes | Ollama `gemma4:12b` |

### Dados Importados

| Fonte | Arquivos | Chunks |
|-------|----------|--------|
| CRIAPA Hub (notas) | 27 | 84 |
| Revisao Sistematica PHD | 254 | 629 |
| Site (workspace + repo) | 30 | 666 |
| **Total** | **311** | **1379** |

### Comandos Uteis

```bash
cd C:\Users\Pichau\gbrain
bun run src/cli.ts query "pergunta"     # Busca hibrida (texto + embeddings)
bun run src/cli.ts search "pergunta"    # Busca por texto
bun run src/cli.ts think "pergunta"     # Sintese com IA (Ollama granite4.1:8b)
bun run src/cli.ts capture "nota"       # Capturar pensamento
bun run src/cli.ts import C:\pasta      # Importar arquivos
bun run src/cli.ts list                 # Listar paginas
```

### Regras de Trabalho

1. **Sempre documentar** decisoes, erros e licoes aprendidas
2. **GBrain aprende continuamente** com novos arquivos importados
3. **Usar `think`** para sintese de respostas baseadas nos documentos
4. **Usar `query`** para busca rapida de informacoes
5. **Usar `capture`** para gravar pensamentos e insights
6. **Ao movimentar arquivos**, usar 4 threads para velocidade nas transferencias
7. **Manter documentacao tecnica atualizada** a cada mudanca significativa

### MCP Server no Hermes

O GBrain esta configurado como MCP server no Hermes:

```yaml
mcp_servers:
  gbrain:
    command: bun
    args: ["run", "src/cli.ts", "serve"]
    env:
      BRAIN_PATH: "C:\\Users\\Pichau\\.gbrain\\brain.pglite"
```
