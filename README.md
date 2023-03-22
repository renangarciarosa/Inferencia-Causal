# Introdução à Inferência Causal

Neste repositório veremos brevemente o que é inferência causal, sua importância, alguns métodos de inferência utilizados e o que são.

## Introdução

Correlação não implica em causalidade. Todo cientista de dados em algum momente já ouviu essa afirmação. Inferência Causal (CI) ou Causalidade é o processo de determinar o efeito de causa e efeito em um sistema, é um método estatístico usualmente usado na econometria e ciências comportamentais para entender as causas por trás dos resultados que vêmos nos experimentos e obersavções.

CI consiste numa família de métodos que buscam respondem o “porquê” das coisas acontecerem. Os métodos comuns como análise de regressão se preocupam em quantificar correlações, como mudanças em X estão associadas em mudanças em Y. Já os métodos de CI buscam determinar SE mudanças em X causam mudanças em Y. As abordagens de CI buscam responder perguntas do tipo “por quê” Y muda. Se X está causalmente relacionado com Y, então a mudança de Y pode ser explicada em termos da mudança de X.

Essa família de métodos de causalidade é relativamente nova e está em desenvolvimento, já que os pesquisadores não costumavam ter redes formais de relações causais. Mas isso mudou na segunda metade do século XX graças ao trabalho de pioneiros como Donald Rubin e Judea Pearl.

## A Importância da Causalidade

Cientistas de dados precisam entender o porquê das coisas, para evitar perdas e/ou apontar possíveis ações. Sabendo o porquê das coisas é possível tornar insights de usuários em ações para atingir objetivos da organização, por exemplo.

Em contexto de negócio, CI pode nos ajudar fornecendo insights para melhorar a experiência de usuários e sobre venda de produtos e serviços identificando pontos que podem causar problemas como churn, devoluções, propensão de compra, etc. Com esse tipo de informação podemos tomar melhores decisões de negócio a partir da desse melhor entendimento sobre o impacto de ações. A CI permite que cientistas de dados respondam perguntas causais com bases de dados observacionais, principalmente quando não é possível realizar testes A/B.

## Métodos
Inferência Causal é uma família bem ampla de métodos, e podem ser divididos em duas categorias de métodos a partir do seu uso com dados: experimentais e dados observacionais. Esses métodos são mutualmente exclusivos e em muitos problemas podem ser usados mais de um método da mesma categoria. Aqui, falaremos exclusivamente dos métodos para dados observacionais.

O método “gold standart” para estabelecer causalidade é através de testes A/B, de experimentos controlados. Neles, criamos variações em que a única diferenca é o fator em que estamos testando e em unidades selecionadas aleatóriamente. Caso observemos diferentes resultados em diferentes unidades dos grupos, então podemos concluir que o tratamento tem efeito causal no resultado. Mas vezes não é possível fazer testes controlados para mensurar causalidade simplesmente porquê não é possível, viável econômicamente ou ético.

