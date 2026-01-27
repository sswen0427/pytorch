# Build Pytorch from Source

```
git clone https://gitee.com/sswen427/pytorch.git
git submodule sync
git submodule update --init --recursive

conda create -n test python=3.10
conda activate test
pip install -r requirements.txt

export USE_CUDA=0
python setup.py develop
```

# Tips
```
# clean DNS dirty cache, execute it when download failed
sudo killall -HUP mDNSResponder

# Try the following command if the above command failed.
# HTTP 1.1 is more robust than HTTP 2.0 when the network is not stable.
# git -c http.version=HTTP/1.1 submodule update --init --recursive

```
