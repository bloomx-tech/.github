# .github — guia do repositório

<!-- regras-agente:inicio -->
## Regras Karpathy — como o agente trabalha aqui

1. **Pense antes.** Declare suposições e interpretações possíveis; sugira caminhos mais simples. Se houver dúvida, pare e pergunte.
2. **Simplifique.** Faça o mínimo necessário, sem features especulativas, abstrações de uso único, flexibilidade não pedida ou erros impossíveis. Encurte o que puder.
3. **Seja cirúrgico.** Toda linha alterada deve servir à tarefa. Siga o estilo local, não refatore o que funciona e remova só os órfãos que criou; reporte código morto preexistente.
4. **Verifique.** Converta a tarefa em critérios testáveis e itere até passar. Validação começa pelo teste da entrada inválida; correção, pela reprodução. Em tarefas com vários passos, dê um plano curto com `verify:` por passo.

<a id="regras-de-escrita"></a>

## Escrita (ASD-STE100)

Todo texto escrito para uma pessoa ler segue seis regras. Elas vêm do ASD-STE100, o inglês
controlado dos manuais de aeronave, adaptadas ao português. Valem para commit, pull request, comentário
de revisão, documentação e mensagem de agente.

1. No máximo 20 palavras por frase.
2. Uma palavra, um sentido.
3. O mesmo termo para a mesma coisa, do começo ao fim. Não troque por sinônimo.
4. Voz ativa: diga quem faz o quê.
5. Uma ideia por frase.
6. Palavras simples. Sem enchimento e sem suposição.

Exemplo. Em vez de: "O cache é essencialmente uma camada de armazenamento de alta velocidade que mantém
por perto o dado mais acessado, para a aplicação recuperar a informação bem mais rápido." Escreva: "O
cache é uma memória pequena e rápida. Ele guarda uma cópia do dado que você usa muito. O sistema lê o
cache primeiro."

Ficam como estão: código, identificadores, comandos, mensagens de erro e citações. A regra vale para
texto novo e para texto que a mudança já reescreve. Não reescreva um documento só para aplicá-la.
<!-- regras-agente:fim -->

## O que é

Este repositório guarda a página pública da org no GitHub (`profile/README.md`) e os logotipos (`profile/assets/`).
Tudo aqui é público, este arquivo também. Nada interno entra neste repositório.

## Regras comuns

- **Idioma.** Commit, PR, este guia e a página pública (`profile/README.md`) ficam em português do
  Brasil. O tipo do commit fica em inglês.
- **Branches.** O padrão é `main`. Use os prefixos `feat/`, `fix/`, `chore/` e `docs/`. O merge publica
  a página na hora.
- **Merge.** O repositório aceita merge commit, squash e rebase.
- **Commits.** `tipo(escopo): resumo em português`.
- **PR.** Cada mudança tem uma branch e no máximo um PR aberto neste repositório.

## Segurança

<!-- seguranca-comum:inicio -->
**Núcleo comum de segurança.** Este bloco é igual, byte a byte, em todo repositório da org `bloomx-tech`.
Mude em todos ou em nenhum. Cada regra é uma ordem. A linha _Porquê_ diz a causa.

1. **Segredo nunca entra no repositório, no log nem na resposta.** Nunca escreva o valor de um segredo em
   código, teste, log, commit, pull request ou saída de ferramenta. Segredo inclui chave, token, senha,
   PAN, CVV, OTP, token de biometria e CPF completo. Todo segredo mora no cofre. Toda entrada no
   `.gitleaksignore` leva uma justificativa ao lado.
   _Porquê:_ um segredo no histórico do Git continua válido até alguém trocar a credencial.
2. **Uma identidade por pessoa, por serviço e por terminal.** Credencial compartilhada nunca prova quem
   chama. Não crie conta de papel, login de grupo nem chave comum a vários serviços.
   _Porquê:_ com identidade compartilhada, um vazamento atinge todos. A trilha não mostra quem agiu.
3. **Material distribuído é público.** Tudo que vai num APK, AAR, SDK, imagem ou bundle web pode ser
   extraído. Nunca trate esse material como segredo nem como prova de identidade.
   _Porquê:_ quem tem o arquivo tem o mesmo material que o terminal ou o navegador.
4. **Confirme na fonte da verdade.** Não aceite a palavra de quem chama sobre valor pago, status do
   provedor, dono do terminal ou cabeçalho de identidade. Confirme com quem tem o dado.
   _Porquê:_ quem chama pode mentir. A fonte da verdade é o adquirente, o provedor ou a chave registrada.
5. **Rota que cria sessão, credencial, certificado, chave ou destino de dinheiro é rota crítica.** O pull
   request que cria ou muda uma rota crítica precisa de quatro coisas:
   - o modelo de ameaça no corpo do pull request: quem chama, o que prova e o efeito se o material vazar;
   - testes negativos: sem prova, com a prova de outro e com replay;
   - a documentação de auth ou de API e o `CHANGELOG` atualizados no mesmo pull request;
   - a revisão de uma segunda pessoa. Agente de IA não aprova nem faz merge desse pull request sozinho.

   _Porquê:_ uma rota crítica sem revisão e sem documentação fica fora do modelo de ameaça.
6. **Nada temporário sem data e dono.** Atalho, flag, acesso, recurso ou rota provisória nasce com data de
   remoção e com um responsável. Os dois dados ficam no código e no pull request.
   _Porquê:_ o temporário sem data fica para sempre.
7. **Controle desligado não é controle.** Produção recusa subir sem o controle. Desligar um controle é uma
   decisão registrada, nunca um valor padrão silencioso.
   _Porquê:_ um controle que existe e está desligado dá uma confiança falsa.
8. **Toda ação sensível deixa trilha.** Ação de admin, de identidade e de dinheiro grava um evento de
   auditoria. Operação em massa também. Nenhuma ação de frota acontece sem registro no backend.
   _Porquê:_ sem trilha, ninguém detecta o abuso nem responde a ele.
9. **Mudança de segurança na frota não quebra a frota.** Primeiro em sombra, depois atrás de uma chave de
   Ops, por fim a recusa. A ponte no backend vem antes do SDK. Uma correção que quebra a frota sai do pull
   request e entra na fila gradual.
   _Porquê:_ a frota inteira depende do caminho atual. Uma recusa direta para a venda.
10. **Cada carga roda no ambiente e na conta dela.** Nada novo nasce na conta de gestão nem num recurso
    legado. Staging nunca usa credencial de produção.
    _Porquê:_ com ambientes misturados, a falha de um atinge os outros.
11. **Regras para agentes de IA.**
    - Nunca contorne um bloqueio do classificador ou de permissão. Entregue o comando para a pessoa.
    - Nunca escreva em produção. Nunca crie recurso de nuvem fora do IaC.
    - Nunca use em sessão humana a credencial de um bot.
    - Leia dados de produção só em modo de leitura e só em agregados.
    - Nunca cole conteúdo sigiloso em pull request, issue ou artefato.

    _Porquê:_ o agente age rápido e em escala. Um erro dele vira incidente antes de alguém ver.
<!-- seguranca-comum:fim -->
