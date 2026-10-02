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

### Disco / filesystem

`execute disk list` identificou:

```text
Disk Virtual-Disk ref: 16  2.0 GiB  type: IDE [Virtio Disk]  dev: /dev/vdb
partition ref: 17  1.9 GiB, 1.9 GiB free, mounted: Y, dev: /dev/vdb1
```

O alerta de filesystem deve ser tratado antes da reutilização definitiva desta VM. O scan recomendado pelo próprio FortiOS é `execute disk scan 16` e implica reboot durante o processo.

### HA atual confirmado

O cluster foi confirmado como saudável e sincronizado:

- Mode: `HA A-P`
- Group Name: `LAB-HA`
- Group ID: `1`
- Health: `OK`
- Membros: `2`
- Primary: `FGT-1`
- Secondary: `FGT-2`
- Configuration Status: `in-sync` em ambos
- Heartbeat device: `port1`
- Session pickup: `enabled`

O FGT-1 foi selecionado como primary por prioridade superior em relação ao FGT-2.

### Observações técnicas

1. A licença está válida no momento da coleta.
2. O appliance apresenta os mesmos limites de recursos observados no FGT-1: `1 vCPU` e `2048 MB RAM`.
3. Existem três interfaces virtuais visíveis (`port1` a `port3`).
4. O equipamento aparece como `HA A-P secondary`, confirmando que os dois FortiGates atualmente fazem parte de um cluster HA.
5. As interfaces apresentam os mesmos endereços vistos no FGT-1, compatível com configuração sincronizada de cluster.
6. O FortiOS exibiu aviso de possível inconsistência de filesystem após reboot inseguro. O disco relevante foi identificado como `ref 16`, `/dev/vdb`.
7. O cluster encontra-se `in-sync`, com heartbeat pela `port1` e dois membros ativos no domínio HA.
8. Não executar factory reset antes de registrar a configuração HA completa, realizar backup/snapshot e concluir o scan do filesystem.

### Coleta ainda necessária

```shell
show system interface
show system ha
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
7. concluir o tratamento do filesystem do FGT-02;
8. fechar o design TO-BE da topologia.

## Status

`EM ANDAMENTO — FGT-01 e FGT-02 inventariados; HA confirmado; filesystem do FGT-02 e backups ainda pendentes`
