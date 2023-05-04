# CUDA Setup

## NVIDIA and TensorFlow

[This guide and linked guides used](https://gist.github.com/p-karanthaker/e9e1f50457ec7db7ebb4904ca9a9f6de)

- Did not use `akmod-nvidia` as kernel updates not done along with software updates
- Uninstall NVIDIA drivers
  - Used `--uninstall` option of lates downloaded version
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
        - Cuda - 11.8.0
          - `conda install -c conda-forge cudatoolkit=11.8.0`
        - cuDNN - 8.9.0.131
          - `pip install nvidia-cudnn-cu12=8.9.0.131`
          - NOTE: Don't forget the environment setup!
      - Install TensorFlow
        - `pip install tensorflow=2.12.*`
        - Also installed the following missing dependencies
          ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
          qtconsole 5.4.2 requires pygments, which is not installed.
          pandas 2.0.1 requires pytz>=2020.1, which is not installed.
          nbconvert 7.3.1 requires beautifulsoup4, which is not installed.
          nbconvert 7.3.1 requires jinja2>=3.0, which is not installed.
          nbconvert 7.3.1 requires pygments>=2.4.1, which is not installed.
          nbclassic 0.5.6 requires jinja2, which is not installed.
          moderngl-window 2.4.2 requires Pillow<10,>=9, which is not installed.
          matplotlib 3.6.0 requires pillow>=6.2.0, which is not installed.
          matplotlib 3.6.0 requires pyparsing>=2.2.1, which is not installed.
          manimgl 1.6.1 requires Pillow, which is not installed.
          manimgl 1.6.1 requires pygments, which is not installed.
          manimgl 1.6.1 requires pyyaml, which is not installed.
          jupyter-server 2.5.0 requires jinja2, which is not installed.
          jupyter-server 2.5.0 requires websocket-client, which is not installed.
          jupyter-events 0.6.3 requires jsonschema[format-nongpl]>=3.2.0, which is not installed.
          jupyter-events 0.6.3 requires pyyaml>=5.3, which is not installed.
          ipykernel 6.22.0 requires psutil, which is not installed.
      - Setup environment
      - Verify install - Section 6
  - Try here and see if it finally works
    - NOTE: Must use activated `tf` environment