
# IPython development in terminal with graphical support (iterm2 or mlterm)
A terminal that is compatible with mrpeek seems to be sufficient, but we only tested mac os (iterm2) and ubuntu (mlterm)
* ssh to a dev machine from iterm2 or mlterm
* activate your environment
* install the following dependencies
```
pip install gr
pip install ipython
pip install matplotlib
```
* run ipython as follows 
```env GKS_WSTYPE=iterm MPLBACKEND=module://gr.matplotlib.backend_gr ipython```
* Inside ipython run this code:
```
import numpy as np
import pylab as plt
plt.imshow(np.random.randn(5,5), interpolation=None)
plt.show()
```