![image](https://user-images.githubusercontent.com/89540415/226983670-a3d8aa09-185a-425a-94e6-4f44187649b8.png)

Para que o um usuário não seja impactado negativamente com os efeitos do experimento, o impacto causal pode ser estimado a partir desses dados observacionais. Por exemplo, em um delivery, para saber como um evento como o atraso da entrega do pedido influencia o envolvimento do cliente com o app ou plataforma. Nesse caso atrasar as entregas de propósito afetaria negativamente o usuário, então é preciso utilizar outra abordagem para estimar o impacto causal desses atrasos.

A partir dos dados observacionais de usuários que tiveram sua entrega atrasada e usuários que não tiveram, podemos começar a entender o impacto da entrega sem utilizar de experimentação. Mas simplesmente comparar a diferença os dois grupos de usuários não dará respostas significativas.

Simplesmente comparar os dois grupos pode nos levar a conclusões equivocadas como a de que quanto mais entregas atrasadas, mais os usuários fazem pedidos. Provavelmente porquê nesse cenário simplificado quem tem mais entregas atrasadas é justamente quem faz mais pedidos.

![image](https://user-images.githubusercontent.com/89540415/226983777-4025d8b1-a30c-4c92-8191-753e45c7aeeb.png)

Neste gráfico acima, o número de pedidos é uma [variável de confusão](https://pt.wikipedia.org/wiki/Vari%C3%A1vel_de_confus%C3%A3o), afetando tanto a variável dependente quanto a independente. Na prática os dados podem ter várias variáveis dependentes, independentes e de confusão. Determinar quais variáveis devem ou não ser controladas é um desafio para análise de inferência causal e deve ter uma colaboração próxima entre cientista de dados com quem domínia do conhecimento do negócio. Após determinar quais variáveis devem ser incluídas, existem várias formas de realizar a modelagem causal.

Num contexto da saúde pública, pelo mesmo motivo não podemos simplesmente comparar pessoas que receberam uma dose de vacina para previnir doenças contra quem não se vacinou, já que não foram selecionados aleatoriamente, assim vai existir um viés de seleção

![image](https://user-images.githubusercontent.com/89540415/226987633-c5a71cb9-75ca-4b2c-9e4e-4b5a955de8b3.png)

![image](https://user-images.githubusercontent.com/89540415/226987712-e8138fb7-df86-4fe5-a41c-b9a07289a169.png)

Notação:

* Di: tratamento (1) ou não tratado (0)
* Yi: resultado observado
* Y1i: resultado potencial do grupo de tratamento
* Y01: resultado potencial do grupo de controle

Aqui, o primeiro termo é resultado real das pessoas que sabemos que receberam a dose. E o segundo termo é resultado potencial das mesmas pessoas (“clones”) se não tivessem recebido a dose, que é um resultado [contrafactual](https://pt.wikipedia.org/wiki/Contrafatual) que não podemos observar

![image](https://user-images.githubusercontent.com/89540415/226988954-7e8b2c36-28d6-4ab4-b2ce-b0d105039e2d.png)

O segundo termo é o resultado das pessoas sabemos que não receberam a dose, mas aqueles que receberam poderiam ter um resultado diferente mesmo sem ela.

Pessoas com problemas de saúde e de maior poder aquisitivo tem mais chances de ter mais cuidados com a saúde. Se vermos diferenças entre os esses dois grupos de pessoas que tomam uma vacina e as que não, pode ser resultado da vacinação ou das variáveis de confusão (confounders) que impactam ambos, o tratamento e o resultado. Para ter uma visão mais clara sobre os causalidade precisamos desenhar [direct acyclic graphs-DAGs](https://en.wikipedia.org/wiki/Directed_acyclic_graph) para o problema, usando os nós como representação das variáveis aleatórias e as setas como como conexões causais.

![image](https://user-images.githubusercontent.com/89540415/226989493-31a350c1-0bc4-4b91-9be0-a9cd8aace364.png)

Para inferir causalidade em dados observacionais podemos utilizar métodos como de controle estatístico, contrafactuais e experimentos naturais.

## Controle Estatístico
Com o controle estatístico a ideia é manter os confounders constantes e variar o tratamento, se o resultado mudar, então podemos ter mais confiança de que o tratamento surtiu efeito. Dois métodos comuns são regressão e matching.

### Regressão
Para regredir todos os confounders relevantes podemos incluir no mesmo modelo de tratamento, como:

infection_rate ~ got_booster + age + social ecom status + health…

Depois de treinar o modelo nos dados, podemos extrair o slope parcial do tratamento (got_booster). O slope mostra, com todo o resto constante, quanto receber uma dose mudaria a taxa de infecção de uma pessoa em comparação com não receber. Um slope horizontal (beta = 0) indicaria nenhum efeito, beta < 0 indicaria que as taxas de infecção foram reduzidas e se por acaso o beta fosse maior que zero, indicaria um aumento.

Mas uma possível modelagem incorreta trás muitos riscos, como não controlar as coisas certas no caso de não incluir confounders no modelo caso não tenha domínio do negócio. Ou ignorar as formas funcionais ou estruturas causais de como as variáveis se conectam. Regressão linear só pode controlar confounders que tem relações lineares com o tratamento e o resultado, se você conhece a forma funcional do confounder então você pode transforma-lo. Mas muitas vezes não conhecemos a forma então não podemos assumir que a regressão os pode controlar. Também podem ocorrer problemas em relação a estrutura causal em relação aos confounders, como não reconhecer e modelar colliders, variáveis influenciadas por duas simultaneamente ( X → Z ←Y), e mediators, um evento entre a causa e o efeito ( X → Z →Y).

### Matching
Matching pode ajudar sobre a questão das formas funcionais que desconhecemos. A ideia por trás dela encontrar é tratados e não tratados que sejam parecidos nos dados observacionais. Assumindo que os dois grupos se diferem apenas se receberam o tratamento ou não, podemos atribuir o resultado ao tratamento. Existem métodos de exact matching e Propensity Score Matching (PSM).

Em exact matching procuramos por tratados e não tratados que possuem exatamente os mesmos valores que queremos controlar. Os benefícios ele é a simplicidade e transparência, diminuindo a incerteza dos modelos preditivos. Mas possui a necessidade de combinar todas as variáveis de controle e podendo não possuir correspondentes em pequenos datasets.

![image](https://user-images.githubusercontent.com/89540415/226992069-1ecddf2f-6d47-4298-abc2-4e43b84f83b5.png)

No Propensity Score Matching (PSM) assumimos a lógica do matching para prever a probabilidade de cada unidade receber o tratamento. Essa probabilidade é o propensity score, que usamos pra combinar os tratados e não tratados. Nela, não temos temos o problema de não combinação de algumas variáveis como ocorre exact matching devido a combinação a partir da probabilidade de receber o tratamento. Mas alguns modelos podem nos levar a combinações erradas ou enganosas.

### Contrafactuais
Para usarmos regressão ou matching precisamos de várias unidades tratadas e não tratada spara comparar o resultado. Mas é difícil mensurar o impacto causal para certos eventos em que não possuímos unidades não tratadas, como eleições, políticas públicas ou a recente pandemia através de controle estatístico.

Nesses casos geralmente são usados estudos de caso comparativos, como comparar diferentes estados diante de um evento (ex. políticas públicas) em que ocorreu em um deles.

Métodos que seguem as teorias da causalidade contrafactual como difference-in-difference (DD) e synthetic control põem a em prática a ideia de que X causa Y, então caso X não ocorra então Y não poderia ocorrer. Ambos usam um cenário em que a unidade não foi tratada. Se o tratamento não tivesse acontecido, o resultado contrafactual nesse cenário alternativo seria o mesmo do cenário real, caso sejam diferentes então temos evidências de que o tratamento possui um impacto causal.

### Difference-in-Differences (DD)
Antes da implantação das várias reações que podem ser feitas nos posts do Facebook, só era possível interagir com as publicações na forma de likes , comentarios, compartilhamentos. Mas algumas em algumas situações é meio inopropriado dar likes como no falecimento de alguem. Então os cientistas de dados da Meta criaram a hipótese de que o engajemento nos posts aumentariam caso fosse possível reagir além dos likes. E não é possível inferir com testes A/B já que os os grupos se influenciariam, se um usuário do grupo de tratamento reagisse a um post de um usuário do grupo de controle, o segundo não poderia vê-lo ou interagir de volta.

No geral, esse tipo de atualização em redes sociais é bem comum, sendo primeiro disponibilizado em algumas regiões e depois dos testes acabam sendo implementados para todos os usuários ou não. Para evitar a influência e contaminação dos resultados da experiência, são feitos testes com regiões diferentes. Foram disponibilizados essa nova funcionalidade de reações para o Canadá (tratamento) mas não para os EUA (controle) e foi mensurado o número de posts reagidos, incluindo os likes, por usuários antes e depois da intervenção.

![image](https://user-images.githubusercontent.com/89540415/226992448-44cb4c8a-73f7-48b4-9963-1eb759fbd8f0.png)

Para medir o efeito do tratamento precisamos assumir que o resultado seguirá a mesma tendência em diferentes regiões caso não houvece intervenção no grupo de tratamento (contrafactual). Esse resultado contrafactual foi representado pela linha pontinhada, e sendo o resultado atual maior que o contrafactual, podemos assumir que as reações provocaram um aumento no engajamento.

![image](https://user-images.githubusercontent.com/89540415/226992805-414a0c2c-a348-44aa-8c8b-86e38d6562d3.png)

Seguindo a lógica de que a tendência em comum seria a mesma, então se o número aumentasse 0.7 nos EUA, então também aumentaria 0.7 no Canadá. Mas o resultado foi de +1.5 no canadá e a diferença de 0.8 é o efeito do tratamento da intervenção. Além disso, um usuário médio dos EUA reagiu a 0.7 posts a mais comparando com o usuário médio canadense antes do lançamento, então devemíramos ver a mesma tendência após o lançamento da nova função, mas o que ocorreu foi que o usuário médio dos EUA reagiu a 0.1 posts a menos que o usuário médio do Canadá.

Caso a premissa de tendência comum não aconteça, a análise acima é inválida. MAs uma forma de checar é usar a unidade (Dtratado = 1: Canadá e Dtratment = 0: EUA), as covariáveis relevantes X para os resultados e sua interação (uma interação significa que a mesma covarivável impact as unidades de forma diferente) para predizer o resultado

![image](https://user-images.githubusercontent.com/89540415/226992914-7e15225b-f4d4-4509-be92-1cca8f4fc20e.png)

Caso as tendências já forem diferentes antes do lançamento podemos usar o matching para selecionar as unidades não tratadas vs tratadas. Se espera que as unidades combinadas sejam mais propensas a compartilhar uma tendência em comum. Nos casos em que não é possível fazer essa suposição, então podemos usar métodos como synthetic control ou CausalImpact para explicitamente modelar as tendências através do tempo.

### Synthetic Control
Para podermos estimar o efeito de tratamento com synthetic control precisamos construir um grupo de tratamento ou unidade que se pareça com com o mesmo antes do tratamento. Então podemos ver como essa unidade se comporta depois da intervenção. A diferença entre a unidade criada (sintética) e a unidade que ele imita é o efeito de tratamento.

As unidades sintéticas são criadas a partir da escolha do donor pool e escolha do peso de cada unidade. Para escolher o grupo de tratamento, precisamos utilizar matching para achar J unidades não tratadas com características similares.

## Experimentos naturais
Experimentos naturais se referem a eventos que únicos.

### Regression Discontinuity Design (RDD)
Em um delivery, entregas que atrasam muitas vezes são um problema e podem causar churn. A Doordash automaticamente faz a devolução de pedidos que demorem 30 minutos ou mais. Agora, como essa política impacta o livetime value (LTV) ? Nesse caso não podemos selecionar aleatoriamente clientes e também não podemos comparar o LTV entre quem recebeu ou não o reembolso, porquê o atraso médio é diferente entre os dois.

![image](https://user-images.githubusercontent.com/89540415/226995327-5224e188-2e00-472e-971f-eedc6046c237.png)

Em vez de compararmos todos os clientes que não receberam e os que receberam, podemos comparar aqueles em torno do ponto de corte para o reembolso, que é 30 minutos. Esse método é chamado de regression discontinuity design (RDD).

![image](https://user-images.githubusercontent.com/89540415/226995387-c757ed8a-b97c-4b11-9cc5-ba3a69783169.png)

Precisamos fazer duas suposições:

* Continuidade: Sem nenhum motivo, o resultado deve mudar de forma contínua e suave com a “running variable”, como nesse caso atraso do pedido.
* Aleatoriedade: A atribuição dos usuários “near-winners” (A) e “near-loosers” (B) é tão boa quanto aleatória, este é o experimento natural.

As duas premissas são razoáveis nesse caso de reembolso, então a descontinuidade pode ser atribuída ao tratamento.

Na prática existem complicações como o ponte de corte nem sempre ser determinístico, fazendo a descontinuidade ser menos suave.

* Determinístico: Pedidos com atraso acima de 30 minutos sempre irão receber o reembolso e aqueles abaixo desse ponto de corte não.
* Probabilístico: Admissão baseado em por meio de testes padronizados como o SAT, mas estudantes abaixo de ponto de corte ainda podem ingressar a partir de programas especiais

O “salto” depois do corte pode não ser significativo, nesse caso, nesse caso podemos usar a running variable e o tratamento (D =1: tratado; D=0: controle) para predizer o resultado, y = f(X) + βD + ϵ, e verificar se o β é estatísticamente significativo.

Em outros casos o relacionamento entre a running variable e o resultado pode não ser linear, nesse caso é mais difícil identificar o salto.

## Instrumental Variables (IVs)
Muitos confounders podem afetar um resultado como a renda de alguem e fazer uma inferência causal é difícil. Mas nos EUA, o sistema educacional criou um experimento natural: As crianças são obrigadas a entrar na escola no ano calendário em que fazem 6 anos de idade, mas podem sair assim que completam 16 anos. Nesse cenário podem existir Alice e Bob.

* Nascimento: Alice nasceu em 1º de janeiro de 2006; Bob nasceu em 31 de dezembro de 2006
* Início escolar: Ambos seriam obrigados a ir à escola em 1º de setembro de 2012
* Abandono: Mas Alice poderá sair em 1º de janeiro de 2022, enquanto Bob terá que ficar até 31 de dezembro de 2022, estudando 1 ano a mais apesar de ter mesma idade.

![image](https://user-images.githubusercontent.com/89540415/226995771-4affa96f-cd2b-4033-8743-bb6096d74092.png)

O período de nascimento não é uma variável de confusão, como riqueza familiar e região em que se nasce, mas tem um efeito causal no tratamento anos de escolaridade, e esse poderia afetar a renda.

Podemos usar o nascimento como um “instrumento” para estimar o efeito causal da escolaridade na renda. Primeiro precisamos regredir os anos de estudo no período de nascimento, X^=αIV. Então regredimos renda na regressão não enviesada de escolaridade obtida no primeiro passo, Ŷ = BX^. Esse método é chamao de “two-stage least-squares”. O coeficiente que conseguimos no segundo passo é o efeito causal da escolaridade na renda. A estimativa de IV nos permite fazer inferência causal na presença de confunders, em vez de regredí-los e causar estragos sem o nosso conhecimento.

Para considerar-mos um instrumento bom, devemos atribuir aleatoriamente às unidades, afetando causalmente o tratamento e correlacionando com o resultado, mas não correlacionando com qualquer confounder. Mesmo com muito conhecimento é difícil encontrar variáveis instrumentais que se encaixem no problema.

# Conclusão
Inferência Causal é uma área nova e que tem ganhado bastante interesse especificamente em data science. Sendo uma área ampla e com diversas aplicações, assim como machine learning, o seu uso pode trazer diversas vantagens competitivas para o negócio e seu domínio ser um diferencial para o cientista de dados.

