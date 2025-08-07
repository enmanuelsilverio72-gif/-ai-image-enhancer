<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IA Mejorador Ultra 8K - Imágenes y Videos</title>
    <meta name="theme-color" content="#667eea">
    <meta name="description" content="Mejora imágenes y videos con IA real hasta 8K usando modelos avanzados de deep learning">
    <link rel="manifest" href="./manifest.json">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: radial-gradient(ellipse at center, #667eea 0%, #764ba2 50%, #f093fb 100%);
            min-height: 100vh;
            padding: 20px;
            color: white;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, rgba(255,255,255,0.1), transparent, rgba(255,255,255,0.05));
            border-radius: 25px;
            pointer-events: none;
        }

        .header {
            text-align: center;
            margin-bottom: 50px;
            position: relative;
            z-index: 1;
        }

        .header h1 {
            font-size: 3.5em;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #fff, #f0f8ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 4px 20px rgba(255, 255, 255, 0.3);
            font-weight: 700;
        }

        .header p {
            font-size: 1.3em;
            opacity: 0.95;
            margin-bottom: 20px;
            line-height: 1.6;
        }

        .ai-badge {
            display: inline-block;
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: bold;
            margin: 10px 5px;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.1);
            padding: 25px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.15);
            transition: all 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 10px 30px rgba(255, 255, 255, 0.1);
        }

        .feature-icon {
            font-size: 3em;
            margin-bottom: 15px;
            display: block;
        }

        .upload-section {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 50px;
            margin-bottom: 40px;
            border: 3px dashed rgba(255, 255, 255, 0.3);
            text-align: center;
            transition: all 0.4s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .upload-section::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.03), transparent);
            transform: rotate(45deg);
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%) rotate(45deg); }
            100% { transform: translateX(100%) rotate(45deg); }
        }

        .upload-section:hover {
            border-color: rgba(76, 175, 80, 0.8);
            background: rgba(76, 175, 80, 0.1);
            transform: scale(1.02);
        }

        .upload-section.dragover {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.2);
            transform: scale(1.05);
        }

        .upload-icon {
            font-size: 6em;
            margin-bottom: 25px;
            opacity: 0.8;
            position: relative;
            z-index: 1;
        }

        .file-input {
            display: none;
        }

        .upload-btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            padding: 20px 50px;
            border: none;
            border-radius: 30px;
            font-size: 1.3em;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
            position: relative;
            z-index: 1;
            font-weight: 600;
        }

        .upload-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(76, 175, 80, 0.5);
        }

        .media-tabs {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .tab-btn {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1em;
            border: 2px solid transparent;
        }

        .tab-btn.active {
            background: linear-gradient(45deg, #2196F3, #21CBF3);
            box-shadow: 0 4px 15px rgba(33, 150, 243, 0.3);
        }

        .ai-model-selector {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            display: none;
        }

        .model-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .model-option {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            text-align: center;
        }

        .model-option:hover {
            background: rgba(255, 255, 255, 0.15);
        }

        .model-option.selected {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.2);
        }

        .model-name {
            font-weight: bold;
            margin-bottom: 8px;
            font-size: 1.1em;
        }

        .model-desc {
            font-size: 0.9em;
            opacity: 0.8;
            margin-bottom: 8px;
        }

        .model-speed {
            font-size: 0.8em;
            color: #4CAF50;
        }

        .process-btn {
            background: linear-gradient(45deg, #FF6B6B, #FF8E8E);
            color: white;
            padding: 20px 60px;
            border: none;
            border-radius: 30px;
            font-size: 1.4em;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
            display: block;
            margin: 30px auto;
            font-weight: 600;
        }

        .process-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.5);
        }

        .process-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .ai-progress {
            margin: 40px 0;
            text-align: center;
            display: none;
        }

        .progress-title {
            font-size: 1.3em;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .progress-bar {
            width: 100%;
            height: 15px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4CAF50, #45a049, #4CAF50);
            width: 0%;
            transition: width 0.5s ease;
            background-size: 200% 100%;
            animation: progressGradient 2s linear infinite;
        }

        @keyframes progressGradient {
            0% { background-position: 200% 0; }
            100% { background-position: -200% 0; }
        }

        .ai-status {
            font-size: 1.1em;
            margin-top: 15px;
            opacity: 0.9;
        }

        .preview-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-top: 40px;
        }

        .preview-container {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .preview-container h3 {
            margin-bottom: 20px;
            font-size: 1.5em;
            font-weight: 600;
        }

        .preview-canvas, .preview-video {
            max-width: 100%;
            border-radius: 15px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
            background: white;
        }

        .download-btn {
            background: linear-gradient(45deg, #2196F3, #21CBF3);
            color: white;
            padding: 18px 40px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            margin-top: 25px;
            transition: all 0.3s ease;
            font-size: 1.2em;
            font-weight: 600;
        }

        .download-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(33, 150, 243, 0.4);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-top: 25px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
        }

        .stat-item {
            text-align: center;
        }

        .stat-value {
            font-size: 1.6em;
            font-weight: bold;
            color: #4CAF50;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9em;
            opacity: 0.8;
        }

        .enhancement-badge {
            background: linear-gradient(45deg, #FF6B6B, #FF8E8E);
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 1em;
            margin: 15px 0;
            display: inline-block;
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .loading-spinner {
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 3px solid #4CAF50;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .ai-info {
            background: rgba(33, 150, 243, 0.1);
            border: 1px solid rgba(33, 150, 243, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            text-align: left;
        }

        .ai-info h4 {
            margin-bottom: 10px;
            color: #21CBF3;
        }

        @media (max-width: 768px) {
            .preview-section {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2.5em;
            }
            
            .features-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🧠 IA Mejorador Ultra 8K</h1>
            <p>Mejora imágenes y videos con modelos de Deep Learning reales</p>
            <div class="ai-badge">🔥 Con TensorFlow.js Real</div>
            <div class="ai-badge">⚡ Modelos Pre-entrenados</div>
            <div class="ai-badge">🚀 Super-Resolution IA</div>
        </div>

        <div class="features-grid">
            <div class="feature-card">
                <span class="feature-icon">🧠</span>
                <h3>IA Real</h3>
                <p>Modelos ESRGAN y SRCNN reales ejecutándose en tu navegador</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">📹</span>
                <h3>Imágenes y Videos</h3>
                <p>Procesa tanto fotos como videos hasta 8K de resolución</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">⚡</span>
                <h3>Sin Servidor</h3>
                <p>Todo el procesamiento ocurre en tu dispositivo, privacidad total</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">🎯</span>
                <h3>Múltiples Modelos</h3>
                <p>ESRGAN, SRCNN, EDSR - elige el mejor para tu contenido</p>
            </div>
        </div>

        <div class="media-tabs">
            <button class="tab-btn active" id="imageTab">📸 Imágenes</button>
            <button class="tab-btn" id="videoTab">📹 Videos</button>
        </div>

        <div class="upload-section" id="uploadSection">
            <div class="upload-icon" id="uploadIcon">📸</div>
            <h3 id="uploadTitle">Sube tu imagen para mejorar con IA real</h3>
            <p id="uploadDesc">Formatos soportados: JPG, PNG, WEBP, MP4, MOV, AVI</p>
            <input type="file" id="fileInput" class="file-input" accept="image/*,video/*">
            <button class="upload-btn" onclick="document.getElementById('fileInput').click()">
                Seleccionar Archivo
            </button>
        </div>

        <div class="ai-model-selector" id="modelSelector">
            <h3>🧠 Selecciona el Modelo de IA</h3>
            <div class="ai-info">
                <h4>ℹ️ Información sobre los Modelos</h4>
                <p>Cada modelo está especializado para diferentes tipos de contenido y calidades.</p>
            </div>
            <div class="model-grid">
                <div class="model-option selected" data-model="esrgan">
                    <div class="model-name">🔥 Real-ESRGAN</div>
                    <div class="model-desc">Mejor para fotos y imágenes reales</div>
                    <div class="model-speed">⚡ Rápido - Alta calidad</div>
                </div>
                <div class="model-option" data-model="srcnn">
                    <div class="model-name">🎯 SRCNN</div>
                    <div class="model-desc">Excelente para texturas y detalles</div>
                    <div class="model-speed">⚡ Muy rápido</div>
                </div>
                <div class="model-option" data-model="edsr">
                    <div class="model-name">💎 EDSR</div>
                    <div class="model-desc">Máxima calidad para arte y gráficos</div>
                    <div class="model-speed">🐌 Lento - Mejor calidad</div>
                </div>
                <div class="model-option" data-model="waifu2x">
                    <div class="model-name">🎨 Waifu2x</div>
                    <div class="model-desc">Especializado en anime/ilustraciones</div>
                    <div class="model-speed">⚡ Rápido - Ilustraciones</div>
                </div>
            </div>
        </div>

        <button id="processBtn" class="process-btn" style="display: none;">
            🧠 Procesar con IA
        </button>

        <div class="ai-progress" id="aiProgress">
            <div class="progress-title">🧠 IA Procesando...</div>
            <div class="progress-bar">
                <div id="progressFill" class="progress-fill"></div>
            </div>
            <div class="loading-spinner"></div>
            <div class="ai-status" id="aiStatus">Cargando modelo de IA...</div>
        </div>

        <div class="preview-section" style="display: none;" id="previewSection">
            <div class="preview-container">
                <h3>📷 Original</h3>
                <canvas id="originalCanvas" class="preview-canvas" style="display: none;"></canvas>
                <video id="originalVideo" class="preview-video" style="display: none;" controls></video>
                <div class="stats-grid" id="originalStats">
                    <div class="stat-item">
                        <div class="stat-value" id="originalWidth">-</div>
                        <div class="stat-label">Ancho</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="originalHeight">-</div>
                        <div class="stat-label">Alto</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="originalSize">-</div>
                        <div class="stat-label">Tamaño</div>
                    </div>
                </div>
            </div>
            
            <div class="preview-container">
                <h3>✨ Mejorado con IA</h3>
                <canvas id="enhancedCanvas" class="preview-canvas" style="display: none;"></canvas>
                <video id="enhancedVideo" class="preview-video" style="display: none;" controls></video>
                <div class="enhancement-badge" id="enhancementBadge">🧠 IA Aplicada</div>
                <button id="downloadBtn" class="download-btn">📥 Descargar Ultra HD</button>
                <div class="stats-grid" id="enhancedStats">
                    <div class="stat-item">
                        <div class="stat-value" id="enhancedWidth">-</div>
                        <div class="stat-label">Ancho</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="enhancedHeight">-</div>
                        <div class="stat-label">Alto</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="enhancedSize">-</div>
                        <div class="stat-label">Tamaño</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="improvementFactor">-</div>
                        <div class="stat-label">Mejora</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
    <script>
        class RealAIEnhancer {
            constructor() {
                this.currentFile = null;
                this.selectedModel = 'esrgan';
                this.currentMediaType = 'image';
                this.model = null;
                this.originalImageData = null; // Agregar esta línea
                
                this.initializeEventListeners()