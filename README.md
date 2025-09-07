# binarizcao-lenna-

# Binarização de Imagem com OpenCV 🖼️

Este projeto aplica técnicas de binarização em uma imagem clássica: Lenna. Utiliza OpenCV para leitura, conversão em escala de cinza, suavização com Gaussian Blur e aplicação de threshold binário e binário inverso.

## Como rodar

1. Instale as dependências:
   ```bash
   pip install opencv-python numpy

import cv2
import numpy as np

# Carrega a imagem da Lenna
img = cv2.imread('lenna.png')  # ou 'lenna.jpg', dependendo do formato

# Converte para escala de cinza
img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Aplica suavização (blur)
suave = cv2.GaussianBlur(img, (7, 7), 0)

# Binarização direta e inversa
(T, bin) = cv2.threshold(suave, 160, 255, cv2.THRESH_BINARY)
(T, bin1) = cv2.threshold(suave, 160, 255, cv2.THRESH_BINARY_INV)

# Combina os resultados
resultado = np.vstack([
    np.hstack([suave, bin]),
    np.hstack([bin1, cv2.bitwise_and(img, img, mask=bin1)])
])

# Exibe a imagem
cv2.imshow("Binarização da Lenna", resultado)
cv2.waitKey(0)
cv2.destroyAllWindows()
