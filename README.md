# 🖧 Script para Ativar o Serviço RPC em Múltiplas Máquinas

![Batchfile](https://img.shields.io/badge/Batch-Script-4D4D4D?style=flat&logo=windowsterminal&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?style=flat&logo=windows&logoColor=white)

Este script usa o PsExec para ativar o serviço RPC (Remote Procedure Call) em várias máquinas remotas listadas em um arquivo de texto.

## 📌 Pré-requisitos

- **PsExec:** certifique-se de que o PsExec esteja disponível no PATH ou no mesmo diretório do script.
- **Permissões administrativas:** você precisa de direitos administrativos nas máquinas remotas.

## 📄 Arquivo de Texto com a Lista de Computadores

Crie um arquivo de texto chamado `computers.txt` contendo os nomes das máquinas ou endereços IP, um por linha. Exemplo:

```
COMPUTADOR1
COMPUTADOR2
192.168.1.10
```

## ⚙️ Script Batch

Crie um arquivo de script batch chamado `enable_rpc.bat` com o seguinte conteúdo:

```bat
@echo off
for /f %%i in (computers.txt) do (
    echo Ativando RPC em %%i
    psexec \\%%i -s -d sc config RpcSs start= auto
    psexec \\%%i -s -d net start RpcSs
)
```

## 🚀 Executando o Script

### 1️⃣ Abra o Prompt de Comando como Administrador

Clique com o botão direito no ícone do Prompt de Comando e selecione "Executar como administrador".

### 2️⃣ Navegue até o Diretório do Script

Use o comando `cd` para ir até o diretório onde o PsExec e o script estão localizados. Exemplo:

```
cd C:\caminho\para\diretorio
```

### 3️⃣ Execute o Script

Execute o script batch usando o PsExec:

```
psexec @computers.txt -s -d C:\caminho\para\diretorio\enable_rpc.bat
```

## 📝 Explicação dos Comandos

- `psexec`: inicia o PsExec.
- `-s`: executa o processo com a conta System.
- `-d`: não espera o processo finalizar (não interativo).
- `@computers.txt`: especifica um arquivo de texto com a lista de computadores para executar o comando.
- `sc config RpcSs start= auto`: define o serviço RPC para iniciar automaticamente.
- `net start RpcSs`: inicia o serviço RPC.

## 🔍 Considerações Finais

Certifique-se de que o PsExec esteja configurado corretamente e que você tenha as permissões necessárias para executar comandos remotos nas máquinas listadas. Se houver problemas, verifique as configurações de rede e firewall.

📌 **Dica:** se estiver com dificuldades, use o comando `psexec \\NOMEDOCOMPUTADOR cmd` para testar a conexão remota antes de executar o script completo.
