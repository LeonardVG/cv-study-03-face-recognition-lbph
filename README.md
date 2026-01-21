# Estudo 03: Reconhecimento Facial com LBPH

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square)
![OpenCV](https://img.shields.io/badge/OpenCV-Contrib-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Educational-orange)

Terceiro projeto da série de estudos em Visão Computacional. Após aprender a **detectar** onde estão os rostos (Haar Cascade e HOG), este repositório foca no passo seguinte: **reconhecer** a identidade da pessoa.

Para isso, implementamos o algoritmo **LBPH** (Local Binary Patterns Histograms), que é robusto, leve e eficiente para aprendizado supervisionado.

## 📂 Sobre o Dataset (Yale Faces)

Neste estudo, utilizamos a clássica base de dados **Yale Faces Database**.
* **O que é:** Um conjunto de imagens contendo 15 indivíduos em 11 condições diferentes (luz central, luz lateral, feliz, triste, com óculos, etc.).
* **Objetivo:** Testar a capacidade do algoritmo de reconhecer a mesma pessoa mesmo com mudanças de iluminação e expressão.
* **Download:** O link direto para download do dataset encontra-se **dentro do notebook**.

## ⚠️ Requisitos Críticos de Instalação

O algoritmo LBPH **não** está incluído na instalação padrão do OpenCV. Ele faz parte do pacote `opencv-contrib` (módulos extras).

### Se você estiver usando Google Colab:
Você encontrará o seguinte erro ao tentar usar `cv2.face`:
> `AttributeError: module 'cv2.face' has no attribute 'LBPHFaceRecognizer_create'`

**Solução:**
É necessário desinstalar a versão padrão e instalar a versão completa. O notebook já contém os comandos, mas fique atento a este passo:

1.  Execute a instalação:
    ```python
    !pip uninstall opencv-python -y
    !pip install opencv-contrib-python-headless
    ```
2.  **OBRIGATÓRIO:** Após a instalação, reinicie o ambiente de execução (*Runtime > Restart Session*) para que a nova biblioteca seja carregada.

---

## ⚙️ Configuração de Caminhos (Google Drive)

O código deste projeto foi estruturado para rodar no Google Colab lendo arquivos diretamente do **Google Drive**.

```python
# Exemplo de caminho usado no código
paths = [os.path.join('/content/drive/MyDrive/SeuCaminho/YaleFaces', f) for f in os.listdir(...)]
```

## Como executar sem erros

### Se usar Drive
- Monte o drive (`drive.mount`) e ajuste o caminho da variável para onde você salvou a pasta **YaleFaces** no seu Drive.

### Se usar Upload Manual
- Se preferir fazer upload das imagens na sessão temporária do Colab, altere os caminhos no código para remover a parte  
  `/content/drive/MyDrive/...`.

---

## 🧠 Como funciona o LBPH?

O **Local Binary Patterns Histograms (LBPH)** analisa a textura local da imagem.

- **Raio e Vizinhos:** Para cada pixel, ele compara o valor com seus vizinhos.  
- **Padrão Binário:** Gera um código binário baseado na diferença de intensidade (pixel mais claro ou mais escuro que o centro).  
- **Grades (Grid X/Y):** A imagem é dividida em regiões (ex: 8x8). Histogramas são criados para cada região e concatenados.  
- **Reconhecimento:** O sistema compara o histograma da nova face com os salvos no treinamento.

---

## Entendendo o Resultado (Confidence)

O retorno `confidence` do OpenCV funciona como uma medida de distância/diferença:

- **Valor Baixo (< 50):** Alta similaridade. O algoritmo tem certeza de que é a pessoa.  
- **Valor Alto (> 80):** Baixa similaridade. O rosto é muito diferente do aprendido.

---

## 🛠️ Tecnologias

- Python  
- OpenCV (`cv2.face`)  
- Numpy  
- Pillow (PIL)

---

## 📂 Estrutura da Série de Estudos

- **cv-study-01-haarcascade** – Detecção facial básica.  
- **cv-study-02-dlib-face-detection** – Comparativo HOG vs CNN.  
- **cv-study-03-face-recognition-lbph** – Reconhecimento Facial (este repositório).

---

Desenvolvido para fins de estudo acadêmico em **Visão Computacional**.
