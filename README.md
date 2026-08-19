# smart-waste-detector-yolo
- Ultralytics YOLO
- Kaggle API
- Google Drive for persistent checkpoints

## Run the Notebook

### 1. Open in Google Colab

[Open the notebook in Google Colab](https://colab.research.google.com/github/HafidIdrissi/smart-waste-detector-yolo/blob/main/smart_waste_detector_yolo.ipynb)

### 2. Configure the runtime

In Colab, select a GPU runtime:

`Runtime` → `Change runtime type` → `T4 GPU`

### 3. Execute the notebook

Run the cells from top to bottom. The notebook will:

1. Install the required packages.
2. Request the Kaggle API token securely at runtime.
3. Download and extract the dataset.
4. Locate the YOLO dataset configuration file.
5. Train the model for 30 epochs.
6. Evaluate the model on the validation set.
7. Run predictions on uploaded personal images.

The Kaggle token is entered at runtime and should never be written directly in the notebook or committed to GitHub.

## Training Configuration

| Parameter | Value |
|---|---:|
| Base model | YOLO nano model |
| Epochs | 30 |
| Image size | 640 × 640 |
| Batch size | 8 |
| Device | Colab GPU |
| Early stopping patience | 10 |

## Evaluation Results

The baseline model achieved the following validation results after 30 epochs:

| Class | Precision | Recall | mAP50 | mAP50-95 |
|---|---:|---:|---:|---:|
| All classes | 0.567 | 0.445 | 0.496 | 0.344 |
| Biodegradable | 0.784 | 0.433 | 0.583 | 0.330 |
| Cardboard | 0.701 | 0.465 | 0.561 | 0.428 |
| Glass | 0.781 | 0.682 | 0.769 | 0.578 |
| Metal | 0.700 | 0.592 | 0.649 | 0.449 |
| Paper | 0.032 | 0.061 | 0.037 | 0.035 |
| Plastic | 0.403 | 0.435 | 0.376 | 0.243 |

`mAP50` measures detection quality with an IoU threshold of 0.50. `mAP50-95` is stricter because it averages results across IoU thresholds from 0.50 to 0.95.

## Observations and Limitations

- The model performs better on glass and metal than on paper and plastic.
- Predictions on personal photos can be less reliable than predictions on images from the original dataset.
- This difference is caused by domain shift: lighting, camera angle, object size, background, and image composition can differ significantly from the training data.
- The validation set is imbalanced, especially for paper and plastic, which affects per-class performance.
- The current model is a baseline and should not be considered production-ready.

## Possible Improvements

- Add more real-world images captured with different phones and lighting conditions.
- Balance the number of examples per class.
- Fine-tune the model for more epochs with systematic experiments.
- Compare several YOLO model sizes.
- Tune the confidence threshold and data augmentation settings.
- Add a confusion matrix and a curated test set from real household waste.

## Dataset Attribution

Dataset: [Garbage Detection - 6 Waste Categories](https://www.kaggle.com/datasets/viswaprakash1990/garbage-detection/data)

The notebook records the dataset attribution and indicates a CC BY 4.0 license. Please review the original dataset page and preserve the required attribution when redistributing derived work.

## License

No separate license has been added to this repository yet. The dataset license and the source code license are separate; check the dataset terms before using or redistributing the data.
