<!-- LEARNINGS.md | Atualizado em: 29-08-2026 11:25:26(GMT-04:00) -->
# 💡 Aprendizados Técnicos e Lições Aprendidas Consolidadas

**Data/Hora de Geração:** `29-08-2026 11:25:26(GMT-04:00)` | **Fuso Horário:** America/Cuiaba `(GMT-04:00)`

## [KIT]
- **Aprendizado:** A centralização de regras em constitution_data.yaml combinada com pruning do guardian_context.py substitui a replicação de arquivos .md em projetos.
  - **Racional:** Evita diluição de contexto em turnos longos e mantém prompts leves.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
- **Aprendizado:** O pre-flight do scan_environment.py retorna status HEALTHY com exit code 0 com .env e .venv configurados.
  - **Racional:** Garante execução fluida dos hooks nos workflows.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)

## [PROJETO]
- **Aprendizado:** O Vitalia SDD opera no paradigma de biblioteca geradora de SKILLs nos projetos via install-project.sh.
  - **Racional:** Mantém inteligência centralizada no Kit e projeta SKILLs limpos nas IDEs.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
