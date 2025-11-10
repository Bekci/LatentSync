This is a fork of the original LatentSync repository for experiementing on below topics

* How to improve runtime of the inference. Switch to [runtime-exps](https://github.com/Bekci/LatentSync/tree/runtime-exps) branch for the changes.
* How to improve quality of the lip-sync. Switch to [sync-improvement](https://github.com/Bekci/LatentSync/tree/sync-improvement) branch for the changes.

The setup of the project is the same with the original. A reference [notebook](notebooks/runtime_exps.ipynb) provides commands to run in Google colab.

## 🔧 Setting up the Environment

Install the required packages and download the checkpoints via:

```bash
source setup_env.sh
```

If the download is successful, the checkpoints should appear as follows:

```
./checkpoints/
|-- latentsync_unet.pt
|-- whisper
|   `-- tiny.pt
```

Or you can download `latentsync_unet.pt` and `tiny.pt` manually from our [HuggingFace repo](https://huggingface.co/ByteDance/LatentSync-1.6)


### For Quality Experiments
For quality experiments run below commands to setup environment:

```[bash]
sudo apt-get install espeak-ng
pip install tiktoken
pip install phonemizer

rm -r './latentsync/whisper/whisper'
cd ..
git clone 'https://github.com/openai/whisper.git'
cp -r 'whisper/whisper' './LatentSync/latentsync/whisper/whisper'
cd LatentSync
```

## 🚀 Inference

Minimum VRAM for inference:

- **8 GB** with LatentSync 1.5
- **18 GB** with LatentSync 1.6

There are two ways to perform inference:


### 2. Command Line Interface

Run the script for inference:

```bash
./inference.sh
```

You can try adjusting the following inference parameters to achieve better results:

- `inference_steps` [20-50]: A higher value improves visual quality but slows down the generation speed.
- `guidance_scale` [1.0-3.0]: A higher value improves lip-sync accuracy but may cause the video distortion or jitter.

## Runtime Experiment Results