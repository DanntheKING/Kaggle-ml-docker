FROM nvidia/cuda:12.1.1-devel-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /app

RUN apt-get update && apt-get install -y git-lfs

# Install system dependencies
RUN apt-get update && apt-get install -y \
    python3 python3-pip python3-dev build-essential libatlas-base-dev \
    libffi-dev libopenblas-dev libomp-dev curl git \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PyTorch first
RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

# Install other libraries
RUN pip3 install --no-cache-dir \
    jupyterlab notebook ipywidgets pandas numpy matplotlib \
    pytorch-forecasting seaborn

# Expose Jupyter Notebook port
EXPOSE 8888

# Set default command to launch Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root", "--NotebookApp.token=''"]
