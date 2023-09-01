# Segmentation of the peri-sinus space

Segmentation tools for the quantification of peri-sinus space using non-invasive MRI


**This Docker image is to be used only for non-commercial and non-medical purposes (research only).** See [license](https://github.com/hettk/spesis/blob/main/README.md#license).


## Quick Start Instructions
If you have already installed Docker, you can get the kilianhett/spesis:1.0.0 image from Docker Hub repository:

```
sudo docker pull kilianhett/spesis:1.0.0
```

Choroid plexus segmentation software currently only supports CPU

```
sudo docker run -v /absolute_path_to_folder/:/data/in  -v /absolute_path_to_folder/:/data/out kilianhett/spesis --name_pattern <name_of_image>
```

See Installation instructions for detailed instructions on how to install all the dependencies.
See How to use SPeSiS for detailed instructions on how to use SPeSiS.

