# VisionGuard

This repository contains the code for VisionGuard.

VisionGuard is a class-agnostic visual anomaly detection model trained using only anomaly-free images.
Built with DINOv3.

## Reproduce our results

### 1. Preparation

Download the DINOv3 weights from [the official meta ai site](https://ai.meta.com/resources/models-and-libraries/dinov3-downloads/).
Place the weights into the `./weights/` directory.
If weights are present elsewhere, you can adjust the `dino_weights_dir` parameter in the `config.json`.

Place the `mvtec_ad_2` dataset into the `./data/` directory.
If the dataset is stored elsewhere, you can adjust the `datasets_dir` parameter in the `config.json`.

### 2. Install

First, install uv (a fast Python package manager):

macOS / Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```bash
irm https://astral.sh/uv/install.ps1 | iex
```

Then run the following to install all dependencies:

```bash
uv sync --all-packages
```

### 3. Run

Train all models by running:

```bash
uv run train-industrial
```

By default, the test script generates predictions for `test_private` and `test_private_mixed` in the `./outputs/` directory.
If you want predictions for `test_public` you can add it to `test_split` in the `config.json` file.

To test models and generate anomaly maps and thresholded anomaly maps, run:

```bash
uv run test-industrial
```

To create the final submission, run:

```bash
uv run submit-industrial
```

## Configuration

The `config.json` file contains all relevant configuration parameters. Make sure to run train, test and submission after
any change.

## Pretrained Models

We provide “pretrained” models for each category for easier reproduction and to skip the training script when evaluating on `mvtec_ad_2`. In our case, a pretrained model does not contain weights and does not replace downloading the DINOv3 weights. Instead, the provided files contain a memory bank with reference embeddings stored in an .npz file, along with the corresponding model settings in a .json file for that category.

Models are available at: https://owncloud.fraunhofer.de/index.php/s/THkX7W8AhRd2RCs

Place all models in the `./models/` directory and make sure you installed DINOv3 weights. After that, you can run inference directly with:

```bash
uv run test-industrial
```

## Dependencies

For a full list of all dependencies, please refer to the `./pyproject.toml`, `./utils/pyproject.toml`,
and `./tracks/industrial/pyproject.toml` files. Additionally, the execution depends on the installed DINOv3 model weights.

## License

Copyright (C) 2026 Rohith Gowda R. All rights reserved.

This software is strictly proprietary and confidential. No individual, organization, or entity is permitted to access, view, use, copy, modify, distribute, sublicense, execute, or exploit this software in whole or in part for any purpose without prior express written permission from Rohith Gowda R.

See the [`LICENSE`](./LICENSE) file for the complete terms and restrictions.
