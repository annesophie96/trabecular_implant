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
You can find the Python notebook under /src/python. Output .step files will be generated in /out/step. Input .csv file can be found under /src/csv.

## Usage
Open src/csv/inputData.csv and set your parameters (structure name, base volume fraction, minimum cell size in mm, maximum cell size in mm, width, depth and height of structure in mm, whether to create an isotropic body or a compacted one, the maximum implant diameter, the pre-drill hole diameter and the width of the compacted region - if applicable). Save and close.
Open generateStructure_final_v4.ipynb and run all.
In field **#6** under the 'for' loop, you can substitute your own code for changing the local volume fracion of the material. You could even call the X and Y values instead of only R _(remembering to change the function call arguments within the main code as well)_, thus creating 2D functions for anisotropy.

```python
def densify(R,VF,d,v):
    volFrac=np.ones(len(R))
    for i in range(len(R)):
        if R[i]<=(d/2):
            volFrac[i]=1
        elif (R[i]>=(d/2) and R[i]<=(d/2+v)):
            volFrac[i]=((VF-1)*pow(v,-3)*(-2*pow(R[i],3)+3*(d+v)*pow(
            R[i],2)-((3*d*(d+2*v))/2)*R[i]+((pow(d,2)*(d+3*v))/4))+1)
        else:
            volFrac[i]=VF

    return volFrac
```

The code exports the created models in multiple places, so that if you experience a crash or some other mishap, you can continue from where you left off. **Please note that this code can be quite time-consuming to finish running, as the subtractions and additions performed on the CAD models can get quite complex.**

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)
