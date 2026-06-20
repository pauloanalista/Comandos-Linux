# Comandos-Linux

## 1. Investigando a Memória e o Swap
free -h
--------------------------------------------------------------
## 2 - SERVIDOR TIRANDO APLICACAO DA MEMORIA
Como verificar a agressividade do Swap
cat /proc/sys/vm/swappiness

OBS: O que significa: O valor padrão no Ubuntu/Debian costuma ser 60. Isso significa que o Linux é bem agressivo para usar o Swap. Para servidores de aplicação, o ideal é que esse valor seja muito menor (como 10 ou até 1), forçando o sistema a manter as coisas na RAM.

Mudando para 1
sudo sysctl vm.swappiness=1



Passo 2: Tornar a configuração permanente
Se você reiniciar o servidor, o valor volta para 60. Para garantir que ele fique fixo em 1 para sempre, siga estes passos:

Abra o arquivo de configuração do sistema:

Bash
sudo nano /etc/sysctl.conf
Vá até o final do arquivo e adicione a seguinte linha:

Plaintext
vm.swappiness=10
--------------------------------------------------------------

## 3 - VERIFICANDO ESPAÇO EM DISCO
df -h

--------------------------------------------------------------
## 4 - VERIFICAR GARGALO DE LEITURA E ESCRITA
htop

--------------------------------------------------------------


## 5. Liberar espaço IMEDIATAMENTE

Execute:

docker system df

Depois:

docker system prune -a

⚠️ Isso remove:

imagens não usadas
containers parados
cache de build

--------------------------------------------------------------

## 6. Limpar logs gigantes do Docker (muito provável)

Veja:

du -sh /var/lib/docker/containers/*/*-json.log

E limpe logs grandes:

truncate -s 0 /var/lib/docker/containers/*/*-json.log
