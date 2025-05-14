# Compile and test example

Compile the example:

```shell
nvcc -o hello_houston.exe hello_houston.cu
```

Run the example:

```shell
./hello_houston.exe
This is Houston. Say again, please.                 From Base
Houston, we have a problem in section [0,0]         From Apollo 13
Houston, we have a problem in section [1,0]         From Apollo 13
Houston, we have a problem in section [0,1]         From Apollo 13
Houston, we have a problem in section [1,1]         From Apollo 13
```

## Run workflow locally

Requirements:
- Docker
- NVIDIA container toolkit
- [act](https://nektosact.com/)

Make sure following command works:
```shell
docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```

Run workflow with:
```shell
act \
-P ubuntu-latest=nvidia/cuda:12.8.1-devel-ubuntu24.04 \
--container-options "--runtime=nvidia --gpus all" \
-W .github/workflows/self_hosted_ci.yml
# Should run nvdia-smi, compile with nvcc and run the compiled executable
```
(If your workflow does not use `runs-on: ubuntu-latest` then update the `-P` option accordingly.)
(Match the nvidia/cuda image tag with the cuda version reported by `nvidia-smi`)
