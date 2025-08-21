

import cv2
import numpy as np
import os
from PIL import Image, ImageEnhance
import imageio.v2 as imageio
from tkinter import Tk, filedialog, Button, Label, StringVar, Entry
from tkinter import ttk
import threading

class VideoImageEnhancer:
    def _init_(self):
        self.root = Tk()
        self.root.title("Mejorador de Calidad - Video e Imágenes")
        self.root.geometry("500x400")
        
        self.setup_ui()
        
    def setup_ui(self):
        Label(self.root, text="Mejorador de Calidad", font=("Arial", 16)).pack(pady=10)
        
        # Selector de archivo
        Button(self.root, text="Seleccionar Archivo", command=self.select_file).pack(pady=5)
        
        # Opciones de mejora
        Label(self.root, text="Nivel de Mejora:").pack(pady=5)
        self.enhance_level = ttk.Combobox(self.root, values=["Bajo", "Medio", "Alto"])
        self.enhance_level.set("Medio")
        self.enhance_level.pack(pady=5)
        
        # Botón de procesamiento
        Button(self.root, text="Mejorar Calidad", command=self.start_processing).pack(pady=10)
        
        # Barra de progreso
        self.progress = ttk.Progressbar(self.root, orient="horizontal", length=300, mode='determinate')
        self.progress.pack(pady=10)
        
        # Etiqueta de estado
        self.status = Label(self.root, text="Listo")
        self.status.pack(pady=5)
        
    def select_file(self):
        file_path = filedialog.askopenfilename(
            filetypes=[("Imágenes", "*.jpg *.jpeg *.png *.bmp"), 
                      ("Videos", "*.mp4 *.avi *.mov *.mkv")]
        )
        if file_path:
            self.file_path = file_path
            self.status.config(text=f"Archivo seleccionado: {os.path.basename(file_path)}")
    
    def start_processing(self):
        if hasattr(self, 'file_path'):
            threading.Thread(target=self.process_file).start()
        else:
            self.status.config(text="Por favor selecciona un archivo primero")
    
    def process_file(self):
        try:
            self.status.config(text="Procesando...")
            self.progress['value'] = 0
            
            # Determinar si es imagen o video
            if self.file_path.lower().endswith(('.png', '.jpg', '.jpeg', '.bmp')):
                self.enhance_image(self.file_path)
            else:
                self.enhance_video(self.file_path)
                
            self.progress['value'] = 100
            self.status.config(text="¡Procesamiento completado!")
            
        except Exception as e:
            self.status.config(text=f"Error: {str(e)}")
    
    def enhance_image(self, image_path):
        # Leer imagen
        image = cv2.imread(image_path)
        
        # Aplicar mejoras según el nivel seleccionado
        level = self.enhance_level.get()
        
        if level == "Bajo":
            enhanced = self.apply_basic_enhancement(image)
        elif level == "Medio":
            enhanced = self.apply_medium_enhancement(image)
        else:
            enhanced = self.apply_high_enhancement(image)
        
        # Guardar imagen mejorada
        output_path = os.path.splitext(image_path)[0] + "_enhanced.jpg"
        cv2.imwrite(output_path, enhanced)
        self.status.config(text=f"Imagen guardada como: {os.path.basename(output_path)}")
    
    def enhance_video(self, video_path):
        # Abrir video
        cap = cv2.VideoCapture(video_path)
        total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
        
        # Preparar video de salida
        fourcc = cv2.VideoWriter_fourcc(*'mp4v')
        fps = cap.get(cv2.CAP_PROP_FPS)
        width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
        height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
        
        output_path = os.path.splitext(video_path)[0] + "_enhanced.mp4"
        out = cv2.VideoWriter(output_path, fourcc, fps, (width, height))
        
        frame_count = 0
        level = self.enhance_level.get()
        
        while True:
            ret, frame = cap.read()
            if not ret:
                break
            
            # Aplicar mejoras al frame
            if level == "Bajo":
                enhanced_frame = self.apply_basic_enhancement(frame)
            elif level == "Medio":
                enhanced_frame = self.apply_medium_enhancement(frame)
            else:
                enhanced_frame = self.apply_high_enhancement(frame)
            
            out.write(enhanced_frame)
            frame_count += 1
            
            # Actualizar progreso
            progress = (frame_count / total_frames) * 100
            self.progress['value'] = progress
            self.status.config(text=f"Procesando frame {frame_count}/{total_frames}")
        
        cap.release()
        out.release()
        self.status.config(text=f"Video guardado como: {os.path.basename(output_path)}")
    
    def apply_basic_enhancement(self, image):
        # Mejoras básicas rápidas
        # Ajuste de contraste y brillo
        enhanced = cv2.convertScaleAbs(image, alpha=1.2, beta=10)
        
        # Enfoque suave
        kernel = np.array([[-1,-1,-1], [-1,9,-1], [-1,-1,-1]])
        enhanced = cv2.filter2D(enhanced, -1, kernel)
        
        return enhanced
    
    def apply_medium_enhancement(self, image):
        # Mejoras moderadas
        # Reducción de ruido
        denoised = cv2.fastNlMeansDenoisingColored(image, None, 10, 10, 7, 21)
        
        # Mejora de color y contraste
        lab = cv2.cvtColor(denoised, cv2.COLOR_BGR2LAB)
        l, a, b = cv2.split(lab)
        clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8,8))
        l = clahe.apply(l)
        enhanced_lab = cv2.merge((l, a, b))
        enhanced = cv2.cvtColor(enhanced_lab, cv2.COLOR_LAB2BGR)
        
        # Enfoque
        kernel = np.array([[-1,-1,-1], [-1,9,-1], [-1,-1,-1]])
        enhanced = cv2.filter2D(enhanced, -1, kernel)
        
        return enhanced
    
    def apply_high_enhancement(self, image):
        # Mejoras avanzadas (más lentas pero mejores resultados)
        # Super-resolución básica (aumento de escala)
        scale_percent = 150  # Aumentar tamaño en 50%
        width = int(image.shape[1] * scale_percent / 100)
        height = int(image.shape[0] * scale_percent / 100)
        dim = (width, height)
        
        # Interpolación de alta calidad
        resized = cv2.resize(image, dim, interpolation=cv2.INTER_CUBIC)
        
        # Mejora de detalles
        enhanced = self.apply_medium_enhancement(resized)
        
        return enhanced

    def run(self):
        self.root.mainloop()

# Ejecutar la aplicación
if _name_ == "_main_":
    app = VideoImageEnhancer()
    app.run()
