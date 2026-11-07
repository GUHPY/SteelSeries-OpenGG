# AGENTS.md - Protocolo Obrigatório de Commits & Desenvolvimento
**Projeto:** `OpenGG`  
**Escopo Principal:** `Gaming Tools, Telemetry, Overlay HUD, Performance`  
**Descrição:** Ferramenta open-source de overlay e telemetria para jogos.

> **DIRETIVA CRÍTICA PARA TODOS OS AGENTES DE IA (Antigravity, Cursor, Claude Code, Codex, Windsurf, OpenHands, etc.):**
> Commits são feitos **no fim da tarefa**, não em tempo real. Uma tarefa (ex.: plano F1…F10) gera
> **poucos commits semânticos** (em geral 1 por fase ou por camada), e o push é feito **uma vez, no final**.
> Meta: uma tarefa inteira cabe em ~3 a 10 commits. Nunca um commit por arquivo.

---

## 1. Princípio Fundamental: Commits por Tarefa, no Final
- **Quando commitar**: só ao terminar a tarefa inteira (todas as fases F1…Fn). Durante o trabalho, nada de commit/push a cada arquivo.
- **Tamanho**: um commit agrupa uma unidade lógica completa (uma fase, uma feature, uma camada). Pode ter quantos arquivos ela precisar.
- **Separação**: separe só o que tem sentido separado: código, testes e docs/checklists podem ir juntos se pertencem à mesma fase. Refatoração grande e feature nova ficam em commits distintos.
- **Teto**: uma tarefa típica = 3 a 10 commits. Mais que isso, junte.
---

## 2. Formato Padronizado de Mensagens (Conventional Commits)
Siga o padrão:
`<tipo>(<escopo>): <descrição clara e objetiva>`

### Tipos Válidos:
- `feat`: Nova funcionalidade, componente, endpoint ou recurso.
- `fix`: Correção de bug, tratamento de exceção ou ajuste de comportamento.
- `perf`: Otimização de desempenho, memória, zero-copy ou renderização.
- `refactor`: Refatoração estrutural sem alteração funcional externa.
- `docs`: Documentação técnica, specs de arquitetura, guias de módulo.
- `test`: Testes unitários, de regressão ou matriz de validação.
- `chore`: Atualização de dependências, scripts de build ou ponteiros de submódulo.

### Exemplos Válidos para OpenGG:
- `feat(gaming tools): add initial implementation`
- `fix(gaming tools): resolve edge case handling`
- `docs(gaming tools): update technical architecture spec`

---

## 3. Regra do Commit Duplo (Sincronização com DevLogs)
Sempre que você implementar uma arquitetura nova, refatoração estrutural ou otimização importante:
1. Ao fim da tarefa, comite as alterações no repositório local deste projeto.
2. Registre uma entrada técnica correspondente no repositório de histórico técnico:
   `X:\gugac\Desktop\Projects\DevLogs\logs\<projeto>\<submodulo>.md`
3. Comite no `DevLogs` detalhando: decisões técnicas tomadas, benchmarks e validações.

---

## 4. Identidade de Git Obrigatória
Antes de commitar, certifique-se de que o autor está configurado como:
```bash
git config user.name "GUHPY"
git config user.email "gugadiamon@gmail.com"
```
Todos os commits devem pertencer à conta oficial para contabilização no perfil do GitHub.

---

## 5. Higiene do Repositório & Árvore Limpa
- **Árvore de Trabalho Limpa**: Nunca encerre um turno ou tarefa deixando arquivos modificados ou `untracked` pendentes no `git status`.
- **Merge & Push Contínuos**: Mantenha a branch `main` atualizada e envie as alterações para o remoto (`git push origin <branch>`).
- **Submódulos**: Se você alterar algo dentro de uma subpasta que seja submódulo git, lembre-se de entrar na pasta pai e commitar a atualização do ponteiro do submódulo.

---

