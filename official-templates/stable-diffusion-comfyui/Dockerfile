FROM runpod/base:0.6.3-cuda12.4.1

ARG COMFYUI_VERSION

WORKDIR /ComfyUI

# Setup Python and pip symlinks
RUN ln -sf /usr/bin/python3.10 /usr/bin/python && \
    ln -sf /usr/bin/python3.10 /usr/bin/python3 && \
    python -m pip install --upgrade pip && \
    ln -sf /usr/local/bin/pip3.10 /usr/local/bin/pip

# Install ComfyUI and ComfyUI Manager
RUN git init && \
    git remote add origin https://github.com/comfyanonymous/ComfyUI.git && \
    git fetch --depth 1 origin tag ${COMFYUI_VERSION} && \
    git checkout FETCH_HEAD && \
    pip install -r requirements.txt && \
    git clone https://github.com/ltdrdata/ComfyUI-Manager.git custom_nodes/ComfyUI-Manager && \
    cd custom_nodes/ComfyUI-Manager && \
    pip install -r requirements.txt

# Create user directory to store logs
RUN mkdir -p user

# Copy the README.md, extra_model_paths.yml and start script
COPY README.md /usr/share/nginx/html/README.md
COPY extra_model_paths.yml extra_model_paths.yml
COPY --chmod=755 pre_start.sh /pre_start.sh

CMD [ "/start.sh" ]
