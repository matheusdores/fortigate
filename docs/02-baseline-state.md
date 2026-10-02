# 02 — Baseline State

## Objetivo

Registrar o estado limpo e funcional dos dois FortiGates após remoção do HA anterior, factory reset, reativação das licenças e restauração do acesso de gerenciamento.

## Estado atual

### FGT-HQ

- Hostname: `FGT-HQ`
- Função: Matriz / HUB
- FortiOS: `v7.6.6 build 3652 (GA.M)`
- Modelo: `FortiGate-VM64-KVM`
- Licença: `Valid`
- HA: `standalone`
- vCPU: `1`
- RAM: `2048 MB`
- VDOMs licenciados: `2`
- Modo: `NAT`
- Management: `port3`
- IP de gerenciamento: `192.168.1.20/24`
- Gateway de gerenciamento/Internet: `192.168.1.1`
- GUI: `HTTP/HTTPS habilitados`
- SSH/Ping: `habilitados`

### FGT-BR01

- Hostname: `FGT-BR01`
- Função: Filial / SPOKE
- FortiOS: `v7.6.6 build 3652 (GA.M)`
- Modelo: `FortiGate-VM64-KVM`
- Licença: `Valid`
- HA: `standalone`
- vCPU: `1`
- RAM: `2048 MB`
- VDOMs licenciados: `2`
- Modo: `NAT`
- Management: `port3`
- IP de gerenciamento: `192.168.1.21/24`
- Gateway de gerenciamento/Internet: `192.168.1.1`
- GUI: `HTTP/HTTPS habilitados`
- SSH/Ping: `habilitados`

## Função das interfaces

| Interface | FGT-HQ | FGT-BR01 |
|---|---|---|
| `port1` | WAN / Underlay | WAN / Underlay |
| `port2` | LAN-HQ | LAN-BR01 |
| `port3` | Management + Internet temporário | Management + Internet temporário |

> A `port3` está sendo utilizada temporariamente para gerenciamento e validação das licenças. O desenho final do underlay será definido no IP Plan e no LLD.

## Próximas etapas

1. Configurar timezone e NTP.
2. Definir IP Plan oficial.
3. Definir endereçamento de `port1` e `port2`.
4. Configurar o roteador `R1-ISP`.
5. Validar underlay entre HQ e filial.
6. Subir e integrar o FortiManager.

## Status

`BASELINE CONCLUÍDO — ambos os FortiGates licenciados, standalone e acessíveis via management.`
