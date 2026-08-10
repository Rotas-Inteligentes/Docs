# Rotas Inteligentes - Escopo final da Fase 0

**Versão:** 1.0  
**Data:** 09 de agosto de 2026  
**Status:** aprovado para início da Fase 1 - definições técnicas

## 1. Decisão de produto

O Rotas Inteligentes deixa de ser tratado apenas como uma ideia acadêmica de mobilidade urbana ampla e passa a ser desenvolvido como um produto B2B para **vans universitárias privadas com rotas recorrentes**.

O primeiro objetivo não é atender todo o transporte público ou todos os tipos de fretamento. É provar que uma operação de van universitária consegue oferecer aos estudantes visibilidade em tempo real sobre a viagem, enquanto reduz a comunicação manual do motorista pelo WhatsApp.

## 2. Problema que será atacado

Passageiros de vans universitárias não têm uma fonte centralizada e confiável para acompanhar a localização, o horário e o status da própria viagem. Por isso, dependem de grupos de WhatsApp, mensagens individuais e compartilhamento manual de localização, o que gera espera, incerteza e dificuldade para organizar a rotina.

Do outro lado, motoristas precisam responder repetidamente perguntas como "onde você está?", informar atrasos e administrar passageiros por canais improvisados. Isso fragmenta a comunicação, consome tempo e pode gerar distração durante a condução.

## 3. Público inicial e papéis

| Papel | Quem é | Necessidade principal |
| --- | --- | --- |
| Comprador | Proprietário da van ou pequena frota | Profissionalizar o serviço e reduzir trabalho operacional |
| Gestor | Proprietário ou responsável pela operação | Administrar veículos, motoristas, rotas e passageiros |
| Motorista | Condutor da van | Iniciar a viagem e transmitir sua localização com o mínimo de interação |
| Passageiro | Estudante universitário vinculado à rota | Saber onde está sua van e quando deve se preparar para embarcar |

O cliente ideal inicial é um motorista autônomo ou pequeno proprietário de frota, com uma a dez vans, rotas recorrentes, grupo fixo de estudantes e comunicação atualmente centralizada no WhatsApp.

## 4. Proposta de valor

> O Rotas Inteligentes permite que estudantes acompanhem sua van em tempo real e recebam alertas da viagem, enquanto motoristas e gestores centralizam comunicação, rotas e passageiros em um aplicativo dedicado.

Para o passageiro, o valor é previsibilidade, menos tempo de espera e informações confiáveis. Para o motorista e gestor, o valor é reduzir mensagens repetitivas, centralizar a operação e entregar uma experiência mais profissional.

## 5. Jornada prioritária do produto

O MVP deverá suportar esta jornada de ponta a ponta:

1. O gestor cadastra a operação, o veículo, o motorista e uma rota.
2. O gestor informa os pontos de embarque e convida os estudantes vinculados à rota.
3. O estudante aceita o convite e acessa apenas sua rota autorizada.
4. O motorista inicia a viagem pelo aplicativo.
5. O aplicativo do motorista transmite a localização enquanto a viagem está ativa.
6. O estudante visualiza a posição da van, o status da viagem e o horário da última atualização.
7. O estudante recebe um alerta de aproximação ou atraso relevante.
8. O motorista encerra a viagem.
9. Gestor e estudante podem consultar um histórico básico da operação ou das viagens.

## 6. Escopo do MVP

### 6.1 Painel do gestor

- Criar e administrar a operação.
- Cadastrar veículos e motoristas.
- Criar uma rota recorrente e seus pontos de embarque.
- Vincular estudantes à rota.
- Gerar e revogar convites de acesso.
- Visualizar uma viagem em andamento.
- Consultar histórico básico de viagens.

### 6.2 Aplicativo do motorista

- Autenticação e acesso apenas às rotas autorizadas.
- Visualização da rota do dia.
- Início e encerramento de viagem.
- Transmissão de localização somente durante uma viagem ativa.
- Indicador de que a localização está sendo enviada.
- Registro simples de atraso ou ocorrência, se não prejudicar a segurança do motorista.

### 6.3 Aplicativo do passageiro

- Entrada por convite e autenticação.
- Visualização da rota vinculada.
- Mapa com a localização da van e horário da última atualização.
- Status da viagem: aguardando início, em andamento ou concluída.
- Notificação de aproximação e de atraso relevante.
- Histórico básico das viagens do próprio passageiro.

### 6.4 Requisitos transversais

- Controle de acesso por papel: gestor, motorista e passageiro.
- Registro de eventos essenciais da viagem.
- Tratamento de ausência de internet e indicação de localização desatualizada.
- Coleta mínima de dados pessoais.
- Registro de erros e monitoramento básico desde o piloto.

## 7. Fora do MVP

Os itens abaixo não serão desenvolvidos antes da validação do piloto:

- Consulta pública de linhas, bairros, ônibus e destinos populares.
- Integração com transporte público ou prefeituras.
- Otimização automática de rotas.
- Lotação automática dos veículos.
- Publicidade, cupons e parceiros comerciais.
- Pagamentos e gestão financeira da van.
- Avaliação de viagem, satisfação e gamificação.
- Indicadores de emissão de carbono ou economia financeira.
- Achados e perdidos, clima, trânsito detalhado e recursos informativos periféricos.
- Login social com Google ou Apple.
- Aplicativo específico para instituições de ensino.

