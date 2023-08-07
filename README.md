# Desafio Numera - Clusterização de Clientes - Gelateria Lillo

##Glauco Pavanelli Zanella

## Introdução
A gelateria Lillo é muito famosa na capital mineira e vende gelatos de altíssima qualidade com foco no público de classe B+. Quando um cliente compra algum produto, é incentivado que ele preencha seu cpf, email e telefone para receber promoções e novidades. Com esses dados, a gelateria possui uma base de clientes robusta.

A gerente da gelateria pediu a nossa ajuda para melhorar as campanhas de marketing e aumentar a receita. Para isso, ela disponibilizou 3 bases com as seguintes informações:

### Dicionário de Variáveis

**Portfolio_ofertas:** contém as ofertas que são enviadas e possui as seguintes colunas:

· ID: código de identificação da oferta

· Oferta: Tipo de oferta enviada, podendo ser informativo, desconto e compre 1 e leve 2.

· Canal: canal de envio da comunicação podendo ser email, web, celular e redes sociais.

· Valor mínimo: valor mínimo necessário a ser gasto para aproveitar a oferta

· Recompensa: pontuação obtida por completar a compra da oferta

· Duração: tempo de duração da oferta em dias.

**Dados_clientes:** dados demográficos dos clientes e possui as seguintes colunas:

· Gênero: gênero do cliente (F: Feminino, M: Masculino, O: Outro)

· Idade: idade dos clientes

· Id: código único de cada cliente

· Membro_desde: data em que o cliente criou uma conta

· Renda_anual: renda anual fornecida pelo cliente.

**Eventos_ofertas:** base com registros de todos os eventos

· Tipo_evento: descrição dos ofentos ocorridos, podendo ser: transação, oferta recebida, oferta vista, oferta finalizada.

· Cliente: código do cliente que executou aquele evento

· Tempo_decorrido: tempo em horas desde o envio da oferta

· Valor: contém informação do valor gasto na compra

· id_oferta: código da oferta


## Objetivo Geral

Criar um relatório com a recomendação de segmentação de clientes e sugestão de estratégia de venda/promoção adequada para cada segmento identificado.

## Objetivos Específicos

**Passo 1: Entendimento do Problema e Objetivos** - Compreender detalhadamente os desafios enfrentados pela gelateria e os objetivos do projeto. Definir claramente as metas, como aumento de receita e melhoria das campanhas de marketing.

**Passo 2: Coleta e Análise dos Dados** - Baixar as três bases de dados: Portfolio_ofertas, Dados_clientes e Eventos_ofertas.
Realizar a análise exploratória dos dados para identificar padrões, tendências e insights iniciais.
Verificar a qualidade dos dados, tratando valores ausentes, outliers e inconsistências.

**Passo 3: Segmentação de Clientes** - Utilizar técnicas de segmentação, como clustering, para agrupar os clientes com base em características demográficas e comportamentais. Aplicar algoritmos de clusterização, como K-means, para criar segmentos de clientes.

**Passo 4: Análise e Interpretação dos Segmentos** - Analisar as características dos diferentes segmentos identificados.
Identificar padrões de comportamento, preferências e hábitos de compra em cada segmento. Compreender como esses segmentos se relacionam com as ofertas, canais de comunicação e recompensas.

**Passo 5: Estratégias de Vendas/Promoção** - Com base na análise dos segmentos, criar estratégias de venda/promoção específicas para cada grupo. Recomendar tipos de ofertas, canais de comunicação e recompensas que melhor se adequem a cada segmento. Priorizar ofertas que tenham maior probabilidade de ressonância com cada segmento.

**Passo 6: Desenvolvimento do Relatório** - Criar um relatório detalhado que descreva todo o processo, desde a coleta de dados até as estratégias de venda/promoção. Incluir visualizações gráficas, tabelas e insights principais. Apresentar os segmentos identificados, suas características e as estratégias recomendadas para cada um.

**Passo 7: Desenvolvimento do Script de Análise** - Escrever um script utilizando uma ferramenta de análise de dados. Organizar o código de forma clara e estruturada. Documentar as etapas do processo, funções e algoritmos utilizados.

**Passo 8: Testes e Validação** - Realizar testes para garantir que as estratégias recomendadas façam sentido e se alinhem aos objetivos da gelateria. Validar as recomendações com base em dados históricos, se disponíveis, ou por meio de simulações.

### Definição da transformação dos dados de idade dos Clientes

- Podemos verificar que existem registros de clientes acima de 100 anos, porém devido a analise por boxplot podemos verificar que o limite superior é de 115 anos, adotando assim 118 anos como outliers.
- Existem 2175 registros de clientes com idade de 118 anos, o que corresponde a 12,8% dos clientes na base de dados.
- É possível que os clientes que não possuem dados de gênero e renda anual sejam exatamente aqueles que possuam a idade mencionada (118 anos). Caso essa suposição seja válida, a abordagem inicial de remover os outliers da base poderia ser considerada, entretanto, é essencial notar que esses clientes também fornecem informações cruciais para a análise, como a data de adesão ao programa de fidelidade e outras possíveis insights que possam surgir.
- Para preservar as características significativas desses clientes, optaremos por substituir o valor de 118 anos pela mediana da distribuição. Ao analisar a distribuição das idades, percebemos que utilizar a média resultaria em um deslocamento da distribuição para a direita.

