# central-monitoramento-apis


Central Inteligente de Monitoramento
Aplicação que integra duas APIs públicas (cotação de moedas e clima), consolida as informações em um banco de dados no-code (Airtable) e apresenta os dados em uma interface web, com uma automação de alerta baseada nos dados coletados.
Projeto desenvolvido para a disciplina de Integração de APIs — UniFECAF.
🔗 Acesse a aplicação
https://louhansantos226575-dotcom.github.io/central-monitoramento-apis/
O problema
Empresas costumam ter informações espalhadas em diferentes sistemas (cotações, indicadores, notificações, documentos), o que obriga colaboradores a consultar várias ferramentas para uma única tarefa. Este projeto demonstra, em escala reduzida, como resolver esse problema: consumindo múltiplas APIs, consolidando os dados em um único lugar e automatizando parte do fluxo.
APIs utilizadas
Frankfurter API (frankfurter.app) — cotações de câmbio (USD/BRL e EUR/BRL), dados do Banco Central Europeu, gratuita e sem necessidade de chave de autenticação.
OpenWeatherMap API (openweathermap.org) — dados climáticos em tempo real de três cidades brasileiras (São Paulo, Rio de Janeiro, Fortaleza), autenticada por API key.
Fluxo de integração
Um cenário no Make.com é executado automaticamente a cada 1 hora.
Para cada moeda (USD e EUR), o cenário busca a cotação atual na Frankfurter API, compara com o último valor salvo (guardado em um Data Store do Make) para calcular a variação percentual, e grava um novo registro na tabela Cotacoes do Airtable.
Se a variação de qualquer uma das moedas ultrapassar 1% desde a última checagem, um e-mail de alerta é disparado automaticamente.
Em paralelo, o cenário busca o clima atual das três cidades na OpenWeatherMap API e grava os dados na tabela Clima do Airtable.
Uma página web estática (hospedada no GitHub Pages) consulta a API do Airtable diretamente do navegador do usuário e exibe os dados mais recentes em cards, com botão de atualização manual.
Armazenamento dos dados
Banco de dados no-code no Airtable, com duas tabelas:
Cotacoes: Data, Moeda, Valor, Variação (%)
Clima: Data, Cidade, Temperatura, Descrição
Autenticação e segurança
O Make se conecta ao Airtable via Personal Access Token com escopo de leitura e escrita, restrito a esta base.
A interface web utiliza um token separado, somente leitura, também restrito a esta única base — já que esse token fica visível no código-fonte da página (aplicação estática, sem backend). Essa decisão é detalhada no documento teórico do projeto.
A OpenWeatherMap é consultada com autenticação via API key.
Como executar/acessar o projeto
Não é necessário instalar nada — a aplicação já está publicada e funcionando em: https://louhansantos226575-dotcom.github.io/central-monitoramento-apis/
Para rodar localmente: baixe o arquivo index.html deste repositório e abra em qualquer navegador.
Prints da aplicação





TABELAS:




AUTOMAÇÃO:


Automação implementada
Alerta por e-mail disparado automaticamente sempre que a variação da cotação do dólar ou do euro ultrapassa 1% entre duas execuções consecutivas do cenário.
Stack utilizada
Make.com — motor de automação e integração das APIs
Airtable — banco de dados no-code
HTML/CSS/JavaScript — interface web (sem frameworks, sem backend)
GitHub Pages — hospedagem da aplicação

