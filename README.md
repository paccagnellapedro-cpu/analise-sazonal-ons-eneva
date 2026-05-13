# Análise de Sazonalidade e Tendência de Carga Global: SIN (2021-2023)

## Visão Geral do Projeto
Este sistema foi desenvolvido para automatizar o ciclo de vida de dados (extração, tratamento e análise) da carga verificada do Sistema Interligado Nacional (SIN). Utilizando dados brutos da API do Operador Nacional do Sistema Elétrico (ONS), a solução fornece subsídios estatísticos para a compreensão de variações sazonais e o planejamento energético.
## Funcionalidades Detalhadas

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

## Análise Técnica e Interpretação dos Resultados

Abaixo, detalha-se a lógica analítica aplicada aos outputs gerados, correlacionando os dados estatísticos com o cenário do setor elétrico brasileiro:

### 1. Dinâmica de Recuperação da Carga (2021-2023)
Através da aba `Crescimento_Delta` do relatório, observa-se a trajetória de recuperação da carga do SIN. Enquanto 2021 apresentava reflexos de restrições de despacho por crise hídrica, 2023 consolidou um novo patamar de demanda. O crescimento detectado não é linear, exigindo uma gestão fina da reserva de potência.

### 2. Anomalia de Demanda Térmica (Primavera de 2023)
O gráfico de tendência (`grafico_comparativo_final.png`) revela um descolamento atípico das curvas de carga no segundo semestre de 2023.
* **Diagnóstico:** A carga na **Primavera de 2023** superou médias históricas devido às ondas de calor intensificadas pelo fenômeno **El Niño**.
* **Impacto:** Evidencia a crescente sensibilidade do SIN à demanda térmica (climatização), fator crítico para o planejamento de despacho termelétrico.

### 3. Utilidade Estratégica para a Operação
Diferente de uma análise puramente acadêmica, esta ferramenta suporta decisões operacionais:
* **Previsibilidade de Despacho:** Identifica janelas críticas para manutenção e disponibilidade de combustível.
* **Estratégia de Oferta:** A métrica de *Delta* por estação auxilia na mensuração de risco e volatilidade de carga.

## Requisitos de Execução
O projeto foi estruturado para ser 100% compatível com ambientes Windows e Python 3.11+:

1. **Clonar o repositório e acessar a pasta do projeto:**
   Abra o seu terminal (Prompt de Comando ou PowerShell) e execute:
   ```bash
   git clone [https://github.com/paccagnellapedro-cpu/analise-sazonal-ons-eneva.git](https://github.com/paccagnellapedro-cpu/analise-sazonal-ons-eneva.git)
   cd analise-sazonal-ons-eneva

2.  **Instalação de Dependências:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Execução do Pipeline:**
    ```bash
    python analise_eneva.py
    ```

## Arquitetura de Arquivos
- `analise_eneva.py`: Script principal com a lógica de negócio.
- `requirements.txt`: Lista de bibliotecas e versões específicas.
- `Analise_Eneva_Pedro.xlsx`: Relatório de saída formatado.
- `log.txt`: Rastro de execução do sistema.
- `grafico_comparativo_final.png`: Visualização de tendências anuais.
