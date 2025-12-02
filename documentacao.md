Plano de Desenvolvimento Profissional para Landing Page de Infoproduto

1. Visão Geral do Projeto

Produto: Infoproduto de Catequese Calvinista (Assinatura Mensal/Anual e Material Gratuito).
Público-alvo: Pais, professores de Escola Dominical e líderes de ministério infantil (Igrejas Presbiterianas/Calvinistas).
Objetivo: Captura de Leads (Material Gratuito) e Venda de Assinatura (Material Pago).

Tecnologias Envolvidas:

Frontend (UI): React + TypeScript + Tailwind CSS (Alta conversão, responsivo).

Backend (API Gateway): Node.js/Express (Para gerenciar a comunicação segura com Pagar.me e Google Sheets/Forms, e o webhook do Pagar.me).

Automação (Workflow): n8n (Orquestração de envio de e-mail e confirmação de pagamento).

Serviços Externos: Pagar.me (Gateway de Pagamento), Google Forms (Captura de Leads Gratuito), Google Sheets (Database de Leads/Assinantes).

2. Frontend - React/TypeScript/Tailwind CSS

Foco: Conversão, Prova Social, Gatilhos Mentais (Escassez, Autoridade, Reciprocidade).

Componentes e Seções da Landing Page:

Hero Section (Acima da Dobra):

Título de Alto Impacto: Claro e focado na dor/benefício ("Transforme a fé dos seus filhos com lições bíblicas inesquecíveis.").

Subtítulo: Benefício direto e alinhado ao público (e.g., "Conteúdo cristocêntrico e fiel à teologia calvinista, pronto para usar.").

CTA Principal (Material Gratuito - Gatilho de Reciprocidade): Botão proeminente: "Baixe a Lição Gratuita Agora!".

Imagem do Produto: Mockup 3D ou imagem de Jesus com crianças (como na prévia PDF) para conexão emocional.

Seção de Gatilho de Autoridade/Compromisso:

Logo da EDITORA REMA VIVA e menção ao alinhamento com a doutrina Presbiteriana/Calvinista.

Breve depoimento ou selo de aprovação de um líder teológico.

Seção de Benefícios (Dores vs. Soluções):

Abordar as dores (e.g., falta de material de qualidade, tempo para preparar aulas, conteúdo não cristocêntrico).

Apresentar o produto como a solução (e.g., pronto para uso, fidelidade bíblica, estrutura pedagógica).

Seção Oferta Principal (Assinatura - Gatilho de Escassez/Urgência):

Explicar o valor da assinatura (mensal e anual).

Listar o que o assinante recebe (Lições completas, atividades, guias para professores).

Incluir um Timer de Escassez (e.g., "Preço de Lançamento por tempo limitado!").

Seção Prova Social (Gatilho de Confiança):

Testemunhos de líderes/pais (Usar placeholders se não houver).

Selos de segurança e formas de pagamento.

FAQ/Perguntas Frequentes: Dúvidas sobre o conteúdo, frequência de envio, e cancelamento.

Footer: Informações de contato, links para termos de uso e política de privacidade.

3. Integrações e Fluxo de Dados (Node.js Backend e Serviços)

O Backend Node.js é crucial para a segurança e orquestração dos fluxos.

Fluxo A: Material Gratuito (Lead Capture)

Frontend (React): O usuário clica no CTA "Baixe a Lição Gratuita Agora!" e um modal/pop-up abre com o formulário.

Formulário de Captura: O formulário deve ter campos simples (Nome, Email, WhatsApp - opcional).

Submissão: O React envia os dados para o endpoint do Google Forms.

Nota de Implementação: Para evitar problemas de CORS, é melhor usar a integração nativa do Google Forms, enviando o formulário diretamente (o que exige que os name dos campos do React correspondam aos id ou name dos campos do Google Form).

Alternativa Profissional: Enviar os dados para um endpoint Node.js, que por sua vez, submete de forma segura ao Google Sheets (via Google Service Account API) ou faz o POST direto para a URL de submissão do Google Forms.

Google Sheets: O Google Forms alimenta uma Planilha Google.

Automação (n8n - Gatilho 1): O n8n monitora a Planilha Google (ou recebe um Webhook do Google Forms/Sheets, se disponível) e inicia o fluxo de envio:

Envia o e-mail de confirmação (Double Opt-in) ou, mais simples, o e-mail direto com o link de download do PDF gratuito.

Fluxo B: Assinatura Paga (Pagar.me)

Frontend (React): O usuário clica em "Assinar Agora" na Seção 4.

Checkout:

Opção A (Recomendada): Usar o Modal de Checkout do Pagar.me (embedded checkout) para simplificar a captura de dados do cartão e reduzir o risco de PCI Compliance. O React apenas chama a função de inicialização do modal.

Opção B (Customizada e Mais Complexa): Capturar os dados do cliente no React e enviá-los (com criptografia) para o Node.js Backend.

Backend (Node.js - Gateway de Transação):

Segurança: O Node.js é o único a possuir a Secret Key do Pagar.me.

Requisição: O Backend recebe a intenção de compra (plano, dados do cliente) e utiliza a API do Pagar.me para criar uma transação ou criar uma Assinatura.

Resposta: O Backend retorna o status da transação ao Frontend.

Pagar.me Webhook (Node.js - Listener):

Endpoint Node.js dedicado (/webhook/pagarme) que recebe notificações em tempo real do Pagar.me sobre a mudança de status da transação (e.g., paid, refused, waiting_payment).

Ação: Quando o Node.js recebe um status de paid (pago), ele aciona o n8n.

Automação (n8n - Gatilho 2 - Confirmação de Pagamento):

O Node.js envia um Webhook customizado (com dados do cliente e do plano) para um Webhook Endpoint do n8n.

Fluxo n8n:

Recebe o webhook de pagamento confirmado.

Registra o novo assinante na Planilha Google (ou banco de dados).

Envia o e-mail de boas-vindas e acesso ao Material Pago (PDFs, links de área de membros, etc.).

4. Requisitos de Código (Pontos Críticos para a IA)

Área

Tecnologia

Ação Crítica

Detalhes

Frontend

React/TS

High-Conversion UI

Uso de Tailwind, design limpo, tipografia legível e cores que remetam ao tema (fé, confiança, o material da prévia PDF: verde, azul, amarelo).

Frontend

JavaScript

Integração Google Forms

Garantir que a submissão do formulário Freebie seja feita de forma limpa, redirecionando ou mostrando uma mensagem de sucesso, e acionando o Google Form (via fetch ou redirecionamento).

Backend

Node.js

Segurança Pagar.me

NUNCA expor a Pagar.me Secret Key no Frontend. Todas as chamadas de API (criação de transação, assinaturas) devem ser feitas via Node.js.

Backend

Node.js

Webhook Listener

Criar um endpoint POST (/webhook/pagarme) que receba e valide a assinatura do webhook (se necessário, para autenticar a origem do Pagar.me) antes de acionar o n8n.

n8n

Automação

Fluxo de Confirmação

O nó inicial deve ser um Webhook Trigger que recebe a confirmação de pagamento do Node.js. O nó seguinte deve ser o Google Sheets Node (Add Row) e, por fim, o Email Sender Node (com o material pago).

Com este plano, a IA tem todas as diretrizes para desenvolver uma solução robusta, segura e totalmente integrada.