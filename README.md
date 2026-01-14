# Análise de Teste A/B - Sistema de Recomendação

## Descrição do Projeto
Este projeto consiste na análise de um teste A/B realizado por uma loja online internacional. O objetivo foi avaliar o impacto de um novo sistema de recomendação melhorado no comportamento dos utilizadores. A expectativa era que o novo sistema (Grupo B) gerasse um aumento de pelo menos 10% na conversão em cada etapa do funil de vendas (visualização de produto, adição ao carrinho e compra) no período de 14 dias após o cadastro.

## Ferramentas e Bibliotecas Utilizadas
- **Python**: Linguagem principal.
- **Pandas**: Manipulação e filtragem de dados.
- **Matplotlib & Seaborn**: Visualização de dados e distribuições.
- **Plotly**: Criação de gráficos de funil interativos.
- **SciPy & Statsmodels**: Realização de testes de proporções (Z-test) e validação estatística.

## Tabela (Dicionário de Dados)
O conjunto de dados é composto por quatro tabelas principais:

**Calendário de Eventos de Marketing (`ab_project_marketing_events_us.csv`):**
- `name` — nome do evento de marketing
- `regions` — regiões onde a campanha foi realizada
- `start_dt` — data de início da campanha
- `finish_dt` — data de término da campanha

**Novos Utilizadores (`final_ab_new_users_upd_us.csv`):**
- `user_id` — ID exclusivo do utilizador
- `first_date` — data de inscrição
- `region` — região do utilizador
- `device` — dispositivo utilizado para inscrição

**Eventos (`final_ab_events_upd_us.csv`):**
- `user_id` — ID do utilizador
- `event_dt` — data e hora do evento
- `event_name` — tipo de evento (`login`, `product_page`, `product_cart`, `purchase`)
- `details` — dados adicionais sobre o evento (ex: preço da compra)

**Participantes do Teste (`final_ab_participants_upd_us.csv`):**
- `user_id` — ID do utilizador
- `group` — grupo do teste (A — controle, B — novo sistema)
- `ab_test` — nome do teste

## Metodologia
**Análise Exploratória de Dados**
- Verificação da integridade dos dados e tratamento de tipos.
- Verificação de sobreposição de utilizadores entre diferentes testes e entre grupos (A e B).
- Análise da distribuição de novos utilizadores por região, garantindo que o público da UE fosse de 15%.

**Pré-processamento**
- Filtragem dos dados para focar exclusivamente no teste `recommender_system_test`.
- Corte dos eventos ocorridos após 14 dias do registo de cada utilizador (conforme especificação técnica).
- Ajuste das datas para o período oficial do teste (07/12/2020 a 01/01/2021).

**Preparação do conjunto para o modelo**
- Construção do funil de conversão agregando utilizadores únicos por tipo de evento e por grupo.
- Definição da hipótese nula: as proporções de conversão entre os grupos A e B são iguais em cada etapa.

## Resultados
Os resultados mostraram que o novo sistema de recomendação (Grupo B) não atingiu o objetivo de 10% de aumento e, em alguns casos, teve um desempenho inferior ao sistema atual:

1. **Página de Produto**: A conversão caiu de 64,80% (A) para 56,36% (B) (P-valor: 0,0000).
2. **Carrinho**: A conversão caiu de 30,00% (A) para 27,48% (B) (P-valor: 0,1453).
3. **Compra**: A conversão caiu de 31,74% (A) para 27,59% (B) (P-valor: 0,0176).



A conclusão estatística é que o sistema B converte menos que o sistema A em etapas cruciais. Portanto, a recomendação é **não implementar** as mudanças do sistema B e realizar novos estudos para entender as causas da queda de interesse.

## Aprendizados
- **Testes de Hipóteses**: Aplicação prática do teste Z para proporções em funis de vendas.
- **Rigor Analítico**: Identificação de problemas na execução do teste (utilizadores que participaram em dois testes simultâneos).
- **Análise de Funil**: Visualização clara da jornada do utilizador e onde ocorrem as maiores perdas de conversão.
- **Tomada de Decisão**: Entender que um resultado negativo em um teste A/B é valioso, pois evita que a empresa implemente mudanças prejudiciais ao lucro.
- **Limpeza de Dados Complexa**: Cruzamento de múltiplos datasets para garantir que apenas os utilizadores qualificados fossem analisados.
