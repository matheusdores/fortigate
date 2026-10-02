# 01 — Discovery Checklist

## Objetivo

Levantar o estado real do ambiente antes de qualquer reset, mudança de licença ou alteração de topologia.

## FortiGate 01

- Hostname: `FGT-1`
- Função futura: `FGT-HQ` (proposta inicial)
- FortiOS: `v7.6.6`
- Build: `3652 (GA.M)`
- Modelo VM: `FortiGate-VM64-KVM`
- Security Level: `High`
- Status da licença: `Valid`
- vCPU: `1 CPU / 1 allowed`
- RAM: `1993 MB / 2048 MB allowed`
- VDOMs: `máximo 2`, atualmente `root`
- Operation Mode: `NAT`
- HA atual: `A-P, primary`
- Log hard disk: `Available`
- Interfaces disponíveis: `port1`, `port2`, `port3`
- Serial sanitizado: `FGVM********SAC8`
- Configuração atual exportada: `PENDENTE`
- Snapshot realizado: `PENDENTE`

### Estado atual das interfaces

| Interface | Modo | Endereço | Estado | Observação |
|---|---|---|---|---|
| `port1` | static | `0.0.0.0/0` | up | Sem IPv4 configurado |
| `port2` | static | `10.10.10.1/24` | down | LAN antiga / estado anterior |
| `port3` | static | `192.168.1.20/24` | up | Rede atual de gerenciamento/conectividade |

### Estado atual de roteamento

```text
S* 0.0.0.0/0 via 192.168.1.1, port3
C  192.168.1.0/24 directly connected, port3
```

### Capacidade observada

Coleta imediatamente após reboot:

- CPU idle: aproximadamente `87%`
- Memória utilizada: aproximadamente `48.4%`
- Sessões médias no primeiro minuto: `32`
- Uptime no momento da coleta: aproximadamente `2 minutos`

> Observação: estes números representam o estado imediatamente após boot e não devem ser utilizados isoladamente como baseline definitivo de performance.

### Observações técnicas

1. A licença está válida no momento da coleta.
2. O appliance está limitado/licenciado para `1 vCPU` e `2048 MB RAM`.
3. Existem três interfaces virtuais visíveis (`port1` a `port3`).
4. O equipamento possui configuração anterior, incluindo rota default pela `port3`.
5. O equipamento aparece como `HA A-P primary`; antes do reset será necessário registrar e remover de forma controlada qualquer configuração HA existente.
6. As bases FortiGuard/IPS exibidas não serão usadas como evidência de assinatura atualizada; a fase inicial deste projeto concentra-se em routing, VPN, gerenciamento e operação.

### Coleta ainda necessária

```shell
show system interface
show system ha
get system ha status
show router static
show firewall policy
```

## FortiGate 02

- Hostname: `FGT-2`
- Função futura: `FGT-BR01` (proposta inicial)
- FortiOS: `v7.6.6`
- Build: `3652 (GA.M)`
- Modelo VM: `FortiGate-VM64-KVM`
- Security Level: `High`
- Status da licença: `Valid`
- vCPU: `1 CPU / 1 allowed`
- RAM: `1993 MB / 2048 MB allowed`
- VDOMs: `máximo 2`, atualmente `root`
- Operation Mode: `NAT`
- HA atual: `A-P, secondary`
- Log hard disk: `Available`
- Interfaces disponíveis: `port1`, `port2`, `port3`
- Serial sanitizado: `FGVM********Y6A6`
- Configuração atual exportada: `PENDENTE`
- Snapshot realizado: `PENDENTE`
- File system warning: `PRESENTE — scan recomendado pelo FortiOS`

### Estado atual das interfaces

| Interface | Modo | Endereço | Estado | Observação |
|---|---|---|---|---|
| `port1` | static | `0.0.0.0/0` | up | Sem IPv4 configurado |
| `port2` | static | `10.10.10.1/24` | down | LAN antiga / configuração sincronizada do cluster |
| `port3` | static | `192.168.1.20/24` | up | Rede atual de gerenciamento/conectividade |

### Estado atual de roteamento

O comando `get router info routing-table all` não apresentou entradas durante a coleta no membro secundário.

> Observação: como o equipamento está em HA `A-P secondary`, essa ausência será analisada junto com o estado completo do cluster antes de qualquer conclusão sobre a configuração de roteamento.

### Capacidade observada

Coleta imediatamente após reboot:

- CPU idle: aproximadamente `97%`
- Memória utilizada: aproximadamente `47.6%`
- Sessões médias no primeiro minuto: `14`
- Uptime no momento da coleta: aproximadamente `4 minutos`

> Observação: estes números representam o estado imediatamente após boot e não devem ser utilizados isoladamente como baseline definitivo de performance.

### Observações técnicas

1. A licença está válida no momento da coleta.
2. O appliance apresenta os mesmos limites de recursos observados no FGT-1: `1 vCPU` e `2048 MB RAM`.
3. Existem três interfaces virtuais visíveis (`port1` a `port3`).
4. O equipamento aparece como `HA A-P secondary`, confirmando que os dois FortiGates atualmente fazem parte de um cluster HA.
5. As interfaces apresentam os mesmos endereços vistos no FGT-1, compatível com configuração sincronizada de cluster.
6. O FortiOS exibiu aviso de possível inconsistência de filesystem após reboot inseguro. Antes de reutilizar a VM no projeto, será necessário identificar o disco com `execute disk list` e executar o scan recomendado em janela controlada.
7. Não executar factory reset antes de registrar a configuração HA, realizar backup/snapshot e tratar o alerta de filesystem.

### Coleta ainda necessária

```shell
execute disk list
show system interface
show system ha
get system ha status
show router static
show firewall policy
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
5. confirmar que a recuperação da licença é possível;
6. registrar/remover configuração HA existente de forma controlada;
7. tratar alertas de filesystem antes de reutilizar a VM.

## Status

`EM ANDAMENTO — FGT-01 e FGT-02 inventariados parcialmente; HA e filesystem do FGT-02 ainda pendentes`
