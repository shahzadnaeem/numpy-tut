# Machine Learning Course Notes

## TensorFlow with NVIDIA GPU Support

A separate environment was created using [Miniconda](https://docs.conda.io/en/latest/miniconda.html) as directed by the [TensorFlow docs](https://www.tensorflow.org/install/pip)

The existing manually installed Fedora 36 NVIDIA Drivers were uninstalled and replaced by a `dnf` installation of the `cuda` meta-package

This was followed by quite a few steps to enable TensorFlow to use the NVIDIA GPU

[This guide and linked guides used](https://gist.github.com/p-karanthaker/e9e1f50457ec7db7ebb4904ca9a9f6de)

- Did not use `akmod-nvidia` as kernel updates not done along with software updates
- Uninstall NVIDIA drivers
  - Used `--uninstall` option of latest downloaded version
- Switch to non-graphical UI and reboot
- Add fedora36 repo for CUDA and install `cuda`
  - `sudo dnf install cuda`
  - Lots gets installed
- Switch back to graphical UI and reboot
  - Gnome desktop should come back
- Install [TensorFlow as directed](https://www.tensorflow.org/install/pip)
  - Miniconda
    - Create a `tf` environment
    - Activate to set up
      - Install Cuda and cuDNN
        - Cuda Toolkit - 11.8.0
          - `conda install -c conda-forge cudatoolkit=11.8.0`
        - cuDNN - 8.9.0.131 (on CUDA 12)
          - `pip install nvidia-cudnn-cu12=8.9.0.131`
          - NOTE: Don't forget the environment setup!
      - Install TensorFlow
        - `pip install tensorflow=2.12.*`
          - A number of missing dependencies were listed and needed to be added to allow execution of notebooks in VSCode
            - `pip install cffi psutil decorator pexpect pygments jsonschema pyyaml jinja2 websocket-client pillow pyparsing beautifulsoup4 pytz ptyprocess`
      - Setup environment

        ```bash
        $ mkdir -p $CONDA_PREFIX/etc/conda/activate.d
        $ echo 'CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
        $ echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/:$CUDNN_PATH/lib' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
        ```

      - Verify install - Section 6
  - Try here and see if it finally works
    - NOTE: Must use activated `tf` conda environment
  
      ```bash
      $ conda activate tf
      $ cd ~/projects/ml/numpy-tut
      $ code .
      ```

      ```text
      Run `simple-lr.ipynb`
        NOTE: IT WORKS!
      ```
