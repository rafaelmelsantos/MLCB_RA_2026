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

