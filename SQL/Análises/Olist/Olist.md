
## Introdução

Análise realizada utilizando a base do Olist Ecommerce disponível em https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce.

Realizei o processo de ETL da base utilizando o SQL Server e suas ferramentas, para gerenciamento do banco e execução das queries fiz por meio do SSMS.

A base possui 7 tabelas referentes aos clientes, pedidos, pagamentos, avaliações, vendedores e produtos, com um total de aproximadamente 200000 registros somando todas as tabelas.

## Métodos de pagamento

Para início da análise pode ser visto o principal método de pagamento para os clientes e o % utilização para cada método.

```
SELECT 
    payment_type,
    COUNT(DISTINCT order_id) AS total_pedidos,
    ROUND((COUNT(DISTINCT order_id) * 100.0) / (SELECT COUNT(DISTINCT order_id) FROM olist_order_payments_dataset WHERE payment_type IS NOT NULL AND payment_type != ''), 2) AS percentual_metodo_pagamento
FROM 
    olist_order_payments_dataset
WHERE
    payment_type IS NOT NULL AND payment_type != '' 
GROUP BY 
    payment_type;
```

| payment_type | total_pedidos | percentual_metodo_pagamento |
| ---- | ---- | ---- |
| credit_card<br>boleto<br>voucher<br>debit_card<br>not_defined | 76505<br>19784<br>3866<br>1528<br>3 | 76.940000000000<br>19.900000000000<br>3.890000000000<br>1.540000000000<br>0.000000000000 |
Podemos observar que o método de pagamento mais utilizado é o cartão de crédito, com quase 77% dos casos, seguido pelo boleto com 19%. São os dois principais métodos de pagamento para parcelamento da compra, o que indica que quase todas as compras são feitas com o pagamento mês a mês ou são empurradas para o dia de vencimento do cartão, apenas 1,5% fazem o pagamento a vista pelo cartão de débito.

Isso também é confirmado quando verificamos a média de valores para cada tipo de pagamento.

```
SELECT        
	payment_type, 
	AVG(CAST(payment_value AS DECIMAL(10, 2))) AS media_por_tipo_de_pagamento
FROM            
	olist_order_payments_dataset
WHERE        
	(payment_type IS NOT NULL) AND (payment_type <> '') AND (payment_value IS NOT NULL) AND (payment_value <> '')
GROUP BY payment_type;
```

| payment_type | media_por_tipo_de_pagamento |
| --- | --- |
| credit_card<br>boleto<br>debit_card<br>voucher<br>not_defined | 163.319020<br>145.034435<br>142.570170<br>65.703354<br>0.000000 |
Como é esperado, quando a compra é feita por cartão de crédito ou boleto, possui algumas parcelas e normalmente o valor é maior justamente por possuir mais tempo para realizar o pagamento.

A média de parcelas para o cartão de crédito gira em torno 3, 4 parcelas.

```
SELECT 
    payment_type,
    ROUND(AVG(CAST(payment_installments AS DECIMAL)), 2) media_parcelas_por_tipo_pagamento
FROM 
    olist_order_payments_dataset
WHERE
    payment_type IS NOT NULL AND payment_type != '' 
    AND payment_installments IS NOT NULL AND payment_installments != ''
	AND payment_type = 'credit_card'
GROUP BY 
    payment_type;
```

| payment_type | media_parcelas_por_tipo_pagamento |
| --- | --- |
| credit_card | 3.510000 |

## Produtos

Dentro dos produtos, podemos analisar o top 10 de produtos vendidos

```
SELECT TOP 10
	p.product_category_name,
	COUNT(oi.product_id) AS total_de_vendas_por_categoria
FROM 
	olist_order_items_dataset oi
JOIN
	olist_products_dataset p
ON  
	oi.product_id = p.product_id
WHERE
	p.product_category_name IS NOT NULL
	AND p.product_category_name != ''
GROUP BY
	p.product_category_name
ORDER BY 
	total_de_vendas_por_categoria DESC;
```

