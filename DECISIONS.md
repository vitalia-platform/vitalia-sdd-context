<!-- DECISIONS.md | Atualizado em: 08-09-2026 17:50:03(GMT-04:00) -->
# 🏛️ Decisões de Arquitetura e Governança Consolidadas (ADRs)

**Data/Hora de Geração:** `08-09-2026 17:50:03(GMT-04:00)` | **Fuso Horário:** America/Cuiaba `(GMT-04:00)`

| ID | Categoria | Decisão | Racional | Máquina | Data |
|---|---|---|---|---|---|
| `1d0f3cdd` | `[ARCH]` | Manter o /vitalia-brainstorming inalterado durante a transição inicial. | O brainstorming está em evolução deliberada para atuar como Hub Socrático Orquestrador do Ecossistema Multiagentes. | `7f367bd3` | 29-08-2026 11:23:41(GMT-04:00) |
| `d32e318c` | `[SCOPE]` | Focar a primeira entrega na adequação dos 4 workflows de gestão de contexto (session-start, session-consolidate, session-end, vitalia-route). | Garantir ciclo limpo de sessão antes de expandir outros domínios. | `7f367bd3` | 29-08-2026 11:23:41(GMT-04:00) |
| `87d16a5b` | `[ARCH]` | Validar schemas estritos via jsonschema em context_engine.py antes da escrita. | Evita corrupção da memória local, bloqueando o persistir de payloads mal-formados gerados por agentes. | `7f367bd3` | 06-09-2026 11:56:55(GMT-04:00) |
| `b98a0db7` | `[ARCH]` | Armazenar JSON schemas canônicos em kit-global/src/schemas/. | Centraliza os artefatos de definição de tipo junto aos pacotes fonte (src) que os processam. | `7f367bd3` | 06-09-2026 11:56:55(GMT-04:00) |
| `d75f2168` | `ARQUITETURA` | constitution.yaml usa Dual-Index (domain_index + principles) — formato O(1) para lookup | GuardianContextV2 detecta 'domain_index' no YAML e seleciona ConstitutionAdapterV2 automaticamente. | `7f367bd3` | 07-09-2026 18:58:42(GMT-04:00) |
| `85a6137b` | `ARQUITETURA` | Q4 Guardian fallback: Opção B agora (fix path) + Opção C em v0.7.0 (remover fallback) | Fix cirúrgico de 1 linha — mínimo risco de regressão. Elimina dívida técnica na próxima versão. | `7f367bd3` | 07-09-2026 18:58:42(GMT-04:00) |
| `a752df1a` | `ARQUITETURA` | profiles/ como pasta única para todas as fontes YAML — schema_type diferencia o tipo | Um único diretório para grep, auditoria e versionamento. Guardian detecta adaptador via schema_type, não pelo path. | `7f367bd3` | 07-09-2026 18:58:42(GMT-04:00) |
| `996ac4fb` | `[ARCH]` | Manter o modelo como consumidor passivo de Markdown gerado, abdicando da consolidação LLM-only. | A nova arquitetura 0.6 delega toda a consolidação ao motor Python. O LLM atua apenas como iterador de UI e coletor de schemas rígidos (session-end). | `7f367bd3` | 08-09-2026 17:46:15(GMT-04:00) |
| `564628ec` | `[ARCH]` | Criação do grounding_domain_schema.json e injeção (reads) no pipeline de finalização. | Estabelece um contrato formal de interoperabilidade que evita comandos shell malformados ou sobrescrita global de config de saúde/domínio. | `7f367bd3` | 08-09-2026 17:46:15(GMT-04:00) |
