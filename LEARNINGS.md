<!-- LEARNINGS.md | Atualizado em: 17-09-2026 14:25:36(GMT-04:00) -->
# 💡 Aprendizados Técnicos e Lições Aprendidas Consolidadas

**Data/Hora de Geração:** `17-09-2026 14:25:36(GMT-04:00)` | **Fuso Horário:** America/Cuiaba `(GMT-04:00)`

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
- **Aprendizado:** O LLM não deve duplicar lógicas implementadas pelo orquestrador Python.
  - **Racional:** Delegar compilação de markdown para o LLM aumenta taxa de erro e vulnerabilidade; o motor nativo garante determinismo e padronização das views (README.md, LEARNINGS.md).
  - **Origem:** `andrenote` | **Data:** 08-09-2026 17:46:15(GMT-04:00)
- **Aprendizado:** Schemas JSON injetados no context (Lifting) blindam a extração do LLM contra Prompt Injection e erros estruturais.
  - **Racional:** A presença do schema durante o session-end e session-consolidate garante as chaves corretas e a semântica de domínios restritos antes do parse no Python/Bash.
  - **Origem:** `andrenote` | **Data:** 08-09-2026 17:46:15(GMT-04:00)
- **Aprendizado:** [KIT] A validação automatizada através de smoke tests CLI confirma paridade de execução entre kit-global e ~/.vitalia.
  - **Racional:** Garante que a reinstalação via kit-bootstrap.sh e install-project reflete instantaneamente as melhorias nos workflows e nos scripts nativos sem divergência de runtime.
  - **Origem:** `andrenote` | **Data:** 14-09-2026 21:05:30(GMT-04:00)
- **Aprendizado:** [KIT] Injeção de gates constitucionais sdd_judge nos TOMLs de workflow padroniza a verificação pré e pós-implementação.
  - **Racional:** Elimina dependência de verificações manuais e garante que specs, plans, tasks e diffs atendam à constituição ativamente.
  - **Origem:** `andrenote` | **Data:** 14-09-2026 21:05:30(GMT-04:00)
- **Aprendizado:** [KIT] A varredura holística de documentos inteiros no sdd_judge.py elimina gargalos de limite de taxa (HTTP 429) e melhora a compreensão contextual cruzada pelo Gemini API.
  - **Racional:** Evita estourar a cota de requisições por minuto e permite avaliação integrada de specs complexas.
  - **Origem:** `andrenote` | **Data:** 16-09-2026 20:01:34(GMT-04:00)
- **Aprendizado:** [KIT] Preservar o motor sdd_judge.py 100% agnóstico de projetos garante interoperabilidade total do Vitalia Kit em múltiplos workspaces.
  - **Racional:** Elimina acoplamento com estruturas locais e permite reutilização em qualquer repositório.
  - **Origem:** `andrenote` | **Data:** 16-09-2026 20:01:34(GMT-04:00)

## [PROJETO]
- **Aprendizado:** O Vitalia SDD opera no paradigma de biblioteca geradora de SKILLs nos projetos via install-project.sh.
  - **Racional:** Mantém inteligência centralizada no Kit e projeta SKILLs limpos nas IDEs.
  - **Origem:** `andrenote` | **Data:** 29-08-2026 11:23:41(GMT-04:00)
- **Aprendizado:** Na transição de registros cru-texto para schemas estruturados, a introdução de campos base (como schema_version e schema_type) no normalizer é crítica.
  - **Racional:** Essencial para garantir a sobrevivência de dados legados e compatibilidade em renderizações futuras e parsers rigorosos.
  - **Origem:** `andrenote` | **Data:** 06-09-2026 11:56:55(GMT-04:00)
