# 00 — Project Overview

## Nome do projeto

**Enterprise Fortinet Multi-Site Lab**

## Contexto

Este projeto simula uma implantação corporativa real utilizando FortiGate e FortiManager, com foco em redes, segurança, gerenciamento centralizado, conectividade entre unidades, automação e troubleshooting.

O laboratório será construído de forma incremental e documentado durante a execução, evitando reconstruir informações de memória no final.

## Objetivo técnico

Projetar, implementar, validar, quebrar propositalmente, diagnosticar, corrigir e documentar uma arquitetura Fortinet multi-site com evidências técnicas verificáveis.

## Objetivo profissional

Produzir um case de portfólio capaz de demonstrar:

- capacidade de desenho de arquitetura;
- domínio de FortiGate e FortiManager;
- operação de redes corporativas;
- troubleshooting estruturado;
- change management;
- documentação técnica;
- automação e padronização;
- capacidade de explicar decisões de design.

## Escopo planejado

### Infraestrutura

- GNS3
- ISP/underlay simulado
- FortiGate HQ
- FortiGate Branch 01
- FortiManager
- Hosts leves para testes
- Evolução para uma terceira unidade conforme recursos e licenciamento

### Tecnologias

- FortiOS
- FortiManager
- IPv4
- Static Routing
- BGP
- IPsec
- SD-WAN
- Performance SLA
- Policy Packages
- Dynamic Mapping
- ADOM
- Revisions
- Workspace
- Metadata
- Jinja

## Premissas

- Existem dois FortiGate-VM já licenciados.
- O estado atual desses equipamentos será inventariado antes de qualquer reset.
- A arquitetura deve respeitar limitações reais de CPU, RAM e licenciamento.
- Nenhuma informação sensível será publicada.
- Parâmetros ainda não levantados permanecerão marcados como `PENDENTE`.

## Critérios de sucesso

O projeto será considerado concluído quando houver:

1. arquitetura documentada;
2. endereçamento validado;
3. FortiManager operacional;
4. FortiGates gerenciados centralmente;
5. VPN e roteamento validados;
6. SD-WAN testado com failover/failback;
7. automação demonstrada;
8. change record e rollback testados;
9. biblioteca de incidentes com RCA;
10. As-Built final;
11. README executivo e evidências sanitizadas.

## Estado atual

**Fase 0 — Discovery e inventário**

Nenhuma alteração destrutiva deve ser executada até concluir o inventário dos FortiGates e da infraestrutura do host.
