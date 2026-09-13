Trabalho de diagnostico de processos em linux

Aluno: Atos Gabriel de Almeida Gomes

Descrição da aplicação: Escolhi rodar um codigo simples em python utilizando o VSCODE, por conhecer o minimo da liguagem e do editor de codigo, assim conseguindo rodar um loop infinito para verificação do serviço

Ambiente utilizado: Xunbuntu 25.10 em maquina virtual (iso fornecida em sala de aula)

Como executar a aplicação analisada: Codigo em python nomeado de "teste.py" basta abrir em um editor de codigo e rodar, como mencionado antes utilizei o VSCODE para a analise.

Comandos utilizados: 
python3 teste.py
Executa o script teste.py usando o Python 3.

pgrep -af teste.py
Localiza o processo teste.py e mostra seu PID e o comando utilizado.

ps -o pid,ppid,cmd -p 8468
Mostra o PID, PPID e o comando do processo.

ps -p 8468 -o args
Mostra o comando completo usado para executar o processo.

pstree 8468
Mostra a árvore relacionada ao processo.

pstree -sp 8468
Mostra a hierarquia de processos pais até chegar ao processo analisado.

ps -o pid,ppid,stat,%cpu,%mem,pri,ni,cmd -p 8468
Mostra o estado, uso de CPU, memória, prioridade, nice, PID e PPID do processo.

ps -L -p 8468
Mostra as threads existentes no processo.

cat /proc/8468/status
Mostra informações detalhadas sobre o estado e características do processo.

tr '\0' ' ' < /proc/8468/cmdline
Mostra o comando utilizado para iniciar o processo através do /proc.

cat /proc/8468/limits
Mostra os limites de recursos definidos para o processo.

ls -l /proc/8468/fd
Mostra os descritores de arquivos associados ao processo.

ps -o pid,stat,cmd -p 8468
Mostra o estado atual do processo antes e depois do envio dos sinais.

kill -STOP 8468
Pausa a execução do processo utilizando o sinal SIGSTOP.

ps -o pid,stat,cmd -p 8468
Verifica o estado do processo após o SIGSTOP.

kill -CONT 8468
Continua a execução do processo utilizando o sinal SIGCONT.

ps -o pid,stat,cmd -p 8468
Verifica o estado do processo após o SIGCONT.

ps -o pid,pri,ni,stat,cmd -p 15145
Mostra a prioridade, o valor nice e o estado da nova instância do processo.

renice 5 -p 15145
Altera o valor nice do processo para 5.

ps -o pid,pri,ni,stat,cmd -p 15145
Confere a alteração da prioridade e do valor nice.

pgrep -af teste.py
Localiza novamente o processo teste.py.

ps -o pid,stat,cmd -p 15145
Verifica o estado do processo antes de encerrá-lo.

kill -TERM 15145
Envia o sinal SIGTERM para encerrar o processo.

ps -o pid,stat,cmd -p 15145
Confirma se o processo foi encerrado.

Evidências para cada requisito

1. PID e PPID

Foi utilizado o comando `pgrep -af teste.py` para localizar o processo e `ps -o pid,ppid,cmd -p 8468` para identificar o PID e o PPID. Na primeira execução, o processo apresentou PID 8468 e PPID 3849.

Evidência: `evidencias/01-pid-ppid/PID-E-PPID.png`

2. Árvore de processos

Foram utilizados os comandos `pstree` e `pstree -sp` para visualizar a posição do processo na árvore. Foi possível observar a hierarquia até `python3(8468)` e a relação entre processo pai e filho.

Evidência: `evidencias/02-arvore-processos/PSTREE.png`

3. Estado, CPU e memória

Foi utilizado o comando `ps -o pid,ppid,stat,%cpu,%mem,pri,ni,cmd -p 8468`. O processo apresentou estado `S+` e foram observados o consumo de CPU e memória durante a execução.

Evidência: `evidencias/03-estado-recursos/ESTADO-INICIAL.png`

4. Prioridade e Nice

Inicialmente o processo apresentou PRI 19 e NI 0. Depois foi utilizado `renice 5 -p 15145` e o valor NI passou para 5, mostrando a alteração da prioridade.