| product_category_name | total_de_vendas_por_categoria |
| --- | --- |
| cama_mesa_banho<br>beleza_saude<br>esporte_lazer<br>moveis_decoracao<br>informatica_acessorios<br>utilidades_domesticas<br>relogios_presentes<br>telefonia<br>ferramentas_jardim<br>automotivo | 11115<br>9670<br>8641<br>8334<br>7827<br>6964<br>5991<br>4545<br>4347<br>4235 |
Os produtos mais vendidos são das categorias móveis, beleza e esportes.

Também podemos analisar qual o top 10 de produtos com maior valor de vendas somados por categoria.

```
SELECT TOP 10
	p.product_category_name,
	SUM(CAST(oi.price AS DECIMAL)) AS total_por_categoria
FROM 
	olist_order_items_dataset oi
JOIN
	olist_products_dataset p
ON  
	oi.product_id = p.product_id
WHERE
	p.product_category_name IS NOT NULL
	AND p.product_category_name != ''
GROUP BY
	p.product_category_name
ORDER BY 
	total_por_categoria DESC;
```

| product_category_name | total_por_categoria |
| --- | --- |
| beleza_saude<br>relogios_presentes<br>cama_mesa_banho<br>esporte_lazer<br>informatica_acessorios<br>moveis_decoracao<br>cool_stuff<br>utilidades_domesticas<br>automotivo<br>ferramentas_jardim	 | 1258951<br>1205213<br>1037729<br>988433<br>912344<br>730156<br>635443<br>632624<br>592843<br>485473 |
As categorias que mais tiveram valor nas vendas foram area de beleza, relógios, esportes, informática e moveis.

## Clientes

Analisando a base de clientes, podemos verificar que os clientes que mais realizaram compras são do estado de SP, RJ e MG.

```
SELECT
	customer_state,
	CAST(COUNT(customer_state) AS decimal) as total_compras_por_estado
FROM
	olist_customers_dataset
GROUP BY
	customer_state
ORDER BY
	total_compras_por_estado DESC;
```

| customer_state | total_compras_por_estado |
| --- | --- |
| SP<br>RJ<br>MG<br>RS<br>PR<br>SC<br>BA<br>DF<br>ES<br>GO<br>PE<br>CE<br>PA<br>MT<br>MA<br>MS<br>PB<br>PI<br>RN<br>AL<br>SE<br>TO<br>RO<br>AM<br>AC<br>AP<br>RR | 41746<br>12852<br>11635<br>5466<br>5045<br>3637<br>3380<br>2140<br>2033<br>2020<br>1652<br>1336<br>975<br>907<br>747<br>715<br>536<br>495<br>485<br>413<br>350<br>280<br>253<br>148<br>81<br>68<br>46 |

Fazendo a mesma análise por região, temos:

```
SELECT
	regiao_cliente,
	CAST(COUNT(*) AS decimal) AS total_compras_por_regiao
FROM (
	SELECT
		CASE
			WHEN customer_state IN ('SP', 'RJ', 'MG', 'ES') THEN 'Sudeste'
			WHEN customer_state IN ('RS', 'PR', 'SC') THEN 'Sul'
			WHEN customer_state IN ('DF', 'GO', 'MS', 'MT') THEN 'Centro Oeste'
			WHEN customer_state IN ('BA', 'SE', 'AL', 'PE', 'RN', 'PB', 'PI', 'CE', 'MA') THEN 'Nordeste'
			WHEN customer_state IN ('TO', 'RO', 'RR', 'PA', 'AM', 'AC', 'AP') THEN 'Norte'
			ELSE 'N/A'
		END AS regiao_cliente
	FROM
		olist_customers_dataset
) AS regioes
GROUP BY
	regiao_cliente
ORDER BY
	total_compras_por_regiao DESC;
```

