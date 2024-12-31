# Proyecto YouTube Downloader y Transcripción

Este proyecto permite descargar videos y audios de YouTube y transcribir el audio utilizando el modelo Whisper de OpenAI.

## Requisitos

- Python 3.7+
- Bibliotecas:
  - `pytubefix`
  - `os`
  - `pathlib`
  - `time`
  - `whisper`

## Instalación

1. Clona este repositorio.
2. Instala las bibliotecas necesarias utilizando pip:

   ```bash
   pip install pytubefix whisper

## Uso
Para descargar videos y audios de YouTube y realizar transcripciones, puedes ejecutar las funciones provistas en el script.

# Ejemplo de uso
## Descargar video
```
from pytubefix import YouTube
from pytubefix.cli import on_progress
import os
from os import remove
from pathlib import Path
import time
import whisper

def descarga_video(link):
    url = link
    yt = YouTube(url, on_progress_callback = on_progress)
    path = 'Videos'
    folder = '@surgir.mp4'
    url_descargas = str(Path.home() / path)
    name ='Asurgir-' + yt.title + '.mp4'
    ys = yt.streams.get_highest_resolution()
    ys.download(output_path=os.path.join(url_descargas, folder), filename=name)
```
## Descargar audio
```
def descarga_audio(link):
    url = link
    yt = YouTube(url, on_progress_callback = on_progress)
    ys = yt.streams.get_audio_only()
    path = 'Videos'
    folder = '@surgir.mp3'
    url_descargas = str(Path.home() / path)
    name ='Asurgir-' + yt.title
    ys.download(output_path=os.path.join(url_descargas, folder), filename=name)
```
## Transcribir audio
```
def video_texto(link):
    url = link
    yt = YouTube(url, on_progress_callback = on_progress)
    ys = yt.streams.get_audio_only()
    name ='Asurgir-' + yt.title
    
    ys.download(filename = name)
    print(name)
    time.sleep(40)

    def transcribe_audio_whisper(audio_file):
        # Cargar el modelo Whisper
        print("Cargando modelo Whisper...")
        model = whisper.load_model("base")  # Cambia "base" por el tamaño que desees
        
        # Transcribir el archivo de audio
        print("Transcribiendo audio...")
        result = model.transcribe(audio_file, language="es")
        
        # Obtener el texto transcrito
        return result["text"]
```
## Ejemplo de uso
```
    audio_path = name + '.m4a'
    texto = transcribe_audio_whisper(audio_path)
    print("Texto transcrito:", texto)
    path_txt = 'Documents'
    folder_txt ='@surgir.txt'
    name_txt= name + '.txt'
    url_descaga_txt = str(Path.home() / path_txt)
    os.makedirs(url_descaga_txt +'/'+folder_txt, exist_ok=True)
    with open(os.path.join(url_descaga_txt, folder_txt, name_txt), 'w') as archivo:
        archivo.write(texto)
    time.sleep(20)
    remove(name + '.m4a')
```
## Contribución
Si deseas contribuir a este proyecto, por favor crea un fork del repositorio y abre un Pull Request con tus cambios.

## Licencia
Este proyecto está bajo la licencia MIT.
