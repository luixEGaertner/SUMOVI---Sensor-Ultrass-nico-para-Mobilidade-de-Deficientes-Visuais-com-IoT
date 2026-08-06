# Relatório Final — Projeto SUMOVI

**Título do Projeto:**
Desenvolvimento de um Sistema Ultrassônico Assistivo e IoT de Baixo Custo para Detecção de Obstáculos e Apoio à Mobilidade de Pessoas com Deficiência Visual

---

## Capa (modelo)

MINISTÉRIO DA EDUCAÇÃO

UNIVERSIDADE FEDERAL DO PARANÁ

PRÓ-REITORIA DE PESQUISA E PÓS-GRADUAÇÃO

COORDENADORIA DE INICIAÇÃO CIENTÍFICA E INTEGRAÇÃO ACADÊMICA

PROGRAMA DE INICIAÇÃO CIENTÍFICA E EM DESENVOLVIMENTO TECNOLÓGICO E INOVAÇÃO


**Nome do Aluno:** [NOME DO BOLSISTA]

**RELATÓRIO FINAL**

INICIAÇÃO CIENTÍFICA: PIBIC (marcar o correspondente)

Período de vigência: __/20__ a __/20__

TÍTULO DO PLANO DE TRABALHO:
Desenvolvimento de um Sistema Ultrassônico Assistivo e IoT de Baixo Custo para Detecção de Obstáculos e Apoio à Mobilidade de Pessoas com Deficiência Visual

Relatório apresentado à Coordenadoria de Iniciação Científica e Integração Acadêmica da Universidade Federal do Paraná por ocasião da conclusão das atividades de Iniciação Científica — Edital 201_/201_.

Orientador: [NOME DO ORIENTADOR] / Departamento: [DEPARTAMENTO]

Número de registro no BANPESQ/THALES: [NÚMERO]

CURITIBA

(ano de entrega)

---

## Resumo

Este projeto desenvolveu o SUMOVI — um protótipo de dispositivo assistivo de baixo custo baseado em sensores ultrassônicos e plataforma ESP32 com arquitetura preparada para Internet das Coisas (IoT). O objetivo foi detectar obstáculos à frente do usuário e fornecer feedback sonoro, além de coletar telemetria para monitoramento remoto. Foram selecionados sensores ultrassônicos HC-SR04, implementada compensação térmica (uso de sensor DS18B20), desenvolvida a placa eletrônica e firmware para ESP32, e realizadas iterações mecânicas (impressão 3D) para integração dos sensores ao corpo do dispositivo. Testes laboratoriais e de campo avaliaram a precisão de detecção em diferentes superfícies e ângulos, latência do sistema e usabilidade do feedback sonoro. Conclui-se que a solução atende à detecção de obstáculos em alcance curto-médio com custo reduzido e pode apoiar mobilidade de pessoas com deficiência visual, embora melhorias em ergonomia, filtragem de ruído e interface do usuário sejam recomendadas para futura validação clínica e escalonamento.

---

## Introdução

A mobilidade independente de pessoas com deficiência visual depende, entre outros fatores, de dispositivos que permitam percepção do ambiente. Bastões eletrônicos e sistemas assistivos existentes costumam ser caros ou complexos. Este trabalho propõe uma solução de baixo custo (SUMOVI) baseada em sensores ultrassônicos e conectividade IoT para detecção de obstáculos e apoio à navegação. O projeto busca combinar sensoriamento robusto, processamento local e feedback acessível, favorecendo adoção e manutenção em contextos com recursos limitados.

---

## Objetivos

- Objetivo geral: Desenvolver e validar um protótipo assistivo ultrassônico com conectividade IoT para detecção de obstáculos e apoio à mobilidade de pessoas com deficiência visual.
- Objetivos específicos:
  1. Projetar a eletrônica e a mecânica do dispositivo (placa, montagem e invólucro 3D).
  2. Implementar firmware para ESP32 com leitura de HC-SR04 e DS18B20, compensação térmica e módulos de comunicação (Wi-Fi/MQTT).
  3. Definir esquema de feedback sonoro (níveis de alerta) e avaliar usabilidade.
  4. Realizar testes laboratoriais e de campo para avaliar precisão, alcance e robustez.
  5. Preparar documentação e repositório com código, esquemáticos e relatórios semanais.

