# 😷 Classificação de Máscara Facial com Deep Learning (AlexNet vs VGG16)

## 🎯 1. Objetivo do Projeto

Este projeto realiza uma **análise comparativa** detalhada entre duas arquiteturas de Redes Neurais Convolucionais (CNN) clássicas, **AlexNet** e **VGG16**, na tarefa de classificação binária de imagens de uso de máscara facial.

O foco é determinar qual arquitetura oferece a melhor **capacidade de generalização** e **confiabilidade** para a aplicação, avaliando a estabilidade do treinamento e, criticamente, o desempenho no conjunto de Teste (Matriz de Confusão).

## 💻 2. Como Executar (Google Colab)

O projeto foi configurado para ser executado integralmente no ambiente **Google Colab**, pois utiliza o hardware com GPU e exige a autenticação via API do Kaggle para acesso ao dataset.

### 2.1. Pré-requisitos

1.  **Conta Kaggle:** Você deve ter uma conta no [Kaggle](https://www.kaggle.com/).
2.  **Chave de API (`kaggle.json`):** Baixe seu arquivo `kaggle.json` gerado na seção "Settings" do Kaggle (vá em "API" e clique em "Create New Token"). Este arquivo é sua chave de autenticação.
3.  **Ambiente Colab:** Abra um novo Notebook no Google Colab.

### 2.2. Passos para Execução

**Atenção:** Os comandos de autenticação e download devem ser rodados em uma célula de código no Colab antes do código principal (`projeto1_(visão)_8132.py`).

| Passo | Ação | Comando Colab |
| :--- | :--- | :--- |
| **1. Upload da Chave** | Carrega o arquivo `kaggle.json` no ambiente Colab. | `from google.colab import files`<br>`files.upload()` |
| **2. Configuração do Kaggle** | Configura a chave de API para que o Kaggle possa ser acessado via linha de comando. | `!mkdir -p ~/.kaggle`<br>`!cp kaggle.json ~/.kaggle/`<br>`!chmod 600 ~/.kaggle/kaggle.json` |
| **3. Download e Descompactação** | Baixa e descompacta o dataset `covid-face-mask-detection-dataset`. | `!kaggle datasets download -d prithwirajmitra/covid-face-mask-detection-dataset`<br>`!unzip covid-face-mask-detection-dataset.zip`<br>`print("Download e Descompactação Concluídos")` |
| **4. Execução do Código** | Insira o conteúdo completo do arquivo `projeto1_(visão)_8132.py` na próxima célula e execute. | `python projeto1_(visão)_8132.py` (ou simplesmente cole o código e execute) |

## 📊 3. Metodologia

O projeto empregou o Transfer Learning com pesos pré-treinados no ImageNet para ambas as arquiteturas. As camadas de extração de características foram congeladas, treinando apenas as camadas densas finais para a classificação binária. O treinamento foi realizado por **50 épocas**.

## 📈 4. Resultados Finais

A avaliação comparativa do desempenho no conjunto de **Teste** foi decisiva:

| Métrica | VGG16 | AlexNet | Nota |
| :--- | :--- | :--- | :--- |
| **Acurácia de Teste** | $\mathbf{100\%}$ | $99,35\%$ | VGG16 eliminou todos os erros. |
| **Falsos Negativos (FN)** | $\mathbf{0}$ | 1 | AlexNet falhou em 1 caso "Com Máscara". |
| **Robustez (\textit{Val Loss})** | Alta Estabilidade | Baixa Estabilidade | VGG16 mostrou menor suscetibilidade ao overfitting. |

### Conclusão

O modelo **VGG16 é o mais recomendado** para esta aplicação. Embora a AlexNet tenha atingido um pico de acurácia de validação similar, a VGG16 demonstrou generalização perfeita -> 100% de acurácia com zero erros críticos) no conjunto de teste, o que é fundamental para sistemas que exigem máxima confiabilidade e segurança.
