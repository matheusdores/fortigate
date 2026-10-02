# 01 — Discovery Checklist

## Objetivo

Levantar o estado real do ambiente antes de qualquer reset, mudança de licença ou alteração de topologia.

## FortiGate 01

- Hostname: `PENDENTE`
- Função futura: `FGT-HQ`
- FortiOS: `PENDENTE`
- Build: `PENDENTE`
- Modelo VM: `PENDENTE`
- Status da licença: `PENDENTE`
- vCPU: `PENDENTE`
- RAM: `PENDENTE`
- Interfaces disponíveis: `PENDENTE`
- Serial sanitizado: `PENDENTE`
- Configuração atual exportada: `PENDENTE`
- Snapshot realizado: `PENDENTE`

### Coleta necessária

```shell
get system status
get system performance status
get system interface physical
show system interface
get router info routing-table all
```

## FortiGate 02

- Hostname: `PENDENTE`
- Função futura: `FGT-BR01`
- FortiOS: `PENDENTE`
- Build: `PENDENTE`
- Modelo VM: `PENDENTE`
- Status da licença: `PENDENTE`
- vCPU: `PENDENTE`
- RAM: `PENDENTE`
- Interfaces disponíveis: `PENDENTE`
- Serial sanitizado: `PENDENTE`
- Configuração atual exportada: `PENDENTE`
- Snapshot realizado: `PENDENTE`

### Coleta necessária

```shell
get system status
get system performance status
get system interface physical
show system interface
get router info routing-table all
```

## Host / GNS3 Server

- Plataforma: `PENDENTE`
- CPU: `PENDENTE`
- Cores/threads: `PENDENTE`
- RAM total: `PENDENTE`
- RAM livre em idle: `PENDENTE`
- Armazenamento livre: `PENDENTE`
- Versão GNS3 Server: `PENDENTE`
- Versão QEMU/KVM: `PENDENTE`
- Virtualização por hardware: `PENDENTE`

### Coleta sugerida no Linux

```shell
lscpu
free -h
df -h
uname -a
gns3server --version
qemu-system-x86_64 --version
ls -l /dev/kvm
```

## FortiManager

- Imagem disponível: `PENDENTE`
- Versão: `PENDENTE`
- Licença/trial: `PENDENTE`
- Recursos mínimos definidos: `PENDENTE`
- IP de gerenciamento: `PENDENTE`

## Regra de mudança

Não executar factory reset antes de:

1. confirmar o estado da licença;
2. salvar backup da configuração;
3. criar snapshot da VM;
4. registrar a versão do FortiOS;
5. confirmar que a recuperação da licença é possível.

## Status

`ABERTO`
