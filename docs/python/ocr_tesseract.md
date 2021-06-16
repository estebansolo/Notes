# OCR con Tesseract

[Tesserocr](https://pypi.org/project/tesserocr/)

Una biblioteca creada por HP (Actualmente mantenida por Google) para realizar reconocimiento optico de caracteres

```python
#import tesserocr # Para hacer OCR
import numpy as np # Para hacer manipulacion basica de imagenes
import matplotlib.pyplot as plt # Para Visualizar imagenes
from PIL import Image # Para cambiar el formato de los archivos

%matplotlib inline
```

```python
texto_largo = plt.imread("ocr_image_test_2.png")
plt.figure(figsize=(15,5))
plt.imshow(texto_largo)
plt.axis(False)
```

(-0.5, 591.5, 147.5, -0.5)

```{figure} ../../images/ocr_image_test_2.png
---
align: center
---
```

```python
texto_ocr = tesserocr.file_to_text("ocr_image_test_2.png", lang="spa")
print(texto_ocr)
```

```python
img = plt.imread("ocr_image_test_1.png")
plt.imshow(img)
```

```{figure} ../../images/ocr_image_test_3.png
---
align: center
---
```

```python
texto_ocr = tesserocr.file_to_text("image_test_1.png", lang="spa")
print(texto_ocr)
```

```python
img.shape
# (62, 228, 4)

img_rgb = img[:,:,:3]
img_rgb.shape
# (62, 228, 3)

img_rgb[0,0,0]
# 0.1764706

img_inv = 1 - img_rgb
plt.imshow(img_inv)
```

```{figure} ../../images/ocr_image_test_4.png
---
align: center
---
```

```python
img_rb = img_inv.mean(axis=2)
plt.imshow(img_rb, cmap="Greys_r")
```

```{figure} ../../images/ocr_image_test_5.png
---
align: center
---
```

```python
img_pil = Image.fromarray(np.uint8(img_rb * 255))

texto_ocr = tesserocr.file_to_text(img_pil, lang="spa")
print(texto_ocr)

texto_ocr = tesserocr.file_to_text(img_inv, lang="spa")
print(texto_ocr)
```