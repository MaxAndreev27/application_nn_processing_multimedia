# Application: Neural Network Processing of Multimedia

This repository contains Jupyter notebooks for estimating a person's age and
gender from still photos and a webcam stream.

## Notebooks

| Project | Description | Environment |
| --- | --- | --- |
| [Photo analysis](./01_determining_gender_age_photo/determining_gender_age_photo.ipynb) | Processes supported image files from the `photos/` folder using DeepFace. | `01_determining_gender_age_photo` |
| [Webcam analysis](./02_determining_gender_age_video/determining_gender_age_video.ipynb) | Uses MiVOLO v2 and a face/person detector to estimate age and gender, and matches faces against local reference photos. Press `q` or close the window to stop. | `02_determining_gender_age_video` |

The environments are separate because the notebooks use different OpenCV
builds. Do not install both projects' requirements into the same virtual
environment.

## Requirements

- Python 3.13 (the tested version is recorded in each project directory's
  `.python-version` file)
- Git, required to install MiVOLO from its pinned source revision
- A webcam for the video notebook
- Internet access on first use to download model weights

## Setup

Create and activate a separate virtual environment for each notebook.

### Photo notebook

```bash
cd 01_determining_gender_age_photo
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Open `determining_gender_age_photo.ipynb` in Jupyter or VS Code and select the
`.venv` interpreter. Put supported images (`.jpg`, `.jpeg`, `.png`, `.bmp`, or
`.webp`) in the `photos/` directory, then run the analysis cell.

### Webcam notebook

MiVOLO's pinned source revision uses a legacy `setup.py` that imports
`pkg_resources`. Install its build dependency first, then install the remaining
requirements without build isolation:

```bash
cd 02_determining_gender_age_video
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install setuptools==80.10.2
python -m pip install --no-build-isolation -r requirements.txt
```

Open `determining_gender_age_video.ipynb` and select the `.venv` interpreter.
The notebook requests 1920x1080 MJPG capture where supported by the webcam.
The first run downloads model files from Hugging Face and the YuNet/SFace
models from OpenCV Zoo into the user's cache directory. Inference runs on CUDA
when available for MiVOLO; face matching uses OpenCV and the CPU.

For local face matching, put reference photos in
`02_determining_gender_age_video/photo/`. Use one clear, front-facing JPG, JPEG,
or PNG image per person; the filename without its extension is displayed as
the name (for example, `Max Andreev.jpg` displays as `Max Andreev`). Images
must be at least 200x200 pixels, with the face clearly visible. Faces that do
not meet the configured similarity threshold are labeled `Unknown`. The
default SFace cosine similarity threshold is `0.363`; this is a score, not a
probability, so validate and adjust it for your camera and lighting conditions.

## Limitations

Age and gender are predictions from visual appearance, not verified personal
attributes. Results can be inaccurate and should not be used for consequential
decisions. Face matching is biometric processing: use reference photos only
with appropriate consent, protect them, and do not use the result as the sole
basis for consequential decisions. Performance depends on image quality,
lighting, pose, and hardware.
The OpenCV Zoo YuNet face detector is MIT-licensed and its SFace recognizer is
Apache-2.0-licensed; consult their upstream licenses when redistributing the
downloaded model files.

The included photos are example inputs. Their publication in this repository
does not grant additional rights to reuse them. MiVOLO, DeepFace, pretrained
weights, and other third-party components are subject to their own licenses and
terms; the repository's MIT license applies to original project code and
documentation only.

## Contributing and security

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting a change.
See [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) for community expectations and
[SECURITY.md](./SECURITY.md) for vulnerability reporting.

## License

Original project code and documentation are released under the MIT License.
See [LICENSE](./LICENSE). Third-party components and example images are not
covered by that license.
