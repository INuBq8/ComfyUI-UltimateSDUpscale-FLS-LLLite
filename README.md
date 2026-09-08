# ComfyUI Ultimate SD Upscale FLS LLLite

ComfyUI custom nodes that extend the Ultimate SD Upscale tile workflow with an FLS-style sampling path and an optional Anima Tile/Repair ControlNet-LLLite conditioning step.

This repository contains only the custom node code. It does not include workflows, checkpoints, LoRAs, ControlNet/LLLite weights, upscale models, generated images, API keys, or environment-specific configuration.

## Nodes

The package registers two nodes:

- `UltimateSDUpscaleFLS`
  - Display name: `Ultimate SD Upscale (FLS Accelerated)`
  - Category: `image/upscaling`
- `UltimateSDUpscaleFLSLLLite`
  - Display name: `Ultimate SD Upscale (FLS + LLLite Tile Repair)`
  - Category: `image/upscaling`

Both nodes keep the usual Ultimate SD Upscale inputs for image, model, conditioning, VAE, upscale model, seed, sampler, scheduler, denoise, tile size, padding, mask blur, seam fix, and tiled decode options.

## Extra Controls

FLS controls:

- `fovea_strength`
- `sharpness`
- `mask_inertia`

LLLite controls, only on `UltimateSDUpscaleFLSLLLite`:

- `lllite_model_name`
- `lllite_strength`
- `lllite_start_percent`
- `lllite_end_percent`

`lllite_model_name` is read from ComfyUI's `controlnet` model folder.

## Installation

Clone into `ComfyUI/custom_nodes`:

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/Lebensignal/ComfyUI-UltimateSDUpscale-FLS-LLLite.git
```

Restart ComfyUI.

On first import, this package creates `repositories/ultimate_sd_upscale` and downloads the original Coyote-A Ultimate SD Upscale script if it is missing.

For offline installation, manually place the contents of:

```text
https://github.com/Coyote-A/ultimate-upscale-for-automatic1111
```

inside:

```text
ComfyUI/custom_nodes/ComfyUI-UltimateSDUpscale-FLS-LLLite/repositories/ultimate_sd_upscale
```

## Optional LLLite Setup

`UltimateSDUpscaleFLSLLLite` applies Anima ControlNet-LLLite through ComfyUI's
own native implementation (`comfy.ldm.anima.lllite` /
`comfy_extras.nodes_model_patch.AnimaLLLiteApply`). No separate LLLite
node/repository needs to be installed; a recent ComfyUI version that ships
native Anima LLLite support is all that's required.

Place compatible LLLite weights in:

```text
ComfyUI/models/controlnet
```

For the public Anima Tile/Repair LLLite model, see:

- https://huggingface.co/LAXMAYDAY/Anima_Tile_and_Repair_ControlNet-LLLite/tree/main
- https://civitai.red/models/2708551/anima-tile-and-repair-controlnet-lllite

## Notes

- The FLS node can be used without the optional LLLite dependency.
- The LLLite node requires a ComfyUI version with native Anima LLLite support and compatible model weights; it does not depend on any separate LLLite custom node.
- No model weights are redistributed here.
- `examples/anima-fls-lllite-basic` contains a placeholder API-format workflow that shows one possible Anima-style graph. Replace all placeholder model and LoRA filenames before use.

## Main Sources

- ComfyUI: https://github.com/comfyanonymous/ComfyUI
- ComfyUI Ultimate SD Upscale: https://github.com/ssitu/ComfyUI_UltimateSDUpscale
- Ultimate SD Upscale script: https://github.com/Coyote-A/ultimate-upscale-for-automatic1111
- BSS FLSampler reference: https://github.com/BlackSnowSkill/ComfyUI-BSS_FLSampler
- Anima Tile/Repair ControlNet-LLLite model: https://huggingface.co/LAXMAYDAY/Anima_Tile_and_Repair_ControlNet-LLLite/tree/main

## License

GPL-3.0. See `LICENSE`.
