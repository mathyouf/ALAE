<h1 align="center">
    Frontend Visualization Playground
    <br>
    for
  <br>
  [CVPR2020] Adversarial Latent Autoencoders
  <br>
</h1>
  <p align="center">
    <a href="https://podgorskiy.com/">Stanislav Pidhorskyi</a> •
    <a href="https://www.statler.wvu.edu/faculty-staff/faculty/donald-a-adjeroh">Donald A. Adjeroh </a> •
    <a href="http://vision.csee.wvu.edu/~doretto/">Gianfranco Doretto</a>
  </p>
<h4 align="center">Original Design</h4>
<table>
<tbody>
<tr>
<td style="padding:0;"><img src="https://user-images.githubusercontent.com/3229783/79670218-63080d80-818f-11ea-9e50-927b8af3e7b5.gif"></td>
<td style="padding:0;"><img src="https://user-images.githubusercontent.com/3229783/79530431-4bb90b00-803d-11ea-9ce3-25dfc3df253a.gif"></td>
</tr>
</tbody>
</table>

<p align="center">
  <img src="https://img.shields.io/badge/pytorch-1.4.0-green.svg?style=plastic" alt="pytorch version">
  <a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg"></a>
</p>

  <p align="center">
    <a href="https://drive.google.com/drive/folders/1iZodDA4q1IKRRgV2nJuAyyuCwQGtL4vp?usp=sharing">Google Drive folder with models and qualitative results</a>
  </p>


# ALAE

## Configuring comptuer for ALAE

### For Windows

Create an ALAE environment and then activate it

    conda create --name ALAE python=3.7
    source activate ALAE

Install pytorch with cuda

    conda install pytorch torchvision cudatoolkit=10.2 -c pytorch
    
Install some packages from conda

    conda install --file requirements.txt

Install some packages with pip

    pip install -r requirements.txt
    
Download pre-trained models:

    python training_artifacts/download_all.py

## Running the demo

Run the demo:

    python new_interactive_demo.py

You can specify **yaml** config to use. Configs are located here: https://github.com/podgorskiy/ALAE/tree/master/configs.
By default, it uses one for FFHQ dataset.
You can change the config using `-c` parameter. To run on `celeb-hq` in 256x256 resolution, run:

    python interactive_demo.py -c celeba-hq256

However, for configs other then FFHQ, you need to obtain new principal direction vectors for the attributes.

To run the demo on custom images, please follow the steps and commands:

    mkdir custom
    # Put your custom images in custom/
    align_custom_faces.py
    # The cropped faces will be located at:
    # dataset_samples/faces/realign_custom1024x1024
    interactive_demo_custom.py

If the min/max of the slide bar isn't suitable for your custom image, modify the following line in `interactive_demo_custom.py`

    bimpy.slider_float(label, v, -40.0, 40.0)

## Generating figures

#### Style-mixing

To generate style-mixing figures run:

    python style_mixing/stylemix.py -c <config>
    
Where instead of `<config>` put one of: `ffhq`, `celeba`, `celeba-hq256`, `bedroom`
    

#### Reconstructions

To generate reconstruction with multiple scale images:

    python make_figures/make_recon_figure_multires.py -c <config>
    
To generate reconstruction from all sample inputs on multiple pages:

    python make_figures/make_recon_figure_paged.py -c <config>

There are also:

    python make_figures/old/make_recon_figure_celeba.py
    python make_figures/old/make_recon_figure_bed.py

To generate reconstruction from test set of FFHQ:

    python make_figures/make_recon_figure_ffhq_real.py
    
To generate interpolation figure:

    python make_figures/make_recon_figure_interpolation.py -c <config>
    
To generate traversals figure:

(For datasets other then FFHQ, you will need to find principal directions first)

    python make_figures/make_traversarls.py -c <config>
    
#### Generations

To make generation figure run:

    make_generation_figure.py -c <config>
