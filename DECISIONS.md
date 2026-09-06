<!-- DECISIONS.md | Atualizado em: 06-09-2026 11:56:55(GMT-04:00) -->
# 🏛️ Decisões de Arquitetura e Governança Consolidadas (ADRs)

**Data/Hora de Geração:** `06-09-2026 11:56:55(GMT-04:00)` | **Fuso Horário:** America/Cuiaba `(GMT-04:00)`

| ID | Categoria | Decisão | Racional | Máquina | Data |
|---|---|---|---|---|---|
| `1d0f3cdd` | `[ARCH]` | Manter o /vitalia-brainstorming inalterado durante a transição inicial. | O brainstorming está em evolução deliberada para atuar como Hub Socrático Orquestrador do Ecossistema Multiagentes. | `7f367bd3` | 29-08-2026 11:23:41(GMT-04:00) |
| `d32e318c` | `[SCOPE]` | Focar a primeira entrega na adequação dos 4 workflows de gestão de contexto (session-start, session-consolidate, session-end, vitalia-route). | Garantir ciclo limpo de sessão antes de expandir outros domínios. | `7f367bd3` | 29-08-2026 11:23:41(GMT-04:00) |
| `87d16a5b` | `[ARCH]` | Validar schemas estritos via jsonschema em context_engine.py antes da escrita. | Evita corrupção da memória local, bloqueando o persistir de payloads mal-formados gerados por agentes. | `7f367bd3` | 06-09-2026 11:56:55(GMT-04:00) |
| `b98a0db7` | `[ARCH]` | Armazenar JSON schemas canônicos em kit-global/src/schemas/. | Centraliza os artefatos de definição de tipo junto aos pacotes fonte (src) que os processam. | `7f367bd3` | 06-09-2026 11:56:55(GMT-04:00) |
