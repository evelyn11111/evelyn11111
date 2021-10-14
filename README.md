#@title Image magic
%cd "/content/dreamtime/src/cli"


path='results'
import os
if not os.path.exists(path):
    os.makedirs(path)

from IPython.display import display
from ipywidgets import widgets
from os import listdir
from os.path import isfile, join

mypath = '/content/dreamtime/src/cli/photos'
onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]

if len(onlyfiles)>0:
  filename_ch = widgets.Dropdown(
      options=onlyfiles,
      description='Choose file:',
  )
  butt = widgets.Button(description='Start')
  def on_butt_clicked(b):
      print(filename_ch.value)
      %cd '/content/dreamtime/src/cli/'
      !python main.py -i "photos/$filename_ch.value" -o "results/$filename_ch.value" --gpu 0


  butt.on_click(on_butt_clicked)
  # display
  display(widgets.VBox([filename_ch,butt]))
else:
  print('Upload photo at first')
  
  
