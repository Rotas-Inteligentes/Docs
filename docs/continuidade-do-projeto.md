# Rotas Inteligentes — Contexto e continuidade

**Última atualização:** 10 de agosto de 2026  
**Objetivo deste arquivo:** permitir que o projeto seja retomado em outro computador, conversa ou ambiente sem perder as decisões, o contexto e as próximas perguntas.

## 1. Visão do produto

Rotas Inteligentes é uma plataforma de mobilidade para **vans universitárias privadas e recorrentes**. Ela conecta gestor, motorista e passageiro para substituir a dependência de mensagens e localização compartilhada no WhatsApp por uma operação dedicada, organizada e previsível.

O motorista inicia e finaliza a viagem e transmite sua localização somente enquanto a viagem está ativa. O passageiro acompanha a van, o estado da viagem e avisos relevantes. O gestor configura a operação e acompanha as viagens por um painel web.

O projeto começou como uma ideia acadêmica e prototipação em Figma. Agora será transformado em produto real, também como item de portfólio e possível negócio SaaS.

## 2. Recorte inicial aprovado

| Item | Definição |
|---|---|
| Segmento inicial | Vans universitárias privadas. |
| Problema | Falta de visibilidade sobre onde a van está e excesso de comunicação manual via WhatsApp. |
| Comprador | Motorista proprietário ou gestor de pequena frota. |
| Usuários | Gestor, motorista e passageiro (estudante). |
| Benefício ao passageiro | Saber o status e a localização da van, com avisos no momento certo. |
| Benefício ao gestor/motorista | Menos mensagens repetidas, operação organizada e serviço mais profissional. |
| Primeiro piloto | A van que transporta o idealizador para a faculdade. |
| Dimensão do piloto | Até 2 vans, 35 passageiros e 2 rotas. |
| Modelo comercial a validar | SaaS B2B mensal por veículo ativo; passageiros incluídos. |

## 3. Canais do produto

1. **Aplicativo Motorista** — iniciar/finalizar viagem, enviar GPS e informar atraso/ocorrência simples.
2. **Aplicativo Passageiro** — acompanhar a viagem, localização, estado e notificações.
3. **Painel Gestor (web)** — cadastrar operação, veículos, motoristas, passageiros, rotas, pontos e acompanhar viagens.

Os dois apps terão distribuição separada, mas podem compartilhar uma base Flutter e módulos comuns. O painel será web responsivo para computador e tablet.

## 4. Escopo do MVP

### Gestor

- Criar organização/operação.
- Cadastrar vans, motoristas, rotas recorrentes e pontos.
- Vincular passageiros às rotas por convite.
- Acompanhar viagem ativa e consultar histórico básico.

### Motorista

- Autenticar-se e visualizar rotas/viagens permitidas.
- Iniciar e finalizar uma viagem.
- Enviar localização enquanto a viagem estiver ativa.
- Indicar atraso simples, com foco em segurança de uso.

### Passageiro

- Aceitar convite e entrar na rota permitida.
- Acompanhar mapa, estado da viagem e horário/atualização mais recente.
- Receber avisos de início, atraso relevante, proximidade e cancelamento/finalização.

### Fora do MVP

- Transporte público e integrações municipais.
- Pagamentos e financeiro.
- Otimização automática de rotas, trânsito avançado e ETA sofisticado.
- Avaliações, gamificação, chat, achados e perdidos e programas de fidelidade.
- Rastreador físico, totens e medição automática de ocupação.
- Integrações com aplicativos de universidades.

## 5. Decisões técnicas tomadas

### Arquitetura de backend

- **Não usar microserviços no MVP.**
- Usar um **monólito modular**: um backend de negócio, organizado em módulos com fronteiras claras (`identity`, `fleet`, `routes`, `trips`, `tracking`, `notifications`, `maps`, `invitations` e `audit`).
- A separação em microserviços só será avaliada quando houver evidência de alto volume de telemetria, processamento pesado ou times independentes.
- **Node.js + TypeScript** é a tecnologia inicial recomendada para a API. C# só entra futuramente se houver uma necessidade específica e mensurável, não por uma ideia genérica de “aplicação pesada”.

### Plataforma

- **Android apenas no piloto.**
- **Flutter** para os aplicativos móveis, deixando caminho aberto para iOS no futuro.
- Painel gestor em **React + TypeScript**; Next.js é a hipótese preferida, mas a decisão final de framework pode acompanhar o início do projeto.

### Dados e serviços

- Banco recomendado: **PostgreSQL com PostGIS**, por causa de organizações, pessoas, veículos, rotas, viagens, permissões e geolocalização.
- DynamoDB não é recomendado para o MVP: aumentaria a complexidade das relações e consultas administrativas.
- Plataforma recomendada para o início: **Supabase** (PostgreSQL, Auth, Realtime e Storage).
- Notificações: **Firebase Cloud Messaging (FCM)**.
- Origem do GPS no piloto: celular Android do motorista. A arquitetura deve ter uma abstração `LocationProvider` para permitir rastreador físico no futuro.

### Estados de viagem

```text
agendada → disponível → iniciada → em_andamento → atrasada → concluída
                                         └──────────────→ cancelada
```

## 6. Estratégia de custo aprovada

### Teste/piloto técnico inicial

