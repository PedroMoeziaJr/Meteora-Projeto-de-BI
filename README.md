# Projeto de BI para empresa METEORA - MODA DE IMPACTO

Projeto parte do Alura Challenge BI 3 e 4 semana

| :placard: Vitrine.Dev |     |
| -------------  | --- |
| :sparkles: Nome        | **Projeto de BI da empresa METEORA**
| :label: Tecnologias | MySQL, Qlik Sense
| :rocket: URL         | [https://url-deploy.com.br](https://www.alura.com.br/challenges/bi-3/semana-03-04-financeiro-empreendendo-dados-comercio-online?utm_source=ActiveCampaign&utm_medium=email&utm_content=%5BChallenge+BI%5D+%C3%9Altimos+desafios+no+ar%2C++FIRSTNAME++%E2%9C%85&utm_campaign=%5BCHALLANGE%5D+%28BI+-+3%C2%AA+ed+%29+E-mail+avisando+libera%C3%A7%C3%A3o+da+aula+03e04+%2B+convite+live+revis%C3%A3o+de+c%C3%B3digo&vgo_ee=aze3E7l1gxtnsu8AnmZeprYY%2Fzumqtc%2B%2Bv737AI3v%2FTB608%3D%3AJzgl9M%2FxDL3YTdrLxMcH67t1apCbsRZ%2F)
| :fire: Desafio     | [https://url-do-desafio.com.br](https://trello.com/b/dlXn3nuM/challenge-bi-semana-3-e-4)

![Prancheta 2](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/f9a558a9-120e-4f5d-bec7-4c470e57afe4#vitrinedev)


## Detalhes do projeto

<h1>1- Criação do Banco de Dados da empresa Meteora.</h1>

<h2>Da Modelagem a criação de um banco de dados.</h2>

![meteora-moda-de-impacto](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/bb915142-e440-4193-9ec3-b94c29c3c70c)
![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/b264f3c0-8fbc-4234-b505-91f7bb72c1fb)

 
>Criação das tabelas.

Fiz o download de cada pasta(produtos, pedidos, itens_pedidos e vendedores) no formato .CSV e salvei em uma pasta no meu computador.
![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/6b4ab758-360c-4adc-92e3-50b0a730974f)
![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/1f4de862-6401-42cf-80d4-e68375bbd4fa)

Depois de baixar todas as pastas no formato .CSV abri o Microsoft SQL Server Managemente Studio e criei o banco de dados da Meteora no meu servidor:

	create database meterora

Depois com o botão direito do mouse em cima do banco de dados fui em:
>Tarefas>Importar Arquivo Simples

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/d742855d-2d5b-4241-b8f2-ad02cca5b7af)

Cliquei em Próxima>Procurar e Procurei os arquivs .CSV e começei pela pasta "produtos"

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/2169c7c6-ba8b-4d0e-bcd6-0fc0284346f0)

>Próxima

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/f1e67847-4b63-42c5-99da-4809af6d2f06)

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/c8170705-5186-424d-abd4-ca696b9abbb6)

>Próxima>Concluir

create database meterora
use meterora
select * from produtos;

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/da864b9f-e6b7-432a-8100-e8b68269bc3e)

E assim fiz com as demais pastas


<H1>EXTRAINDO OS DADOS PARA O QLIK SENSE</H1>

<H2>CRIANDO A DASHBOARD</H2>

<H3>-Calcule o valor da Receita da Meteora para posteriormente utilizarmos na criação de mais métricas.</H3>

Criar a seguinte medida RECEITA

	sum(valor_total*quantidade)

Nesse caso, você multiplicaria o valor total de cada item pelo seu respectivo valor na coluna "quantidade" e, em seguida, somaria esses valores para obter a receita total.

A multiplicação pelo campo "quantidade" é necessária para levar em consideração a quantidade de cada item vendido ao calcular a receita.

Novamente, peço desculpas pela confusão anterior e agradeço por trazer o erro ao meu conhecimento.

<H3>-Calcule e exiba o lucro da Meteora</H3>

Criar a seguinte medida LUCRO com a seguinte fórmula

	Receita - SUM(valor_unitario * quantidade)
 
<h3>-Calcule e exiba a despesas da Meteora.</h3>

Criar a medida DESPESA com a seguinte fórmula:

	sum(frete)

<h3>-Vamos mostrar a quantidade de vendas por estado.</h3>

Criando um gráfico de MAPA no Qlik apenas coms os campo Estados o programa não detectou. Portanto retirei do campo o "BR-" usando o seguinte comando:
	
	Replace(Estado, 'BR-', '') as Estado	

Mesmo assim a localização não condiz com os Estados nos campos:
![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/ad265375-37d4-4517-aa50-85c364ec6ff7)

Por isso, criei o seguinte script:

	IF(Estado = 'BR-SP', 'São Paulo',
	IF(Estado = 'BR-PA', 'Pará',
	IF(Estado = 'BR-PI', 'Piauí',
	IF(Estado = 'BR-MG', 'Minas Gerais', 
	IF(Estado = 'BR-ES', 'Espírito Santo',
	IF(Estado = 'BR-RJ', 'Rio de Janeiro',
	IF(Estado = 'BR-RN', 'Rio Grande do Norte',
	IF(Estado = 'BR-MS', 'Mato Grosso do Sul',
	IF(Estado = 'BR-DF', 'Brasília',
	IF(Estado = 'BR-AP', 'Amapá',
	IF(Estado = 'BR-CE', 'Ceará',
	IF(Estado = 'BR-PR', 'Paraná',
	IF(Estado = 'BR-RR', 'Roraima',
	IF(Estado = 'BR-TO', 'Tocantins',
	IF(Estado = 'BR-SC', 'Santa Catarina',
	IF(Estado = 'BR-AM', 'Amazonas',
	IF(Estado = 'BR-PE', 'Pernambuco',
	IF(Estado = 'BR-RS','Rio Grande do Sul',
	IF(Estado = 'BR-RO', 'Rondônia',
	IF(Estado = 'BR-MT', 'Mato Grosso',
	IF(Estado = 'BR-MA', 'Maranhão',
	IF(Estado = 'BR-AC', 'Acre',
	IF(Estado = 'BR-AL', 'Alagoas', 
	IF(Estado = 'BR-BA', 'Bahia', 
	IF(Estado = 'BR-GO', 'Goiás', 
	IF(Estado = 'BR-PB', 'Paraíba',
	IF(Estado = 'BR-BR-RR', 'Roaima',
	IF(Estado = 'BR-SE', 'Sergipe','')))))))))))))))))))))))))))) as ESTADO,
	
Após essa correção a localização ficou acertada:
![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/4e1c8716-605d-44a0-8aa9-7f4b19c2afe0)

<h3>Exibindo as métricas as métricas de forma temporal</h3>

Antes de inserir um gráfico barras, criei a dimensão MÊS usando o campo data_compra:

	=Month(data_compra)

Logo em seguida, depois de colocar o gráfico de barra inserimos as medidas LUCRO, RECEITA e DESPESA.

![image](https://github.com/PedroMoeziaJr/Meteora-Projeto-de-BI/assets/112977342/296c26d6-25bc-45cb-9c6d-0d0872ce4e18)

Para complementar colocamos um filtro para selecionar o ANO usando a fórmula:

	=Year(data_compra)

 







