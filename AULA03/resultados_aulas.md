
//Relatório de Execução - Lab 01 (Aula 03)

1. Impacto das Stopwords no Vocabulário
A filtragem de termos como "de" "da" "meu" e "preciso" remove o ruído sintático, reduzindo o tamanho do vocabulário final e garantindo que apenas termos relevantes para o negócio sejam vetorizados

2. Configuração: ngram_range=(1, 2)
A captura de unigramas e bigramas permite ao modelo reconhecer combinações frequentes de palavras. Termos compostos como "segunda via" passam a ser tratados como uma única unidade de significado relevante em vez de duas palavras isoladas

3. Prevenção de Erros por Palavras Genéricas
Ao ignorar verbos de solicitação comuns (ex.: "quero" "preciso") o modelo evita criar correlações falsas entre intenções distintas. A classificação passa a responder primariamente aos substantivos e conceitos centrais da mensagem

//Relatório de Avaliação - Lab 02 (Aula 03)

1. Métricas Principais

Precision: Mede a confiabilidade do modelo ao atribuir uma intenção (evita falsos positivos)
Recall: Mede a capacidade do modelo de mapear todas as instâncias reais de uma intenção (evita falsos negativos)
F1-Score: Resume a performance equilibrando a precisão e a taxa de captura em uma única nota

2. Diagonal Principal da Matriz de Confusão
Os elementos alinhados na diagonal principal indicam as instâncias em que a intenção prevista coincide exatamente com a intenção real (acertos). Os elementos fora da diagonal representam os erros de classificação entre as diferentes classes

3. Acurácia x Desbalanceamento
Em conjuntos de dados onde uma classe predomina sobre as outras, a acurácia cria uma falsa sensação de alto desempenho. O modelo pode obter uma pontuação alta apenas acertando a classe majoritária, ignorando completamente as intenções menos frequentes

Relatório de Execução - Lab 03 (Aula 03)

1. Código Corrigido e Resultado
python
Execução do pipeline encapsulado
pipeline = Pipeline([
    ('vectorizer', TfidfVectorizer(stop_words=['de', 'o', 'meu', 'minhas'])),
    ('classifier', LogisticRegression())
])
pipeline.fit(X_train, y_train)
predicoes = pipeline.predict(X_test)

2. Vantagem do Pipeline no Scikit-Learn
Abstrai o fluxo completo do projeto de Machine Learning Transforma múltiplos passos sequenciais de vetorização e modelagem em uma única estrutura modular facilitando chamadas com métodos simples como .fit() e .predict()

3. Prevenção de Data Leakage e Erros de Pré-processamento
Evita contaminação entre treino e teste. O Pipeline assegura que os hiperparâmetros e estatísticas (como o vocabulário TF-IDF) sejam aprendidos estritamente sobre os dados de treino. Ao receber novos dados de teste ou produção, aplica apenas a transformação com os parâmetros já ajustados, eliminando riscos de inconsistência matricial.
