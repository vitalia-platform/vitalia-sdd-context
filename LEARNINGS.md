<!-- LEARNINGS.md | Atualizado em: 07-09-2026 19:02:29(GMT-04:00) -->
# 💡 Aprendizados Técnicos e Lições Aprendidas Consolidadas

**Data/Hora de Geração:** `07-09-2026 19:02:29(GMT-04:00)` | **Fuso Horário:** America/Cuiaba `(GMT-04:00)`

## [KIT]
- **Aprendizado:** A centralização de regras em constitution_data.yaml combinada com pruning do guardian_context.py substitui a replicação de arquivos .md em projetos.
  - **Racional:** Evita diluição de contexto em turnos longos e mantém prompts leves.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
- **Aprendizado:** O pre-flight do scan_environment.py retorna status HEALTHY com exit code 0 com .env e .venv configurados.
  - **Racional:** Garante execução fluida dos hooks nos workflows.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
- **Aprendizado:** Havia uma grave dessincronização de arquitetura: o prompt session-end orientava a IA a escrever o shard YAML "na mão" com chaves antigas (task, p0), causando falha invisível nos renderizadores do schema v0.5.0. Delegação de I/O complexo deve sempre passar pelas flags CLI do motor.
  - **Racional:** Garante a integridade do schema persistido e evita alucinações ou quebras de sintaxe.
  - **Origem:** `andrenote` | **Data:** 06-09-2026 08:42:22(GMT-04:00)
- **Aprendizado:** Desalinhamento técnico de tipagem corrigido: o learning_schema.json exigia a chave content, mas o Python extraía learning e rationale.
  - **Racional:** Schemas estáticos foram atualizados para refletir o comportamento real do parser, alinhando a documentação com a execução.
  - **Origem:** `andrenote` | **Data:** 06-09-2026 08:42:22(GMT-04:00)
- **Aprendizado:** Para blindar especificações arquiteturais, a inspeção de arquivos-fonte reais é indispensável. O uso de planos puramente dedutivos e genéricos gera lacunas e o risco de implementações destrutivas por IA.
  - **Racional:** Baseado na falha evitada durante o ciclo SDD onde um plano vago teria corrompido o código local.
  - **Origem:** `andrenote` | **Data:** 06-09-2026 11:56:55(GMT-04:00)

## [PROJETO]
- **Aprendizado:** O Vitalia SDD opera no paradigma de biblioteca geradora de SKILLs nos projetos via install-project.sh.
  - **Racional:** Mantém inteligência centralizada no Kit e projeta SKILLs limpos nas IDEs.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
- **Aprendizado:** Na transição de registros cru-texto para schemas estruturados, a introdução de campos base (como schema_version e schema_type) no normalizer é crítica.
  - **Racional:** Essencial para garantir a sobrevivência de dados legados e compatibilidade em renderizações futuras e parsers rigorosos.
  - **Origem:** `andrenote` | **Data:** 06-09-2026 11:56:55(GMT-04:00)

## KIT
- **Aprendizado:** [KIT] Motor Guardian configurado mas nunca conectado aos workflows — [guardian] nunca declarado em nenhum TOML
  - **Racional:** Todos os 9 workflows prioritários operavam sem injeção de contexto constitucional. Fix: [guardian] adicionado em session-start, brainstorming, vitalia-route, analyze, spec-specify, spec-plan, task-verifier, spec-implement, medical-gate.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)
- **Aprendizado:** [KIT] grounding-domains-local.yaml em profiles/ era VIEW em local incorreto — naming causava confusão com arquivo-fonte
  - **Racional:** Arquivo VIEW gerado pelo motor de contexto estava sendo tratado como fonte. Correto: profiles/grounding_domains.yaml é a fonte; VIEW vai para .vitalia/memory/session/ (futuro).
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)
- **Aprendizado:** [KIT] machine_id hardcoded '7f367bd3' = SHA256('andrenote')[:8] em vitalia_context_engine.py
  - **Racional:** Fix P1 aplicado: derivar de VITALIA_MACHINE_NAME env var ou socket.gethostname() com SHA256[:8]. Princípio P11 (Hardware-Agnostic).
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)
- **Aprendizado:** [KIT] scan_environment.py com exit(1) em DEGRADED bloqueava todos os workflows sem Redis
  - **Racional:** Redis é infraestrutura opcional. Fix: exit(0) em DEGRADED; exit(1) apenas quando .env está ausente (sem configuração básica).
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)

## PROJETO
- **Aprendizado:** [PROJETO] TOMLs spec-plan e spec-specify referenciavam profiles/grounding_domains.yaml inexistente — grounding silenciosamente ignorado
  - **Racional:** Arquivo criado com 9 domínios (llm_models, python_packages, external_apis, security_practices, regulations, cloud_services, scientific_claims, clinical_safety, hardware_specs) + authoritative_sources + trigger.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)
