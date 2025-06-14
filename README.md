# Deteccion-de-objetos
# Equipo: Braulio Santiago Altamirano López 22310243---Aldo Melo Fregoso 22310201---Joaquin Monroy Navarro 22310267

# Abre tu editor de texto y su correspondeinte terminal, en este caso es vs code y la terminal de powershell
# 1-Crea un entorno virtual en tu equipo, ejemplo:
python -m venv yolov7_env_py38

# 2-Activa tu entorno virtual:
.\yolov7_env_py38\Scripts\actívate

# 3-Descarga los requierimientos:pytorch
pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html

# 4-Descarga Python 3.8.10 (64-bit) e instala automáticamente
Invoke-WebRequest -Uri "https://www.python.org/ftp/python/3.8.10/python-3.8.10-amd64.exe" -OutFile "$env:TEMP\python38.exe"
Start-Process -Wait -FilePath "$env:TEMP\python38.exe" -ArgumentList "/quiet InstallAllUsers=1 PrependPath=1"

# 5-Descarga el repositorio https://github.com/WongKinYiu/yolov7

# 6-Configura tus archivos data/custom_data.yaml con la cantidad y nombre de clases, ejemplo:

# train: ../train/images
# val: ../valid/images
# nc: 3  # Número de clases
# names: ['clase1', 'clase2', 'clase3']  # Tus clases

# 7-Configura tus archivos cfg/yolov7_custom.yaml con la cantidad de clases:
# parameters
# nc: (number of classes)
# depth_multiple: 1.0  # model depth multiple
# width_multiple: 1.0  # layer channel multiple

# 7-Estructura tus carpetas e ingresa tu dataset a la data de yolov7
# yolov7/
# ├── data/
# │   ├── train/
# │   │   ├── images/  # Imágenes JPG/PNG
# │   │   └── labels/  # Archivos .txt (etiquetas YOLO)
# │   └── valid/       # Misma estructura que train
# └── custom_data.yaml

# 8-Descarga del repositorio yolov7 https://github.com/WongKinYiu/yolov7 los assets, los archivos yolov7.pt y yolov7-tiny.pt y ponlos dentro de la carpeta principal de yolov7

# 9-Dirigete a la carpeta yolov7 custom para comenzar a entrenar tu modelo
cd C:\Users\braul\Desktop\yolov7\SCRIPS\yolov7-custom

# 10-Entrena tu modelo, puedes modificar el tamaño del batch y el numero de epocas 
python train.py --workers 1 --device 0 --batch-size 4 --epochs 100 --img 640 640 --data data/custom_data.yaml --hyp data/hyp.scratch.custom.yaml --cfg cfg/training/yolov7-custom.yaml --name yolov7-custom --weights yolov7.pt

# 11-Cuando el entrenamiento termina busca la carpeta de runs, entra a train,encuentra el numero de entrenamiento correspondiente, entra a wheghts y encuentra el archivo best.pt, muevelo a la carpeta principal de yolov7

# 12 inicia tu deteccion de objetos con:
# Puedes mover la confiaza del algoritmo en cof 0.5---0.1 etc.
python detect.py --weights best.pt --conf 0.5 --img-size 640 --source 0 --view-img --no-trace
