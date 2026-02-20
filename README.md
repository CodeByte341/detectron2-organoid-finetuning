# Detectron2 Organoid Detection

Fine-tuning Meta's Detectron2 framework for brain organoid detection in microscopy images.

## Overview

This project demonstrates the application of instance segmentation techniques to biomedical imaging, specifically for detecting brain organoids in bright-field microscopy images. The code and methodology are heavily inspired by and derived from Meta's Detectron2 framework.

Developed as part of a bioengineering project at SupBiotech in collaboration with the CellTechs research team.

**Related Publication**: [SupBiotech Article](XXXXXX)

## Authors

Axel Fontanier¹*, Rosa Abdiche¹*, Eva Alpande Dos Santos¹*, Périne Fischer¹*, Camille Franceschi¹*, Axelle Guillier¹*, Jeanne Rouilleaux¹*, Julien Grimaud²

¹ Students in the 5th year of the engineering program through the apprenticeship track, Sup'Biotech, Villejuif, France  
² Associate PhD, Professor in Life Sciences, Head of the Student Research Valorization Office  
*These authors contributed equally to the study

**Corresponding author**: fontanieraxelpro@gmail.com

## Project Structure

The complete project is hosted on Google Drive with the following organization:

```
Detectron2_Organoid_FineTuning/
├── 01_Notebooks/
│   ├── Model_Training.ipynb
│   └── Model_Inference.ipynb
│
├── 02_Model/
│   ├── model_final.pth
│   ├── events.out.tfevents.1769091283.27339c062a08.2949
│   ├── last_checkpoint
│   └── metrics.json
│
├── 03_Data/
│   ├── Evaluation_Test/
│   │   ├── Ground_Truth/
│   │   ├── Inputs/
│   │   ├── Masks/
│   │   └── Visual_Results/
│   └── Training_Data/
│       └── [Your dataset here, e.g., organoid.zip]
│
└── 04_Metrics_and_Results/
    └── metrics.json
```

**Google Drive Link**: [Access Project Files](https://drive.google.com/drive/folders/1wAj3cnUmtYKuFIq_exkQeIpbaqb5n2-c?usp=drive_link)

## Getting Started

### Prerequisites

- Google account
- Web browser
- Internet connection

### Setup Instructions

#### Step 1: Duplicate Google Drive Folder

The project files are hosted on Google Drive and must be duplicated to your account.

1. Open the [shared folder link](https://drive.google.com/drive/folders/1wAj3cnUmtYKuFIq_exkQeIpbaqb5n2-c?usp=drive_link)
2. Right-click on "Detectron2_Organoid_FineTuning"
3. Select "Make a copy"
4. The duplicated folder will appear in your "My Drive"

#### Step 2: Open Notebooks in Google Colab

For inference:
1. Navigate to `01_Notebooks/` in your Drive
2. Right-click `Model_Inference.ipynb`
3. Select "Open with > Google Colab"

For training:
1. Navigate to `01_Notebooks/` in your Drive
2. Right-click `Model_Training.ipynb`
3. Select "Open with > Google Colab"

#### Step 3: Configure Runtime

Enable GPU for faster processing:
1. In Google Colab menu: Runtime > Change runtime type
2. Select "T4 GPU" from Hardware accelerator dropdown
3. Click Save

#### Step 4: Mount Google Drive

When executing notebooks:
1. Run the drive mount cell
2. Click the authorization link
3. Select your Google account
4. Click "Allow" to grant permissions

## Usage

### Testing the trained Model

The repository includes 21 example images (used in the publication) for immediate testing of the trained model.

To run inference:
1. Open `Model_Inference.ipynb` in Google Colab
2. Execute all cells sequentially
3. Results will be saved to `03_Data/Evaluation_Test/Visual_Results/`

The inference notebook processes the example images and generates visual predictions showing the detected organoids.

### Training a Custom Model

To train your own model on custom data:

1. **Prepare your dataset** following the methodology in [PREPROCESSING_GUIDE.md](PREPROCESSING_GUIDE.md)
2. **Upload your dataset** to `03_Data/Training_Data/` in your Google Drive
3. **Open** `Model_Training.ipynb` in Google Colab
4. **Update paths** in the notebook to point to your dataset
5. **Execute all cells** sequentially

Training outputs will be saved to `02_Model/` and metrics to `04_Metrics_and_Results/`.

## Dataset Information

### Example Images

21 microscopy images with corresponding ground truth masks are provided in `03_Data/Evaluation_Test/`. These images were used in the publication and serve as examples for testing the pre-trained model.

Users can test the model on any microscopy images following the same format.

### Training Dataset

The complete original training dataset used to fine-tune this model is not publicly available due to data ownership by CellTechs research team.

To train a custom model, users must prepare their own datasets following the preprocessing guidelines provided in this repository.

## Data Preprocessing

Creating a custom dataset requires:
1. Microscopy image acquisition
2. Manual annotation with FIJI/ImageJ
3. Binary mask generation
4. Conversion to COCO format
5. Train/validation split

See [PREPROCESSING_GUIDE.md](PREPROCESSING_GUIDE.md) for the complete methodology used in this project.

## Technical Details

**Model Architecture**: Mask R-CNN with ResNet-50-FPN backbone

**Framework**: Detectron2 (Meta AI Research)

**Base Model**: COCO pre-trained weights

**Image Dimensions**: 519×693 pixels

**Annotation Format**: COCO JSON

## Repository Contents

Documentation:
- `README.md` - Project documentation and setup instructions
- `PREPROCESSING_GUIDE.md` - Data preparation methodology
- `CONTRIBUTING.md` - Contribution guidelines
- `LICENSE` - Apache 2.0 License

Code:
- Jupyter notebooks available in Google Drive folder
- Model weights available in Google Drive folder

## Troubleshooting

**"Permission denied" errors**:
- Ensure you duplicated the folder rather than accessing the shared link directly
- Re-authorize Drive mount in Colab

**"File not found" errors**:
- Verify folder structure is intact
- Check path variables match your folder location
- Ensure Drive is properly mounted

**Runtime disconnections**:
- Google Colab free tier has session time limits
- Save work frequently

## Citation

```bibtex
@misc{detectron2_organoid_2025,
  author = {Fontanier, Axel and Abdiche, Rosa and Alpande Dos Santos, Eva and Fischer, Périne and Franceschi, Camille and Guillier, Axelle and Rouilleaux, Jeanne and Grimaud, Julien},
  title = {Detectron2 Fine-Tuning for Brain Organoid Detection},
  year = {2025},
  publisher = {GitHub},
  howpublished = {\url{https://github.com/YOUR_USERNAME/detectron2-organoid-detection}}
}
```

## Acknowledgments

This project uses Detectron2, developed by Meta AI Research (FAIR). The code and methodology presented here are heavily inspired by and derived from Detectron2.

- **Meta AI Research (FAIR)** for developing and maintaining Detectron2
- **SupBiotech** for the academic framework
- **CellTechs research team** for providing microscopy images and domain expertise

## Additional Resources

- [Detectron2 Documentation](https://detectron2.readthedocs.io/)
- [Detectron2 GitHub Repository](https://github.com/facebookresearch/detectron2)
- [COCO Dataset Format](https://cocodataset.org/#format-data)
- [FIJI/ImageJ](https://fiji.sc/)

## License

This project is licensed under the Apache License 2.0 - see [LICENSE](LICENSE) for details.

The original training dataset remains the property of CellTechs and is not included in this repository.

## Contact

For questions or collaboration:

**Email**: fontanieraxelpro@gmail.com
