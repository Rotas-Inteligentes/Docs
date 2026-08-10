# 🚌 Rotas Inteligentes — Especificação de Funcionalidades

> **Versão:** 1.3.0  
> **Status:** Em Desenvolvimento  
> **Classificação:** Interno

---

## 📋 Sumário

1. [Visão Geral](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#vis%C3%A3o-geral)
2. [Arquitetura de Módulos](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#arquitetura-de-m%C3%B3dulos)
3. [Distribuição por Perfil](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#distribui%C3%A7%C3%A3o-por-perfil)
4. [Módulos e Funcionalidades](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#m%C3%B3dulos-e-funcionalidades)
    - [Linhas Rodoviárias](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#1-linhas-rodovi%C3%A1rias)
    - [Avaliação](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#2-avalia%C3%A7%C3%A3o)
    - [Estoque](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#3-estoque)
    - [Acessibilidade](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#4-acessibilidade)
    - [Rastreamento](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#5-rastreamento)
    - [Usuários](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#6-usu%C3%A1rios)
5. [Fluxos Críticos](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#fluxos-cr%C3%ADticos)
6. [Matriz de Prioridades](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#matriz-de-prioridades)
7. [Glossário](https://claude.ai/chat/4f1a988c-3b52-43a1-95a8-9cfa2e542ecb#gloss%C3%A1rio)

---

## Visão Geral

Este documento descreve as funcionalidades do sistema de transporte público, organizadas por módulo e perfil de acesso. O sistema atende dois perfis principais: **Business** (operadores e gestores) e **Customer** (passageiros e usuários finais).

### Resumo Executivo

|Indicador|Valor|
|---|---|
|Total de módulos|6|
|Total de funcionalidades|28|
|Funcionalidades Business|9|
|Funcionalidades Customer|16|
|Funcionalidades Compartilhadas|3|
|Funcionalidades que requerem conectividade em tempo real|4|

---

## Arquitetura de Módulos

```mermaid
mindmap
  root((Sistema de
  Transporte))
    Linhas Rodoviárias
      Mapeamento
      Filtragem
      Motoristas e Turnos
      Rotina de Viagem
    Avaliação
      Motorista
      Ônibus
      Chat Matriz
    Estoque
      Achados e Perdidos
    Acessibilidade
      Voz
      Modo off-line
    Rastreamento
      Totens
      Cálculo de Rotas
      Super-lotação
      Chegada
      Tempo de Rota
      Localização RT
    Usuários
      Benefícios
      Notificações
      Perfil de Rotina
      Customização
```

---

## Distribuição por Perfil

```mermaid
pie title Funcionalidades por Perfil de Acesso
    "Customer" : 16
    "Business" : 9
    "Compartilhado" : 3
```

---

## Módulos e Funcionalidades

### 1. Linhas Rodoviárias

> Gestão das rotas e operação das linhas de transporte. Envolve configuração de trajetos, motoristas e controle de pontualidade.

| Funcionalidade                         | Perfil     | Conectividade | Detalhes                                                          |
| -------------------------------------- | ---------- | ------------- | ----------------------------------------------------------------- |
| Mapeamento                             | `Customer` | Online        | Visualização de linhas no mapa                                    |
| Filtragem                              | `Customer` | Online        | Filtro por linha, região ou horário                               |
| Definição de motoristas e turnos       | `Business` | Offline       | Cadastro e escalonamento de equipe                                |
| Rotina de início de viagem             | `Business` | Online        | Agendamento recorrente SEG–SEX às 06:00                           |
| ↳ Início atrasado / adiantado          | `Business` | Online        | Detecção de desvio de horário                                     |
| ↳ Notificação de atraso / adiantamento | `Business` | Tempo Real ⚡  | Alerta automático para gestores **e usuários vinculados à linha** |

---

### 2. Avaliação

> Canal de feedback e supervisão da qualidade operacional. Permite que passageiros avaliem a experiência e que gestores monitorem a comunicação com motoristas.

|Funcionalidade|Perfil|Conectividade|Detalhes|
|---|---|---|---|
|Avaliação de Motorista|`Customer`|Online|Nota e comentário pós-viagem|
|Avaliação de Ônibus|`Customer`|Online|Avaliação de conservação e conforto|
|Chat em tempo real — motorista e matriz|`Business`|Tempo Real ⚡|Canal direto entre motorista e Corregedoria / Dono da empresa|

---

### 3. Estoque

> Controle de itens perdidos dentro dos veículos e terminais.

|Funcionalidade|Perfil|Conectividade|Detalhes|
|---|---|---|---|
|Achados e Perdidos|`Customer` / `Business`|Online|Registro e consulta de itens perdidos|

---

### 4. Acessibilidade

> Recursos que garantem o uso do sistema por diferentes perfis de usuário, incluindo suporte a voz e operação sem internet.

|Funcionalidade|Perfil|Conectividade|Detalhes|
|---|---|---|---|
|Comando rápido por voz|`Customer`|Offline|Acionamento de funções por voz|
|Modo off-line|`Customer`|Offline|Acesso a dados em cache sem conexão|

---

### 5. Rastreamento

> Núcleo operacional do sistema. Concentra as funcionalidades de localização, cálculo de rotas e monitoramento de capacidade em tempo real.

> **📡 Fonte de GPS:** A localização do veículo pode ser obtida por dois meios — um **celular da empresa** instalado no veículo, ou um **sistema de localização embutido** no próprio veículo. Ambos enviam pings periódicos ao servidor central.

> **🔔 Sistema de Totem (Pings):** O Totem não é um painel físico isolado — é um sistema de pings enviados pelo veículo ao servidor. Esses pings também são recebidos pelos dispositivos de usuários próximos ao veículo, confirmando a presença do passageiro a bordo e fornecendo uma contagem aproximada de ocupantes.

|Funcionalidade|Perfil|Conectividade|Detalhes|
|---|---|---|---|
|Totem — localização do ônibus|`Customer` / `Business`|Tempo Real ⚡|Pings do veículo ao servidor; posição exibida no app e em painéis nos pontos|
|Totem — confirmação de passageiros a bordo|`Customer` / `Business`|Tempo Real ⚡|Pings recebidos pelos devices próximos confirmam presença; estima ocupação do veículo|
|Cálculo de rotas|`Customer` / `Business`|Online|Melhor rota entre origem e destino|
|↳ Previsão de tempo por geolocalização|`Customer`|Online|ETA com base na posição atual|
|Identificação de super-lotação|`Customer`|Online|Alerta de capacidade excedida — **visível apenas ao Customer**|
|Identificação de chegada|`Customer`|Online|Notificação ao aproximar do ponto|
|Acompanhamento de tempo de rota|`Customer`|Online|Progresso da viagem em andamento|
|Localização em tempo real do veículo ⚡|`Business`|Tempo Real ⚡|GPS ao vivo via celular da empresa ou sistema embutido no veículo|
|Rastreamento aproximado* do veículo e pontos|`Customer`|Online|Posição estimada para passageiros|
|Tempo aproximado de chegada ao ponto|`Customer`|Online|ETA ao ponto de embarque do usuário|

---

### 6. Usuários

> Personalização da experiência, programa de benefícios e comunicação proativa com o passageiro.

|Funcionalidade|Perfil|Conectividade|Detalhes|
|---|---|---|---|
|Benefícios — Fidelidade|`Customer`|Online|Pontos acumulados por viagem|
|Benefícios — Fidelidade por loja|`Customer`|Online|Pontos e descontos em parceiros comerciais|
|Notificações de emergência|`Customer`|Tempo Real ⚡|Alertas críticos de segurança e operação|
|Perfil de rotina do usuário|`Customer`|Online|Aprendizado de rotas e horários frequentes|
|Sistema customizável por companhia|`Business`|Offline|White-label e configurações por operadora|
|Envio de notificações para aluno / customer|`Business`|Tempo Real ⚡|Ex.: _"Só falta você. O veículo está te esperando..."_|
|Notificação em tempo real enviada pelo motorista|`Customer`|Tempo Real ⚡|Mensagens diretas do motorista ao passageiro|

---

## Fluxos Críticos

### Fluxo de Rotina de Viagem com Desvio de Horário

```mermaid
flowchart TD
    A([⏰ Horário programado\nSEG–SEX 06:00]) --> B{Veículo\npartiu?}
    B -- Sim, no horário --> C([✅ Viagem iniciada\nnormalmente])
    B -- Não --> D{Atraso\ndetectado}
    B -- Sim, antes --> E{Adiantamento\ndetectado}
    D --> F[🔔 Notificação de atraso\npara gestores e usuários vinculados]
    E --> G[🔔 Notificação de adiantamento\npara gestores e usuários vinculados]
    F --> H[Gestor aciona\nmotorista via Chat RT]
    G --> H
    H --> I{Situação\nresolvida?}
    I -- Sim --> C
    I -- Não --> J([🚨 Escalonamento\npara Corregedoria])
```

---

### Fluxo de Notificação ao Passageiro

```mermaid
sequenceDiagram
    participant M as 🚌 Motorista
    participant S as ⚙️ Sistema
    participant C as 👤 Customer

    M->>S: Envia notificação em tempo real
    S->>S: Valida perfil e localização
    S->>C: Push notification entregue
    C-->>S: Confirmação de leitura
    S->>M: Status: visualizado ✓

    Note over S,C: Em caso de não entrega, o sistema<br/>retenta por até 3 minutos
```

---

### Fluxo de Rastreamento por Perfil

```mermaid
flowchart LR
    CEL([📱 Celular da empresa\nno veículo])
    EMB([🔌 Sistema embutido\nno veículo])

    CEL -->|ping periódico| SRV[⚙️ Servidor Central]
    EMB -->|ping periódico| SRV

    SRV -->|Tempo Real ⚡| B[Painel Business\nLocalização exata]
    SRV -->|Aproximado ~| C[App Customer\nLocalização estimada]
    SRV -->|Ping recebido por\ndispositivos próximos| OCP[📊 Estimativa de\nocupação do veículo]

    B --> D[Chat Motorista e Matriz]
    C --> F[ETA até o ponto]
    C --> G[Notificação de chegada]
    C --> AL[⚠️ Alerta de super-lotação\nsomente Customer]
    OCP --> AL
```

---

### Fluxo de Jornada do Usuário (Customer)

```mermaid
flowchart TD
    A([👤 Usuário faz login\nno sistema]) --> B[Escolhe destino\ne horário de partida]
    B --> C[⚙️ Sistema calcula\nponto mais próximo\nconsiderando horário]
    C --> D[📍 Sugestão de ponto\nexibida ao usuário]
    D --> E{Usuário\nconfirma o ponto?}
    E -- Não --> B
    E -- Sim --> F[⚙️ Sistema grava\ndestino, ponto e\nhorário de chegada do ônibus]
    F --> G[⏰ Sistema monitora\nhorário e localização]
    G --> H[🔔 Notificação enviada\npróximo ao horário de saída]
    H --> I([🚌 Usuário embarca\nno veículo])
    I --> J[Acompanha trajeto\nem tempo real]
    J --> K{Próximo\ndo destino?}
    K -- Não --> J
    K -- Sim --> L[🔔 Notificação de\naproximação ao destino]
    L --> M([🏁 Usuário desembarca\nno destino])
    M --> N[⭐ Avalia o ônibus\ne o motorista]
    N --> O([✅ Viagem concluída])
```

---

### Fluxo do Sistema de Totem — Pings e Ocupação

```mermaid
sequenceDiagram
    participant V as 🚌 Veículo
    participant S as ⚙️ Servidor
    participant D as 📱 Devices próximos
    participant G as 👔 Gestor Business
    participant C as 👤 Customer

    loop A cada intervalo de ping
        V->>S: Envia ping com localização GPS
        S->>G: Atualiza posição exata em tempo real
        S->>C: Atualiza posição aproximada no app
        V-->>D: Ping recebido por devices próximos
        D->>S: Confirma presença no veículo
        S->>S: Calcula estimativa de ocupação
    end

    S->>C: Exibe alerta de super-lotação (se aplicável)
    Note over S,C: Alerta de super-lotação visível apenas ao Customer
```

---

```mermaid
quadrantChart
    title Prioridade vs Complexidade de Implementação
    x-axis Baixa Complexidade --> Alta Complexidade
    y-axis Baixa Prioridade --> Alta Prioridade
    quadrant-1 Planejar com cuidado
    quadrant-2 Implementar primeiro
    quadrant-3 Reavaliar
    quadrant-4 Simplificar antes
    "Rastreamento RT": [0.80, 0.95]
    "Notificações de Emergência": [0.25, 0.90]
    "Cálculo de Rotas": [0.60, 0.85]
    "Chat Motorista/Matriz": [0.55, 0.75]
    "Rotina de Viagem": [0.45, 0.80]
    "Modo off-line": [0.85, 0.50]
    "Avaliações": [0.20, 0.60]
    "Fidelidade por Loja": [0.80, 0.20]
    "Achados e Perdidos": [0.25, 0.35]
    "Comando por Voz": [0.70, 0.40]
```

---

## Glossário

| Termo           | Definição                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Business`      | Perfil destinado à gestão e operação da empresa de transporte (gestores, corregedoria, donos de empresa)                                                                                                 |
| `Customer`      | Perfil destinado ao passageiro ou usuário final do aplicativo                                                                                                                                            |
| `Compartilhado` | Funcionalidade acessível por ambos os perfis com diferentes níveis de permissão                                                                                                                          |
| ⚡ Tempo Real    | Requer conexão ativa e transmissão contínua de dados (GPS, WebSocket ou similar)                                                                                                                         |
| `*` Aproximado  | Dado calculado com margem de estimativa; não requer precisão de GPS em tempo real                                                                                                                        |
| ETA             | _Estimated Time of Arrival_ — tempo estimado de chegada                                                                                                                                                  |
| RT              | Tempo Real (_Real Time_)                                                                                                                                                                                 |
| Corregedoria    | Órgão interno de fiscalização e supervisão dos motoristas                                                                                                                                                |
| Totem           | Sistema de pings enviados pelo veículo ao servidor para rastrear localização. Os pings também são recebidos pelos dispositivos de usuários próximos, confirmando presença a bordo e estimando a ocupação |
| White-label     | Sistema configurável com a identidade visual e regras da operadora parceira                                                                                                                              |

---

> 📌 **Nota de conectividade:** Funcionalidades marcadas com ⚡ exigem infraestrutura de rede estável. Recomenda-se análise de cobertura de sinal nas rotas antes da implantação dessas features.