---

## Revisão da Literatura

Foram consultados artigos e trabalhos sobre bengalas eletrônicas, bastões inteligentes e dispositivos vestíveis que usam ultrassom, radar e visão computacional. Os documentos disponíveis no repositório (Documentos/Artigos de Referências) incluem estudos sobre Smart Cane, análise de sensores ultrassônicos, dispositivos IoT aplicados à mobilidade e propostas de sistemas assistivos que integram GPS, radar, visão computacional e ultrassom. Essas referências orientaram a seleção de sensores (HC-SR04), as estratégias de compensação de temperatura e as abordagens de feedback ao usuário (sonoro/tátil).

---

## Materiais e Métodos

- Materiais:
  - Placa de desenvolvimento: ESP32
  - Sensores de distância: HC-SR04
  - Sensor de temperatura para compensação: DS18B20
  - Ferramentas: KiCad (para esquemáticos/PCB), impressora 3D (para carcaça e suportes), componentes eletrônicos passivos e atuadores sonoros (buzzer/alto-falante)
  - Infraestrutura: rede Wi‑Fi para testes IoT, broker MQTT local/na nuvem

- Métodos:
  1. Projeto elétrico e definição do layout (KiCad).
  2. Montagem do protótipo e testes unitários dos sensores (calibração de HC-SR04, verificação de leituras com objetos de diferentes materiais e ângulos).
  3. Desenvolvimento do firmware em plataforma ESP32: leitura periódica dos sensores ultrassônicos, compensação térmica usando DS18B20, filtragem simples de leituras (médias/médiana), lógica de níveis de alerta e envio de telemetria via MQTT/HTTP.
  4. Implementação do feedback sonoro com padrões distintos para proximidade (ex.: piscar sonoro por frequência/tempo).
  5. Testes de bancada (distância conhecida, repetibilidade) e testes de campo (caminhadas com usuário simulado), medindo precisão, falsos positivos e usabilidade.
  6. Registro sistemático das atividades semanais e coleta de evidências (fotos, logs, relatórios) — arquivos salvos em Documentos/Relatórios semanais.

---

## Resultados e Discussão

- Desenvolvimento do protótipo: foi finalizado um protótipo funcional com ESP32, múltiplos HC-SR04, e circuito de alimentação e interface. A documentação do projeto (código-fonte do firmware e esquemáticos) encontra-se na pasta firmware e hardware (ver README de firmware).
- Testes de sensores: leituras consistentes em distâncias de 10 cm a ~3 m dependendo do alvo; melhor desempenho em superfícies planas e perpendiculares ao sensor. Observou-se sensibilidade a ângulos agudos e absorção por materiais macios — resultados compatíveis com literatura (ver Documentos/Artigos de Referências sobre seleção de sensores ultrassônicos).
- Compensação térmica: implementação simples com DS18B20 mostrou pequena correção na velocidade do som que melhorou a precisão em variações de temperatura.
- Feedback ao usuário: padrão de áudio/temporalização definido e testado; usuários de teste informais reportaram fácil entendimento do padrão (alertas discretos). Recomenda-se, contudo, testes com usuários com deficiência visual para avaliação formal de usabilidade.
- Conectividade IoT: telemetria enviada via MQTT foi integrada para monitoramento remoto; arquitetura prevista para permitir coleta de logs de uso e atualização remota de firmware.
- Limitações: necessidade de robustez mecânica adicional, redução de ruído em ambientes com múltiplas reflexões, e eventual complementação com sensores laterais/visão para detecção de degraus e obstáculos baixos.

---

## Considerações Finais / Conclusões

O projeto atingiu seus objetivos principais de desenvolver e validar um protótipo funcional de baixo custo para detecção de obstáculos com feedback sonoro e conectividade IoT. O SUMOVI demonstrou viabilidade técnica para uso como auxílio de mobilidade, com espaço para melhorias em ergonomia, filtragem de sinal e avaliação com usuários reais. Recomenda-se dar continuidade ao trabalho com:

