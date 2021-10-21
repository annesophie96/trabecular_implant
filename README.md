# trabecular_implant

trabecular_implant is a project created for generating anisotropic cancellous bone models useful for simulating dental implantation.

## Installation
I recommend using Anaconda and JupyterLab. Make sure the prerequisites are installed:
* [jupyter-cadquery](https://github.com/bernhard-42/jupyter-cadquery)
* [plotly](https://github.com/plotly/plotly.py)
* [tqdm](https://github.com/tqdm/tqdm) (included with Anaconda)
* [numpy](https://numpy.org/install/) (included with Anaconda)
* [matplotlib](https://matplotlib.org/stable/users/installing.html) (included with Anaconda)
* [ipython](https://ipython.org/install.html) (included with Anaconda)

Clone this repository, and the setup is complete.

## Folder structure
You can find the Python notebook under /src/python. Output .step files will be generated in /out/step.

## Usage
Open generateStructure_final_v3.ipynb. In field **#11**, fill out the first 9 or 10 parameters with the desired values:

```python
# DATA
VF=0.27         #Volume Fraction
minCellSize=0.5 #[mm] Minimum Cell Size
maxCellSize=1.0 #[mm] Maximum Cell Size
L=10            #[mm] Min Length (x) of Sample
T=10            #[mm] Min Width (y) of Sample
U=12            #[mm] Min Height (z) of Sample
holeDiam=2.7    #[mm] Diameter of Drilled Hole
dImpl=3.8       #[mm] Greatest Outer Diameter of the Implant

isotropicTestBodyGen=0 #turn 1 for isotropic test body generation, 0 for regular run
numberOfLayers=5       #control test body size, no need to change
```
In field **#6** under the 'else' case, you can substitute your own code for changing the local volume fracion of the material. You could even call the X and Y values instead of only R _(remembering to change the function call arguments within the main code as well)_, thus creating 2D functions for anisotropy.

```python
def densify(R,VF,d):
    volFrac=np.ones(len(R))
    for i in range(len(R)):
        if R[i]<=(d/2):
            volFrac[i]=1
        else:
            volFrac[i]=np.exp(-0.4*(R[i]-d/2)+np.log(1-VF))+VF
    return volFrac
```

The code exports the created models in multiple places, so that if you experience a crash or some other mishap, you can continue from where you left off. **Please note that this code can be quite time-consuming to finish running, as the subtractions and additions performed on the CAD models can get quite complex.**

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)