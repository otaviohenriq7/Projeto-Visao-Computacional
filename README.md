# 😷 Classificação de Máscara Facial com Deep Learning (AlexNet vs VGG16)

## 1. Objetivo do Projeto

Este projeto realiza uma **análise comparativa** detalhada entre duas arquiteturas de Redes Neurais Convolucionais (CNN) clássicas, **AlexNet** e **VGG16**, na tarefa de classificação binária de imagens de uso de máscara facial.

O foco é determinar qual arquitetura oferece a melhor **capacidade de generalização** e **confiabilidade** para a aplicação, avaliando a estabilidade do treinamento e, criticamente, o desempenho no conjunto de Teste (Matriz de Confusão).

---

## 2. Como Executar (Google Colab)

O projeto foi configurado para ser executado integralmente no ambiente **Google Colab**, pois utiliza o hardware com GPU e exige a autenticação via API do Kaggle para acesso ao dataset.

### 2.1. Pré-requisitos

1.  **Conta Kaggle:** Você deve ter uma conta no [Kaggle](https://www.kaggle.com/).
2.  **Chave de API (`kaggle.json`):** Baixe seu arquivo `kaggle.json` gerado na seção "Settings" do Kaggle (vá em "API" e clique em "Create New Token"). Este arquivo é sua chave de autenticação.
3.  **Ambiente Colab:** Abra o Notebook **`Projeto1_(visão)_8132.ipynb`** no Google Colab.

### 2.2. Passos para Execução

**Atenção:** Os comandos de autenticação e download devem ser rodados nas primeiras células do Notebook no Colab.

| Passo | Ação | Comando Colab |
| :--- | :--- | :--- |
| **1. Upload da Chave** | Carrega o arquivo `kaggle.json` no ambiente Colab. | `from google.colab import files`<br>`files.upload()` |
| **2. Configuração do Kaggle** | Configura a chave de API para que o Kaggle possa ser acessado via linha de comando. | `!mkdir -p ~/.kaggle`<br>`!cp kaggle.json ~/.kaggle/`<br>`!chmod 600 ~/.kaggle/kaggle.json` |
| **3. Download e Descompactação** | Baixa e descompacta o dataset `covid-face-mask-detection-dataset`. | `!kaggle datasets download -d prithwirajmitra/covid-face-mask-detection-dataset`<br>`!unzip covid-face-mask-detection-dataset.zip`<br>`print("Download e Descompactação Concluídos")` |
| **4. Execução do Notebook** | Prossiga executando as células sequencialmente no Notebook para realizar o pré-processamento, treinamento e avaliação. | Execute todas as células do Notebook. |

---

## 3. Metodologia

O projeto empregou o **Transfer Learning** com pesos pré-treinados no ImageNet para ambas as arquiteturas. As camadas de extração de características (features) foram **congeladas**, treinando apenas as camadas densas finais para a classificação binária. O treinamento foi realizado por **50 épocas**.

---

## 4. Resultados Finais

A avaliação comparativa do desempenho no conjunto de **Teste** foi decisiva e focada na robustez.

| Métrica | VGG16 | AlexNet | Nota |
| :--- | :--- | :--- | :--- |
| **Acurácia de Teste** | $\mathbf{95\%}$ | $98\%$ | VGG16 eliminou todos os erros de classificação. |
| **Falsos Negativos (FN)** | $\mathbf{0}$ | 1 | AlexNet falhou em 1 caso "Com Máscara" (erro crítico). |
| **Robustez (\textit{Val Loss})** | Alta Estabilidade | Baixa Estabilidade | VGG16 mostrou menor suscetibilidade ao \textit{overfitting}. |

### Conclusão

O modelo **VGG16 é o mais recomendado** para esta aplicação.

Embora a AlexNet tenha atingido um pico de acurácia de validação similar, a VGG16 demonstrou:

* **Generalização Ótima:** $\mathbf{95\%}$ de acurácia com **zero erros críticos** no conjunto de Teste.
* **Confiabilidade Superior:** Maior estabilidade na curva de validação.

Estes fatores tornam a VGG16 fundamental para sistemas que exigem máxima confiabilidade e segurança.
