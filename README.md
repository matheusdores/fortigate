# Enterprise Fortinet Multi-Site Lab

Projeto de laboratório enterprise voltado para redes e segurança com FortiGate e FortiManager.

## Objetivo

Simular uma implementação corporativa completa, desde o levantamento de requisitos até o As-Built final, incluindo gerenciamento centralizado, VPN IPsec, BGP, SD-WAN, automação, change management e troubleshooting documentado.

## Escopo inicial

- 2 FortiGate-VM licenciados já disponíveis
- FortiManager-VM
- GNS3 como plataforma principal
- ISP/underlay simulado
- Matriz (HQ) + filial inicial
- Evolução para terceira unidade conforme recursos/licenciamento
- Documentação completa no GitHub

## Princípios do projeto

1. Não inventar endereços ou parâmetros ainda não definidos.
2. Registrar o estado atual antes de qualquer reset ou alteração destrutiva.
3. Documentar cada mudança, teste, falha e correção.
4. Sanitizar qualquer informação sensível antes de publicar.
5. Tratar o lab como uma implementação real de empresa.

## Arquitetura alvo

A arquitetura será definida após o inventário dos recursos disponíveis e validação das licenças dos FortiGates.

```text
                    INTERNET / ISP SIMULADO
                              |
                           ISP-R1
                         /        \
                        /          \
                    FGT-HQ       FGT-BR01
                      |              |
                    HQ-LAN        BR01-LAN

                    MANAGEMENT NETWORK
                           |
                     FortiManager
```

## Fases

- Fase 0 — Discovery e inventário
- Fase 1 — Baseline e underlay
- Fase 2 — FortiManager onboarding
- Fase 3 — Policy Packages e Dynamic Mapping
- Fase 4 — IPsec Hub-and-Spoke + BGP
- Fase 5 — SD-WAN e Performance SLA
- Fase 6 — Automação com metadata/Jinja
- Fase 7 — Change Management e rollback
- Fase 8 — Troubleshooting Library + RCA
- Fase 9 — As-Built e publicação final

## Segurança da documentação

Nunca publicar:

- senhas
- PSKs reais
- API keys/tokens
- serial completo
- arquivo de licença
- IP público real
- identificadores de clientes ou ambientes de produção

## Status

**Em andamento — Fase 0: Discovery e inventário.**
