# Validação para uso por agentes de IA

Data da validação: 2026-07-03

## Resultado executivo

O pacote está pronto como skill reutilizável para Codex e como base de conhecimento/instrução para agentes de IA que aceitam arquivos Markdown, contexto de projeto ou conhecimento anexado. Para Gemini, Claude, ChatGPT customizado, agentes internos e cursos, o conteúdo está pronto em formato portátil, mas pode exigir empacotamento ou adapter específico da plataforma, porque nem todas leem `SKILL.md` e `agents/openai.yaml` nativamente.

Veredito: **PRONTO COM ADAPTER OPCIONAL**

## Evidências da validação

| Critério | Resultado | Evidência |
|---|---|---|
| Validação Codex de skill | Conforme | `quick_validate.py .` retornou `Skill is valid!` |
| Frontmatter `SKILL.md` | Conforme | contém apenas `name` e `description` |
| Progressive disclosure | Conforme | `SKILL.md` tem 112 linhas e roteia para referências sob demanda |
| Referências internas | Conforme | referências principais estão listadas em `SKILL.md` e existem no pacote |
| Fontes oficiais | Conforme | Planalto, ANPD, Senacon, Consumidor.gov.br e STJ documentados em `docs/fontes-oficiais.md` |
| Cobertura temática | Conforme | CDC, LGPD, Marco Civil, produtos digitais, e-commerce, SAC, Procon, Consumidor.gov.br, marketplaces, incidentes e plataformas |
| Evals/casos de teste | Conforme | 17 casos cobrindo CDC clássico, produtos digitais, Marco Civil e LGPD |
| Portabilidade | Parcialmente conforme | Markdown é portátil; metadados `agents/openai.yaml` são específicos de interfaces compatíveis |
| Segurança jurídica | Conforme | política proíbe prometer resultado, inventar jurisprudência, tratar privacidade só por CDC ou afirmar dano moral automático |
| Resíduos de ambiente | Conforme | não foram encontrados links `sandbox:/`, `/mnt/data`, `utm_source`, `TODO`, `FIXME` ou caminhos absolutos locais em conteúdo do pacote |

## Compatibilidade por ambiente

| Ambiente | Status | Como usar |
|---|---|---|
| Codex | Pronto | Instalar a pasta como skill; `quick_validate.py` já validou a estrutura |
| OpenAI custom agents | Pronto com ajuste leve | Usar `SKILL.md` como instrução principal e anexar `docs/`, `templates/` e `evals/` como conhecimento |
| ChatGPT/GPTs | Pronto como conhecimento | Usar `SKILL.md` no prompt de instruções e anexar os arquivos de referência |
| Claude Projects | Pronto como conhecimento | Colocar `SKILL.md`, `docs/`, `templates/` e `evals/` no projeto; instruir o modelo a seguir `SKILL.md` como roteador |
| Gemini/Gems | Pronto como conhecimento | Usar `SKILL.md` como instrução da Gem e anexar referências essenciais; se houver limite de contexto, priorizar `fontes-oficiais`, `matriz`, `politica-de-resposta`, `lgpd` e `marco-civil` |
| Agentes internos/RAG | Pronto | Indexar `docs/` por arquivo e usar `SKILL.md` como policy/router |
| Cursos/treinamento | Pronto | Usar `README.md`, `SKILL.md`, checklists e `evals/casos-teste.md` como material prático |

## Arquivos essenciais

Para uso mínimo:

- `SKILL.md`
- `docs/fontes-oficiais.md`
- `docs/pesquisa-e-atualizacao.md`
- `docs/matriz-temas-e-fontes.md`
- `docs/politica-de-resposta.md`
- `docs/lgpd-protecao-dados.md`
- `docs/marco-civil-internet.md`
- `docs/revisao-produtos-digitais.md`

Para uso completo:

- todos os arquivos em `docs/checklists/`
- todos os arquivos em `templates/`
- `evals/casos-teste.md`
- `agents/openai.yaml` quando a interface aceitar metadados

## Testes recomendados antes de publicar

Use `evals/casos-teste.md` e verifique se o agente:

1. cita CDC, LGPD e Marco Civil apenas quando pertinentes;
2. separa fato, prova, base provável e ressalva;
3. pede documentos mínimos antes de concluir;
4. não promete resultado jurídico;
5. usa LGPD como base primária para política de privacidade;
6. ressalva vigência do Decreto nº 12.975/2026 quando aplicável;
7. diferencia controlador, operador, titular, provedor de conexão e provedor de aplicação;
8. encaminha casos de risco para advogado, Defensoria, Procon, ANPD, Anatel, autoridade policial ou órgão competente.

## Limitações

- A skill não é um parecer jurídico e não substitui revisão profissional.
- As plataformas Gemini, Claude e outras podem ter formatos próprios de prompt, projeto, arquivo ou limite de contexto; este pacote é portátil em Markdown, mas não garante importação nativa sem adapter.
- Como CDC, LGPD, Marco Civil, ANPD e jurisprudência podem mudar, respostas sensíveis devem consultar fontes oficiais em tempo real.
- Para uso em produção, mantenha um processo periódico de atualização normativa e reexecute os casos de teste.

## Veredito final

O pacote está apto para uso por agentes de IA como skill/knowledge pack jurídico-informativo brasileiro, com escopo claro, fontes oficiais, roteamento por tema, checklists, templates e evals. A única ressalva é de integração: Codex consome o formato diretamente; outras plataformas devem receber o conteúdo como instrução + arquivos de conhecimento ou via adapter.
