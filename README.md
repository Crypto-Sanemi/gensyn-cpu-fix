# How to Fix Gensyn RL-Swarm CPU bf16/gpu Error
A simple guide to understand why this error occurs and how to fix it for CPU-only setups.

<img width="1248" height="614" alt="image" src="https://github.com/user-attachments/assets/0886c5c3-ed54-4433-955c-7cb86cbb1e9c" />


## 🛑 The Error
When running Gensyn RL-Swarm node in CPU mode, you may see the following error
`Your setup doesn't support bf16/gpu`

---
## 🧠 Why Does This Happen?

The RL training configuration **defaults to `bf16` (bfloat16) precision**, which requires GPU support. On a CPU-only setup, this precision is **not available**, causing the trainer to fail.

- **bf16 (bfloat16)**: a data type optimized for faster training on modern GPUs.
- On systems **without a GPU**, you must force the node to run in CPU mode to avoid this error.

---
## ⚙️ Step-by-Step Fix

### 1. Locate the config file

File can be found at:
```sh
rl-swarm/rgym_exp/config/rg-swarm.yaml
```

---
### 2. Edit `rg-swarm.yaml`

Open it and scroll to the game_manager.trainer.config section and add the line bf16: false
```sh
nano rl-swarm/rgym_exp/config/rg-swarm.yaml
```

<img width="1047" height="821" alt="image" src="https://github.com/user-attachments/assets/0aa289ff-4341-49d8-985f-6e975c2f088f" />

---
### 3. Run the node again
```sh
docker compose run --rm --build -Pit swarm-cpu
```

### 💡 Tips & Notes

***GPU Usage:*** If you have a GPU available, you can re-enable bf16 for faster training. Make sure your environment supports GPU and PyTorch’s bfloat16 operations.

***FP16 Setting:*** Keep fp16: ${training.fp16}; it can also be enabled if your GPU supports mixed precision.

***Configuration Backup:*** Always back up rg-swarm.yaml before making edits.

***Further Resources:***
* https://docs.gensyn.ai/testnet/rl-swarm
* https://github.com/0xmoei/gensyn-ai

## Conclusion
By disabling bf16 in the configuration, you can run Gensyn RL-Swarm in CPU mode without encountering GPU-only errors.

Hope this guide helps, now proceedtraining your RL-Swarm CPU node.


