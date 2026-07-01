# skills

🇺🇸 [Read in English](./README.md)

Uma biblioteca pessoal e crescente de skills do Claude Code que eu uso com frequência. Pública caso seja útil pra mais alguém — instale via [skills.sh](https://www.skills.sh/) ou pela CLI `skills`, use como quiser.

## Estrutura

```
skills/
├── skills/
│   ├── atomic-commits/    # SKILL.md — divide mudanças em commits lógicos, formato Conventional Commits
│   └── git-safe-rename/   # SKILL.md — força `git mv` em renomeações/movimentações, preserva histórico
└── AGENTS.md               # filosofia, convenções, como contribuir (humanos + agentes de IA)
```

## Como usar

Instalar todas as skills:

```
npx skills add sergiooak/skills
```

Ou instalar uma só:

```
npx skills add sergiooak/skills/atomic-commits
npx skills add sergiooak/skills/git-safe-rename
```

- [`atomic-commits`](./skills/atomic-commits/SKILL.md) — divide as mudanças da working tree em múltiplos commits lógicos e atômicos (nunca um commit gigante só), agrupados por feature/tópico, e escreve cada mensagem seguindo as regras do Conventional Commits.
- [`git-safe-rename`](./skills/git-safe-rename/SKILL.md) — força `git mv` em vez de mover/renomear no nível do SO em arquivos versionados, pra o histórico do Git seguir o arquivo.

Pra entender a lógica por trás da estrutura e como adicionar novas skills, veja [`AGENTS.md`](./AGENTS.md) (em inglês).

## Licença

MIT — veja [LICENSE](./LICENSE).
