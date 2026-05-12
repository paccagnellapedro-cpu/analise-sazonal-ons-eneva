# Análise de Sazonalidade e Tendência de Carga Global: SIN (2021-2023)

## 📖 Visão Geral do Projeto
Este sistema foi desenvolvido para automatizar o ciclo de vida de dados (extração, tratamento e análise) da carga verificada do Sistema Interligado Nacional (SIN). Utilizando dados brutos da API do Operador Nacional do Sistema Elétrico (ONS), a solução fornece subsídios estatísticos para a compreensão de variações sazonais e o planejamento energético.
## ⚙️ Funcionalidades Detalhadas

### 1. Ingestão de Dados Resiliente
- **Paginação Mensal:** O motor de busca fraciona as requisições mês a mês para contornar limites de *rate limiting* e volume de dados da API do ONS, garantindo que 100% da série histórica seja recuperada sem perdas.
- **Tratamento de Erros:** Implementação de lógica de retentativa e travas de segurança para interrupção limpa em caso de falha de conexão.

### 2. Engenharia de Dados e Sazonalidade
- **Classificação Geoclimática:** Diferente de modelos genéricos, o script utiliza os equinócios e solstícios precisos do Hemisfério Sul para classificar cada linha de carga, permitindo uma análise climática fidedigna à realidade brasileira.
- **Normalização Estrita:** Conversão de tipos de dados (strings para floats e datetimes) para permitir cálculos matemáticos de alta precisão.

### 3. Motor Estatístico e Relatórios
- **Matriz de Crescimento (Delta):** Cálculo automático da variação percentual entre 2021 e 2023 por estação.
- **Detecção de Extremos:** Identificação algorítmica dos pontos máximos e mínimos históricos de consumo.
- **Exportação Multiformato:** Geração de relatórios em Excel (.xlsx) com múltiplas abas organizadas e gráficos de tendência (.png) prontos para apresentações executivas.

### 4. Governança e Transparência
- **Sistema de Logs:** Registro detalhado de cada etapa do pipeline no arquivo `log.txt`, permitindo auditoria técnica do status das requisições à API.

## 📊 Insights Identificados
Durante a execução, o projeto evidenciou padrões críticos no triênio analisado:
- **Impacto do El Niño (2023):** Foi detectada uma anomalia na carga da Primavera de 2023, superando médias históricas devido às ondas de calor intensas no segundo semestre.
- **Evolução da Carga Base:** Crescimento sustentado do consumo nos subsistemas analisados, refletindo a dinâmica econômica do período.

## 🛠️ Requisitos de Execução
O projeto foi estruturado para ser 100% compatível com ambientes Windows e Python 3.11+:

1.  **Instalação de Dependências:**
    ```bash
    pip install -r requirements.txt
    ```
2.  **Execução do Pipeline:**
    ```bash
    python analise_eneva.py
    ```

## 📂 Arquitetura de Arquivos
- `analise_eneva.py`: Script principal com a lógica de negócio.
- `requirements.txt`: Lista de bibliotecas e versões específicas.
- `Analise_Eneva_Pedro.xlsx`: Relatório de saída formatado.
- `log.txt`: Rastro de execução do sistema.
- `grafico_comparativo_final.png`: Visualização de tendências anuais.