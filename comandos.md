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
