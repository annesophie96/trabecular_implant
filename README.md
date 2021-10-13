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
You can find the Python notebooks under /src/python, any implants you might want to use, you can put to /src/implants. Output .step files will be generated in /out/step.

## Usage
Open generateStructure_final_v1.ipynb. In field **#11**, fill out the first 7 parameters with your desired values:

```python
# DATA
VF=0.14      #Volume Fraction
a0=0.625     #[mm] Average Cell Size / 2
L=20         #[mm] Length (x) of Sample
T=20         #[mm] Width (y) of Sample
U=20         #[mm] Height (z) of Sample
holeDiam=2.7 #[mm] Diameter of Drilled Hole
dImpl=3.8    #[mm] Greatest Outer Diameter of the Implant
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
In field **#36**, you will want to substitute the implant model's filename for your own implant model's filename, and change the implant's neck height (aka. how much it should be sticking out of the top) as needed:
```python
implant=cq.importers.importStep(home+'\\src\\implants\\your_implant.step')
implNeckHeight=1.5 #[mm]
```

The code exports the created models in multiple places, so that if you experience a crash or some other mishap, you can continue from where you left off. **Please note that this code can be quite time-consuming to finish running, as the subtractions and additions performed on the CAD models can get quite complex.**

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)