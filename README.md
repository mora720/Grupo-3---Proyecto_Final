# Grupo-3---Proyecto_Final
Integrantes del grupo: Matias Mora, Jhoel Marin, Mateo Flores, Litzy Conde, Alexander Mujica

Para ejecutar el sistema, descargue el modelo ‘modelo_protección_de_cultivos.h5’ y ejecute las siguientes líneas de comando en el script de Python:
from PIL import Image
import requests
from io import BytesIO
import cv2

def categorizar(url):
  respuesta = requests.get(url)
  img = Image.open(BytesIO(respuesta.content))
  img = np.array(img).astype(float)/255

  img = cv2.resize(img, (224,224))
  prediccion = modelFinal.predict(img.reshape(-1, 224, 224, 3))
  return np.argmax(prediccion[0], axis=-1)
#0 = Bird, 1 = Cat  2 = Crop , 3 = Dog 4 = Rabbirt,
url = 'https://thumb.mp-farm.com/69018651/preview.jpg'
prediccion = categorizar (url)
print(prediccion)
if(int(prediccion)==0):
  print("Bird")
if(int(prediccion)==1):
  print("Cat")
if(int(prediccion)==2):
  print("Crop")
if(int(prediccion)==3):
  print("Dog")
if(int(prediccion)==4):
  print("Rabbit")
Ingres el url de su elección para la identificación de animales de acuerdo a las categorías establecidas