## 6. Checklist de Execução para Agentes
- [ ] Tarefa inteira concluída e verificada (typecheck/testes) antes de commitar.
- [ ] `git status` checado; arquivos agrupados em poucos commits lógicos (fase/feature).
- [ ] `git commit -m "<tipo>(<escopo>): <mensagem>"` com mensagem descritiva.
- [ ] Um único `git push origin <branch>` no fim da tarefa.
---

## 7. Fluxo Obrigatório de Documentação por Etapa

Toda tarefa que não seja trivial (mais de um arquivo ou mais de um passo) segue este ciclo. **Nunca substitua a documentação existente do projeto: acrescente.**

1. **Plano por fases**: antes de codar, escreva ou atualize o plano na pasta de docs do projeto (ex.: `Docs/<área>/ativo/<tarefa>/<nome>-PLANO.md`). Divida em fases F1…Fn. Cada fase tem: o escopo, os arquivos tocados, a origem (de onde vem a referência) e o **aceite** (o que prova que ficou pronto).
2. **Execução fase a fase**: implemente uma fase por vez, na ordem. Não peça permissão entre fases quando o plano já foi aprovado.
3. **Reverificação ao fim de CADA fase**, antes de seguir:
   - typecheck/compilação do que foi tocado;
   - testes unitários da área (e um teste novo para lógica não trivial);
   - os greps/checagens de aceite que o plano definir;
   - falhas que já existiam antes da tarefa são registradas como pré-existentes, nunca escondidas.
4. **Checklist por fase**: ao fim de cada fase, acrescente uma seção ao checklist acumulado do projeto (ex.: `Docs/<área>/checklists.md`), no formato:
   - `## <Plano> · Fn — <título> (<data>)`;
   - itens `- [ ]` que o usuário consegue testar na tela, escritos como passo + resultado esperado;
   - linhas `- Fora: …` e `- Nota: …` para o que ficou de fora ou mudou, sempre com o motivo.
   Preserve o fim de linha (CRLF/LF) do arquivo.
5. **Documentação por etapa**: atualize as specs, os READMEs ou os guias que a fase deixou desatualizados. Simplificações com teto conhecido levam um comentário no código dizendo o teto e o caminho de upgrade.
6. **Fechamento**: no fim do plano, marque cada item do documento de origem (comparativo, issue, spec) como **feito (Fn)**, **Fora (motivo)** ou **aguardando o usuário**. Rode de novo todas as checagens de aceite.
7. **DevLogs**: registre em `X:\gugac\Desktop\Projects\DevLogs\logs\<projeto>\<submodulo>.md` as decisões, o que ficou fora e a validação (seção 3).

### Commits: poucos e no final
- Commite **ao fim da tarefa**, agrupando por fase ou por feature (não por arquivo).
- Testes, docs e checklists podem ir no commit da fase a que pertencem.
- Push único no final; `git status` limpo ao encerrar.
---

## 8. Commit Duplo + Credencial Única

### Espelho no DevLogs: um por tarefa
- Ao **terminar a tarefa**, registre **uma** entrada em `X:\gugac\Desktop\Projects\DevLogs\logs\<projeto>\<submodulo>.md` cobrindo a tarefa toda (o que mudou, por quê, hashes dos commits, checklist `- [ ]` e `Fora:`/`Nota:`).
- **Um** commit no DevLogs por tarefa (`docs(<projeto>): <resumo da tarefa>`), não um por commit do projeto.
- Ordem: commits do projeto → entrada no DevLogs → commit no DevLogs → push dos dois, uma vez.

### Credencial: somente a do dono
- Todo commit é feito **somente** com a identidade `GUHPY <gugadiamon@gmail.com>` (seção 4).
- **Nunca** use a identidade de agente/IA (Claude, Codex, Cursor, Copilot etc.): sem `Co-Authored-By`, sem trailer "Generated with" e sem autor ou committer de bot, em commits e PRs.
---

