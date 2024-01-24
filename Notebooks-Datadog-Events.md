## Documentação do Notebook: SC -> PZ: DataDog - Events

### Visão Geral

Este notebook é responsável por realizar a requisição dos registros da API do DataDog e escrever na PZ (Prelanding Zone). O script automatiza a coleta de eventos do DataDog, facilitando o monitoramento e a análise de dados em ambientes complexos.

### Estrutura do Script

- **Importação de Bibliotecas**: Utiliza bibliotecas como `FileSystemConfig`, `LoadService`, `FileWriter`, `FileReader` do pacote `pyiris`, `Spark` da infraestrutura PySpark, entre outras.
- **Definição de Variáveis e Caminhos**: Realiza a definição dos caminhos da PZ e HZ e faz a configuração de variáveis relacionadas à data, nomes de colunas e caminhos de arquivos.
- **Requisição da API**: Realiza a request da API com as funções próprias da documentação do Datadog.
- **Gravação de Dados**: Gravação dos dados processados na PZ.

## Documentação do Notebook: PZ -> HZ: DataDog - Events

### Visão Geral

Este notebook é responsável por ler os dados atuais da PZ, realizar o versionamento e escrever na HZ. O processo inclui a manipulação de eventos coletados do DataDog, garantindo uma organização eficiente e estruturada dos dados para análises subsequentes.

### Estrutura do Script

- **Importação de Bibliotecas**: Importa bibliotecas do PySpark para tipos de dados e funções, bem como módulos de transformações customizadas do `pyiris`.
- **Definição de Variáveis e Caminhos**: Definição de variáveis relacionadas a datas e caminhos dos dados.
- **Processamento e Versionamento de Dados**: O script parece realizar transformações nos dados, aplicando versionamento antes de movê-los para a HZ

## Documentação do Notebook: HZ -> CZ: DataDog - Events

### Visão Geral

Este notebook é responsável por ler os dados atuais da HZ (History Zone), realizar as transformações necessárias e escrever na CZ (Consume Zone). O foco está na manipulação de eventos do DataDog, garantindo que os dados sejam devidamente transformados e armazenados para uso posterior.

### Estrutura do Script

- **Importação de Bibliotecas**: Importa bibliotecas do PySpark para tipos de dados e funções, bem como módulos de transformações customizadas do `pyiris`.
- **Processamento dos Dados**: Realização de seleção de tags específicas para pivoteamento e criação de colunas das tags, tranformação da coluna de categoria de evento para controle de tasks.
- **Transformação de Data/Hora**: Transformação de Timestamp para DateTime

## Documentação do Notebook: CZ -> Presto: DataDog - Events

### Visão Geral

Este notebook é responsável por ler os dados atuais da CZ (Consume Zone) e realizar o salvamento da tabela no Presto. O script foca na transferência de eventos do DataDog, assegurando que os dados sejam armazenados de forma eficiente no sistema de banco de dados Presto para consultas e análises futuras.

### Estrutura do Script

- **Importação de Bibliotecas**: Utiliza bibliotecas como `PrestoWriter`, `PrestoConfig`, do `pyiris`, além de `FileReader`, `LoadService`, e `Spark`.
- **Leitura de Tickets Full da CZ**: Lê a visão completa dos registros de eventos do Datadog.
- **Salvamento no Presto**: Configura o `PrestoWriter` com parâmetros específicos, incluindo formato, caminho, modo de sincronização, e detalhes da tabela, para escrever os dados do DataFrame no Presto.
