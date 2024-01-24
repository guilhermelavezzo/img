# Documentação do Pipeline de Registros de Eventos do DataDog

## Visão Geral
Este pipeline é projetado para extrair métricas de eventos do DataDog, processá-los e armazená-los dentro do datalake para criação de insights em dashboards. 

## Documentação do Fluxo de Dados ETL para Eventos DataDog
![Alt text](https://github.com/guilhermelavezzo/img/blob/main/Datadog-5.jpg?raw=true)

## Fontes de Dados
- **API Do Datadog**: Dados extraídos da API do DataDog.

## Tecnologias Utilizadas
- **Databricks/Apache PySpark**: Processamento e transformação de dados.
- **Azure Data Lake**: Armazenamento de dados brutos e processados.
- **Azure Data Factory**: Orquestração e agendamento de tarefas.

## Processamento de Dados
1. **Limpeza de Dados**: Remoção de registros duplicados e correção de formatos inconsistentes.
2. **Enriquecimento e Transformação de Tags**: Tags de eventos são extraídas, transformadas e agregadas para formar uma estrutura de dados detalhada.
3. **Categorização de Eventos**: Eventos são categorizados com base em seus títulos usando expressões regulares e lógica condicional
4. **Conversão de Timestamps**: Campos de timestamp e duração são convertidos para formatos mais legíveis e padronizados.
5. **Seleção de Colunas e Filtragem Final**: Seleção do conjunto final de colunas e aplicação de filtragem baseada em intervalos de datas.

## Agendamento e Orquestração
- O pipeline é executado diariamente às 07:00 AM UTC.
- Azure Data Factory é usado para gerenciar a dependência das tarefas e falhas.

## Destino dos Dados
- Os dados processados são armazenados no Azure Data Lake, em formato Avro e Parquet, em 4 fontes de dados: 
  - PrelandingZone: realiza a operação de salvamento de registros diários na pipeline, o salvamento é realizado no formato Avro no seguinte path: `Datadog/Events/data`
  - HistoryZone: é a pasta no lake onde é guardados os registros históricos dos dados, o salvamento é realizado no path: `Datadog/Events`
  - ConsumeZone: é a pasta do lake onde são disponibilizados os dados para consumo em ferramentas externas, o salvamento é realizado no path: `TechOps/Monitoramento/Datadog/Events`
  - Trino/Presto: onde adicionamos os registros da consumezone para conectarmos com o Power BI e Metabase, a tabela é essa: `datadog_events`

## Diagrama das Tabelas

![Alt text](https://github.com/guilhermelavezzo/img/blob/main/Datadog-2.jpg?raw=true)

# Documentação dos notebooks
![Fluxo de Dados](https://github.com/guilhermelavezzo/img/blob/main/Datadog-1.jpg?raw=true)


## Arquitetura dos dados
![Alt text](https://github.com/guilhermelavezzo/img/blob/main/Datadog.jpg?raw=true)

# Histórico de Mudanças
- **v1.2 (2024-01-10)**: Realizando primeiro processo da pipeline.