Objetivo: realizar as primeiras viagens e provar o funcionamento antes de existir contrato.

- Supabase Free: US$ 0.
- Firebase Cloud Messaging: US$ 0.
- API em plano/crédito inicial do Railway: US$ 0 durante o teste inicial; após o crédito, pode haver custo mínimo aproximado de US$ 1/mês.
- Sem AWS no início.
- Sem compromisso de disponibilidade comercial.
- Fazer exportação manual do banco antes/depois dos testes, porque o Supabase Free não possui backup automático.

### Após contrato assinado

- Supabase Pro: **US$ 25/mês**.
- Railway Hobby para API Node: **aproximadamente US$ 5/mês**.
- FCM: US$ 0.
- Total-base de infraestrutura, sem mapas e domínio: **aproximadamente US$ 30/mês**, mais impostos e câmbio.

O plano pago deve ser adotado antes de depender do serviço diariamente como produto contratado. A migração não exige reescrever banco ou backend.

## 7. Geolocalização e tempo real

- O GPS deve ser enviado **somente em viagem ativa**; não haverá rastreamento contínuo fora dela.
- A posição é recebida pela API, validada, gravada como posição atual e publicada em canal privado para gestor e passageiros autorizados.
- A interface precisa mostrar “sinal desatualizado” se não receber uma localização recente.
- Internet perdida não pode finalizar nem corromper a viagem: o aplicativo deve informar o problema e retomar o envio quando possível.
- O intervalo inicial de GPS **ainda não está fechado**. Há a hipótese de 5 a 10 segundos.
- Não deixar o broadcast sem limite: mesmo com consentimento de localização, a frequência impacta bateria, dados móveis e custo. O canal ao vivo deve permanecer conectado apenas enquanto o usuário estiver visualizando a viagem.

## 8. Modelo de dados inicial

- `organization`
- `user_profile`
- `organization_member`
- `vehicle`
- `driver_assignment`
- `route`
- `route_stop`
- `passenger_enrollment`
- `trip`
- `trip_event`
- `vehicle_live_location`
- `location_event`
- `device_push_token`
- `invitation`
- `audit_log`

## 9. Decisão de repositório — ainda pendente

Foi sugerido um monorepo com aplicações separadas:

```text
rotas-inteligentes/
├── apps/
│   ├── motorista/
│   ├── passageiro/
│   ├── gestor-web/
│   └── api/
├── packages/
│   └── shared/
└── docs/
```

O ponto em discussão é se usar um repositório único (monorepo) ou múltiplos repositórios.

Pontos importantes já esclarecidos:

- Monorepo não significa publicar tudo a cada commit.
- A `main` deve ser protegida; toda mudança passa por branch, Pull Request, CI, homologação e aprovação.
- O CI pode ser configurado por caminho: mudança em `apps/motorista` gera teste/build apenas do motorista; mudança em `packages/shared` valida todos os consumidores.
- Monorepo facilita alteração coordenada entre contrato da API, backend e apps.
- Múltiplos repositórios fazem sentido se houver times independentes, permissões isoladas ou necessidade forte de ciclos totalmente separados.

**Essa decisão não foi fechada.**

## 10. Próximas decisões — tratar uma por vez

1. **Definir monorepo ou múltiplos repositórios** e o fluxo de CI/CD correspondente.
2. Definir o esqueleto dos projetos escolhidos (Flutter motorista, Flutter passageiro, painel e API).
3. Escolher formalmente o framework da API: NestJS/Fastify como recomendação; Hono/Vercel Functions como alternativa mais enxuta.
4. Definir onde a API ficará no piloto técnico e como será feita a homologação.
5. Definir o intervalo e a estratégia de envio de GPS após a prova técnica (5 s, 10 s ou adaptativo).
6. Criar o modelo ER detalhado, índices e políticas de Row Level Security.
7. Escrever o contrato de API v1.
8. Criar a prova técnica de localização em segundo plano: motorista → API → Realtime → passageiro/painel.
9. Testar perda de internet, retomada do aplicativo e consumo de bateria.
10. Só depois discutir Google Maps versus Mapbox, incluindo custos; essa conversa foi intencionalmente adiada.

## 11. Critérios de conclusão da Fase 1

- Stack e hospedagem aprovadas.
- Repositório(s) organizado(s) e ambiente de homologação acessível.
- Modelo de dados, permissões e contrato de API revisados.
- GPS funciona com celular bloqueado em viagem simulada e atualiza passageiro/painel de forma privada.
- Perda de conexão não encerra nem corrompe a viagem.
- Estimativa de custo aprovada e alertas/configuração de gastos definidos.

## 12. Documentos já existentes

- [Escopo final da Fase 0](./fase-0-escopo-final.md)
- [Proposta de arquitetura e backend da Fase 1](./fase-1-arquitetura-backend-proposta.md)
- [`git/design.md`](../git/design.md): documento original de design, amplo e com recursos futuros.
- [`git/a.md`](../git/a.md): especificação funcional original, que contém ideias para fases futuras.

## 13. Regra de trabalho para a continuidade

As pendências da Fase 1 serão tratadas **uma por vez**. Antes de tomar uma decisão, discutir contexto, impactos e alternativas; depois registrar a definição no documento técnico. Não avançar automaticamente para todas as próximas decisões de uma vez.

