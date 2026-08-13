# Tool Pick

Uma skill para pesquisar e recomendar bibliotecas e ferramentas de software com critérios verificáveis. Ela existe para evitar escolhas baseadas só em listas genéricas, resultados patrocinados ou uma métrica isolada. O fluxo começa por coleções curadas "awesome" no GitHub e valida cada candidato no repositório upstream, equilibrando adequação técnica, licença, atividade, adoção e maturidade.

## Princípios

- **Descoberta curada primeiro:** usar listas "awesome" relevantes como ponto de partida, preferindo as populares e mantidas recentemente.
- **Evidência primária:** avaliar candidatos no repositório original, e não em forks ou agregadores.
- **Open source:** confirmar a licença e destacar incompatibilidades.
- **Saúde acima de hype:** considerar releases, commits, contribuidores, comunidade e adoção; estrelas são um sinal, não a decisão inteira.
- **Aderência ao problema:** escolher pelo encaixe técnico antes de popularidade.

## Instalação

Clone ou baixe este diretório. Depois, copie a pasta `tool-pick` para o diretório de skills do harness escolhido.

### Codex

```bash
git clone <URL-DO-SEU-REPOSITORIO>
mkdir -p ~/.codex/skills
cp -R <DIRETORIO-CLONADO>/tool-pick ~/.codex/skills/
```

### Claude Code

Para disponibilizar a skill em todos os projetos:

```bash
mkdir -p ~/.claude/skills
cp -R <DIRETORIO-CLONADO>/tool-pick ~/.claude/skills/
```

Para disponibilizá-la apenas no projeto atual, use `.claude/skills/` na raiz do projeto.

### Outros harnesses

Use a convenção de skills do seu ambiente e preserve a pasta `tool-pick` com o arquivo `SKILL.md` em sua raiz. O diretório `agents/` é opcional: contém metadados de interface específicos do OpenAI e pode ser ignorado por outros harnesses.

Abra uma nova sessão, se o seu harness exigir, e peça algo como:

```text
Use a skill tool-pick para encontrar uma biblioteca TypeScript open source para gerar PDFs no servidor.
```

Em harnesses com descoberta automática, a skill também pode ser ativada quando o pedido corresponde à descrição dela. Use a sintaxe de invocação explícita do seu ambiente quando quiser garanti-la (por exemplo, `$tool-pick` no Codex).

## Contribuições

Melhorias devem preservar os princípios acima e incluir instruções que possam ser verificadas em pesquisas reais. Evite transformar a skill em uma lista fixa de ferramentas: o objetivo é pesquisar evidências atuais para cada pedido.

Licenciada sob a [MIT License](LICENSE).
