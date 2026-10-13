FROM dockerdex.umcn.nl:5005/diag/base-images:base-pt2.7.1

ENV PIP_NO_CACHE_DIR=1

RUN python3 -m pip install --upgrade pip setuptools wheel
RUN python3 -m pip install --no-cache-dir numpy scipy tqdm torch monai[all] transformers

RUN python3 -m pip install --no-cache-dir "spectre-fm[training]==0.2.1"

# Fix negative NumPy strides in Spectre's load_ct() 
RUN python3 - <<'PY' 
from pathlib import Path 
import spectre.io 
path = Path(spectre.io.__file__) 
source = path.read_text() 

old = "torch.from_numpy(array).to(dtype).unsqueeze(0)" 
new = "torch.from_numpy(np.ascontiguousarray(array)).to(dtype).unsqueeze(0)" 

if old not in source: 
    raise RuntimeError( f"Expected code not found in {path}. Inspect spectre/io.py and apply the fix manually." ) 
    
path.write_text(source.replace(old, new, 1)) 
print(f"Patched {path}") 
PY

ENTRYPOINT ["/bin/bash"]