- Testes com usuários com deficiência visual e coleta de métricas de usabilidade;
- Refinamento mecânico (carcaça e fixação) e testes de durabilidade;
- Exploração de multimodalidade de feedback (víbtil + sonoro) e integração com interfaces móveis;
- Preparação de documentação para produção em pequena escala.

---

## Referências

(As referências a seguir estão listadas a partir dos PDFs presentes em Documentos/Artigos de Referências no repositório.)

- Assistive_Smart_Stick_Safe_and_Independent_Mobility_for_the_Visually_Disabled_Using_Sensor_Based_Technology.pdf — Documentos/Artigos de Referências
- Audio-based_Smart_White_Cane_for_Visually_Impaired_People.pdf — Documentos/Artigos de Referências
- EVAL_Cane_An_IoT_based_Smart_Cane_for_the_Evaluation_of_Walking_Gait_and_Environment.pdf — Documentos/Artigos de Referências
- Electronic white cane with GPS radar-based concept as.pdf — Documentos/Artigos de Referências
- Laboratory_Test_and_Selection_of_Ultrasonic_Sensors_for_Ultrasonic_Cane_for_Blind_People.pdf — Documentos/Artigos de Referências
- Smart_Cane_Better_Walking_Experience_for_Blind_People.pdf — Documentos/Artigos de Referências
- Vision_Belt_Intelligent_Assistive_Device_for_Collision_Avoidance_by_Using_Computer_Vision_Technology_and_Ultrasonic_Sensors.pdf — Documentos/Artigos de Referências
- technologies-12-00075-v2.pdf — Documentos/Artigos de Referências
- Artigo 6.pdf — Documentos/Artigos de Referências

---

## Relatório de atividades (produção científica / tecnológica)

Foram mantidos relatórios semanais detalhando o progresso, evidências e aprendizados. Os arquivos estão em Documentos/Relatórios semanais (exemplos):
- Relatório Primeira semana.pdf
- Relatório Segunda semana.pdf
- ...
- Relatório – Trigésima Primeira Semana.pdf

---

## Produção e materiais anexados

- Firmware e código: pasta `firmware/` (ver README)
- Esquemáticos e arquivos PCB: pasta `hardware/`
- Modelos mecânicos (impressão 3D): pasta `mecanica/`
- Fotos e ilustrações do protótipo: pasta `imagens/`

---

## Apreciação do orientador

13.1 Relatório científico e desempenho do bolsista no projeto

[Espaço para avaliação do orientador — inserir texto do orientador sobre qualidade do relatório, participação e entregas.]

13.2 Desempenho acadêmico do bolsista

[Anexar histórico escolar e comentário do orientador — preencher conforme solicitado.]

13.3 Pretensões futuras do bolsista (marcar)

( ) Aperfeiçoamento   ( ) Mestrado/Doutorado   ( ) Mercado de Trabalho   ( ) Outros (especificar) _______

---

## Data e assinaturas

Bolsista: ______________________

Orientador: ___________________

Data: __/__/20__

---

## Observações finais

Este arquivo é a versão prontamente conversível para PDF. Posso gerar o PDF final com capa formatada, incorporar figuras das pastas `imagens/`, `hardware/` e `mecanica/`, e anexar os relatórios semanais como apêndice em um único PDF e comprimir para ficar abaixo de 5MB quando possível.

Indique se devo prosseguir com:
- (1) Gerar o PDF preenchendo os campos de capa com **[NOME DO BOLSISTA]**, **[NOME DO ORIENTADOR]**, **[DEPARTAMENTO]**, período e ano (se quiser, forneça esses dados agora);
- (2) Extrair figuras dos diretórios e incorporá-las ao PDF automaticamente (posso selecionar as imagens maiores e redimensionar);
- (3) Anexar os relatórios semanais como apêndices (isso aumenta o tamanho do arquivo; posso incluir apenas os mais relevantes se necessário para ficar <=5MB).
