# Minhas Skills

Este repositório reúne minhas skills reutilizáveis para agentes de IA, incluindo Codex e Claude Code. Código-fonte: [github.com/RobertoBarros/skills](https://github.com/RobertoBarros/skills).

Cada pasta em `skills/` representa uma skill independente. O arquivo `SKILL.md` contém as instruções principais; pastas adicionais, como `scripts/`, `references/` e `assets/`, são incluídas apenas quando necessárias.

## Skills disponíveis

- [`tool-pick`](skills/tool-pick/): pesquisa e compara bibliotecas, frameworks, pacotes, CLIs e outras ferramentas de software open source.

As skills seguem o formato `SKILL.md` para permanecerem portáveis entre diferentes harnesses.

## Instalação

### Com `npx skills` (opcional)

O [Skills CLI](https://skills.sh/) é uma ferramenta para instalar skills de repositórios Git. Use os comandos abaixo somente se você já tiver o `npx skills` instalado; a instalação manual continua sendo uma alternativa.

Para instalar todas as skills deste repositório no Codex, no projeto atual:

```bash
npx skills add RobertoBarros/skills --skill '*' --agent codex --yes
```

Para instalá-las globalmente no Codex, deixando-as disponíveis em todos os projetos:

```bash
npx skills add RobertoBarros/skills --skill '*' --agent codex --global --yes
```

Troque `codex` pelo identificador de outro agente, como `claude-code` ou `cursor`, se necessário.
