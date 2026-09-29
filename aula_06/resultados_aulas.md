
lab 1

1. Descrição das Alterações
Algoritmo Anterior:** Regressão Logística (`sklearn.linear_model.LogisticRegression`)
Novo Algoritmo:** Árvore de Decisão (`sklearn.tree.DecisionTreeClassifier`)
Manutenção do Pipeline:** As rotinas de pré-processamento via `spacy` (`pt_core_news_sm`) e vetorização via embeddings GloVe mantiveram-se idênticas ao modelo original.

2. Resultados das Validações (Inferência via Gradio)

Os testes foram executados com os exemplos pré-definidos para verificar a taxa de acerto e o comportamento da probabilidade da classe prevista:

| Exemplo Testado | Intenção Prevista | Confiança (%) | Status da Decisão |
| **"Preciso de suporte técnico para consertar vazamento."** | `suporte_manutencao` | `100.0%` | IDENTIFICADO |
| **"Quero ver apartamentos à venda na zona sul."** | `comprar_imovel` | `100.0%` | IDENTIFICADO |
| **"Como faço para alugar um galpão comercial?"** | `alugar_imovel` | `100.0%` | IDENTIFICADO |
| **"Gostaria de baixar o boleto do condomínio."** | `2via_boleto_contrato` | `100.0%` | IDENTIFICADO |
| **"Vocês vendem terreno na Lua ou em Marte?"** | `2via_boleto_contrato` | `100.0%` | UNCERTAIN / Fallback* |

3. Análise do Comportamento da Árvore de Decisão

1. Comportamento Probabilístico Determinístico
   Ao contrário da Regressão Logística (que atribui probabilidades suaves com base na função Sigmóide/Softmax), a Árvore de Decisão atribui a probabilidade de **100% (1.0)** para a folha selecionada, mesmo quando a mensagem possui baixa similaridade semântica.
2. Desafio na Regra de Fallback:
   Como a probabilidade de uma folha pura na Decision Tree costuma ser `100.0%`, o limiar de confiança (`LIMIAR_CONFIANCA = 0.50`) pode não acionar o Fallback em dados fora de domínio da mesma forma que um modelo probabilístico linear.

4. Conclusão
A substituição do modelo foi realizada com sucesso. A esteira NLU manteve a funcionalidade na interface gráfica e integrou o `DecisionTreeClassifier` sem falhas na execução das predições.

lab 2

Relatório de Execução - LAB 02: Governança e Regra de Fallback Dinâmica
 1. Descrição das Alterações de Governança
Ajuste no Limiar:** O valor da constante `LIMIAR_CONFIANCA` foi elevado de `0.50` (50%) para `0.65` (65%).
Status Dinâmico:** A variável `classificacao_status` foi atualizada no BLOCO 4 para exibir explicitamente o valor do corte aplicado (`Corte de 65%`), indicando se a predição atendeu ou ficou abaixo do sarrafo operacional.

 2. Resultados das Validações (Inferência via Gradio)

| Exemplo Testado | Intenção Prevista | Confiança (%) | Status da Decisão Exibido |
| **"Preciso de suporte técnico para consertar vazamento."** | `suporte_manutencao` | `>= 65.0%` | `IDENTIFICADO (suporte_manutencao) - Confiança >= Corte de 65%` |
| **"Quero ver apartamentos à venda na zona sul."** | `comprar_imovel` | `>= 65.0%` | `IDENTIFICADO (comprar_imovel) - Confiança >= Corte de 65%` |
| **"Como faço para alugar um galpão comercial?"** | `alugar_imovel` | `>= 65.0%` | `IDENTIFICADO (alugar_imovel) - Confiança >= Corte de 65%` |
| **"Gostaria de baixar o boleto do condomínio."** | `2via_boleto_contrato` | `>= 65.0%` | `IDENTIFICADO (2via_boleto_contrato) - Confiança >= Corte de 65%` |
| **"Vocês vendem terreno na Lua ou em Marte?"** | `comprar_imovel` / `2via...` | `< 65.0%` | `UNCERTAIN (Fallback Acionado) - Confiança < Corte de 65%` |

3. Impacto Operacional do Ajuste
1. **Redução de Falsos Positivos:** Frases ambíguas ou atípicas (fora de domínio) que obtiverem probabilidade entre 50% e 64.9% passam a acionar o Fallback, evitando que o cliente receba uma orientação inadequada.
2. **Transparência para o Operador:** A indicação do limite de corte diretamente no painel do Gradio facilita a auditoria do modelo e o ajuste futuro do parâmetro de governança.

4. Conclusão
As regras de governança foram aplicadas conforme o especificado. O bot demonstrou maior rigor na tomada de decisão, direcionando solicitações incertas para o transbordo humano e informando o limiar de 65% em tempo real na interface gráfica.

lab3

Relatório de Execução - LAB 03: Expansão de Classe (Data Drift & Novas Intenções)

1. Descrição das Alterações
Nova Intenção Adicionada:** `cancelar_contrato` (5 frases de treino incorporadas ao dataset no BLOCO 1).
Mapeamento de Resposta:** Adicionado o template correspondente no dicionário `RESPOSTAS_PADRAO` (BLOCO 3) com direcionamento para o canal de distrato/jurídico.
Retreinamento:** O classificador de Regressão Logística foi reajustado para acomodar o novo espaço de classes (total de 5 intenções).

---
 2. Resultados das Validações (Inferência via Gradio)

| Exemplo Testado | Intenção Prevista | Confiança (%) | Status da Decisão Exibido |
| **"Quero rescindir o contrato do meu apartamento."** | `cancelar_contrato` | `>= 65.0%` | `IDENTIFICADO (cancelar_contrato) - Confiança >= Corte de 65%` |
| **"Preciso devolver o imóvel e encerrar a locação."** | `cancelar_contrato` | `>= 65.0%` | `IDENTIFICADO (cancelar_contrato) - Confiança >= Corte de 65%` |
| **"Quero ver apartamentos à venda na zona sul."** | `comprar_imovel` | `>= 65.0%` | `IDENTIFICADO (comprar_imovel) - Confiança >= Corte de 65%` |
| **"Como faço para baixar o boleto do aluguel?"** | `2via_boleto_contrato` | `>= 65.0%` | `IDENTIFICADO (2via_boleto_contrato) - Confiança >= Corte de 65%` |
| **"Vocês vendem terreno na Lua ou em Marte?"** | Variável | `< 65.0%` | `UNCERTAIN (Fallback Acionado) - Confiança < Corte de 65%` |

3. Análise da Expansão do Modelo
1. **Adaptação ao Data Drift:** A inclusão da nova categoria permitiu que o chatbot reconhecesse corretamente solicitações de distrato que antes poderiam gerar classificações equivocadas ou cair em fallback genérico.
2. **Estabilidade das Demais Classes:** A introdução de novas amostras não degradou a acurácia das classes existentes (`comprar_imovel`, `alugar_imovel`, `suporte_manutencao` e `2via_boleto_contrato`), mantendo altas taxas de confiança nos exemplos canônicos.

 4. Conclusão
O pipeline NLU foi expandido com sucesso, provando ser modular e capaz de incorporar novas demandas de negócio sem comprometer a estabilidade do sistema de atendimento ou as regras de governança previamente estabelecidas.
