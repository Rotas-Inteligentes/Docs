🚌 DESIGN.md — Rotas InteligentesVersão: 1.0.0Status: Pronto para PrototipaçãoFramework de Design: Design Thinking (Imersão, Definição e Ideação)📌 1. Visão Geral e Objetivos (Imersão)O Rotas Inteligentes é um ecossistema de transporte inteligente que conecta passageiros e gestores em tempo real para criar uma experiência de deslocamento previsível, acessível e eficiente.Objetivos do ProdutoPara o Usuário (Customer): Fornecer previsibilidade de rotas, alertas de super-lotação, recursos de acessibilidade e um programa de fidelidade.Para a Empresa/Governo (Business): Permitir a gestão completa da frota, controle de turnos, fiscalização via Corregedoria e monitoramento de desempenho.🎨 2. Identidade Visual e BrandingA interface foi projetada para transmitir confiança, modernidade e clareza visual, com foco em leitura rápida para usuários em movimento.Logotipo e SimbologiaSímbolo: Um marcador de localização (pin) envolvendo uma estrada estilizada em perspectiva, unindo o destino final à jornada.Tipografia do Logo: Sans-serif robusta, com kerning (espaçamento) aberto na palavra "INTELIGENTE", conferindo um aspecto limpo e tecnológico.Paleta de CoresAs cores foram selecionadas para garantir alto contraste (acessibilidade) e interfaces baseadas em estados.Azul Elétrico (Principal): #0026E6 – Cor de destaque para ações principais e tecnologia.Azul Marinho Profundo: #001066 – Utilizado para superfícies, backgrounds e menus.Azul Real Clássico: Usado para criar profundidade e suporte à marca.Branco Puro: #FFFFFF – Utilizado para textos em fundos escuros e ícones.Escala de Cinzas (Neutros): #EAEAEA a #2A2A2A – Para estados desativados e backgrounds secundários.Preto Profundo / Grafite: #1A1A1A – Base para o modo escuro (Dark Mode), crucial para o conforto visual nas ruas e economia de bateria.TipografiaTítulos: Fira Sans – Fornece clareza técnica e legibilidade em títulos destacados.Corpo de Texto: Montserrat – Fonte geométrica que mantém excelente leitura em telas de smartphones.🛠️ 3. Arquitetura de Informação e MódulosO sistema é dividido em 6 módulos principais, atendendo aos perfis Customer e Business com diferentes níveis de permissão:Snippet de códigomindmap
  root((Rotas Inteligentes))
    Linhas Rodoviárias
      Mapeamento
      Filtragem
      Motoristas e Turnos
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
    Usuários
      Fidelidade
      Notificações
      Perfil de Rotina
📱 4. Experiência do Usuário (UX) e Fluxos CríticosPara guiar a prototipação das telas no Stick.beta, os seguintes fluxos devem ser priorizados:4.1. Jornada do Passageiro (Customer)Snippet de códigoflowchart TD
    A([👤 Login / Início]) --> B[Escolher destino e horário]
    B --> C[⚙️ Sistema calcula ponto mais próximo]
    C --> D[📍 Sugestão de ponto exibida]
    D --> E{Confirma o ponto?}
    E -- Não --> B
    E -- Sim --> F[⚙️ Salva destino e ponto]
    F --> G[⏰ Monitoramento em tempo real]
    G --> H[🔔 Notificação de proximidade do ônibus]
    H --> I([🚌 Embarque])
    I --> J[Acompanha trajeto no mapa]
    J --> K{Próximo do destino?}
    K -- Sim --> L[🔔 Notificação de desembarque]
    L --> M([🏁 Desembarque])
    M --> N[⭐ Avaliação da viagem]
4.2. Sistema de Totem — Pings e OcupaçãoO veículo envia pings de localização via celular ou sistema embutido. Esses dados alimentam a posição exata para os gestores e geram a estimativa de ocupação.Snippet de códigosequenceDiagram
    participant V as 🚌 Veículo
    participant S as ⚙️ Servidor
    participant D as 📱 Devices próximos
    participant G as 👔 Gestor Business
    participant C as 👤 Customer

    loop A cada ping
        V->>S: Envia localização exata
        S->>G: Atualiza posição real no painel
        S->>C: Atualiza posição aproximada no mapa
        V-->>D: Ping Bluetooth/Proximidade
        D->>S: Confirma presença a bordo
        S->>S: Calcula estimativa de ocupação
    end

    S->>C: Exibe alerta de super-lotação (se aplicável)
🏗️ 5. Stack Tecnológica PropostaPara suportar todas as funcionalidades do projeto, a stack foi desenhada visando tempo real e alta disponibilidade:Front-End (Web Gestor): React.Front-End (Mobile Customer/Motorista): Flutter.Back-End: Node.js com arquitetura de microserviços para escalabilidade.Banco de Dados: Oracle.Protocolos de Comunicação: WebSockets (para Chat em Tempo Real e Atualizações de Viagem) e REST APIs.🎯 6. Roadmap de Prototipação (Matriz de Prioridades)O desenvolvimento dos protótipos de alta fidelidade deve seguir a matriz de impacto versus complexidade:SprintMódulo / FuncionalidadePerfilComplexidadeSprint 1Rastreamento RT & LocalizaçãoAmbosAltaSprint 1Notificações de EmergênciaCustomerBaixaSprint 2Cálculo de Rotas & ETACustomerMédiaSprint 2Rotina de Viagem e Alertas de DesvioBusinessMédiaSprint 3Chat Motorista / MatrizBusinessMédiaSprint 3Avaliações (Ônibus/Motorista)CustomerBaixaSprint 4Comando rápido por voz (Acessibilidade)CustomerAltaSprint 4Modo offlineCustomerAlta📑 7. Glossário de Termos do ProjetoBusiness: Perfil destinado à gestão e operação da empresa de transporte (gestores, corregedoria).Customer: Perfil destinado ao passageiro ou usuário final do aplicativo.ETA: Estimated Time of Arrival (Tempo Estimado de Chegada).RT: Real Time (Tempo Real).Totem: Sistema de pings enviados pelo veículo para rastreamento de localização e cálculo de passageiros.