## 9. Push + Merge na `main` no Fim da Tarefa
- Ao terminar a tarefa, um único `git push origin <branch>`.
- Se o trabalho está numa branch que não é a `main`, faça o merge na `main` em seguida (`git checkout main && git merge --no-ff <branch> && git push origin main`) e volte para a branch.
- O espelho no DevLogs segue a mesma regra: um commit e um push por tarefa.
- Conflito no merge: resolva sem descartar o trabalho de ninguém. Se não der para resolver com segurança, pare e avise o dono antes de forçar qualquer coisa.

---

## Deploy na HostGator: "Update from Remote" por SSH

Os sites ficam na HostGator (cPanel › Git Version Control). Cada site é um clone de um repositório do GitHub numa branch. O botão **Update from Remote** do cPanel só faz o servidor puxar essa branch do GitHub. Por SSH, o agente roda o mesmo comando.

### Regra padrão: NÃO fazer o update a cada alteração
- Por padrão, o dono **não** quer um Update from Remote depois de toda alteração. Commit e push seguem o protocolo normal deste arquivo; o update, não.
- Só rode o update quando o dono **pedir para aquela sessão** (ex.: "nesta sessão, depois de commitar, dá o update") ou disser **claramente** que é para fazer. Na dúvida, não rode: avise no fim que o site só muda depois do update.
- Pedido de uma sessão não vale para a próxima.

### Acesso
- Atalho já configurado em `C:\Users\gugac\.ssh\config`: `ssh hostgator` (chave `C:\Users\gugac\.ssh\hostgator`, ed25519, sem senha, autorizada no cPanel). IP e usuário moram só nesse config, nunca em repositório.
- Nunca use a chave `id_rsa (cPanel)` nem senha nenhuma; nunca leia nem repita o arquivo `senha id_rsa (cPanel).txt`.
- O domínio dos sites passa pela Cloudflare: SSH sempre pelo atalho `hostgator`, nunca pelo domínio.
- Teste: `ssh -o BatchMode=yes hostgator 'echo ok'`.

### Como fazer (sempre nesta ordem)
1. Commit e **push** para a branch que o cPanel acompanha. O update puxa do GitHub: sem push, nada muda no site.
2. Descobrir a pasta e a branch do site. **Atenção:** a saída crua do `retrieve` mostra a URL do GitHub com token; nunca imprima nem copie essa saída, filtre assim:
   ```bash
   ssh hostgator 'uapi --output=json VersionControl retrieve' | python -c "import sys,json;[print(r['repository_root'],r['branch']) for r in json.load(sys.stdin)['result']['data']]"
   ```
3. Rodar o update (o mesmo do botão) e conferir que `status` é 1 e que o commit é o que você empurrou:
   ```bash
   ssh hostgator 'uapi --output=json VersionControl update repository_root=/home4/<usuario>/<dominio> branch=<branch>' | python -c "import sys,json;r=json.load(sys.stdin)['result'];print(r['status'],r['errors'],(r['data'] or {}).get('last_update',{}).get('identifier'))"
   ```
   O `<usuario>` aparece no `repository_root` do passo 2.
- Só atualize o site do projeto em que você está trabalhando. Nunca mexa nos repositórios dos outros sites da conta.

### Sites da conta (07/11/2026)
| Pasta no servidor | Branch | Projeto |
| --- | --- | --- |
| `devdesignlibrary.com` | `site` | Parallel (DDL), worktree `Parallel Canvas/ddl-site` |
| `luz.gg` | `site` | Luz |
| `econographs.com` | `site` | Econographs |
| `appduobot.com` | `site` | Duobot |
| `betterlandingco.com` | `main` | Better Landing |
| `brandmydiploma.com`, `brandmydegree.com` | `main` | Brand My Diploma |
| `thedoctorlogos.com`, `thedrlogos.com`, `thedrbrands.com` | `main` | Dr Logos (fora deste workspace) |
