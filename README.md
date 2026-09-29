# Intelligent Kinetic Activity Recognition (IKAR) - Fall Detection Dataset

## Introduction
Falls among elderly individuals represent a major global public health concern, affecting approximately one in three people aged 65 and older (according to the World Health Organization - WHO). These incidents often lead to severe injuries, prolonged immobilization, and long-term loss of personal autonomy. Key physiological and clinical risk factors include neurological disorders, joint degenerative conditions, dizzy spells, medication complications, and impaired balance control.

The aftermath of fall incidents encompasses both severe physical trauma—such as bone fractures, traumatic brain injuries, and spinal damage—and debilitating psychosocial consequences (specifically post-fall syndrome, which leads to chronic fear of falling and progressive reduction in physical activity).

Rapid notification and emergency response times are decisive in preventing life-threatening complications. In situations where an elderly individual lives alone, issuing an immediate manual alert is often unfeasible. The IKAR (Intelligent Kinetic Activity Recognition) project addresses this challenge by developing computer vision and machine learning frameworks capable of automated, continuous fall detection via video streaming feeds to alert caregivers without delay.

To train, evaluate, and benchmark these detection models, we created this standardized video dataset containing diverse fall scenarios recorded under rigorous, controlled conditions.

## Dataset Overview & Categories
The dataset comprises 278 video recordings captured using mobile devices across 7 volunteer participants representing varied heights, silhouettes, and body dynamics. All recordings were executed safely on protective mats in a controlled environment. 

The dataset is partitioned into four distinct fall categories:
1. **Trips**: Sudden loss of forward balance caused by an obstacle obstructing foot trajectory, resulting in abrupt, forward-oriented momentum. (Total: 92 recordings)
2. **Slips**: Abrupt loss of traction between the foot and ground surface, causing dynamic feet displacement forward and a rapid backward/lateral fall. (Total: 64 recordings)
3. **Faintings**: Temporary weakness or presyncope where the individual retains partial motor control, attempting to cushion the fall or brace against surrounding objects/hands. (Total: 65 recordings)
4. **Blackouts**: Complete and sudden loss of consciousness (syncope), leading to immediate neuromuscular collapse and an inert, unmitigated fall without protective reflexes. (Total: 57 recordings)

## Data Collection & Ethics
* **Environment & Setup**: Multi-angle recording configurations across varying elevation points and perspectives to ensure invariance to real-world camera installations.
* **Safety & Ethics**: All falls were simulated by healthy volunteers on high-density landing mats with designated rest intervals to ensure zero risk of injury. Informed participant consent was obtained prior to data acquisition.
* **Annotation**: Ground-truth spatial annotations were generated via the Labelbox platform, consisting of tight bounding boxes surrounding the subject throughout the fall sequence.

## Basic Requirements
* **Video Decoding**: FFmpeg, OpenCV (`opencv-python`), or VLC Media Player.
* **Data Processing**: Python 3.8+ with standard scientific libraries (`numpy`, `pandas`, `json`).
* **Hardware**: Standard x86_64 CPU workstation; GPU acceleration recommended if running neural inference workflows.

## Folder Structure
The dataset is organized into four main category folders. Each category contains a `videos/` subdirectory with the raw MP4 files and a `labels/` subdirectory with the corresponding JSON bounding box annotations.

```text
IKAR_Dataset/
├── blackouts/
│   ├── labels/
│   └── videos/
├── faintings/
│   ├── labels/
│   │   ├── fainting_0.json
│   │   ├── ...
│   └── videos/
│       ├── fainting_0.mp4
│       ├── ...
├── slips/
│   ├── labels/
│   └── videos/
├── trips/
│   ├── labels/
│   └── videos/
└── README.md
```

## File Formats & Naming Conventions
* **Video Formats**: Standard video containers (`.mp4`).
* **Annotation Formats**: JSON files (`.json`) containing video stream metadata and sequential frame annotations.
* **File Naming Convention**: Files are named according to their category and a sequential integer ID: `[category]_[id].[ext]`. For example, the video `fainting_3.mp4` corresponds directly to the annotation file `fainting_3.json`.

## Codebook
Each annotation file contains a root JSON object with two primary keys: `media_attributes` and `annotations`. 
*Note: The values in the "Example" columns below are strictly illustrative samples from a single file, not fixed constants for the entire dataset.*

### 1. Video Metadata (`media_attributes`)
| Variable | Description | Data Type | Example |
| :--- | :--- | :--- | :--- |
| `height` | Frame resolution height in pixels | Integer | `720` |
| `width` | Frame resolution width in pixels | Integer | `1280` |
| `asset_type` | Type of media asset | String | `video` |
| `mime_type` | Media MIME format container | String | `video/mp4` |
| `frame_rate` | Video acquisition rate (frames per second) | Integer | `30` |
| `frame_count` | Total number of frames in the video clip | Integer | `137` |
| `duration` | Total video duration in seconds | Float | `4.567` |

### 2. Bounding Box Coordinates (`annotations.frames`)
The `frames` array contains frame-indexed objects mapping each chronological frame number (as a numeric string key) to its bounding box geometry (using YOLO format):

| Variable | Description | Data Type | Example |
| :--- | :--- | :--- | :--- |
| `x_center` | Horizontal coordinate of the bounding box center in px | Float | `452.0` |
| `y_center` | Vertical coordinate of the bounding box center in px | Float | `65.0` |
| `w` | Width dimension of the bounding box in px | Float | `126.0` |
| `h` | Height dimension of the bounding box in px | Float | `435.0` |

## License
* **Dataset & Code**: This repository, including the dataset, companion tooling, and automation scripts, is distributed under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license. You are free to share, copy, and adapt the material as long as appropriate credit is attributed to the original authors.

## Citation
If you use this dataset or associated tooling in your academic work, please cite it as follows:

```bibtex
@misc{ikar_dataset_2026,
  author = {Kamil Opyrchał and Łukasz Burliga and Maja Zielińska and Karolina Zając and Maria Potwora and Martyna Jagoda and Dominik Mika and Franciszek Kubala},
  title = {{IKAR: Intelligent Kinetic Activity Recognition - Fall Detection Dataset}},
  year = {2026},
  publisher = {RODBUK Cracow Open Research Data Repository},
  doi = {[DOI]}
}
```

## Acknowledgements
* This research was carried out using equipment sponsored by MyChinaPal Sp. z o.o.
* The authors thank the Centre of Physical Education and Sport (SWFiS) of AGH University of Krakow for making the facility available free of charge for the recording during data acquisition.
* The authors would like to thank all the participants for their time and voluntary participation in this data acquisition.

## Authors & Affiliation
* **Authors**: Kamil Opyrchał, Łukasz Burliga, Maja Zielińska, Karolina Zając, Maria Potwora, Martyna Jagoda, Dominik Mika, Franciszek Kubala
* **Research Group**: Artificial Intelligence in Medicine Student Research Club
* **Department**: Department of Biocybernetics and Biomedical Engineering
* **Faculty**: Faculty of Electrical Engineering, Automatics, Computer Science and Biomedical Engineering
* **Institution**: AGH University of Krakow, al. A. Mickiewicza 30, 30-059 Krakow, Poland

## Contact
* **Affiliation**: Artificial Intelligence in Medicine Student Research Club, AGH University of Krakow
* **Primary Contact**: Franek Kubala (frkubala@student.agh.edu.pl)
* **Repository Issues & Feedback**: Please report any anomalies, data integrity issues, or schema errors exclusively via the official project issue tracker.
