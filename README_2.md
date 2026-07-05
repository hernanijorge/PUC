# MVP - Previsão de Direção do Dólar (DXY) a partir de Notícias do NYT

Autor: Hernani de Paula Jorge · **Matrícula:** 4052023000213
Sprint: Machine Learning & Analytics

## Sobre o projeto
Esse MVP testa se sentimento e volume de notícias econômicas do New York Times,
com defasagem de 1 a 3 dias, ajudam a prever se o índice DXY vai subir ou cair
no dia seguinte. É continuação de um trabalho anterior da Sprint de Análise de
Dados e Boas Práticas (nota 9,5/10), agora com modelagem preditiva completa:
baseline, modelos candidatos, otimização de hiperparâmetros e avaliação crítica
dos resultados.

## Dataset
- Notícias: [`nyt_articles_3_14_2026.csv`](https://raw.githubusercontent.com/hernanijorge/hernanijorge/main/nyt_articles_3_14_2026.csv), artigos reais do NYT coletados via API (01/01/2025 a 14/03/2026).
- Câmbio: índice DXY e USDBRL, baixados durante a execução via `yfinance` (Yahoo Finance), sem precisar de chave de API.

## Como executar
1. Abra `MVP_ML_Analytics_NYT_Dolar.ipynb` no Google Colab.
2. Rode as células em ordem. A primeira célula já instala `vaderSentiment` e
   `yfinance`, e os dados são carregados direto por URL.
3. Não precisa de login, upload manual nem configuração adicional.

## Estrutura do notebook
1. Definição do problema
2. Ambiente, bibliotecas e reprodutibilidade
3. Seleção e carga dos dados
4. Análise exploratória
5. Preparação dos dados e divisão treino/teste (split temporal)
6. Pré-processamento e pipeline
7. Baseline e modelos candidatos
8. Treinamento e avaliação inicial
9. Otimização de hiperparâmetros (RandomizedSearchCV + TimeSeriesSplit)
10. Avaliação final no conjunto de teste
11. Comparação final dos modelos
12. Boas práticas e rastreabilidade
13. Conclusão
14. Salvamento de artefatos

## Principais decisões
- Divisão temporal (não aleatória): os últimos 20% dos dias viram teste, na
  ordem cronológica real.
- Features defasadas (lag 1 a 3): só uso notícias de dias anteriores ao alvo,
  para não vazar informação do próprio dia.
- TimeSeriesSplit na validação cruzada, consistente com a divisão externa.
- VADER para sentimento: leve, sem download de corpus, roda em segundos para
  mais de 50 mil artigos.

## Artefatos gerados
modelo_final_dxy_direction.pkl, dataset_final_nyt_dxy.csv,
comparacao_modelos.csv, além dos gráficos de EDA e avaliação em .png.

## Limitações
Cobertura de um único veículo de imprensa, léxico de sentimento genérico (não
financeiro), dados só diários, sem variáveis macroeconômicas além do próprio
câmbio. Câmbio é um mercado eficiente, então o sinal esperado de sentimento
textual defasado é fraco por natureza. O objetivo aqui é ter um pipeline
correto e uma discussão honesta dos resultados, não uma acurácia inflada.
