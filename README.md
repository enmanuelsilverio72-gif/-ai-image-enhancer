<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="pageTitle">IA Mejorador Ultra 8K - Instantáneo</title>
    <meta name="theme-color" content="#667eea">
    <meta name="description" content="Mejora imágenes y videos con IA real instantánea hasta 8K">
    <link rel="manifest" href="./manifest.json">
    <style>
        :root {
            --primary: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --secondary: linear-gradient(45deg, #4CAF50, #45a049);
            --accent: linear-gradient(45deg, #FF6B6B, #FF8E8E);
            --blue: linear-gradient(45deg, #2196F3, #21CBF3);
            --glass: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
            --text: white;
            --shadow: 0 8px 32px rgba(31, 38, 135, 0.37);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: var(--primary);
            min-height: 100vh;
            padding: 15px;
            color: var(--text);
            overflow-x: hidden;
            position: relative;
        }

        /* Animación de fondo */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(ellipse at center, transparent 0%, rgba(102, 126, 234, 0.1) 50%, rgba(118, 75, 162, 0.2) 100%);
            animation: backgroundPulse 4s ease-in-out infinite alternate;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes backgroundPulse {
            0% { opacity: 0.3; }
            100% { opacity: 0.7; }
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: var(--glass);
            backdrop-filter: blur(25px);
            border-radius: 30px;
            padding: 40px;
            box-shadow: var(--shadow);
            border: 1px solid var(--glass-border);
            position: relative;
            z-index: 1;
            animation: containerFloat 6s ease-in-out infinite;
        }

        @keyframes containerFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        /* Header mejorado */
        .header {
            text-align: center;
            margin-bottom: 40px;
            position: relative;
        }

        .header::after {
            content: '';
            position: absolute;
            bottom: -20px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 3px;
            background: var(--secondary);
            border-radius: 2px;
        }

        .header h1 {
            font-size: clamp(2.5rem, 5vw, 4rem);
            font-weight: 800;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #fff, #f0f8ff, #e6f3ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 4px 20px rgba(255, 255, 255, 0.3);
            letter-spacing: -0.02em;
            animation: titleGlow 2s ease-in-out infinite alternate;
        }

        @keyframes titleGlow {
            0% { filter: drop-shadow(0 0 10px rgba(255,255,255,0.3)); }
            100% { filter: drop-shadow(0 0 20px rgba(255,255,255,0.6)); }
        }

        .subtitle {
            font-size: 1.3em;
            opacity: 0.95;
            margin-bottom: 25px;
            font-weight: 500;
            line-height: 1.6;
        }

        /* Selector de idiomas */
        .language-selector {
            position: absolute;
            top: 20px;
            right: 20px;
            z-index: 100;
        }

        .language-btn {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            color: var(--text);
            padding: 10px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9em;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .language-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px);
        }

        .language-dropdown {
            position: absolute;
            top: 100%;
            right: 0;
            background: var(--glass);
            backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
            border-radius: 15px;
            padding: 10px;
            display: none;
            min-width: 200px;
            box-shadow: var(--shadow);
            animation: dropdownSlide 0.3s ease;
        }

        @keyframes dropdownSlide {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .language-option {
            padding: 10px 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 0.9em;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .language-option:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        /* Badges animados */
        .badges {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .badge {
            background: var(--accent);
            padding: 8px 20px;
            border-radius: 25px;
            font-size: 0.9em;
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
            animation: badgeBounce 2s ease-in-out infinite;
            transition: transform 0.3s ease;
        }

        .badge:hover {
            transform: scale(1.05);
        }

        .badge:nth-child(1) { animation-delay: 0s; }
        .badge:nth-child(2) { animation-delay: 0.2s; }
        .badge:nth-child(3) { animation-delay: 0.4s; }

        @keyframes badgeBounce {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-3px); }
        }

        /* Grid de características mejorado */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .feature-card {
            background: var(--glass);
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid var(--glass-border);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s;
        }

        .feature-card:hover::before {
            left: 100%;
        }

        .feature-card:hover {
            transform: translateY(-8px) scale(1.02);
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 15px 35px rgba(255, 255, 255, 0.1);
        }

        .feature-icon {
            font-size: 3.5em;
            margin-bottom: 20px;
            display: block;
            animation: iconFloat 3s ease-in-out infinite;
        }

        @keyframes iconFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .feature-card h3 {
            font-size: 1.3em;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .feature-card p {
            opacity: 0.9;
            line-height: 1.6;
        }

        /* Pestañas mejoradas */
        .media-tabs {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 35px;
        }

        .tab-btn {
            background: var(--glass);
            color: var(--text);
            padding: 15px 35px;
            border: 2px solid transparent;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1em;
            font-weight: 600;
            backdrop-filter: blur(10px);
            position: relative;
            overflow: hidden;
        }

        .tab-btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: radial-gradient(circle, rgba(255,255,255,0.2) 0%, transparent 70%);
            transition: all 0.3s ease;
            transform: translate(-50%, -50%);
        }

        .tab-btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .tab-btn.active {
            background: var(--blue);
            border-color: rgba(33, 150, 243, 0.5);
            box-shadow: 0 4px 20px rgba(33, 150, 243, 0.3);
            transform: translateY(-2px);
        }

        /* Sección de carga ultra mejorada */
        .upload-section {
            background: var(--glass);
            border-radius: 25px;
            padding: 60px 40px;
            margin-bottom: 40px;
            border: 3px dashed var(--glass-border);
            text-align: center;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
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
            background: conic-gradient(from 0deg, transparent, rgba(255,255,255,0.05), transparent);
            animation: uploadSpin 4s linear infinite;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .upload-section:hover::before {
            opacity: 1;
        }

        @keyframes uploadSpin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .upload-section:hover {
            border-color: rgba(76, 175, 80, 0.8);
            background: rgba(76, 175, 80, 0.1);
            transform: scale(1.02);
            box-shadow: 0 20px 40px rgba(76, 175, 80, 0.2);
        }

        .upload-section.dragover {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.2);
            transform: scale(1.05);
            box-shadow: 0 25px 50px rgba(76, 175, 80, 0.3);
        }

        .upload-icon {
            font-size: 6em;
            margin-bottom: 25px;
            opacity: 0.9;
            position: relative;
            z-index: 1;
            animation: uploadPulse 2s ease-in-out infinite;
        }

        @keyframes uploadPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .upload-title {
            font-size: 1.6em;
            font-weight: 600;
            margin-bottom: 15px;
            position: relative;
            z-index: 1;
        }

        .upload-desc {
            font-size: 1.1em;
            opacity: 0.8;
            margin-bottom: 30px;
            position: relative;
            z-index: 1;
        }

        .file-input {
            display: none;
        }

        .upload-btn {
            background: var(--secondary);
            color: var(--text);
            padding: 18px 45px;
            border: none;
            border-radius: 30px;
            font-size: 1.3em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
            position: relative;
            z-index: 1;
            overflow: hidden;
        }

        .upload-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .upload-btn:hover::before {
            left: 100%;
        }

        .upload-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(76, 175, 80, 0.5);
        }

        /* Selector de modelos IA mejorado */
        .ai-model-selector {
            background: var(--glass);
            border-radius: 25px;
            padding: 35px;
            margin-bottom: 35px;
            display: none;
            border: 1px solid var(--glass-border);
        }

        .model-title {
            font-size: 1.8em;
            font-weight: 700;
            margin-bottom: 20px;
            text-align: center;
            background: linear-gradient(45deg, #4CAF50, #45a049);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .ai-info {
            background: rgba(33, 150, 243, 0.1);
            border: 1px solid rgba(33, 150, 243, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 25px;
            animation: infoGlow 3s ease-in-out infinite;
        }

        @keyframes infoGlow {
            0%, 100% { box-shadow: 0 0 10px rgba(33, 150, 243, 0.2); }
            50% { box-shadow: 0 0 20px rgba(33, 150, 243, 0.4); }
        }

        .model-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .model-option {
            background: var(--glass);
            padding: 25px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border: 2px solid transparent;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .model-option::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: radial-gradient(circle, rgba(76,175,80,0.1) 0%, transparent 70%);
            transition: all 0.4s ease;
            transform: translate(-50%, -50%);
        }

        .model-option:hover::before {
            width: 200px;
            height: 200px;
        }

        .model-option:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateY(-5px) scale(1.02);
        }

        .model-option.selected {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.2);
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(76, 175, 80, 0.3);
        }

        .model-name {
            font-weight: 700;
            margin-bottom: 12px;
            font-size: 1.2em;
            position: relative;
            z-index: 1;
        }

        .model-desc {
            font-size: 0.95em;
            opacity: 0.85;
            margin-bottom: 12px;
            line-height: 1.5;
            position: relative;
            z-index: 1;
        }

        .model-speed {
            font-size: 0.85em;
            color: #4CAF50;
            font-weight: 600;
            position: relative;
            z-index: 1;
        }

        /* Botón de procesamiento épico */
        .process-btn {
            background: var(--accent);
            color: var(--text);
            padding: 22px 60px;
            border: none;
            border-radius: 35px;
            font-size: 1.5em;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 8px 25px rgba(255, 107, 107, 0.4);
            display: block;
            margin: 35px auto;
            position: relative;
            overflow: hidden;
            letter-spacing: 0.5px;
        }

        .process-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.6s;
        }

        .process-btn:hover::before {
            left: 100%;
        }

        .process-btn:hover {
            transform: translateY(-4px) scale(1.05);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.6);
        }

        .process-btn:disabled {
            opacity: 0.7;
            cursor: not-allowed;
            transform: none;
        }

        /* Progress ultra mejorado */
        .ai-progress {
            margin: 40px 0;
            text-align: center;
            display: none;
            padding: 30px;
            background: var(--glass);
            border-radius: 20px;
            border: 1px solid var(--glass-border);
        }

        .progress-title {
            font-size: 1.4em;
            margin-bottom: 20px;
            font-weight: 600;
            animation: progressPulse 1.5s ease-in-out infinite;
        }

        @keyframes progressPulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .progress-bar {
            width: 100%;
            height: 18px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            overflow: hidden;
            margin: 25px 0;
            position: relative;
        }

        .progress-bar::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, transparent 30%, rgba(255,255,255,0.1) 50%, transparent 70%);
            animation: progressShimmer 2s infinite;
        }

        @keyframes progressShimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4CAF50, #45a049, #4CAF50);
            width: 0%;
            transition: width 0.1s ease;
            background-size: 200% 100%;
            animation: progressGradient 1s linear infinite;
            border-radius: 12px;
            position: relative;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            right: -20px;
            width: 20px;
            height: 100%;
            background: linear-gradient(90deg, rgba(76,175,80,0.8), transparent);
            border-radius: 0 12px 12px 0;
        }

        @keyframes progressGradient {
            0% { background-position: 200% 0; }
            100% { background-position: -200% 0; }
        }

        .ai-status {
            font-size: 1.2em;
            margin-top: 20px;
            opacity: 0.9;
            font-weight: 500;
        }

        .loading-spinner {
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 4px solid #4CAF50;
            width: 50px;
            height: 50px;
            animation: spin 0.8s linear infinite;
            margin: 25px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