### Abordagem para o tratamento de dados faltantes na coluna gênero

Para a coluna gênero vamos adotar a seguinte estratégia:
- Vamos substituir os valores faltantes por 'O' (Outro), partindo da premissa que uma vez que a pessoa não preencheu esta não gostaria de informar seu gênero.

### Abordagem para o tratamento de dados faltantes na coluna renda_anual

Para a coluna 'renda_anual' vamos adotar a seguinte estratégia:
- Vamos substituir os valores faltantes pela mediana da distribuição, partindo da premissa que utilizando a mediana não estaremos deslocando o comportamento da distibuição em relação a mediana.

### Considerações em relação ao comportamento de cadastro dos clientes da Gelateria

De acordo com a USP [Link](http://www.estacao.iag.usp.br/seasons/index.php#:~:text=Ver%C3%A3o%3A%20Dezembro%2C%20Janeiro%20e%20Fevereiro%20(DJF)), os meses que faz mais calor são os meses da Primavera e Verão.
- Primavera: Setembro, Outubro e Novembro
- Verão: Dezembro, Janeiro e Fevereiro
- Outono: Março, Abril, Maio
- Inverno: Junho, Julho e Agosto

Porém, podemos concluir que nos anos de 2015 e 2017 houve uma diferença na quantidade de clientes cadastrados nos meses mais quentes do final de ano em relação ao outros anos, onde houve um cadastro de clientes aparentemente variando pouco de um mês para outro.

### Entendendo a Base de Dados de Ofertas

- Para a Oferta Compre 1 e Leve 2 os canais de marketing mais utilizados são Email e Celular.
- Para a Oferta de Desconto os canais de marketing mais utilizado são Internet e Email.
- E Para a divulgação de Informativos os canais mais utilizados são email e celular.

### Entendendo a Base de Dados de Eventos

Podemos notar que os eventos ocorrem de três maneiras distintas:

- O cliente recebe a oferta e a utiliza para efetuar uma compra;
- O cliente recebe a oferta, mas não a utiliza e consequentemente não realiza uma compra;
- O cliente não recebe a oferta, mas ainda assim efetua uma compra.


### Entendendo a Problemática

Precisamos encontrar uma maneira de determinar a eficácia de diferentes ofertas para cada cliente. Essa análise é viável devido à ordem cronológica dos eventos registrados. Quando consideramos uma oferta como eficaz (ou seja, o cliente a usou para realizar uma compra), os eventos que levam o cliente a converter a oferta em uma compra podem ocorrer de duas formas:

1. Recebimento da oferta -> Visualização da oferta -> Transação -> Conclusão da oferta (aqui tratamos ofertas de cupom e desconto);

2. Recebimento da oferta -> Visualização da oferta -> Transação (aqui tratamos ofertas informativas, onde as transações devem ocorrer durante o período da oferta)

Apenas quando essas duas sequências de eventos de conversão são observadas, consideramos a oferta como eficaz.

Além disso, existem cenários que caracterizam ofertas ineficazes:

- Oferta recebida, mas nenhum evento subsequente ocorre (a oferta não é visualizada nem utilizada);
- Recebimento da oferta -> Transação -> Visualização da oferta (nesse caso, o cliente não usou a oferta na transação, comprando antes de vê-la);
- Transação sem oferta (clientes desse tipo realizam transações independentemente de ofertas, tornando menos vantajoso enviar ofertas a eles do ponto de vista financeiro da empresa).

## Metodologia

### Clusterização e Segmentação dos Clientes de acordo com os Eventos relacionados e Ofertas definidas

Foi utlizado o método KMeans da biblioteca ScikitLearn para realizar a segmentação ded clientes da Gelateria Lillo.
O Comportamento do Aprendizado de M´quina pode ser observado no Jupyter Notebook 'Desafio_Numera_Gelateria_Lillo.ipynb'

## Conclusão

- Podemos concluir que o K-means realizou a Clusterização de acordo com a Renda Anual dos Clientes para o número ideal de cluster. Portanto a partir da segmentação dos clientes podemos promover as estratégias de Marketing para a Gelateria Lillo.
- Em trabalhos futuros podemos avaliar a Engenharia de Recursos para poder segmentar de maneira mais acertiva de acordo com as compras realziadas pelos clientes, e poder aumentar a efetividade das promoções enviadas para os clientes.
- De acordo com a FGV, conforme mencionado anteriormente, a Gelateria Lillo precisa rever seu publico alvo, uma vez que a Classe economica predominante não foi a Classe B+ como exposta no enunciado do problema.