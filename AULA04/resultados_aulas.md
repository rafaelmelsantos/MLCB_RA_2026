Atividade 3: Relatório Comparativo de Modelos
1 - Ao concluir a execução dos dois scripts, consolide as análises no arquivo resultados_aula04.md seguindo o modelo abaixo:

# Relatório de Avaliação NLU - SAC Móveis Residenciais
## 1. Tabela Comparativa de Métricas (Dados de Teste)

| Modelo | Acurácia Geral | F1-Score (Weighted) | Principais Erros na Matriz |
| :--- | :--- | :--- | :--- |
| **KNN (K=3)** | % | % | [Descreva quais classes se confundiram] |
| **Decision Tree** | % | % | [Descreva quais classes se confundiram] |

## 2. Análise dos Testes de Entrada (`input()`)
- **Comportamento do KNN (10 testes):** [Como o KNN reagiu às variações das frases digitadas e ao fallback?]
- **Comportamento da Decision Tree (8 testes):** [Como a Árvore de Decisão se comportou em comparação ao KNN?]

## 3. Veredito Final
- **Melhor modelo para este projeto:** [KNN ou Decision Tree]
- **Justificativa técnica:** [Explique a escolha com base nas métricas estatísticas e no comportamento do fallback]


//1.

Modelo	      |   Acurácia Geral	|   F1-Score (Weighted)	|  Principais Erros na Matriz
KNN (K=3)     | 	90%	            |0.9                    |Leves confusões pontuais entre trocas_devolucoes e reclamacoes devido ao uso de palavras sobrepostas (ex: "defeito" / "quebrado").
Decision Tree |	83%	              |0.83                   |Maior taxa de erro ao classificar frases mais longas, confundindo suporte com trocas_devolucoes e vendas com logistica_entregas


//2.

KNN (10 testes): Apresentou alta sensibilidade à proximidade semântica (graças à distância de cosseno no TF-IDF) Em frases com palavras totalmente fora do vocabulário de treino a probabilidade caiu abaixo de 50% acionando com precisão o mecanismo de Fallback e evitando previsões equivocadas

Demonstrou maior rigidez devido às divisões exatas por palavras-chave (splits do nó).

//3.

KNN (K=3) = melhor

O KNN superou a Árvore de Decisão tanto nas métricas gerais de teste (Acurácia de ~90% contra ~83%) quanto no cálculo de probabilidades via predict_proba()