Esses itens continuam registrados como possibilidades de pós-MVP, mas não podem ampliar o escopo do primeiro piloto.

## 8. Piloto inicial

O primeiro piloto será realizado com a van universitária utilizada pelo proponente do projeto.

### Configuração esperada

- Uma van e um motorista.
- Uma rota de ida e, se possível, uma rota de volta.
- Grupo inicial de 5 a 20 estudantes convidados.
- Duração prevista de duas a quatro semanas.
- Cadastro, importação e suporte realizados manualmente pela equipe do projeto.

### Indicadores de sucesso do piloto

- Pelo menos 70% dos estudantes convidados ativam o acesso.
- O motorista consegue iniciar e encerrar viagens sem suporte recorrente.
- A localização fica disponível na maior parte das viagens ativas.
- Os passageiros conseguem identificar se a van está a caminho.
- Perguntas repetidas sobre localização diminuem na comunicação do motorista.
- Nenhuma falha crítica impede a conclusão de uma viagem.
- Motorista ou gestor demonstra intenção de continuar usando o produto após o período de teste.

## 9. Hipóteses a validar

### Problema

- A falta de visibilidade da van gera incômodo real aos estudantes.
- O motorista recebe perguntas recorrentes sobre localização e atraso.
- O WhatsApp não resolve sozinho a necessidade de acompanhamento.

### Solução

- O motorista aceita iniciar e encerrar a viagem no aplicativo.
- O envio de localização por smartphone é tecnicamente confiável para o piloto.
- Passageiros aceitam usar um aplicativo acessado por convite.
- Mapa, status e alerta de aproximação são suficientes para gerar valor inicial.

### Negócio

- O proprietário percebe valor em profissionalizar a operação.
- A cobrança por veículo ativo é compreensível e aceitável.
- Uma assinatura mensal oferece mais previsibilidade que a cobrança por viagem ou passageiro.

## 10. Modelo de negócio inicial

O modelo a ser testado é **SaaS B2B por veículo ativo**, com passageiros incluídos no plano.

| Elemento | Hipótese inicial |
| --- | --- |
| Contratante | Motorista proprietário ou dono da frota |
| Unidade de cobrança | Veículo ativo por mês |
| Cobrança | Mensal recorrente |
| Implantação | Taxa única opcional para configuração e treinamento |
| Piloto | Gratuito ou subsidiado, por prazo definido |
| Contrato após piloto | Assinatura mensal com compromisso inicial sugerido de três meses |

Preço final, faixa de planos e política de desconto ainda não estão definidos. Eles dependem do custo técnico da Fase 1, do uso observado no piloto e da conversa comercial com o primeiro cliente.

## 11. Riscos e respostas iniciais

| Risco | Resposta prevista |
| --- | --- |
| Localização parar em segundo plano | Testes em celulares reais e mecanismos de monitoramento da sessão de viagem |
| Internet móvel instável | Exibir a última localização recebida e seu horário |
| Consumo excessivo de bateria | Ajustar frequência de atualização sem perder a utilidade do rastreamento |
| Motorista esquecer de iniciar a viagem | Fluxo simples, lembretes e orientação durante o piloto |
| Passageiros não aderirem | Convite rápido, onboarding curto e apoio presencial ou por WhatsApp no início |
| Dados de localização acessados indevidamente | Vínculos por rota, autenticação e revogação de acesso pelo gestor |
| Expectativa de segurança absoluta | Comunicação clara: o serviço é informativo e não substitui os cuidados operacionais do transportador |
| Falha crítica durante uma viagem | Registros de erro, suporte manual e plano de contingência via WhatsApp no piloto |
| Cliente não quiser pagar | Validar disposição de pagamento antes e durante o piloto |

Questões de privacidade, tratamento de localização e documentos contratuais deverão ser revisadas antes de qualquer operação comercial em produção.

## 12. Decisões para a Fase 1

A Fase 1 deverá definir, com base neste escopo:

1. Arquitetura do sistema e divisão entre painel web, aplicativo do motorista e aplicativo do passageiro.
2. Stack de desenvolvimento e padrão de código.
3. Estratégia de rastreamento em segundo plano.
4. Banco de dados, autenticação, controle de acesso e modelagem dos principais dados.
5. Provedor de mapas, geolocalização e notificações.
6. Infraestrutura, ambientes, observabilidade e backups.
7. Custos estimados por veículo, passageiro e viagem.
8. Segurança, privacidade e requisitos de operação para o piloto.
9. Prova técnica de envio e exibição de localização em tempo real.

## 13. Condição de aprovação da Fase 0

Esta fase está aprovada para avanço técnico porque o nicho, o comprador, os usuários, a proposta de valor, a jornada prioritária, o piloto e o limite do MVP foram definidos.

Entrevistas com motorista e estudantes continuam obrigatórias, mas passam a ocorrer em paralelo à Fase 1. Elas podem ajustar prioridades do MVP, sem alterar o foco em vans universitárias privadas sem uma nova decisão formal de produto.
