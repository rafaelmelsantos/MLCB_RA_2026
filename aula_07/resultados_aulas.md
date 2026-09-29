
lab 1

Explicação das lacunas preenchidas:TODO 1.1 (List Comprehension):[token for token in tokens if token not in stopwords]Itera sobre os tokens e mantém apenas os termos que não estão presente na lista de stopword
TODO 1.2 (Fit e Transform):vectorizer.fit_transform(X_treino_limpo)Aprende os termos do vocabulário e gera a matriz TF-IDF de treino em uma única chamada.
TODO 1.3 (Ternário para RegEx):float(match.group(1)) if match else NoneCaptura o valor numérico (grupo 1 da expressão regular) e o converte para float caso haja correspondência (match), retornando None se o padrão não for encontrado.
TODO 1.4a & 1.4b (Probabilidades com NumPy):maior_confianca = np.max(probas) — busca o maior valor probabilístico atribuído pelo modelo.intencao_prevista = modelo.classes_[np.argmax(probas)] — obtém a classe do Scikit-Learn correspondente ao índice da maior probabilidade (argmax).
TODO 1.5 (Validação de Threshold e Escopo):Garante que mensagens com confiança abaixo de $55\%$ ou classificadas como fora_escopo caiam na regra de tratamento de fallback da NLU.

lab 2

TODO 2.1 (Remoção de Stopwords):
[token for token in tokens if token not in stopwords]
List comprehension equivalente ao LAB 1 para remover termos irrelevantes da mensagem.

TODO 2.2 (Instanciação do Modelo):
modelo_nb = MultinomialNB()
Cria a instância do classificador Multinomial Naive Bayes, muito eficiente para contagem de termos e dados categorizados via TF-IDF.

TODO 2.3 (Treinamento do Modelo):
modelo_nb.fit(X_vetorizado, y_treino)
Aplica o algoritmo de aprendizagem com base na matriz TF-IDF e os rótulos do dataset.

TODO 2.4 (Extração e Normalização de Protocolo):
match.group(0).upper() if match else None
Obtém a sequência de texto casada pela RegEx (ex: inc-9982) e a converte para caixa alta (INC-9982). Retorna None se a mensagem não tiver um padrão de protocolo válido.

TODO 2.5 (Verificação de Regras de Negócio):
Aplica o limite probabilístico (threshold=0.60) e filtra mensagens fora de escopo para determinar se o chamado entra no fluxo de fallback ou de sucesso.

lab 3

TODO 3.1 (Remoção de Stopwords):
[token for token in tokens if token not in stopwords]
Filtra a lista de tokens removendo as palavras definidas na lista stopwords.

TODO 3.2 (Instanciação da Árvore de Decisão):
modelo_tree = DecisionTreeClassifier()
Cria a instância do classificador DecisionTreeClassifier, responsável por dividir o espaço de termos em nós de decisão baseados em métricas como Gini ou Entropia.

TODO 3.3 (Treinamento do Modelo):
modelo_tree.fit(X_vetorizado, y_treino)
Realiza o ajuste da Árvore de Decisão associando a matriz de feições TF-IDF aos rótulos das intenções de e-commerce.

TODO 3.4 (Regex para Código de Rastreio):
match.group(0).upper() if match else None
Capta o padrão do código de rastreamento (duas letras BR seguidas por 9 dígitos) e o padroniza em letras maiúsculas. Retorna None se a entrada não contiver o código.

TODO 3.5 (Tratamento do Pipeline NLU):
Aplica a regra de corte usando a probabilidade (pureza da folha atingida) e redireciona mensagens com baixa confiança ou classificadas como fora_escopo para o fallback.
