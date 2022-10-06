# King County Houses - Insight Project


## Conhecendo o Negócio:

A House Rocket é uma empresa fictícia do ramo imobiliário que tem como principal meio de lucro a compra de casas em boas condições à preços mais baixos para revendas futuras a preços mais elevados. O objetivo deste projeto é utilizar análise de dados para maximixar o lucro obtido através das melhores oportunidades de negócio.

#### Acesse o Link e faça sua própria análise:
<  https://wesleymartins95-house-rocket-streamlit-app-8u2lcd.streamlitapp.com/>

(*aplicação web para visualização dos dados, contém : gráficos,mapas e análise descritiva*.)
________________________________________________________________________________________________

## 1. Questão de negócio

Aumentar o lucro da empresa através de análise dos dados, encontrando as melhores oportunidades de compra de imóveis com preços baixos e com qualidade para revenda.

Perguntas a serem respondidas:

1.Quais são os imóveis que a House Rocket deveria comprar e por qual preço?

2.Uma vez o imóvel comprado, qual o melhor momento para vendê-lo e por qual preço?

## 1.1. Entendendo os dados

A base de dados é referente a vendas realizadas entre Maio de 2014 e Maio de 2015 no Condado de King em Washington.


| Atributo    |    Definição      |
|-----|----------|
| id    | Número de identificação único de casa imóvel.         |
| date    | 	Data de venda do imóvel |
|  price   | 	Preço de venda do imóvel |
|  bedrooms   | 	Número de quartos |
|   bathrooms  | Número de banheiros         |
| sqft_living    | 	Área interna do imóvel em pés quadrados |
| sqft_lot    |	Área do lote em pés quadrados|
|floors|	Número de andares|
|waterfront|Indica se o imóvel tem vista para água|
|view|Índice de 0 a 4 para qualidade da vista da propriedade |
|condition|	Índice de 1 a 5 sobre a condição do apartamento|
|grade|	Índice de 1 a 13 que representa o nível de qualidade da construção e design|
|sqft_above|	Espaço interno em pés quadrados que está acima do nível do solo|
|sqft_basement|	Espaço interno em pés quadrados que está abaixo do nível do solo|
|yr_built|Ano de construção do imóvel|
|yr_renovated|	Ano da última renovação do imóvel|
|zipcode|código postal|
|lat|latitude	|
|long|longitude|
|sqft_living15|Área interior em pés quadrados dos 15 imóveis vizinhos|
|yr_renovated|sqft_lot15	Área do lote em pés quadrados dos 15 imóveis vizinhos|

## 1.2. Novas Features
Essas colunas foram criadas para a base de dados original.

| Feature |    Definição      |
|-----|----------|
|year|Ano extraído da data	|
|month| Mês extraído da data|
|day| Dia extraído da data	|
|season|Época do ano|
|m²|Conversão de "sqft_lot" para m²	|
|price/m²|Preço de m²|
|city|Cidade recolhida via API a partir de lat e long|
|basement|Quer o imóvel tenha ou não porão|
|renovated|Quer a propriedade tenha sido renovada ou não|


## 2. Premissas de negócio

- 1.0 banheiro contém uma pia, um toalete, um chuveiro e uma banheira, valores flutuantes representam banheiros que não contém todos os elementos.
- A classificação da coluna view foi definida como: 0 = sem vista, 1 = regular, 2 = média, 3 = boa e 4 = excelente.
- A classificação da coluna condition foi definida como: 1 = muito ruim, 2 = ruim, 3 = média, 4 = boa, 5 = muito boa.
- A classificação da coluna grade foi definida como: 1-3 = muito baixa, 4-6 = baixa, 7 = média, 8-10 = alta, 11-13 = muito alta.
- Os valores iguais a 0 na coluna yr_renovated são casas que nunca foram reformadas.
- O imóvel com 33 quartos foi considerado um erro de digitação e removido do dataset.
- Localização e condição do imóvel são os principais fatores na valorização e desvalorização dos imóveis, sendo características decisivas na escolha de imóveis.
- A sazonalidade tem grande impacto no mercado imobiliário, onde as estações mais quentes apresentam maiores preços.

## 3. Planejamento da solução
O planejamento foi dividido em três etapas:

### 3.1. Produto Final
- Relátorio com os imóveis a serem comprados.  
- Relátorio com os valores dos imóveis para venda.  
- Mapa de calor   
- Aplicativo em nuvem com análise exploratória dos dados.  

