# Segmentation of the peri-sinus space

Segmentation tools for the quantification of peri-sinus space using non-invasive MRI

If you use this software for scientific publications, please cite the associated manuscript.

Hett, K., McKnight, C. D., Leguizamon, M., Lindsey, J. S., Eisma, J. J., Elenberger, J., ... & Donahue, M. J. (2024). Deep learning segmentation of peri-sinus structures from structural magnetic resonance imaging: validation and normative ranges across the adult lifespan. Fluids and Barriers of the CNS, 21(1), 1-15. [https://doi.org/10.1186/s12987-024-00516-w](https://doi.org/10.1186/s12987-024-00516-w)


**This Docker image is to be used only for non-commercial and non-medical purposes (research only).** See [license](https://github.com/hettk/spesis/blob/main/README.md#license).


## Quick Start Instructions
If you have already installed Docker, you can get the kilianhett/spesis:1.0.0 image from Docker Hub repository:

```
sudo docker pull kilianhett/spesis:1.0.0
```

The software for the segmentation of the peri-sinus space currently only supports CPU

```
sudo docker run -v /absolute_path_to_folder/:/data/in  -v /absolute_path_to_folder/:/data/out kilianhett/spesis:1.0.0 --name_pattern <name_of_image>
```

See Installation instructions for detailed instructions on how to install all the dependencies.
See How to use SPeSiS for detailed instructions on how to use SPeSiS.

# Installation instructions 

## Prerequisites

To run this Docker image on a CPU, you will need:
* a x86_64 CPU 
* At least 6GB of RAM
* GNU/Linux [[supported distributions]](https://docs.docker.com/engine/install/#server), MacOS, or Windows 10/11 with WSL [[supported versions]](https://docs.docker.com/desktop/windows/install/)
* Docker >= 19.03 
* SPeSiS Docker image 
* MRI files in nifti format

## Installation 

Docker may be installed on supported versions of [GNU/Linux] or [Windows 10/11 with WSL]. The docker image can also be transformed in a [Singularity image]

### Docker

#### Installation on MacOS

Here are the detailed installation instructions on MacOS [[instructions]](https://docs.docker.com/desktop/install/mac-install/)

#### Installation on GNU/Linux

Here are the detailed installation instructions on Ubuntu (18.04 or above).

Install Docker from the official repository [[instructions]](https://docs.docker.com/engine/install/ubuntu/).  
(Docker no longer releases updated packages for Ubuntu 16.04)
```
#Uninstall old versions of docker
sudo apt-get remove docker docker-engine docker.io containerd runc
#Install using the official repository
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
#Verify that Docker Engine is installed correctly
sudo docker run hello-world
# it may download the hello-world docker image and then print "Hello from Docker!" and other information.
```

#### Installation on Windows 10/11 with WSL

Here are the detailed installation instructions on Windows 10 or 11.

##### Check Windows version

You need:
* Windows 10 64-bit: Home or Pro 2004 (build 19041) or higher, or Enterprise or Education 1909 (build 18363) or higher.
* Windows 11 64-bit: Home or Pro version 21H2 or higher, or Enterprise or Education version 21H2 or higher.

To check your Windows version and build number, select Windows logo key + R, type winver, select OK. 
You can update to the latest Windows version by selecting Start > Settings > Windows Update > Check for updates.

##### Enable BIOS virtualization support

BIOS-level hardware virtualization support must be enabled.

You can check the Performance tab on the Task Manager to see if virtualization is enabled, see [virtualization support](https://docs.docker.com/desktop/windows/troubleshoot/#virtualization-must-be-enabled).

##### WSL2

Install Windows Subsystem for Linux (WSL) 2 [[instructions]](https://docs.microsoft.com/en-us/windows/wsl/install)

Open PowerShell as Administrator (Start menu > PowerShell > right-click > Run as Administrator) and enter this command:
```
wsl --install
```
It should install the last Ubuntu LTS. You may need to reboot your machine.

You can check that WSL version 2 was installed:
Open PowerShell as Administrator (Start menu > PowerShell > right-click > Run as Administrator) and enter this command:
```
wsl -l -v
```

Launch Ubuntu (Start menu > ubuntu). It should ask to create a default user. 
You may upgrade the system: 
```
sudo apt-get update
sudo apt-get upgrade
```


# How to use SPeSiS 

## Inputs

This Docker image requires 3D T2-weighted images in nifti format (.nii or .nii.gz) as inputs.

To convert your DICOM files into nifti format, you can use [dcm2niix](https://github.com/rordenlab/dcm2niix), a multiplatform and open source software.

## Outputs

For each processed image, the following files will be produced and stored separately in folder named *filename* (where *filename* is replaced by the original filename):

* *filename*.nii.gz: Native image corrected for N4 inhomogeneity 
* *filename*_mask.nii.gz: Segmentation maps of the peri-sinus space structures
* *filename*_lobe.nii.gz: Mask defining sub-region of the peri-sinus space (i.e., prefrontal, frontal, parietal, and occipital)
* report_*filename*.pdf: PDF format volumetry report. The reports will show the expected limits/normative bounds of normalized volumes in the function of age, if age and optionally sex were specified.
* *filename*_metrics.csv: CSV format volumetry report

## Command options

The Docker image has the following arguments: 
```
[--name_pattern `<filename/pattern>`] [--overwrite True/False (default=False]
```

* `<filename/pattern>`: Filter the filenames with a specific pattern in the input directory.
* `<overwrite>`: Allow to replace already existing processing output.



