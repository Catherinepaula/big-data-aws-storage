🗄️ Big Data AWS Storage
Pipeline de dados com AWS S3, IAM e Athena utilizando Python e Boto3 — com foco em particionamento e orientação à coluna.

📌 Sobre o projeto
Este projeto implementa um pipeline completo de armazenamento e consulta de dados em nuvem, utilizando o dataset de crimes de Chicago (2014). O objetivo é demonstrar boas práticas de armazenamento de dados em escala, com particionamento eficiente e consultas otimizadas via SQL.

🛠️ Tecnologias utilizadas

Python — processamento e automação
Pandas — leitura e transformação dos dados
Apache Parquet — formato colunar com compressão Snappy
Boto3 — SDK Python para AWS
AWS S3 — armazenamento dos dados em CSV e Parquet
AWS IAM — gerenciamento de usuários e permissões
AWS Athena — consultas SQL serverless sobre os dados no S3


🗂️ Estrutura do projeto
big-data-aws-storage/
│
├── notebook.ipynb        # Pipeline completo
├── README.md             # Documentação

🔄 Pipeline
crime.csv
    │
    ▼
DataFrame Pandas
    │
    ├── Criação da coluna reference_date (YYYY-MM)
    │
    ├── Persistência em CSV ──────────────► S3 (Bucket CSV)
    │
    └── Persistência em Parquet ──────────► S3 (Bucket Parquet)
              (Snappy + particionado)
                    │
                    ▼
              AWS Athena
         (tabela externa + SQL)

📊 Consultas SQL executadas
#ConsultaDescrição1SHOW PARTITIONSPartições disponíveis na tabela2COUNT(1)Total de registros (548.846)3GROUP BY reference_dateTotal de crimes por mês4WHERE reference_date = '2014-01'Crimes em Janeiro/2014 por tipo5CASE WHEN arrest = trueTaxa de prisão por tipo de crime

💡 Destaques técnicos

Particionamento por reference_date — reduz o volume de dados escaneados pelo Athena em filtros por período, diminuindo custo e tempo de resposta
Compressão Snappy — equilíbrio entre velocidade de leitura e taxa de compressão
MSCK REPAIR TABLE — carrega automaticamente as partições existentes no S3
Infraestrutura como código — todos os recursos AWS criados via Boto3 (sem uso do console)


📈 Resultado

548.846 registros processados
12 partições criadas (uma por mês de 2014)
28.8% taxa média de prisão nos crimes registrados


▶️ Como executar

Clone o repositório
Abra o notebook.ipynb no Google Colab
Configure suas credenciais AWS na célula de configuração
Execute as células em ordem


👩‍💻 Autora
Catherine Paula Chitolina Cornelio
