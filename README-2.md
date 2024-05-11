
## Mendeteksi Warna dan Urutan Ambang batas dari yang terkecil hingga terbesar dengan OpenCv.

import cv2
import numpy as np
import matplotlib.pyplot as plt

def ubah_latar_belakang_putih(gambar):
    
    hsv = cv2.cvtColor(gambar, cv2.COLOR_BGR2HSV)

    
    lower_white = np.array([0, 0, 200], dtype=np.uint8)
    upper_white = np.array([255, 30, 255], dtype=np.uint8)


    mask = cv2.inRange(hsv, lower_white, upper_white)

    
    gambar[mask > 0] = [255, 255, 255]

    return gambar

gambar = cv2.imread('widyyyy.jpeg')

gambar_white = ubah_latar_belakang_putih(gambar)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(gambar_white, cv2.COLOR_BGR2RGB))
plt.title('Hasil dengan Latar Belakang Putih')

plt.show()

hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

lower_green = np.array([35, 100, 100])
upper_green = np.array([90, 255, 255])

lower_blue = np.array([90, 100, 100])
upper_blue = np.array([150, 255, 255])

lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([179, 255, 255])

mask_green = cv2.inRange(hsv_image, lower_green, upper_green)
mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)
mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = cv2.bitwise_or(mask_red1, mask_red2)

green_result = cv2.bitwise_and(image, image, mask=mask_green)
blue_result = cv2.bitwise_and(image, image, mask=mask_blue)
red_result = cv2.bitwise_and(image, image, mask=mask_red)

plt.figure(figsize=(12, 6))

plt.subplot(131)
plt.imshow(cv2.cvtColor(green_result, cv2.COLOR_BGR2RGB))
plt.title('Green Detection')

plt.subplot(132)
plt.imshow(cv2.cvtColor(blue_result, cv2.COLOR_BGR2RGB))
plt.title('Blue Detection')

plt.subplot(133)
plt.imshow(cv2.cvtColor(red_result, cv2.COLOR_BGR2RGB))
plt.title('Red Detection')

plt.show()






## Untuk mencari ambang batas setiap warna

hsv_image_display = hsv_image.copy()

lower_green = np.array([35, 100, 100])
upper_green = np.array([90, 255, 255])

mask_green = cv2.inRange(hsv_image, lower_green, upper_green)

hsv_image_display[np.where(mask_green == 0)] = 0

lower_blue = np.array([90, 100, 100])
upper_blue = np.array([150, 255, 255])

mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)

hsv_image_display[np.where(mask_blue == 0)] = 0

lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([179, 255, 255])

mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = cv2.bitwise_or(mask_red1, mask_red2)

hsv_image_display[np.where(mask_red == 0)] = 0

final_image = cv2.cvtColor(hsv_image_display, cv2.COLOR_HSV2RGB)

plt.figure(figsize=(12, 6))
plt.imshow(final_image)
plt.axis('off')
plt.title('Deteksi Warna Hijau, Biru, dan Merah')
plt.show()

_, binary_thresh = cv2.threshold(gray_image, 0, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
_, binary_inv_thresh = cv2.threshold(gray_image, 0, 255, cv2.THRESH_BINARY_INV | cv2.THRESH_OTSU)
adaptive_thresh_mean = cv2.adaptiveThreshold(gray_image, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 11, 2)
adaptive_thresh_gaussian = cv2.adaptiveThreshold(gray_image, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 11, 2)

plt.figure(figsize=(12, 6))

plt.subplot(231)
plt.imshow(gray_image, cmap='gray')
plt.title('Original Image')

plt.subplot(232)
plt.imshow(binary_thresh, cmap='gray')
plt.title('Binary Threshold')

plt.subplot(233)
plt.imshow(binary_inv_thresh, cmap='gray')
plt.title('Binary Inverted Threshold')

plt.subplot(234)
plt.imshow(adaptive_thresh_mean, cmap='gray')
plt.title('Adaptive Threshold (Mean)')

plt.subplot(235)
plt.imshow(adaptive_thresh_gaussian, cmap='gray')
plt.title('Adaptive Threshold (Gaussian)')

plt.show()
# Tahapan Meneyelesaikan Project

Gunakan fungsi cv2.imread() untuk membaca gambar dari file.
Gambar yang dibaca memiliki format yang sesuai (misalnya, RGB atau HSV).

Menggunakan fungsi cv2.cvtColor() untuk mengonversi gambar dari ruang warna BGR (default OpenCV) ke HSV.
Ruang warna HSV lebih sesuai untuk mendeteksi warna daripada ruang warna RGB karena pemisahan warna ke dalam hue, saturation, dan value.

Gunakan fungsi cv2.inRange() untuk membuat mask untuk setiap warna berdasarkan nilai ambang batas yang telah ditentukan.

Gunakan operasi bitwise cv2.bitwise_and() untuk mendeteksi warna pada gambar asli menggunakan mask yang telah dibuat.

Menggunakan Matplotlib, konversikan gambar ke format RGB (jika perlu) dan gunakan plt.imshow() untuk menampilkan gambar.

# Teori yang mendukung Project 

1. Ruang Warna HSV
Ruang warna HSV (Hue, Saturation, Value) memisahkan informasi warna menjadi tiga komponen: hue (warna sebenarnya), saturation (kejenuhan), dan value (nilai kecerahan).

2. Thresholding
Thresholding adalah proses mengubah gambar menjadi citra biner dengan cara membagi piksel berdasarkan ambang batas tertentu.

3. Deteksi Warna
Deteksi warna adalah proses mengidentifikasi dan memisahkan objek berdasarkan warna mereka dalam gambar.

4. Bitwise Operations
Operasi bitwise adalah operasi logika yang dilakukan pada setiap bit citra.

5. Pemrosesan Citra Digital
 Pemrosesan citra digital adalah manipulasi gambar dengan menggunakan algoritma komputer untuk meningkatkan citra atau mengekstraksi informasi.