- **Aprendizado:** Diferenciar caminhos de leitura e escrita isola variáveis de estado global versus logs locais
  - **Racional:** Forçar leitura do Global YAML e restrição de append no Local JSONL evita corrupção assíncrona entre módulos do sistema SDD e agentes satélites.
  - **Origem:** `andrenote` | **Data:** 08-09-2026 17:46:15(GMT-04:00)

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
- **Aprendizado:** [KIT] Falha na leitura do env_context.json no brainstorming
  - **Racional:** O hook_runner redireciona o stdout do subprocesso (scan_environment.py) para o stderr, impedindo que o tmp/env_context.json seja gerado fisicamente no disco. Isso bloqueia o Socratic Gate de acessar o contexto do ambiente.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 21:34:49(GMT-04:00)
- **Aprendizado:** [KIT] Ausência de persistência do payload gerado pelo hook runner
  - **Racional:** O vitalia_hook_runner.py emite o json compilado (prompt + guardian_json) apenas no stdout para a IA, dificultando auditoria. O ideal seria persistir uma cópia em tmp/.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 21:34:49(GMT-04:00)
- **Aprendizado:** [KIT] Context Engineering para Modelos Locais
  - **Racional:** Para suportar limites estritos de 8192 tokens, o payload do Guardian não pode ser ejetado integralmente no prompt inicial. O uso de arquivos temporários combinados com um Stub Referencial obriga o LLM a fazer Lazy Loading via tools, evitando OOM.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 23:30:11(GMT-04:00)
- **Aprendizado:** [KIT] Fallback de Sessão
  - **Racional:** A variável VITALIA_SESSION_ID ainda não é exportada pela IDE no bootstrap. O uso de um timestamp higienizado (ex: YYYYMMDD_HHMMSS) como fallback garante a continuidade do fluxo temporal na nomenclatura dos arquivos de contexto temporários.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 23:30:11(GMT-04:00)
- **Aprendizado:** [KIT] A inicialização da nova versão do Kit (v0.6.0) flui sem falhas locais.
  - **Racional:** O scan_environment.py reconhece com precisão as portas locais de Redis e Postgres, permitindo o avanço sem erros de dependência.
  - **Origem:** `andrenote` | **Data:** 08-09-2026 20:09:41(GMT-04:00)
- **Aprendizado:** [KIT] Trativa de comentários no parser load_dotenv_native
  - **Racional:** Comentários inline no formato KEY= # comment sem espaço prévio devem ser sanitizados para não poluir variáveis em os.environ nem bloquear redefinições posteriores no arquivo .env.
  - **Origem:** `andrenote` | **Data:** 17-09-2026 14:01:08(GMT-04:00)
- **Aprendizado:** [KIT] Resiliência de APIs de Nuvem via Exponential Backoff
  - **Racional:** Requisições de inferência cloud submetidas a flutuações de cota (HTTP 429) ou sobrecarga (HTTP 503) necessitam de retries com backoff exponencial progressivo (ex: 3s, 6s, 12s) para permitir o reset das janelas de taxa da API sem falhar precocemente.
  - **Origem:** `andrenote` | **Data:** 17-09-2026 14:01:08(GMT-04:00)

## PROJETO
- **Aprendizado:** [PROJETO] TOMLs spec-plan e spec-specify referenciavam profiles/grounding_domains.yaml inexistente — grounding silenciosamente ignorado
  - **Racional:** Arquivo criado com 9 domínios (llm_models, python_packages, external_apis, security_practices, regulations, cloud_services, scientific_claims, clinical_safety, hardware_specs) + authoritative_sources + trigger.
  - **Origem:** `andrenote` | **Data:** 07-09-2026 18:58:42(GMT-04:00)
- **Aprendizado:** [PROJETO] Auto-bootstrap em CLI entrypoints
  - **Racional:** Pontos de entrada CLI invocados diretamente pelo usuário (fora do vitalia_hook_runner.py) devem chamar kit_env_bootstrap.init() no início da função main() para garantir que o ambiente .env e .venv estejam carregados.
  - **Origem:** `andrenote` | **Data:** 17-09-2026 14:01:08(GMT-04:00)
