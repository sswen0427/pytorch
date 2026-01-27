# Build Pytorch from Source

```
# clean DNS dirty cache, execute it when download failed
sudo killall -HUP mDNSResponder
# HTTP 1.1 is more stable than HTTP 2.0
git config http.version HTTP/1.1

git clone https://gitee.com/sswen427/pytorch.git
git submodule sync
git submodule update --init --recursive
# or git -c http.version=HTTP/1.1 submodule update --init --recursive

conda create -n test python=3.10
conda activate test
pip install -r requirements.txt

export USE_NCCL=0
python setup.py develop
```
