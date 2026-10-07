FROM dockerdex.umcn.nl:5005/diag/base-images:base-pt2.7.1

ENV PIP_NO_CACHE_DIR=1

RUN python3 -m pip install --upgrade pip setuptools wheel
RUN python3 -m pip install --no-cache-dir numpy scipy tqdm torch monai[all] transformers

RUN python3 -m pip install --no-cache-dir "spectre-fm[training]==0.2.1"

ENTRYPOINT ["/bin/bash"]
