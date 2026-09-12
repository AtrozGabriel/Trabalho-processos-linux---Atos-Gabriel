Trabalho de diagnostico de processos em linux

Aluno: Atos Gabriel de Almeida Gomes

Descrição da aplicação: Escolhi rodar um codigo simples em python utilizando o VSCODE, por conhecer o minimo da liguagem e do editor de codigo, assim conseguindo rodar um loop infinito para verificação do serviço

Ambiente utilizado: Xunbuntu 25.10 em maquina virtual (iso fornecida em sala de aula)

Como executar a aplicação analisada: Codigo em python nomeado de "teste.py" basta abrir em um editor de codigo e rodar, como mencionado antes utilizei o VSCODE para a analise.

Comandos utilizados: 
pgrep - af teste.py
ps -o pid,ppid,cmd PID
ps -p  PID -o args
pstree PID
pstree -sp PID


