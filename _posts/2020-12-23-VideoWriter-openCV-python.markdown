---
title: VideoWriter openCV python
date: 2020-12-22 00:01:00 +0300
categories: [Python, openCV ]
tags: [videowriter, video, openCV, python, ubuntu, fourcc, mp4v, DIVX, XVID]    
image: https://res.cloudinary.com/dxh1bpaim/image/upload/c_scale,w_500/v1612401185/kipunaEC/frames-to-video/2_pyhtp7.jpg
---

***

# Objeto de tipo VideoWriter 
Para guardar un video con [**python**](https://www.python.org/) y [**openCV**](https://opencv.org/), se usa un objeto de tipo [**VideoWriter**](https://docs.opencv.org/master/dd/d43/tutorial_py_video_display.html) 
```python
<VideoWriter object> = cv2.VideoWriter(filename, fourcc, fps, frameSize)
```
1. **filename** es el nombre que tendrá el archivo de video y la extensión `'video.avi'`
2. [**fourcc**](https://es.wikipedia.org/wiki/FourCC) es un código que utiliza 4 caracteres con que se identifica cada [**códec**]( https://www.fourcc.org/fourcc.php).
3. [**fps**](https://es.wikipedia.org/wiki/FPS) velocidad de fotogramas de la secuencia de video.
4. **frameSize** tamaño de los frames que componen el video

***

## fourcc

En ubuntu probé algunos `FourCC` y estos funcionaron para mi.

Para archivos `.mp4`, `.mkv`, `.mov`, `.wmv`

```python
cv2.VideoWriter_fourcc(*'mp4v')
```
Para archivos `.avi`, `.mkv`, `mov`, `wmv`

```python
cv2.VideoWriter_fourcc(*'DIVX')
```

```python
cv2.VideoWriter_fourcc(*'XVID')
```
# Ejemplos con **VideoWriter**

1. [OpenCV - Python creación de video con frames](../Crear-un-video-con-frames-openCV-python/)

***

> Aprendan siempre, aprendan mucho — Mimi

***

