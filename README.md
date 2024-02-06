# AzureML
Uso de modelo com regressão para análise de aluguel de bicicletas.

## O que é um modelo de regressão?
Trata-se de uma forma de aprendizado de máquina supervisionado, em que o retorno será um número inteiro.

## Passo a passo para criar um workspace no Azure Machine Learning

- Criação de conta na Azure
- Criar um recurso: Assinatura, Resource Group...

Configurações básicas:

- Nome do trabalho: mslearn-bike-automl
- Nome do novo experimento: mslearn-bike-rental
- Descrição: machine learning automatizado para previsão de aluguel de bicicletas
- Marcas: nenhuma

Tipo de tarefa e dados:

- Selecionar tipo de tarefa: regressão
- Selecionar conjunto de dados: crie um novo conjunto de dados com as seguintes configurações:

Tipo de dados:

- Nome: bike-rentals
- Descrição: dados históricos de aluguel de bicicletas
- Tipo: tabular

Fonte de dados:

- Selecione De arquivos da Web

URL da Web:

- URL da Web: https://aka.ms/bike-rentals
- Ignorar validação de dados: não selecionar

Configurações:

- Formato de arquivo: delimitado
- Delimitador: vírgula
- Codificação: UTF-8
- Cabeçalhos de coluna: somente o primeiro arquivo tem cabeçalhos
- Ignorar linhas: Nenhum
- O conjunto de dados contém dados multilinhas: não selecione

Esquema:

- incluir todas as colunas que não sejam Caminho
- Examinar os tipos detectados automaticamente

Selecione o conjunto de dados de aluguel de bicicletas depois de criá-lo.

Configurações da tarefa:

- Tipo de tarefa: regressão
- Conjunto de dados: bike-rentals
- Coluna de destino: aluguéis (inteiro)
- Definições de configuração adicionais:
- Métrica primária: erro quadrático médio da raiz normalizada
- Explicar o melhor modelo: não selecionado
- Usar todos os modelos com suporte: Nãoselecionado. Você restringirá o trabalho para experimentar apenas alguns algoritmos específicos.
- Modelos permitidos: selecione apenas RandomForest e LightGBM. O ideal seria tentar usar o máximo possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.
- Limites: expanda esta seção
- Avaliações máximas: 3
- Máximo de avaliações simultâneas: 3
- Máximo de nós: 3
- Limite de pontuação da métrica: 0,85 (de modo que se um modelo atingir uma pontuação de métrica de raiz do erro quadrático médio normalizada de até 0,085, o trabalho será encerrado.)
- Tempo limite: 15
- Tempo limite de iteração: 5
- Habilitar encerramento antecipado: selecionado

Validação e teste:

- Tipo de validação: divisão de validação de treinamento
- Percentual de dados de validação: 10
- Conjunto de dados de teste: nenhum

Computação:

- Selecionar tipo de computação: sem servidor
- Tipo de máquina virtual: CPU
- Camada da máquina virtual: dedicada
- Tamanho da máquina virtual: Standard_DS3_V2
- Número de instâncias: 1

Envie o trabalho para treinamento.

Entrada para o serviço implantado: 

```
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```

A saída está disponível no arquivo result.json, presente neste repositório.

Todas essas informações podem ser encontradas em: [Microsoft Learn - AI900](https://microsoftlearning.github.io/AI-900-AIFundamentals.pt-BR/Instructions/02-module-02.html)