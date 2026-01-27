# Build Pytorch for Debian from source code
```
# The following commands were tested on my singapore dev-box.
# Step1: Requirements: python 3.10 or later, gcc 9.3 or later
conda create -n test python=3.10
conda activate test
conda install -c conda-forge cmake
conda install -c conda-forge gcc
conda install -c conda-forge gxx

# Step2: Force cmake to use installed gcc and g++
export CC=$(which gcc)
export CXX=$(which g++)

# Step3: Clone Pytorch source code
git clone https://gitee.com/sswen427/pytorch.git
cd pytorch
git submodule sync
git submodule update --init --recursive
pip install -r requirements.txt

# Step4: Make sure the source code is clean
# It's mainly used to clean the cmake cache
git clean -dfx

# Step5: Build Pytorch
USE_MPI=0 python setup.py develop

# Step6: Test Pytorch
python -c "
import torch
import sys

print('PyTorch', torch.__version__, 'installed successfully!')
print('Location:', torch.__file__)
print('CUDA:', 'Available' if torch.cuda.is_available() else 'Not Available')

if hasattr(torch.backends, 'mps'):
    print('MPS:', 'Available' if torch.backends.mps.is_available() else 'Not Available')

print('Test computation:', torch.tensor([1,2,3]) + torch.tensor([4,5,6]))
"
```

# Build Pytorch for MacOS from source code

```
# The following commands were tested on my MacBook Pro with M1 chip.
# Step1: Create a conda environment
conda create -n test python=3.10
conda activate test

# Step2: Clone Pytorch source code
git clone https://gitee.com/sswen427/pytorch.git
git submodule sync
git submodule update --init --recursive
pip install -r requirements.txt

# Step3: Build Pytorch
python setup.py develop

# Step4: Test Pytorch
python -c "
import torch
import sys

print('PyTorch', torch.__version__, 'installed successfully!')
print('Location:', torch.__file__)
print('CUDA:', 'Available' if torch.cuda.is_available() else 'Not Available')

if hasattr(torch.backends, 'mps'):
    print('MPS:', 'Available' if torch.backends.mps.is_available() else 'Not Available')

print('Test computation:', torch.tensor([1,2,3]) + torch.tensor([4,5,6]))
"
```

# Debug All CPP Code
```
rm -rf build
DEBUG=1 BUILD_TEST=1 python setup.py build
```

# Tips
```
# clean DNS dirty cache, execute it when download failed
sudo killall -HUP mDNSResponder

# Try the following command if the above command failed.
# HTTP 1.1 is more robust than HTTP 2.0 when the network is not stable.
# git -c http.version=HTTP/1.1 submodule update --init --recursive

```