### 3.2. Ferramentas
- Python 3.10.4    
- Visual Studio Code  
- Jupyter Notebook  
- Geopy API  
- Streamlit  

### 3.3. Processo
Para responder as perguntas de negócio, após a coleta dos dados, foi realizado o processamento e transformação, limpezas necessárias e análise exploratória.

#### 1. Quais são os imóveis que a House Rocket deveria comprar e por qual preço?  

Como a localização e condição são um grandes fatores no preço, os imóveis foram agrupados por código postal e determinada a mediana de cada grupo para encontrar os preços intermediários.Os imóveis com valores abaixo da mediana regional foram pré-selecionados e filtrados,ou seja, aqueles com boas condições ou superior (>=4).

#### 2. Uma vez o imóvel comprado, qual o melhor momento para vendê-lo e por qual preço?  

Foi analisado que a sazonalidade influencia na valorização dos imóveis, tendo esse insight foi recomendado reagrupar por zipcode e estação do ano e uma nova mediana foi determinada. Em seguida as seguintes condições são aplicadas:

- Se o preço de compra for **maior** que a mediana regional com sazonalidade: o preço de venda é 10% acima do valor de compra.  
- Se o preço de compra for **menor** que a mediana regional com sazonalidade: o preço de venda é 30% acima do valor de compra.

## 4. Os 10 principais insights dos dados

#### H1. As casas aumentam 10% do valor a cada quantidade de quartos construidos.    
**Falso:** o numero de quartos influencia no preço mas é desproporcional. Entre 0 quartos e 1 o preço cai. Entre 5 e 6 quartos o preço se mantém. E de 10 a 11 quartos o preço volta a cair.
_______________
#### H2. As casas vendidas no Verão são 20% mais caras em relação ao Inverno, na média.  
**Falso.** As casas vendidas no verão são 5% mais caras em média.
_______________

#### H3. Imóveis que possuem vista para água, são 30% mais caros, na média.  
**Verdadeiro.** Imoveis com vista para água são mais caros, ultrapassando a porcentagem de 200%. 
_______________

#### H4. Imóveis sem porão possuem lote 50% maior do que com porão.
**Falso.** Imoveis sem porão tem lote menor, em média 22.56%.
_______________
#### H5. Imóveis com vista boa ou excelente são 30% mais caros, na média.  
**Verdadeiro.** Imóveis com vista boa ou excelente são em média 125% mais caros.
_______________
#### H6. Imóveis com qualidade de construção acima da média são 15% mais caros.  
**Verdadeiro.** Imóveis com qualidade de construção acima da média são 93% mais caros.
_______________
#### H7. Imóveis com 3 quartos tem um crescimento MoM (Month over Month) de 15%.  
**Falso.** A média de crescimento MoM é de -0.22% (negativo).
_______________
#### H8. Imóveis com data de construção menor que 1955, são 50% mais baratos, na média.  
**Falso.** Imóveis construídos após 1955 são em média 0.79% mais caros.
_______________
#### H9. O crescimento do preço dos imóveis YoY (Year over Year) é de 10%.  
**Falso.** O crescimento do preço dos imóveis YOY é de 0.52%.
_______________
#### H10. A cada andar, o valor dos imóveis aumentam em 15% .  
**Verdadeiro.** Em excessão aos imóveis com 3 quartos que tem queda nos valores.

## 4.1 Criando recomendações
Foi criado dois relatórios:
- 1. Recomendações de casas para compra, agrupadas por cep,preço por região e condição do imóvel.  

- 2. Recomendação em qual momento vender, agrupadas por cep e estação do ano.   
Incluindo o retorno financeiro de cada imóvel dadas as condições.  

## 5. Resultados financeiros para o negócio

Escolhendo as melhores propriedades com base na localização, características e tempo, obtém-se um **lucro médio por imóvel de US$ 71.700,00.**  

Podem ser feitas renovações para aumentar o valor, talvez escolhendo a quantidade de atributos ou aumentando o valor da porcentagem de venda.

## 6. Conclusão e próximos passos

Todas as perguntas do CEO foram respondidas, trazendo insights através de hipóteses e gerando retorno financeiro.
Porém, pode haver melhorias trazendos novos insights com outras ferramentas. 

Próximos passos:

- Adicionar dados externos de criminalidade das regiões tendo como  insight a influência na valorização do imóvel.
- Criar um modelo de Machine Learning para prever o preço com base nas características da propriedade.


