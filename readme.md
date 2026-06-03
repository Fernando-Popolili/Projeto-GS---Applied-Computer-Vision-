# EpiSat — Applied Computer Vision

> Classificação de áreas ambientais de risco epidemiológico em imagens Sentinel-2

Módulo de Visão Computacional do projeto **EpiSat / Controllus** — Global Solution 2026 · FIAP · Engenharia de Software · 4º Ano

---

##  Integrantes

| Nome                          | RM      |
| ----------------------------- | ------- |
| Augusto Milreu                | RM98245 |
| David Guilherme B. Denunci    | RM98603 |
| Fernando Popolili             | RM99919 |
| Lucas Palamartschuk de Toledo | RM97913 |
| Matheus Zanardi               | RM98832 |

---

##  Sobre o projeto

O EpiSat utiliza imagens do satélite **Sentinel-2 (ESA/Copernicus)** para antecipar surtos de doenças transmitidas por vetores — dengue, malária, leishmaniose e leptospirose — com **2 a 4 semanas de antecedência**.

Este módulo de **Applied Computer Vision (ACV)** treina duas Redes Neurais Convolucionais (**CNNs**) desenvolvidas do zero, sem utilização de modelos pré-treinados, para classificar patches RGB de imagens satelitais em quatro categorias ambientais.

### Classes utilizadas

| Classe            | Relevância                               |
| ----------------- | ---------------------------------------- |
| `corpos_agua`     | Criadouros potenciais de vetores         |
| `vegetacao_densa` | Microambientes de umidade favoráveis     |
| `area_urbana`     | Alta concentração populacional exposta   |
| `area_agricola`   | Irrigação e proximidade de corpos d'água |

---

## Resultados

| Modelo             | Acurácia   | F1-macro   | Parâmetros  |
| ------------------ | ---------- | ---------- | ----------- |
| CNN1 — Baseline    | 92,00%     | 91,94%     | ~540 mil    |
| CNN2 — Aprofundada | **95,83%** | **95,82%** | ~1,2 milhão |

Ambos superam a meta mínima de **88%** exigida pela disciplina.

O modelo deployado na demonstração é a **CNN2**.

---

## Estrutura do repositório

```text
VISÃO COMPUTACIONAL APLICADA/
├── episat-acv/
│   ├── episat_acv_best_model.pt
│   └── episat_acv_metadata.json
│
├── Imagens usadas real/
│   ├── area_urbana.png
│   └── Vegetacao_densa.png
│
├── episat_acv_colab_v2.ipynb
├── EpiSat_ACV_Documentacao.docx
├── README.md
└── requirements.txt
```

---

## 🚀 Como executar

### Opção 1 — Google Colab (recomendado)

1. Abra o notebook `episat_acv_colab_v2.ipynb` no Google Colab.
2. Ative a GPU:

   * Ambiente de execução
   * Alterar tipo de ambiente de execução
   * GPU T4
3. Execute todas as células (`Ctrl + F9`).
4. O download do dataset EuroSAT é realizado automaticamente (~90 MB).
5. Ao final, a interface Gradio será iniciada com um link público temporário.

> Tempo estimado: 15–25 minutos utilizando GPU T4.

### Opção 2 — Ambiente local

**Requisitos:** Python 3.10+ e CUDA (opcional)

```bash
# Clonar o repositório
git clone https://github.com/seu-usuario/episat-acv.git

# Entrar na pasta
cd episat-acv

# Criar ambiente virtual
python -m venv venv

# Linux/Mac
source venv/bin/activate

# Windows
venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Executar notebook
jupyter notebook episat_acv_colab_v2.ipynb
```

---

## Dependências principais

```text
torch>=2.0.0
torchvision>=0.15.0
scikit-learn>=1.3.0
gradio>=4.0.0
matplotlib>=3.7.0
pandas>=2.0.0
pillow>=10.0.0
numpy>=1.24.0
```

Instalação:

```bash
pip install -r requirements.txt
```

---

## Dataset

### EuroSAT RGB

Disponível via:

```python
torchvision.datasets.EuroSAT
```

Características:

* 27.000 imagens originais do satélite Sentinel-2
* Resolução: 64 × 64 pixels
* 3 canais RGB
* Resolução espacial de 10 m/pixel
* Remapeamento de 10 classes originais para **4 classes EpiSat**
* Dataset balanceado

Divisão utilizada:

* Treinamento: 70%
* Validação: 15%
* Teste: 15%

Total utilizado:

* 1.000 imagens por classe
* 4.000 imagens totais

---

##  Demo funcional

A interface Gradio é iniciada automaticamente ao final do notebook.

O usuário envia uma imagem RGB e recebe:

* Classe ambiental prevista
* Probabilidade para cada uma das 4 classes
* Interpretação operacional para o EpiSat

 **Vídeo de demonstração:** *[Inserir link do YouTube]*

---

##  Conexão com a Indústria Espacial

As imagens são derivadas do **Sentinel-2**, satélite da ESA que orbita a aproximadamente **786 km de altitude**, possui revisita de **5 dias** e resolução de **10 metros por pixel**.

Os dados são disponibilizados gratuitamente pelo programa **Copernicus**, viabilizando aplicações de monitoramento ambiental e saúde pública sem custos de aquisição de imagens.

---

##  Documentação

O projeto inclui documentação complementar contendo:

* Fundamentação teórica
* Arquitetura das CNNs
* Metodologia de treinamento
* Resultados experimentais
* Discussão dos resultados

Arquivo:

```text
EpiSat_ACV_Documentacao.docx
```

---

*Global Solution 2026 · FIAP · Turma 4ESPX · Orientador: Paulo Sergio Silva*
