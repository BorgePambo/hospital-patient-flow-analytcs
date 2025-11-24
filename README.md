# Real-Time Patient Flow Analytics on Azure

📌 Project Overview
Este projeto demonstra um #pipeline de engenharia de dados em tempo real para a área da saúde, projetado para analisar o fluxo de pacientes entre os departamentos de um hospital utilizando serviços da nuvem Azure.
O pipeline ingere dados em streaming, processa-os no Databricks (PySpark) e os armazena no Azure Synapse SQL Pool para análise e visualização.

###### Parte 1 – Engenharia de Dados: Construir o pipeline de ingestão e transformação em tempo real.
###### Parte 2 – Análises: Conectar o Synapse ao Power BI e criar um dashboard interativo com KPIs hospitalares.

PIPELINE DESIGN
<img width="1071" height="610" alt="pipeline_hospi" src="https://github.com/user-attachments/assets/9f83f05a-4cb8-4017-ad74-7771f4901be2" />

# OBJETIVO
    1 - Coletar dados de pacientes em tempo real via Azure Event Hub.
    
    2 - Processar e limpar os dados usando Databricks (camadas Bronze → Silver → Gold).
    
    3 - Implementar um esquema estrela no Synapse SQL Pool para consultas eficientes.
    
    4 - Habilitar Controle de Versão com Git.

# Project Structure
    real-time-patient-flow-azure/
    │
    ├── databricks-notebooks/  # Transformation notebooks
    │   ├── 01_bronze_rawdata.py
    │   ├── 02_silver_cleandata.py
    │   └── 03_gold_transform.py
    ├── simulator/             # Data simulation scripts
    │   └── patient_flow_generator.py
    ├── sqlpool-quries/        # SQL scripts for Synapse
    │   └── SQL_pool_quries.sql
    ├── git_commands/                  # Git Commands
    └── README.md              # Project documentation

# Arquitetura de Dados
    O pipeline usa uma arquitetura em múltiplas camadas:
    
     **Bronze**: Dados brutos em JSON vindos do Event Hub armazenados no ADLS.  
     **Silver**: Dados limpos e estruturados (tipos validados e tratamento de nulos).   
     **Gold**: Dados agregados e prontos para consumo em BI.

# Tools & Technologies: 
    Azure Event Hub – Ingestão de dados em tempo real
    Azure Databricks – Processamento ETL usando PySpark.
    Azure Data Lake Storage – Armazenamento de dados brutos e dados tratados
    Azure Synapse SQL Pool – Data warehouse para análise 
    Power BI – Visualização
    Python 3.9+ – Core programming
    Git – Version control

# Design de Star Schema

A camada Gold no Synapse usa um esquema em estrela para análises rápidas:
Tabela Fato: FactPatientFlow — contém visitas dos pacientes, tempos de espera, entrada/saída.
Tabelas Dimensão:
        DimDepartment: informações dos departamentos.
        DimPatient: dados demográficos dos pacientes.
        DimTime: dimensão de datas e horários.


# Implementação passo a passo
##### 1. Configuração do Event Hub
Criado o namespace do Event Hub e o hub patient-flow.
Configurados os grupos de consumidores para o streaming no Databricks.

#### 2. Simulação de Dados
Desenvolvido o script Python patient_flow_generator.py para enviar dados falsos de pacientes (departamentos, tempo de espera, status de alta) para o Event Hub.
Inclui o código do produtor (producer).

#### 3. Configuração do Storage
Configurado o Azure Data Lake Storage (ADLS Gen2).

#### 4. Notebooks: https://github.com/BorgePambo/hospital-patient-flow-analytcs/blob/main/databricks-notebook/01-bronze_raw_data.ipynb




