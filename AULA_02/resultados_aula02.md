--- RESULTADOS DO LAB 01 ---
Mensagem: 'Quero consultar quanto dinheiro tenho' ==> Intenção Predita: [fazer_pix]
Mensagem: 'Pode me ajudar a fazer um pix?' ==> Intenção Predita: [fazer_pix]
Mensagem: 'Gostaria de cancelar meu cartão de crédito' ==> Intenção Predita: [cancelar_conta]

 1 - Avaliem os resultados e verifiquem se os resultados foram corretos ou incorretos. Coloque a resposta no arquivo do relatório do laboratório

RESULTADOS INCORRETOS

mensagem: 'Quero consultar quanto dinheiro tenho' ==> Intenção Predita: [fazer_pix]

RESULTADO ESPERADO

mensagem: 'Quero consultar quanto dinheiro tenho' ==> Intenção Predita: [consultar_saldo]

 2 - Detectado algum erro, qual seria a maneira mais correta de melhorar o resultado do algoritmo?

recolocaria a frase incorreta em DADOS-mensagem
avaliaria a mensagem em questão como em DADOS-intencao ('consultar_saldo')

 3 - Detalhe a função do LogisticRegression no algorítmo.

ele transforma os resultados em 0 ou 1 / sim ou não.


--- RESULTADOS DO LAB 02 ---
Mensagem de Teste: 'Gostaria de devolver o produto que comprei'
Intenção Predita: troca_devolucao

--- Distribuição de Probabilidades por Classe ---
Classe [duvida_frete]: 27.99%
Classe [rastrear_pedido]: 24.54%
Classe [troca_devolucao]: 47.46%

 1 - Avaliem os resultados e verifiquem se os resultados foram corretos ou incorretos. Coloque a resposta no arquivo do relatório do laboratório

resultado foram corretos.

 2 - Detectado algum erro, qual seria a maneira mais correta de melhorar o resultado do algoritmo?

não houve erro.

 3 - Detalhe a função do Naive Bayes no algorítmo.

o algorítmo detalha qual a resposta certa dado a pergunta, ela estima com base em uma porcentagem.

--- RESULTADOS DO LAB 03 ---

#========== PRODUÇÃO DO RELATÓRIO:==============

1 - Qual foi a acurácia obtida pelo modelo no conjunto de teste e por que, em um dataset tão pequeno (9 exemplos), essa métrica pode ser enganosa?

acuracia de modelo: 33.33%

2 - Como o modelo de Árvore de Decisão (DecisionTreeClassifier) toma a decisão de separar as intenções do usuário?

O modelo utiliza a representação vetorial do CountVectorizer (frequência de palavras) e busca as palavras mais decisivas para dividir o dataset.

3 - Qual é o risco de utilizar uma Árvore de Decisão sem limite de profundidade (max_depth) em datasets de texto maiores?

Em datasets de texto maiores, o número de palavras únicas no vocabulário explode. Sem o parâmetro max_depth, a árvore cresce até memorizar ruídos, regras extremamente específicas e palavras raras do treino.

--- RESULTADOS DO LAB 04 ---

#========== PRODUÇÃO DO RELATÓRIO:==============


1. Descrição do Experimento
Desenvolvimento de um protótipo de classificação de intenções (NLU) utilizando a biblioteca Scikit-Learn. O dataset contém 15 frases divididas igualmente entre 3 intenções operacionais: `comprar_passagem`, `cancelar_reserva` e `falar_atendente`.

2. Justificativa Técnica
* **TfidfVectorizer:** Selecionado no lugar do `CountVectorizer` por penalizar termos genéricos de alta frequência (como preposições e artigos) e dar mais destaque a palavras com alto poder de diferenciação semântica (ex: "passagem", "anular", "humano").
* **LogisticRegression:** Escolhido por ser um algoritmo eficiente para classificação de texto em datasets menores, garantindo boa capacidade de generalização com baixo risco de overfitting.

3. Predição em Frases Inéditas
O modelo avaliou 3 frases totalmente inéditas (fora do conjunto de treino) e obteve os seguintes resultados:
1. *"Quero comprar uma passagem barata para Buenos Aires"* → **comprar_passagem**
2. *"Preciso anular meu bilhete de voo de amanhã"* → **cancelar_reserva**
3. *"Por favor me passe para um suporte humano"* → **falar_atendente**