Evidência: `evidencias/03-estado-recursos/RENICE.png`

5. Threads

Foi utilizado o comando `ps -L -p 8468`. A consulta mostrou apenas uma thread observável, confirmada também pelo campo `Threads: 1` em `/proc/8468/status`.

Evidência: `evidencias/04-threads/THREADS.png`

6. Informações em /proc/PID

Foram analisados `/proc/8468/status`, `/proc/8468/cmdline`, `/proc/8468/limits` e `/proc/8468/fd`, obtendo informações sobre estado, comando de execução, limites de recursos e descritores de arquivos.

Evidências: `evidencias/05-proc/STATUS-PROCESSO.png`, `CMDLINE.png`, `LIMITS.png` e `FD.png`

7. Sinais

Foram testados `SIGSTOP`, `SIGCONT` e `SIGTERM`. O `SIGSTOP` pausou o processo, o `SIGCONT` retomou sua execução e o `SIGTERM` encerrou o processo.

Evidências: `evidencias/06-sinais/KILL-STOP.png`, `KILL-CONT.png` e `KILL-TERM.png`

8. Observação sobre a mudança de PID e PPID

Durante o experimento a máquina virtual travou e precisou ser reiniciada. O `teste.py` foi executado novamente e recebeu novos valores de PID e PPID. Por isso algumas capturas mostram o PID 8468 e outras o PID 15145, mas todas pertencem ao mesmo programa executado em momentos diferentes do experimento.

Interpretação dos resultados

Os resultados mostraram na prática como o Linux gerencia os processos durante sua execução. Com o PID e o PPID foi possível identificar o processo teste.py e seu processo pai. A árvore de processos também mostrou a hierarquia existente entre eles.
Durante a execução foram observados diferentes estados do processo. Em alguns momentos ele apareceu como S, indicando que estava aguardando para continuar sua execução. Quando foi enviado o SIGSTOP, o estado mudou para T, mostrando que o processo estava pausado. Após o SIGCONT, ele voltou ao estado normal de execução. Já o SIGTERM encerrou o processo e ele deixou de aparecer na consulta.
A análise de CPU e memória permitiu observar os recursos utilizados pelo programa durante sua execução. Também foi possível verificar que o processo possuía apenas uma thread observável. As consultas no /proc/PID forneceram informações mais detalhadas, como estado, PID, PPID, quantidade de threads, comando de execução, limites de recursos e descritores de arquivos.
Na parte de prioridade, o renice alterou o valor nice de 0 para 5, mostrando que é possível modificar a prioridade relativa de um processo durante sua execução.
Durante o experimento a máquina virtual travou e precisou ser reiniciada. Por isso o teste.py recebeu novos valores de PID e PPID quando foi executado novamente. Isso mostrou também que esses identificadores pertencem àquela execução do processo e podem mudar quando uma nova instância é criada.
No geral, os resultados ajudaram a entender na prática conceitos de gerenciamento de processos como PID, PPID, hierarquia, estados, recursos, prioridade, threads, /proc e sinais.

Conclusão:

O experimento ajudou a entender na prática como o Linux realiza o gerenciamento de processos. Foi possível identificar o processo e seu processo pai, visualizar sua posição na árvore de processos, acompanhar seus estados e observar o uso de CPU e memória. Também foram verificadas as threads e as informações disponíveis no /proc/PID.
Os testes com renice mostraram como a prioridade de um processo pode ser alterada. Já os sinais SIGSTOP, SIGCONT e SIGTERM permitiram observar como um processo pode ser pausado, retomado e encerrado.
Durante o experimento a máquina virtual travou e precisou ser reiniciada. Por esse motivo o teste.py recebeu novos valores de PID e PPID. Isso também mostrou na prática que esses identificadores pertencem a uma determinada instância do processo e podem mudar quando o programa é executado novamente.
No final, o trabalho permitiu relacionar os comandos utilizados com os conceitos estudados em Sistemas Operacionais, principalmente PID, PPID, hierarquia de processos, estados, prioridade, threads, /proc e sinais.