| regiao_cliente | total_compras_por_regiao |
| ---- | ---- |
| Sudeste<br>Sul<br>Nordeste<br>Centro Oeste<br>Norte | 68266<br>14148<br>9394<br>5782<br>1851 |
Como pode ser observado, grande maioria das compras desse ecommerce são realizadas pela região sudeste, seguida pela sul e pela nordeste.
Esses números fazem sentido uma vez que o sudeste é a região mais populosa e rica do país, portanto é normal possuir mais gente fazendo compras.

## Vendedores

Analisando os vendedores, podemos verificar o top 10 de cidades com mais vendedores:

```
SELECT TOP 10
    CONCAT(seller_city, ' - ', seller_state) AS cidade,
    CAST(COUNT(DISTINCT seller_id) AS DECIMAL) AS vendedores_por_cidade
FROM 
    olist_sellers_dataset 
GROUP BY
    CONCAT(seller_city, ' - ', seller_state)
ORDER BY
    vendedores_por_cidade DESC;
```

| cidade | vendedores_por_cidade |
| --- | --- |
| sao paulo - SP<br>curitiba - PR<br>rio de janeiro - RJ<br>belo horizonte - MG<br>ribeirao preto - SP<br>guarulhos - SP<br>ibitinga - SP<br>santo andre - SP<br>campinas - SP<br>maringa - PR | 694<br>124<br>93<br>66<br>52<br>50<br>49<br>45<br>41<br>40 |
Podemos observar que no top 10 cidades com mais vendedores, 6 ficam no estado de SP e apenas 1 fora da região sudeste.

Observando o total de vendedores por região temos:

```
SELECT
	regiao_vendedor,
	CAST(COUNT(*) AS decimal) AS total_vendedor_por_regiao
FROM (
	SELECT
		CASE
			WHEN seller_state IN ('SP', 'RJ', 'MG', 'ES') THEN 'Sudeste'
			WHEN seller_state IN ('RS', 'PR', 'SC') THEN 'Sul'
			WHEN seller_state IN ('DF', 'GO', 'MS', 'MT') THEN 'Centro Oeste'
			WHEN seller_state IN ('BA', 'SE', 'AL', 'PE', 'RN', 'PB', 'PI', 'CE', 'MA') THEN 'Nordeste'
			WHEN seller_state IN ('TO', 'RO', 'RR', 'PA', 'AM', 'AC', 'AP') THEN 'Norte'
			ELSE 'N/A'
		END AS regiao_vendedor
	FROM
		olist_sellers_dataset
) AS regioes
WHERE
	regiao_vendedor != 'N/A'
GROUP BY
	regiao_vendedor
ORDER BY
	total_vendedor_por_regiao DESC;
```

| regiao_vendedor | total_vendedor_por_regiao |
| --- | --- |
| Sudeste<br>Sul<br>Centro Oeste<br>Nordeste<br>Norte | 2286<br>667<br>79<br>56<br>5 |
Podemos observar que a grande maioria dos vendedores estão na região sudeste e a região norte possui apenas 5, o que indica que possivelmente podem sofrer com valores maiores de frete já que as vendas precisam vir de lugares distantes ou ter menos variedade de itens para comprar.

## Conclusão

Com a análise da base podemos retirar alguns insights:
- O método de pagamento mais utilizado é o cartão de crédito, cerca de 76% dos casos.
- O valor médio de gasto numa compra utilizando o parcelamento é de 163 reais e para compras a vista é de 142 reais.
- A média de parcelas escolhidas pelos clientes gira em torno de 3 a 4.
- Produtos da categoria cama, mesa e banho são os mais vendidos;
- Produtos de beleza e saúde foram aqueles que mais movimentaram dinheiro.
- O estado que mais teve compras foi o de São Paulo com 41746 compras.
- A região com mais compras foi a sudeste com 68266 compras.
- A cidade com mais vendedores é São Paulo com 694 vendedores.
- A região norte possui apenas 5 vendedores sendo a região que possui menos vendedores.

## Ferramentas

Para realizar a análise utilizei:
- Kaggle
- Sql Server
- Sql Server Managment Studio
- Git
- Obsidian