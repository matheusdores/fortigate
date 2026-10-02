# 02 — Baseline Implementation

## Objetivo

Estabelecer a configuração base dos dois FortiGate-VM que compõem o projeto enterprise multi-site.

## Arquitetura definida

- `FGT-HQ` — Matriz / Hub
- `FGT-BR01` — Filial / Spoke
- `FortiManager` — Gerenciamento centralizado
- `R1-ISP` — Underlay / Internet simulada

### Padrão de interfaces

| Interface | Função |
|---|---|
| `port1` | WAN / ISP |
| `port2` | LAN local |
| `port3` | Management |

## FGT-HQ

Status atual informado durante a implementação:

- Hostname configurado: `FGT-HQ`
- Licença: validada
- HA: standalone
- `port3`: rede de gerenciamento configurada
- Acesso administrativo: HTTP, HTTPS, SSH e ping habilitados na interface de management
- `port1`: reservada para WAN
- `port2`: reservada para LAN-HQ

### Próximos passos do FGT-HQ

1. Definir endereçamento definitivo de WAN no IP Plan.
2. Definir subnet definitiva da LAN-HQ.
3. Conectar ao underlay via `R1-ISP`.
4. Validar conectividade antes do onboarding no FortiManager.

## FGT-BR01

Status: `PENDENTE DE BASELINE`.

### Baseline planejado

- Renomear para `FGT-BR01`.
- Confirmar licença válida.
- Confirmar HA standalone.
- Configurar `port3` para gerenciamento com endereço distinto do FGT-HQ.
- Reservar `port1` para WAN/ISP.
- Reservar `port2` para LAN-BR01.

## Critério de conclusão da fase

A baseline será considerada concluída quando os dois FortiGates estiverem:

- licenciados;
- standalone;
- acessíveis pela management network;
- com naming padrão aplicado;
- sem configuração HA antiga;
- prontos para receber o endereçamento definitivo do underlay e das LANs.
