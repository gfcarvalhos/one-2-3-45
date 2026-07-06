# README: One-2-3-45: Single Image to 3D Mesh

Este notebook Colab implementa o modelo 'One-2-3-45' para gerar meshes 3D a partir de uma única imagem. Ele configura o ambiente, instala as dependências necessárias, baixa os checkpoints do modelo e executa a inferência para converter imagens 2D em modelos 3D, além de permitir a visualização dos resultados.

## Setup Inicial

**Requisitos de Runtime:**
- Runtime: `2025.07`
- GPU: A100 (ou compatível com alta RAM)

**Passos:**
1. Certifique-se de que o runtime do Colab está configurado conforme os requisitos (GPU A100, alta RAM).
2. Rode todas as células na ordem. Após a Célula 2, o Colab pode pedir para reiniciar o runtime — faça isso e continue a partir da Célula 3.

### Clonar Repositório
Para começar, clone o repositório do projeto. Se você já tem o código no seu Google Drive, pode pular esta etapa e ajustar o `PROJECT_DIR` na Célula 3.

```bash
!git clone https://github.com/your_username/One-2-3-45-master.git
# Substitua 'your_username' pelo nome de usuário ou organização do repositório original, se disponível.
```

## Fluxo do Notebook

### Célula 1 — Instalar PyTorch 2.1 + CUDA 12.1
Esta célula substitui a versão padrão do PyTorch no Colab por uma versão específica (2.1 + CUDA 12.1) que é compatível com a biblioteca `torchsparse` utilizada pelo projeto. Isso garante que todas as dependências funcionem corretamente juntas.

### Célula 2 — Instalar TorchSparse v1.4.0
Compila e instala a biblioteca `TorchSparse` versão 1.4.0 com suporte a CUDA. Este é um passo crucial para o desempenho do modelo. **IMPORTANTE:** Após a execução desta célula, se o Colab solicitar, **REINICIE O RUNTIME** (`Runtime > Restart runtime`) antes de prosseguir para a Célula 3.

### Célula 3 — Montar Drive e configurar projeto
Monta seu Google Drive no ambiente do Colab para acessar arquivos e salvar resultados. Você precisará **AJUSTAR O CAMINHO DA PASTA (`PROJECT_DIR`)** para onde o repositório 'One-2-3-45-master' está localizado no seu Drive. A célula também verifica a versão do PyTorch, CUDA e a GPU em uso.

### Célula 4 — Instalar dependências Python
Instala todas as bibliotecas Python adicionais necessárias para o projeto, como `albumentations`, `opencv-python`, `pytorch-lightning`, `diffusers`, `CLIP`, `segment-anything`, entre outras. Também inclui um patch para garantir a compatibilidade com a versão do PyTorch e NumPy.

### Célula 5 — Download dos Checkpoints (apenas primeira vez)
Esta célula gerencia o download dos checkpoints do modelo necessários para a inferência. Os arquivos são salvos no seu Google Drive (cerca de 10 GB). O script verifica se os checkpoints já existem e baixa apenas os que estiverem faltando, economizando tempo e banda.

### Célula 6 — Executar Inferência
Executa o processo de inferência para gerar um mesh 3D a partir de uma imagem de exemplo (`./demo/demo_examples/01_wild_hydrant.png`). O tempo estimado de processamento é de aproximadamente 2-3 minutos em uma GPU A100. O output é um arquivo `.ply` (mesh 3D).

### Célula 7 — Usar sua própria imagem
Permite que você processe suas próprias imagens localizadas na pasta `./inputs/edited/`. A célula itera sobre todas as imagens encontradas nessa pasta e executa a inferência 3D para cada uma, gerando os respectivos meshes. Se quiser usar uma imagem de outro local no seu Drive, use a **Opção B** na célula `a4pbp5xPwsiQ`, descomentando e ajustando o caminho.

### Célula 8 — Visualizar resultados
Esta seção contém duas células para visualizar os resultados:

- **Visualização de Meshes 3D (`qbJY06U_BBqv`):** Carrega e exibe os arquivos `.ply` gerados usando `plotly.graph_objects.Mesh3d`, permitindo uma inspeção interativa dos modelos 3D.
- **Visualização das Views (`Yel9KzgiwsiQ`):** Exibe as diferentes vistas 2D (views) geradas durante o processo de inferência, que são usadas para construir o modelo 3D. Isso ajuda a entender como o modelo 'enxerga' o objeto antes da reconstrução final.

### Célula Final — Copiar Meshes para a Pasta de Saída
Esta célula coleta todos os arquivos `mesh.ply` gerados nas pastas de experimento (`./exp/`) e os copia para uma pasta centralizada `./outputs/`. Isso facilita o acesso e a organização de todos os modelos 3D resultantes do processamento.