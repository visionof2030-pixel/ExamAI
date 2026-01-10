<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="نظام اختبار تفاعلي ذكي - توليد أسئلة باستخدام الذكاء الاصطناعي من ملفات PDF">
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
    <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.worker.min.js"></script>
    <style>
        :root {
            --primary: #1A5F7A;
            --primary-glow: #2D8F9D;
            --primary-light: #57C3C2;
            --accent: #159895;
            --accent-glow: #1DB9B6;
            --accent-light: #57C3C2;
            --secondary: #4CAF50;
            --secondary-glow: #66BB6A;
            --secondary-light: #81C784;
            --tertiary: #FF9800;
            --tertiary-glow: #FFB74D;
            --tertiary-light: #FFCC80;
            --quaternary: #9C27B0;
            --quaternary-glow: #BA68C8;
            --quaternary-light: #CE93D8;
            --islamic-green: #228B22;
            --islamic-blue: #1A5F7A;
            --islamic-gold: #D4AF37;
            --islamic-teal: #159895;

            --primary-gradient: linear-gradient(135deg, var(--primary) 0%, var(--primary-glow) 50%, var(--primary-light) 100%);
            --accent-gradient: linear-gradient(135deg, var(--accent) 0%, var(--accent-glow) 50%, var(--islamic-teal) 100%);
            --secondary-gradient: linear-gradient(135deg, var(--secondary) 0%, var(--secondary-glow) 50%, var(--islamic-green) 100%);
            --tertiary-gradient: linear-gradient(135deg, var(--tertiary) 0%, var(--tertiary-glow) 50%, var(--islamic-gold) 100%);
            --islamic-gradient: linear-gradient(135deg, var(--islamic-blue) 0%, var(--islamic-teal) 50%, var(--islamic-green) 100%);

            --glow-primary: 0 0 20px rgba(26, 95, 122, 0.7), 0 0 40px rgba(26, 95, 122, 0.5), 0 0 60px rgba(26, 95, 122, 0.3);
            --glow-accent: 0 0 20px rgba(21, 152, 149, 0.7), 0 0 40px rgba(21, 152, 149, 0.5), 0 0 60px rgba(21, 152, 149, 0.3);
            --glow-secondary: 0 0 20px rgba(76, 175, 80, 0.7), 0 0 40px rgba(76, 175, 80, 0.5), 0 0 60px rgba(76, 175, 80, 0.3);
            --glow-tertiary: 0 0 20px rgba(255, 152, 0, 0.7), 0 0 40px rgba(255, 152, 0, 0.5), 0 0 60px rgba(255, 152, 0, 0.3);
            --glow-islamic: 0 0 20px rgba(26, 95, 122, 0.8), 0 0 40px rgba(21, 152, 149, 0.6), 0 0 60px rgba(34, 139, 34, 0.4);

            --bg: linear-gradient(135deg, var(--primary) 0%, var(--accent) 100%);
            --card-bg: rgba(255, 255, 255, 0.95);
            --text: #1F2937;
            --light-text: #6B7280;
            --border: rgba(26, 95, 122, 0.2);
            --shadow: 0 8px 32px rgba(26, 95, 122, 0.1);
            --shadow-hover: 0 20px 40px rgba(26, 95, 122, 0.2);
        }

        .dark-theme {
            --bg: linear-gradient(135deg, #0A3D62 0%, #1A5F7A 100%);
            --card-bg: rgba(15, 30, 45, 0.95);
            --text: #F1F5F9;
            --light-text: #CBD5E1;
            --border: rgba(26, 95, 122, 0.1);
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            --shadow-hover: 0 20px 40px rgba(0, 0, 0, 0.4);
        }

        * {
            box-sizing: border-box;
            font-family: 'Tajawal', Tahoma, Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        body {
            background: var(--bg);
            color: var(--text);
            line-height: 1.7;
            overflow-x: hidden;
            padding-top: 80px;
            transition: all 0.5s ease;
            min-height: 100vh;
        }

        header {
            background: rgba(26, 95, 122, 0.1);
            backdrop-filter: blur(20px);
            color: white;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: var(--shadow);
            border-bottom: 1px solid var(--border);
            padding: 15px 0;
        }

        .header-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }

        .title-section h1 {
            font-size: 1.5rem;
            font-weight: 800;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 2px 10px rgba(26, 95, 122, 0.3);
        }

        .header-actions {
            display: flex;
            gap: 10px;
        }

        .theme-btn, .back-btn {
            background: rgba(26, 95, 122, 0.2);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.3);
            padding: 10px 20px;
            border-radius: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            backdrop-filter: blur(20px);
            text-decoration: none;
            position: relative;
            overflow: hidden;
            box-shadow: 0 0 15px rgba(26, 95, 122, 0.3);
        }

        .theme-btn:hover, .back-btn:hover {
            background: rgba(26, 95, 122, 0.3);
            transform: translateY(-3px);
            box-shadow: 0 0 25px rgba(26, 95, 122, 0.5), 0 5px 20px rgba(0, 0, 0, 0.2);
            border-color: rgba(255, 255, 255, 0.5);
        }

        main {
            max-width: 1000px;
            margin: 30px auto;
            padding: 0 20px;
        }

        .hero-section {
            background: linear-gradient(135deg, rgba(26, 95, 122, 0.15), rgba(21, 152, 149, 0.15));
            backdrop-filter: blur(30px);
            color: white;
            border-radius: 24px;
            padding: 40px;
            margin-bottom: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(26, 95, 122, 0.15),
                        inset 0 1px 0 rgba(255, 255, 255, 0.2);
            border: 2px solid rgba(255, 255, 255, 0.1);
        }

        .hero-section::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: var(--accent-gradient);
            opacity: 0.1;
            z-index: -1;
        }

        .hero-content {
            position: relative;
            z-index: 1;
        }

        .hero-title {
            font-size: 2.2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #fff 0%, #f0f0f0 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 20px;
        }

        .hero-subtitle {
            font-size: 1.1rem;
            margin-bottom: 25px;
            opacity: 0.9;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(30px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1),
                        inset 0 1px 0 rgba(255, 255, 255, 0.1);
            transition: all 0.4s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
        }

        .card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 5px;
            background: var(--islamic-gradient);
        }

        .card:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: var(--shadow-hover);
        }

        .input-group {
            margin: 25px 0;
        }

        .input-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--text);
            font-size: 1.1rem;
        }

        .input-field {
            width: 100%;
            padding: 18px 25px;
            border: 2px solid var(--border);
            border-radius: 15px;
            font-size: 1.1rem;
            background: var(--card-bg);
            color: var(--text);
            transition: all 0.3s ease;
            border: 2px solid rgba(26, 95, 122, 0.3);
            box-shadow: 0 5px 15px rgba(26, 95, 122, 0.1);
        }

        .input-field:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 20px rgba(21, 152, 149, 0.3);
        }

        .file-upload-container {
            position: relative;
            margin: 25px 0;
        }

        .file-upload-label {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 20px;
            border: 3px dashed var(--accent);
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(21, 152, 149, 0.05);
            text-align: center;
        }

        .file-upload-label:hover {
            background: rgba(21, 152, 149, 0.1);
            border-color: var(--accent-glow);
            transform: translateY(-5px);
        }

        .file-upload-label i {
            font-size: 3rem;
            color: var(--accent);
            margin-bottom: 15px;
        }

        .file-upload-label h4 {
            color: var(--text);
            margin-bottom: 10px;
        }

        .file-upload-label p {
            color: var(--light-text);
            font-size: 0.9rem;
        }

        .file-input {
            display: none;
        }

        .file-preview {
            margin-top: 20px;
            padding: 20px;
            border-radius: 15px;
            background: rgba(26, 95, 122, 0.05);
            border: 2px solid var(--border);
            display: none;
        }

        .file-preview.active {
            display: block;
            animation: slideDown 0.5s ease;
        }

        .file-info {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .file-icon {
            font-size: 2rem;
            color: var(--accent);
        }

        .file-details h5 {
            color: var(--text);
            margin-bottom: 5px;
        }

        .file-details p {
            color: var(--light-text);
            font-size: 0.9rem;
        }

        .pdf-preview {
            max-height: 300px;
            overflow-y: auto;
            padding: 15px;
            background: var(--card-bg);
            border-radius: 10px;
            border: 1px solid var(--border);
            font-size: 0.9rem;
            line-height: 1.6;
        }

        .pdf-preview h6 {
            color: var(--primary);
            margin-bottom: 10px;
            padding-bottom: 5px;
            border-bottom: 2px solid var(--accent);
        }

        .pdf-text {
            white-space: pre-wrap;
            font-family: 'Tajawal', sans-serif;
        }

        .remove-file-btn {
            background: rgba(220, 38, 38, 0.1);
            color: #dc2626;
            border: 2px solid #dc2626;
            padding: 8px 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            margin-top: 10px;
        }

        .remove-file-btn:hover {
            background: rgba(220, 38, 38, 0.2);
            transform: translateY(-2px);
        }

        .method-selector {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .method-tab {
            flex: 1;
            min-width: 200px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            border: 2px solid transparent;
        }

        .method-tab.active {
            background: rgba(21, 152, 149, 0.15);
            border-color: var(--accent);
            box-shadow: 0 0 20px rgba(21, 152, 149, 0.3);
        }

        .method-tab:hover:not(.active) {
            background: rgba(255, 255, 255, 0.1);
            transform: translateY(-5px);
        }

        .method-icon {
            font-size: 2rem;
            color: var(--accent);
            margin-bottom: 10px;
        }

        .method-title {
            font-weight: 700;
            color: var(--text);
            margin-bottom: 5px;
        }

        .method-desc {
            color: var(--light-text);
            font-size: 0.9rem;
        }

        .btn {
            padding: 15px 30px;
            border-radius: 15px;
            font-weight: 700;
            text-decoration: none;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            font-size: 1rem;
            border: none;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .btn-primary {
            background: var(--accent-gradient);
            color: white;
            box-shadow: var(--glow-accent), 0 8px 25px rgba(21, 152, 149, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .btn-secondary {
            background: var(--primary-gradient);
            color: white;
            box-shadow: var(--glow-primary), 0 8px 25px rgba(26, 95, 122, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .btn-islamic {
            background: var(--islamic-gradient);
            color: white;
            box-shadow: var(--glow-islamic), 0 8px 25px rgba(26, 95, 122, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
            animation: islamic-pulse 2s infinite alternate;
        }

        @keyframes islamic-pulse {
            0% {
                box-shadow: var(--glow-islamic), 0 8px 25px rgba(26, 95, 122, 0.4);
            }
            100% {
                box-shadow: 0 0 25px rgba(26, 95, 122, 0.8),
                            0 0 50px rgba(21, 152, 149, 0.6),
                            0 0 75px rgba(34, 139, 34, 0.4),
                            0 15px 40px rgba(26, 95, 122, 0.6);
            }
        }

        .btn-success {
            background: var(--secondary-gradient);
            color: white;
            box-shadow: var(--glow-secondary), 0 8px 25px rgba(76, 175, 80, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .btn-warning {
            background: var(--tertiary-gradient);
            color: white;
            box-shadow: var(--glow-tertiary), 0 8px 25px rgba(255, 152, 0, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            transition: left 0.7s;
            z-index: -1;
        }

        .btn:hover {
            transform: translateY(-8px) scale(1.05);
            border-color: rgba(255, 255, 255, 0.5);
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn-primary:hover {
            box-shadow: var(--glow-accent), 0 15px 40px rgba(21, 152, 149, 0.6);
        }

        .btn-secondary:hover {
            box-shadow: var(--glow-primary), 0 15px 40px rgba(26, 95, 122, 0.6);
        }

        .btn:disabled {
            background: #9CA3AF;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
            opacity: 0.6;
        }

        .btn:disabled:hover::before {
            left: -100%;
        }

        .question-box {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 30px;
            margin-bottom: 25px;
            border-radius: 20px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .question-box::before {
            content: "";
            position: absolute;
            top: 0;
            right: 0;
            width: 100%;
            height: 5px;
            background: var(--primary-gradient);
        }

        .question-box:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow-hover);
        }

        .question-number {
            font-size: 1.3em;
            color: var(--primary);
            margin-bottom: 15px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .question-number i {
            color: var(--accent);
            font-size: 1.2em;
        }

        .question-text {
            font-size: 1.2em;
            margin-bottom: 25px;
            line-height: 1.7;
            color: var(--text);
            font-weight: 500;
        }

        .options {
            position: relative;
        }

        .options label {
            display: flex;
            align-items: center;
            padding: 18px 20px;
            margin: 12px 0;
            border: 2px solid var(--border);
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: var(--card-bg);
            position: relative;
            overflow: hidden;
            font-weight: 500;
        }

        .options label::before {
            content: "";
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 0;
            background: var(--primary-gradient);
            transition: width 0.3s ease;
            z-index: 0;
        }

        .options label:hover:not(.locked) {
            border-color: var(--primary);
            transform: translateX(-8px);
            box-shadow: 0 5px 15px rgba(26, 95, 122, 0.2);
        }

        .options label:hover:not(.locked)::before {
            width: 4px;
        }

        .options input[type="radio"] {
            margin-left: 12px;
            transform: scale(1.3);
            z-index: 1;
        }

        .options label.locked {
            cursor: not-allowed;
            opacity: 0.8;
            pointer-events: none;
        }

        .options input[type="radio"]:disabled {
            cursor: not-allowed;
        }

        .options label.selected {
            background: linear-gradient(135deg, rgba(26, 95, 122, 0.15), rgba(21, 152, 149, 0.15));
            border: 2px solid var(--accent);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.3);
        }

        .options label.selected::before {
            width: 6px;
            background: var(--accent-gradient);
        }

        .options label.correct-answer {
            background: linear-gradient(135deg, rgba(76, 175, 80, 0.2), rgba(102, 187, 106, 0.2));
            border: 2px solid var(--secondary);
            box-shadow: 0 0 15px rgba(76, 175, 80, 0.3);
            animation: correctPulse 0.5s ease;
        }

        @keyframes correctPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        .options label.correct-answer::before {
            width: 6px;
            background: var(--secondary-gradient);
        }

        .options label.wrong-answer {
            background: linear-gradient(135deg, rgba(21, 152, 149, 0.2), rgba(45, 143, 157, 0.2));
            border: 2px solid var(--accent);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.3);
            animation: wrongShake 0.5s ease;
        }

        @keyframes wrongShake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .options label.wrong-answer::before {
            width: 6px;
            background: var(--accent-gradient);
        }

        .explanation {
            margin-top: 25px;
            padding: 25px;
            border-radius: 15px;
            display: none;
            background: linear-gradient(135deg, rgba(26, 95, 122, 0.05), rgba(21, 152, 149, 0.05));
            border-left: 4px solid var(--secondary);
            animation: slideDown 0.5s ease;
            backdrop-filter: blur(10px);
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-15px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .progress-bar {
            height: 15px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            margin-bottom: 30px;
            overflow: hidden;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
            position: relative;
            backdrop-filter: blur(10px);
        }

        .progress {
            height: 100%;
            background: var(--islamic-gradient);
            box-shadow: 0 0 15px rgba(26, 95, 122, 0.5);
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 10px;
            position: relative;
            overflow: hidden;
        }

        .progress::after {
            content: "";
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            animation: shimmer 1.5s infinite;
        }

        @keyframes shimmer {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        #result-box {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 30px;
            margin-top: 30px;
            border-radius: 20px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            display: none;
            animation: slideUp 0.6s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 30px;
            flex-wrap: wrap;
            gap: 20px;
        }

        .quiz-info {
            font-size: 1rem;
            color: var(--light-text);
            background: linear-gradient(135deg, rgba(26, 95, 122, 0.1), rgba(21, 152, 149, 0.1));
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: 600;
            backdrop-filter: blur(10px);
        }

        #timer {
            font-size: 1.1rem;
            font-weight: bold;
            color: white;
            margin-left: 20px;
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(26, 95, 122, 0.2);
            backdrop-filter: blur(20px);
            padding: 10px 20px;
            border-radius: 25px;
            border: 2px solid rgba(26, 95, 122, 0.3);
            box-shadow: 0 0 15px rgba(26, 95, 122, 0.2);
        }

        .timer-warning {
            background: rgba(255, 152, 0, 0.2) !important;
            border-color: rgba(255, 152, 0, 0.3) !important;
            box-shadow: 0 0 20px rgba(255, 152, 0, 0.3) !important;
            animation: warning-pulse 0.8s infinite alternate;
        }

        @keyframes warning-pulse {
            from {
                box-shadow: 0 0 15px rgba(255, 152, 0, 0.3);
            }
            to {
                box-shadow: 0 0 25px rgba(255, 152, 0, 0.5), 0 0 40px rgba(255, 152, 0, 0.3);
            }
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1001;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(10px);
        }

        .modal-content {
            background: var(--card-bg);
            margin: 5% auto;
            padding: 30px;
            border-radius: 25px;
            width: 90%;
            max-width: 800px;
            max-height: 85vh;
            overflow-y: auto;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
            border: 2px solid var(--border);
            animation: modalSlideIn 0.5s ease;
        }

        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .close-modal {
            color: var(--light-text);
            float: left;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s;
        }

        .close-modal:hover {
            color: var(--text);
        }

        .modal-header {
            margin-bottom: 25px;
            text-align: center;
            border-bottom: 2px solid var(--accent);
            padding-bottom: 15px;
        }

        .modal-header h3 {
            color: var(--text);
            font-size: 1.5rem;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        @media (max-width: 768px) {
            body {
                padding-top: 70px;
            }

            .header-container {
                padding: 0 15px;
                flex-direction: column;
                gap: 15px;
            }

            .title-section h1 {
                font-size: 1.3rem;
            }

            .hero-title {
                font-size: 1.8rem;
            }

            .hero-subtitle {
                font-size: 1rem;
            }

            .card, .question-box {
                padding: 25px;
            }

            .controls {
                flex-direction: column;
                align-items: stretch;
            }

            .btn {
                width: 100%;
                justify-content: center;
                padding: 14px 25px;
                font-size: 1rem;
            }

            .method-selector {
                flex-direction: column;
            }

            .method-tab {
                min-width: 100%;
            }
        }

        .loading {
            display: none;
            text-align: center;
            padding: 30px;
        }

        .loader {
            border: 5px solid rgba(26, 95, 122, 0.2);
            border-top: 5px solid var(--accent);
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .error-message {
            background: linear-gradient(135deg, rgba(220, 38, 38, 0.1), rgba(239, 68, 68, 0.1));
            border: 2px solid #ef4444;
            color: #dc2626;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            display: none;
        }

        .api-key-section {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 25px;
            margin: 20px 0;
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        .api-info {
            background: rgba(26, 95, 122, 0.1);
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            font-size: 0.9rem;
        }

        .api-info a {
            color: var(--accent);
            text-decoration: none;
            font-weight: bold;
        }

        .api-info a:hover {
            text-decoration: underline;
        }

        .current-quiz-title {
            font-size: 1.8rem;
            font-weight: 800;
            text-align: center;
            margin: 20px 0;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        /* Navigation styles */
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
            gap: 20px;
        }

        /* Questions Grid Modal */
        #questions-grid-modal {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .question-status-grid-modal {
            width: 60px;
            height: 60px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            background: var(--card-bg);
            border: 2px solid var(--border);
            color: var(--text);
        }

        .question-status-grid-modal:hover {
            transform: translateY(-5px) scale(1.1);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }

        .question-status-grid-modal.current {
            border-color: var(--accent);
            background: rgba(21, 152, 149, 0.2);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.4);
        }

        .question-status-grid-modal.answered {
            border-color: var(--secondary);
            background: rgba(76, 175, 80, 0.2);
        }

        .question-status-grid-modal.flagged {
            border-color: var(--tertiary);
            background: rgba(255, 152, 0, 0.2);
        }

        /* Current Score Modal */
        .current-score-content {
            text-align: center;
            padding: 20px;
        }

        .score-circle {
            position: relative;
            width: 150px;
            height: 150px;
            margin: 0 auto 30px;
        }

        .score-bg {
            fill: none;
            stroke: rgba(26, 95, 122, 0.1);
            stroke-width: 10;
        }

        .score-fill {
            fill: none;
            stroke: var(--accent);
            stroke-width: 10;
            stroke-linecap: round;
            stroke-dasharray: 440;
            stroke-dashoffset: 440;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
            transition: stroke-dashoffset 1s ease;
        }

        .score-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--text);
        }

        .score-details {
            text-align: right;
            padding: 20px;
            background: rgba(26, 95, 122, 0.05);
            border-radius: 15px;
            margin-top: 20px;
        }

        .score-details p {
            margin: 10px 0;
            color: var(--text);
        }

        /* New Styles for Enhanced Features */
        @keyframes slideInRight {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        @keyframes slideOutRight {
            from {
                transform: translateX(0);
                opacity: 1;
            }
            to {
                transform: translateX(100%);
                opacity: 0;
            }
        }

        .success-message {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: bold;
            position: fixed;
            top: 100px;
            right: 20px;
            background: var(--secondary-gradient);
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            z-index: 10000;
            box-shadow: var(--glow-secondary);
            animation: slideInRight 0.5s ease;
        }

        .quiz-stats {
            background: rgba(26, 95, 122, 0.1);
            padding: 10px 15px;
            border-radius: 10px;
            margin: 10px 0;
            font-size: 0.9rem;
            color: var(--text);
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }

        .batch-indicator {
            background: var(--tertiary-gradient);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8rem;
            margin-right: 10px;
        }

        .category-badge {
            background: var(--accent-gradient);
            color: white;
            padding: 5px 10px;
            border-radius: 10px;
            font-size: 0.8rem;
            margin-right: 10px;
        }

        .difficulty-badge {
            background: var(--primary-gradient);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8rem;
            margin-right: 10px;
        }

        .source-info {
            background: rgba(21, 152, 149, 0.1);
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 0.85rem;
            color: var(--light-text);
            margin-top: 10px;
            border-right: 3px solid var(--accent);
        }

        .question-meta {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .add-more-section {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            background: rgba(255, 152, 0, 0.1);
            border-radius: 15px;
            border: 2px dashed var(--tertiary);
        }

        .add-more-section h4 {
            color: var(--text);
            margin-bottom: 15px;
            font-size: 1.2rem;
        }

        .stats-overview {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .stat-card {
            background: rgba(255, 255, 255, 0.05);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid var(--border);
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--light-text);
        }

        .pdf-context-info {
            background: rgba(26, 95, 122, 0.05);
            padding: 10px 15px;
            border-radius: 10px;
            margin: 10px 0;
            font-size: 0.9rem;
            color: var(--light-text);
        }

        .pdf-context-info i {
            color: var(--accent);
            margin-left: 5px;
        }

        .batch-navigation {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .batch-btn {
            padding: 8px 15px;
            border-radius: 8px;
            background: rgba(26, 95, 122, 0.1);
            border: 1px solid var(--border);
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .batch-btn:hover {
            background: rgba(26, 95, 122, 0.2);
            transform: translateY(-2px);
        }

        .batch-btn.active {
            background: var(--accent-gradient);
            color: white;
            border-color: var(--accent);
        }

        .smart-suggestions {
            background: rgba(76, 175, 80, 0.1);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            border-right: 4px solid var(--secondary);
        }

        .smart-suggestions h5 {
            color: var(--secondary);
            margin-bottom: 10px;
            font-size: 1rem;
        }

        .suggestions-list {
            list-style: none;
            padding-right: 20px;
        }

        .suggestions-list li {
            margin-bottom: 8px;
            position: relative;
        }

        .suggestions-list li:before {
            content: "✓";
            position: absolute;
            right: -20px;
            color: var(--secondary);
        }

        @keyframes pulse {
            0% {
                box-shadow: 0 0 0 0 rgba(255, 152, 0, 0.4);
            }
            70% {
                box-shadow: 0 0 0 10px rgba(255, 152, 0, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(255, 152, 0, 0);
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="glass-effect">
        <div class="header-container">
            <div class="title-section">
                <h1 id="main-title">نظام الاختبارات الذكي</h1>
            </div>
            <div class="header-actions">
                <button class="theme-btn" id="themeBtn">
                    <i class="fas fa-moon"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main>
        <!-- Setup Section -->
        <section id="setup-section" class="hero-section">
            <div class="hero-content">
                <h1 class="hero-title">نظام الاختبارات الذكي التفاعلي</h1>
                <p class="hero-subtitle">أنشئ اختبارات مخصصة في أي مجال باستخدام الذكاء الاصطناعي</p>
                
                <!-- طريقة الاختيار -->
                <div class="method-selector">
                    <div class="method-tab active" onclick="selectMethod('manual')" id="manual-tab">
                        <div class="method-icon">
                            <i class="fas fa-keyboard"></i>
                        </div>
                        <div class="method-title">إدخال يدوي</div>
                        <div class="method-desc">أدخل عنوان وموضوع الاختبار</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('pdf')" id="pdf-tab">
                        <div class="method-icon">
                            <i class="fas fa-file-pdf"></i>
                        </div>
                        <div class="method-title">رفع ملف PDF</div>
                        <div class="method-desc">تحميل ملف وتوليد أسئلة منه</div>
                    </div>
                </div>

                <!-- قسم مفتاح API -->
                <div class="api-key-section">
                    <div class="input-group">
                        <label for="api-key"><i class="fas fa-key"></i> مفتاح Google Gemini API</label>
                        <input type="password" id="api-key" class="input-field" 
                               placeholder="أدخل مفتاح API الخاص بك هنا">
                        <div class="api-info">
                            <p><i class="fas fa-info-circle"></i> للحصول على مفتاح API:</p>
                            <ol style="margin-right: 20px; margin-top: 10px;">
                                <li>اذهب إلى <a href="https://makersuite.google.com/app/apikey" target="_blank">Google AI Studio</a></li>
                                <li>سجل الدخول بحساب Google</li>
                                <li>أنشئ مفتاح API جديد</li>
                                <li>انسخ المفتاح وألصقه هنا</li>
                            </ol>
                            <p style="margin-top: 10px; color: var(--accent);">
                                <i class="fas fa-lightbulb"></i> يستخدم النظام نموذج: <strong>Gemini 2.5 Flash Lite</strong>
                            </p>
                        </div>
                    </div>
                </div>

                <!-- قسم الإدخال اليدوي -->
                <div id="manual-section">
                    <div class="input-group">
                        <label for="quiz-title"><i class="fas fa-heading"></i> عنوان الاختبار</label>
                        <input type="text" id="quiz-title" class="input-field" 
                               placeholder="مثال: الفقه الإسلامي - أحكام الصلاة">
                    </div>

                    <div class="input-group">
                        <label for="quiz-topic"><i class="fas fa-book"></i> تفاصيل الموضوع (اختياري)</label>
                        <textarea id="quiz-topic" class="input-field" rows="3" 
                                  placeholder="يمكنك إضافة تفاصيل إضافية عن الموضوع الذي تريد اختباره..."></textarea>
                    </div>
                </div>

                <!-- قسم رفع ملف PDF -->
                <div id="pdf-section" style="display: none;">
                    <div class="file-upload-container">
                        <label for="pdf-file" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <h4>انقر لرفع ملف PDF</h4>
                            <p>أو اسحب وأفلت الملف هنا</p>
                            <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;">
                                الحد الأقصى لحجم الملف: 10MB
                            </p>
                        </label>
                        <input type="file" id="pdf-file" class="file-input" accept=".pdf" onchange="handlePDFUpload(event)">
                        
                        <div class="file-preview" id="pdf-preview">
                            <div class="file-info">
                                <div class="file-icon">
                                    <i class="fas fa-file-pdf"></i>
                                </div>
                                <div class="file-details">
                                    <h5 id="pdf-filename"></h5>
                                    <p id="pdf-filesize"></p>
                                    <p id="pdf-pages"></p>
                                </div>
                            </div>
                            <div class="pdf-preview" id="pdf-content-preview">
                                <h6>عينة من المحتوى:</h6>
                                <div class="pdf-text" id="pdf-sample-text"></div>
                            </div>
                            <button class="remove-file-btn" onclick="removePDF()">
                                <i class="fas fa-trash"></i> إزالة الملف
                            </button>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="num-questions"><i class="fas fa-question-circle"></i> عدد الأسئلة المطلوبة</label>
                        <select id="num-questions" class="input-field">
                            <option value="5">5 أسئلة</option>
                            <option value="10" selected>10 أسئلة</option>
                            <option value="15">15 أسئلة</option>
                            <option value="20">20 أسئلة</option>
                        </select>
                    </div>

                    <div class="input-group">
                        <label for="question-type"><i class="fas fa-filter"></i> نوع الأسئلة</label>
                        <select id="question-type" class="input-field">
                            <option value="mixed">مختلطة (معلومات + تطبيقات)</option>
                            <option value="concepts">مفاهيم أساسية</option>
                            <option value="applications">أسئلة تطبيقية</option>
                            <option value="analysis">أسئلة تحليلية</option>
                        </select>
                    </div>
                </div>

                <!-- زر التوليد -->
                <button class="btn btn-islamic" onclick="generateQuiz()" style="width: 100%; margin-top: 20px;">
                    <i class="fas fa-robot"></i> توليد اختبار باستخدام الذكاء الاصطناعي
                </button>

                <div class="loading" id="loading">
                    <div class="loader"></div>
                    <p>جارٍ توليد الأسئلة باستخدام الذكاء الاصطناعي...</p>
                    <p style="font-size: 0.9rem; opacity: 0.7;" id="loading-details"></p>
                </div>

                <div class="error-message" id="error-message"></div>
            </div>
        </section>

        <!-- Quiz Section (Hidden Initially) -->
        <section id="quiz-section" style="display: none;">
            <h2 class="current-quiz-title" id="current-quiz-title"></h2>
            
            <!-- Progress Bar -->
            <div class="progress-bar glass-effect">
                <div class="progress" id="progress"></div>
            </div>

            <!-- Quiz Container -->
            <div id="quiz"></div>

            <!-- Controls -->
            <div class="controls">
                <div class="quiz-info" id="quiz-info"></div>
                <div id="timer">⏱️ <span id="time-display">10:00</span></div>
                <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                    <button class="btn btn-primary" onclick="openQuestionsModal()">
                        <i class="fas fa-list"></i>
                        قائمة الأسئلة
                    </button>
                    <button class="btn btn-warning" onclick="toggleMarkForReview()" id="mark-review-btn">
                        <i class="fas fa-flag"></i>
                        وضع علامة للمراجعة
                    </button>
                    <button class="btn btn-islamic" onclick="finishQuiz()">
                        <i class="fas fa-flag-checkered"></i>
                        إنهاء الاختبار
                    </button>
                    <button class="btn btn-secondary" onclick="openCurrentScoreModal()">
                        <i class="fas fa-chart-bar"></i>
                        الدرجات الحالية
                    </button>
                </div>
            </div>

            <!-- قسم إضافة المزيد من الأسئلة -->
            <div class="add-more-section" id="add-more-section" style="display: none;">
                <h4><i class="fas fa-plus-circle"></i> هل تريد المزيد من الأسئلة؟</h4>
                <p style="color: var(--light-text); margin-bottom: 15px;">
                    يمكنك إضافة المزيد من الأسئلة من نفس ملف PDF، مع ضمان عدم التكرار وتغطية أجزاء جديدة
                </p>
                <button class="btn btn-warning" onclick="addMoreQuestions()" id="add-more-questions-btn">
                    <i class="fas fa-plus"></i> إضافة 10 أسئلة أخرى
                </button>
                <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;">
                    <i class="fas fa-lightbulb"></i> يستخدم نظام الذكاء الاصطناعي: <strong>Gemini 2.5 Flash Lite</strong>
                </p>
            </div>
        </section>

        <!-- Final Results -->
        <div id="result-box" class="card">
            <h3 id="result" style="color: var(--text); margin-bottom: 20px;"></h3>
            <p id="percentage" style="font-size: 1.4rem; margin-bottom: 15px;"></p>
            <p id="evaluation" style="font-weight: bold; font-size: 1.3rem;"></p>

            <!-- قسم النتائج المتقدمة -->
            <div id="advanced-results" style="display: none;">
                <!-- قسم الإحصائيات -->
                <div class="stats-overview" id="stats-overview"></div>

                <!-- قسم النصائح الذكية -->
                <div class="smart-suggestions" id="smart-suggestions"></div>

                <!-- قسم تحميل PDF -->
                <div class="share-results">
                    <h4 style="color: var(--text); margin-bottom: 20px;">
                        <i class="fas fa-file-pdf"></i> تقرير النتائج
                    </h4>
                    <div class="share-buttons" style="display: flex; gap: 15px; flex-wrap: wrap;">
                        <button class="btn btn-success" onclick="generatePDF()">
                            <i class="fas fa-file-pdf"></i> تحميل تقرير PDF
                        </button>
                        <button class="btn btn-secondary" onclick="restartQuiz()">
                            <i class="fas fa-redo"></i> إعادة الاختبار
                        </button>
                        <button class="btn btn-primary" onclick="backToSetup()">
                            <i class="fas fa-plus"></i> إنشاء اختبار جديد
                        </button>
                        <button class="btn btn-warning" onclick="addMoreQuestionsAfterTest()">
                            <i class="fas fa-plus-circle"></i> إضافة المزيد من الأسئلة
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- النافذة المنبثقة لعرض الدرجات الحالية -->
    <div id="currentScoreModal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCurrentScoreModal()">&times;</span>
            <div class="modal-header">
                <h3><i class="fas fa-chart-bar"></i> الدرجات الحالية</h3>
            </div>
            <div class="current-score-content">
                <div class="score-circle">
                    <svg width="150" height="150">
                        <circle class="score-bg" cx="75" cy="75" r="70"></circle>
                        <circle class="score-fill" cx="75" cy="75" r="70" id="score-circle-fill"></circle>
                    </svg>
                    <div class="score-text" id="score-percentage">0%</div>
                </div>
                <div class="score-details">
                    <p id="current-score-details"></p>
                    <p id="current-correct-details"></p>
                    <p id="current-progress-details"></p>
                    <p id="current-batch-details"></p>
                </div>
            </div>
        </div>
    </div>

    <!-- النافذة المنبثقة لقائمة الأسئلة -->
    <div id="questionsModal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeQuestionsModal()">&times;</span>
            <div class="modal-header">
                <h3><i class="fas fa-th-list"></i> قائمة الأسئلة</h3>
            </div>
            <div id="questions-grid-modal"></div>
            <button class="btn btn-primary" onclick="closeQuestionsModal()" style="margin-top:20px; width: 100%;">
                <i class="fas fa-times"></i>
                إغلاق القائمة
            </button>
        </div>
    </div>

    <script>
        // المتغيرات العامة
        let questions = [];
        let currentQuestionIndex = 0;
        let userAnswers = [];
        let timeLeft = 10 * 60;
        let timerInterval;
        let markedQuestions = [];
        let answerLocked = [];
        let shuffledQuestions = [];
        let soundEnabled = true;
        let currentQuizTitle = "";
        let apiKey = "";
        let pdfFile = null;
        let pdfText = "";
        let currentMethod = "manual";
        
        // متغيرات جديدة للتحسينات
        let pdfContext = "";
        let existingQuestions = [];
        let currentBatch = 1;
        let totalQuestionsGenerated = 0;
        let allQuestionsHistory = [];
        
        // تحديد نموذج Gemini المستخدم
        const GEMINI_MODEL = "gemini-2.5-flash-lite";
        const GEMINI_API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-lite:generateContent";

        // اختيار طريقة الاختبار
        function selectMethod(method) {
            currentMethod = method;
            
            document.getElementById('manual-tab').classList.remove('active');
            document.getElementById('pdf-tab').classList.remove('active');
            document.getElementById(`${method}-tab`).classList.add('active');
            
            document.getElementById('manual-section').style.display = method === 'manual' ? 'block' : 'none';
            document.getElementById('pdf-section').style.display = method === 'pdf' ? 'block' : 'none';
        }

        // التحقق من تفضيل الوضع الداكن
        function checkDarkModePreference() {
            const darkMode = localStorage.getItem('darkMode');
            const icon = document.querySelector('#themeBtn i');

            if (darkMode === 'enabled') {
                document.body.classList.add('dark-theme');
                icon.classList.remove('fa-moon');
                icon.classList.add('fa-sun');
            } else {
                document.body.classList.remove('dark-theme');
                icon.classList.remove('fa-sun');
                icon.classList.add('fa-moon');
            }
        }

        // تبديل الوضع الليلي
        document.getElementById('themeBtn').addEventListener('click', function() {
            document.body.classList.toggle('dark-theme');
            const icon = this.querySelector('i');
            if (document.body.classList.contains('dark-theme')) {
                icon.classList.remove('fa-moon');
                icon.classList.add('fa-sun');
                localStorage.setItem('darkMode', 'enabled');
            } else {
                icon.classList.remove('fa-sun');
                icon.classList.add('fa-moon');
                localStorage.setItem('darkMode', 'disabled');
            }
        });

        // التعامل مع رفع ملف PDF
        async function handlePDFUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            if (file.type !== 'application/pdf') {
                showError('الرجاء رفع ملف PDF فقط');
                return;
            }

            if (file.size > 10 * 1024 * 1024) {
                showError('حجم الملف كبير جداً. الحد الأقصى 10MB');
                return;
            }

            pdfFile = file;

            // عرض معلومات الملف
            document.getElementById('pdf-filename').textContent = file.name;
            document.getElementById('pdf-filesize').textContent = `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            document.getElementById('pdf-preview').classList.add('active');

            // إظهار مؤشر التحميل
            document.getElementById('loading').style.display = 'block';
            document.getElementById('loading-details').textContent = 'جارٍ تحليل ملف PDF...';

            try {
                const arrayBuffer = await file.arrayBuffer();
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                
                document.getElementById('pdf-pages').textContent = `عدد الصفحات: ${pdf.numPages}`;
                
                // استخراج النص من أول 10 صفحات لتسريع العملية
                let fullText = '';
                let totalPages = Math.min(pdf.numPages, 10);
                
                for (let i = 1; i <= totalPages; i++) {
                    try {
                        const page = await pdf.getPage(i);
                        const textContent = await page.getTextContent();
                        const pageText = textContent.items.map(item => item.str).join(' ');
                        fullText += `\n--- الصفحة ${i} ---\n${pageText}\n`;
                        
                        // تحديث حالة التحميل
                        document.getElementById('loading-details').textContent = 
                            `جارٍ تحليل الصفحة ${i} من ${totalPages}...`;
                    } catch (pageError) {
                        console.warn(`خطأ في تحليل الصفحة ${i}:`, pageError);
                    }
                }
                
                pdfText = fullText.substring(0, 5000);
                pdfContext = fullText;
                
                // عرض عينة من النص
                const sampleText = fullText.substring(0, 500) + '...';
                document.getElementById('pdf-sample-text').textContent = sampleText;
                
                // إعادة تعيين المتغيرات
                existingQuestions = [];
                currentBatch = 1;
                totalQuestionsGenerated = 0;
                allQuestionsHistory = [];
                
                showSuccessMessage('تم تحليل ملف PDF بنجاح! يمكنك الآن توليد الأسئلة.');
                
            } catch (error) {
                console.error('Error reading PDF:', error);
                showError('حدث خطأ في قراءة ملف PDF: ' + error.message);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        // إزالة ملف PDF
        function removePDF() {
            pdfFile = null;
            pdfText = "";
            pdfContext = "";
            document.getElementById('pdf-file').value = "";
            document.getElementById('pdf-preview').classList.remove('active');
            existingQuestions = [];
            currentBatch = 1;
            totalQuestionsGenerated = 0;
            allQuestionsHistory = [];
        }

        // توليد الاختبار باستخدام الذكاء الاصطناعي
        async function generateQuiz() {
            const apiKeyInput = document.getElementById('api-key').value.trim();
            
            if (!apiKeyInput) {
                showError('الرجاء إدخال مفتاح Google Gemini API');
                return;
            }

            apiKey = apiKeyInput;

            let prompt = '';
            let title = '';

            if (currentMethod === 'manual') {
                const quizTitleInput = document.getElementById('quiz-title').value.trim();
                const quizTopicInput = document.getElementById('quiz-topic').value.trim();

                if (!quizTitleInput) {
                    showError('الرجاء إدخال عنوان للاختبار');
                    return;
                }

                title = quizTitleInput;
                prompt = `أنشئ اختباراً تعليمياً حول الموضوع التالي:
العنوان: ${quizTitleInput}
${quizTopicInput ? `التفاصيل: ${quizTopicInput}` : ''}

أرغب في اختبار مكون من 10 أسئلة مع 4 خيارات لكل سؤال.
الرجاء الالتزام بالتنسيق التالي:

{
  "questions": [
    {
      "id": 1,
      "q": "نص السؤال هنا",
      "options": ["الخيار الأول", "الخيار الثاني", "الخيار الثالث", "الخيار الرابع"],
      "answer": 0,
      "explanations": {
        "correct": "شرح الإجابة الصحيحة",
        "wrong1": "شرح الخطأ الأول",
        "wrong2": "شرح الخطأ الثاني",
        "wrong3": "شرح الخطأ الثالث"
      }
    }
  ]
}`;
            } else if (currentMethod === 'pdf') {
                if (!pdfFile) {
                    showError('الرجاء رفع ملف PDF أولاً');
                    return;
                }

                if (!pdfContext) {
                    showError('الرجاء الانتظار حتى يكتمل تحليل ملف PDF');
                    return;
                }

                const numQuestions = document.getElementById('num-questions').value;
                const questionType = document.getElementById('question-type').value;
                
                title = `${pdfFile.name.replace('.pdf', '')} - اختبار - الدفعة ${currentBatch}`;
                
                let typeDescription = '';
                switch(questionType) {
                    case 'concepts':
                        typeDescription = 'أسئلة تركز على المفاهيم الأساسية';
                        break;
                    case 'applications':
                        typeDescription = 'أسئلة تطبيقية';
                        break;
                    case 'analysis':
                        typeDescription = 'أسئلة تحليلية';
                        break;
                    default:
                        typeDescription = 'مزيج من أنواع الأسئلة';
                }

                // بناء على الدفعة، إنشاء محتوى مختلف
                const contextPart = existingQuestions.length > 0 ? 
                    `لدي بالفعل ${existingQuestions.length} سؤالاً. الرجاء إنشاء أسئلة جديدة مختلفة عن السابقة.` : 
                    `الرجاء إنشاء أول دفعة من الأسئلة بناءً على المحتوى.`;

                prompt = `${contextPart}

المحتوى من ملف PDF:
${pdfContext.substring(0, 7000)}

الرجاء إنشاء ${numQuestions} أسئلة من النوع: ${typeDescription}

متطلبات الأسئلة:
1. الاستناد إلى محتوى PDF
2. 4 خيارات لكل سؤال
3. تحديد الإجابة الصحيحة بوضوح
4. كتابة شرح لكل إجابة
5. الإشارة إلى المصدر في النص
6. تجنب تكرار الأسئلة السابقة

التنسيق المطلوب:
{
  "questions": [
    {
      "id": ${totalQuestionsGenerated + 1},
      "q": "نص السؤال هنا",
      "options": ["خيار 1", "خيار 2", "خيار 3", "خيار 4"],
      "answer": 0,
      "explanations": {
        "correct": "شرح الإجابة الصحيحة",
        "wrong1": "شرح الخطأ الأول",
        "wrong2": "شرح الخطأ الثاني",
        "wrong3": "شرح الخطأ الثالث"
      },
      "source": "المصدر في النص",
      "batch": ${currentBatch},
      "questionType": "${questionType}",
      "category": "تصنيف السؤال"
    }
  ]
}`;
            }

            currentQuizTitle = title;
            document.getElementById('main-title').textContent = currentQuizTitle;
            document.getElementById('current-quiz-title').textContent = currentQuizTitle;

            document.getElementById('loading').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
            
            const numQuestions = document.getElementById('num-questions').value;
            document.getElementById('loading-details').textContent = 
                `جارٍ توليد الدفعة ${currentBatch} (${numQuestions} أسئلة)...`;

            try {
                const response = await fetch(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{
                                text: prompt
                            }]
                        }],
                        generationConfig: {
                            temperature: 0.7,
                            topK: 40,
                            topP: 0.95,
                            maxOutputTokens: 4096,
                        }
                    })
                });

                if (!response.ok) {
                    const errorText = await response.text();
                    throw new Error(`خطأ: ${response.status} - ${errorText}`);
                }

                const data = await response.json();
                
                if (!data.candidates || !data.candidates[0] || !data.candidates[0].content || !data.candidates[0].content.parts[0]) {
                    throw new Error('استجابة غير صالحة من API');
                }

                const responseText = data.candidates[0].content.parts[0].text;
                
                // استخراج JSON من الاستجابة
                const jsonMatch = responseText.match(/\{[\s\S]*\}/);
                if (!jsonMatch) {
                    console.error('استجابة API:', responseText.substring(0, 500));
                    throw new Error('تعذر استخراج البيانات');
                }

                const quizData = JSON.parse(jsonMatch[0]);
                
                if (!quizData.questions || !Array.isArray(quizData.questions)) {
                    throw new Error('لم يتم توليد الأسئلة بشكل صحيح');
                }

                // إضافة الأسئلة الجديدة إلى الأسئلة الحالية
                const newQuestions = quizData.questions;
                
                // التحقق من عدم تكرار الأسئلة
                const uniqueQuestions = newQuestions.filter(newQ => {
                    return !existingQuestions.some(existingQ => 
                        existingQ.q === newQ.q || 
                        existingQ.q.includes(newQ.q.substring(0, 50))
                    );
                });

                if (uniqueQuestions.length === 0) {
                    throw new Error('الأسئلة الجديدة مكررة');
                }

                if (existingQuestions.length > 0) {
                    questions = [...existingQuestions, ...uniqueQuestions];
                } else {
                    questions = uniqueQuestions;
                }
                
                existingQuestions = questions;
                allQuestionsHistory = [...allQuestionsHistory, ...uniqueQuestions];
                totalQuestionsGenerated += uniqueQuestions.length;
                
                // تهيئة المتغيرات
                userAnswers = Array(questions.length).fill(null);
                answerLocked = Array(questions.length).fill(false);
                shuffledQuestions = questions.map(q => shuffleOptions(q));
                timeLeft = questions.length * 60;
                currentQuestionIndex = 0;
                markedQuestions = [];

                document.getElementById('setup-section').style.display = 'none';
                document.getElementById('quiz-section').style.display = 'block';
                document.getElementById('add-more-section').style.display = 'block';

                clearInterval(timerInterval);
                startTimer();
                loadQuiz();

                showSuccessMessage(`تم توليد ${uniqueQuestions.length} سؤالاً في الدفعة ${currentBatch}!`);

            } catch (error) {
                showError(`حدث خطأ: ${error.message}`);
                console.error('Error:', error);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        // دالة لعرض الأخطاء
        function showError(message) {
            const errorDiv = document.getElementById('error-message');
            errorDiv.innerHTML = `<i class="fas fa-exclamation-triangle"></i> ${message}`;
            errorDiv.style.display = 'block';
            
            setTimeout(() => {
                errorDiv.style.display = 'none';
            }, 5000);
        }

        // دالة لعرض رسائل النجاح
        function showSuccessMessage(message) {
            const successDiv = document.createElement('div');
            successDiv.className = 'success-message';
            successDiv.innerHTML = `<i class="fas fa-check-circle"></i> ${message}`;
            
            document.body.appendChild(successDiv);
            
            setTimeout(() => {
                successDiv.style.animation = 'slideOutRight 0.5s ease';
                setTimeout(() => successDiv.remove(), 500);
            }, 3000);
        }

        // دالة لترتيب الخيارات بشكل عشوائي
        function shuffleOptions(question) {
            const options = [...question.options];
            const answer = question.answer;
            
            const shuffledIndices = [...Array(options.length).keys()];
            for (let i = shuffledIndices.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffledIndices[i], shuffledIndices[j]] = [shuffledIndices[j], shuffledIndices[i]];
            }
            
            const shuffledOptions = shuffledIndices.map(idx => options[idx]);
            const newAnswer = shuffledIndices.indexOf(answer);
            
            return {
                ...question,
                options: shuffledOptions,
                answer: newAnswer
            };
        }

        // بدء المؤقت
        function startTimer() {
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();

                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    finishQuiz();
                }
            }, 1000);
        }

        // تحديث عرض المؤقت
        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            const timeDisplay = document.getElementById('time-display');
            timeDisplay.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;

            if (timeLeft < 300) {
                timeDisplay.classList.add('timer-warning');
            } else {
                timeDisplay.classList.remove('timer-warning');
            }
        }

        // تحميل الاختبار
        function loadQuiz() {
            const quizDiv = document.getElementById("quiz");

            if (shuffledQuestions.length === 0) {
                shuffledQuestions = questions.map(q => shuffleOptions(q));
            }
            
            const question = shuffledQuestions[currentQuestionIndex];
            const isLocked = answerLocked[currentQuestionIndex];

            let html = `
            <div class="question-box fade-in">
                <div class="question-number">
                    <i class="fas fa-question-circle"></i>
                    السؤال ${currentQuestionIndex + 1} من ${questions.length}
                    ${question.batch ? `<span class="batch-indicator">دفعة ${question.batch}</span>` : ''}
                    ${question.category ? `<span class="category-badge">${question.category}</span>` : ''}
                    ${isLocked ? '<span style="color: var(--accent); margin-right: 10px;"><i class="fas fa-lock"></i> مقفل</span>' : ''}
                    ${markedQuestions.includes(currentQuestionIndex) ? '<span style="background: var(--tertiary-gradient); color: white; padding: 5px 10px; border-radius: 10px; font-size: 0.8rem; margin-right: 10px;"><i class="fas fa-flag"></i> معلمة</span>' : ''}
                </div>
                
                <div class="quiz-stats">
                    <span><i class="fas fa-layer-group"></i> إجمالي الأسئلة: ${questions.length}</span>
                    <span><i class="fas fa-history"></i> عدد الدفعات: ${currentBatch}</span>
                    <span><i class="fas fa-question"></i> تم الإجابة: ${userAnswers.filter(a => a !== null).length}</span>
                    <span><i class="fas fa-flag"></i> معلمة: ${markedQuestions.length}</span>
                </div>
                
                <div class="question-text">${question.q}</div>
                
                ${question.source ? `<div class="source-info"><i class="fas fa-map-marker-alt"></i> المصدر: ${question.source}</div>` : ''}
                
                <div class="options">
            `;

            question.options.forEach((opt, i) => {
                const isChecked = userAnswers[currentQuestionIndex] === i;
                const isDisabled = isLocked;
                let labelClass = '';

                if (isLocked) {
                    labelClass = 'locked';
                    if (isChecked) {
                        labelClass += userAnswers[currentQuestionIndex] === question.answer ? ' correct-answer' : ' wrong-answer';
                    } else if (i === question.answer) {
                        labelClass += ' correct-answer';
                    }
                } else if (isChecked) {
                    labelClass = 'selected';
                }

                html += `
                <label class="${labelClass}">
                    <input type="radio" name="q${currentQuestionIndex}" value="${i}" ${isChecked ? 'checked' : ''} ${isDisabled ? 'disabled' : ''} onchange="selectAnswer(${i})">
                    ${opt}
                    ${isLocked && i === question.answer ? ' <i class="fas fa-check" style="color: var(--secondary);"></i>' : ''}
                </label>
                `;
            });

            html += `
                </div>
                <div id="explanation" class="explanation"></div>
            </div>
            <div class="navigation">
                <button class="btn btn-secondary" onclick="previousQuestion()" ${currentQuestionIndex === 0 ? 'disabled' : ''}>
                    <i class="fas fa-arrow-right"></i> السابق
                </button>
                <button class="btn btn-primary" onclick="nextQuestion()" ${currentQuestionIndex === questions.length - 1 ? 'disabled' : ''}>
                    التالي <i class="fas fa-arrow-left"></i>
                </button>
            </div>
            `;

            quizDiv.innerHTML = html;

            // تحديث شريط التقدم
            const progress = document.getElementById('progress');
            progress.style.width = questions.length > 0 ? `${((currentQuestionIndex + 1) / questions.length) * 100}%` : '0%';

            // تحديث معلومات الاختبار
            document.getElementById('quiz-info').innerHTML = `
                السؤال ${currentQuestionIndex + 1} من ${questions.length} 
                | تم الإجابة: ${userAnswers.filter(a => a !== null).length}
                | معلمة: ${markedQuestions.length}
            `;

            // تحديث زر وضع العلامة
            const markBtn = document.getElementById('mark-review-btn');
            if (markedQuestions.includes(currentQuestionIndex)) {
                markBtn.innerHTML = '<i class="fas fa-flag"></i> إزالة العلامة';
                markBtn.style.background = 'var(--tertiary-gradient)';
            } else {
                markBtn.innerHTML = '<i class="fas fa-flag"></i> وضع علامة';
                markBtn.style.background = 'var(--secondary-gradient)';
            }

            // عرض الشرح إذا كان المستخدم قد أجاب على السؤال
            if (userAnswers[currentQuestionIndex] !== null) {
                showExplanation();
            }
        }

        // اختيار إجابة
        function selectAnswer(answerIndex) {
            if (answerLocked[currentQuestionIndex]) {
                return;
            }
            
            userAnswers[currentQuestionIndex] = answerIndex;
            answerLocked[currentQuestionIndex] = true;

            // تعطيل جميع خيارات الراديو في السؤال الحالي
            const radioInputs = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
            radioInputs.forEach(input => {
                input.disabled = true;
            });

            // إضافة فئة locked لجميع labels
            const labels = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
            labels.forEach(input => {
                input.closest('label').classList.add('locked');
            });

            // إظهار الشرح
            showExplanation();
        }

        // عرض الشرح
        function showExplanation() {
            const question = shuffledQuestions[currentQuestionIndex];
            const explanationDiv = document.getElementById("explanation");
            const userAnswer = userAnswers[currentQuestionIndex];

            if (userAnswer !== null) {
                explanationDiv.style.display = "block";

                let resultHTML = "";

                if (userAnswer === question.answer) {
                    resultHTML = `<p style="color: var(--secondary);"><i class="fas fa-check-circle"></i> إجابة صحيحة!</p>`;
                } else {
                    resultHTML = `
                    <p style="color: #dc2626;"><i class="fas fa-times-circle"></i> إجابة خاطئة</p>
                    <p style="color: var(--secondary);">الإجابة الصحيحة: ${question.options[question.answer]}</p>
                    `;
                }

                // إضافة الشروح
                if (questions[currentQuestionIndex]?.explanations?.correct) {
                    resultHTML += `
                    <div style="margin-top: 15px; padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px;">
                        <strong>📚 التفسير الصحيح:</strong><br>
                        ${questions[currentQuestionIndex].explanations.correct}
                    </div>
                    `;
                }

                explanationDiv.innerHTML = resultHTML;
            }
        }

        // الانتقال إلى السؤال التالي
        function nextQuestion() {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                loadQuiz();
            }
        }

        // الانتقال إلى السؤال السابق
        function previousQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                loadQuiz();
            }
        }

        // فتح نافذة قائمة الأسئلة
        function openQuestionsModal() {
            const grid = document.getElementById('questions-grid-modal');
            grid.innerHTML = '';

            questions.forEach((question, index) => {
                const btn = document.createElement('div');
                btn.className = `question-status-grid-modal ${index === currentQuestionIndex ? 'current' : ''} ${userAnswers[index] !== null ? 'answered' : ''} ${markedQuestions.includes(index) ? 'flagged' : ''}`;
                btn.innerHTML = `<span>${index + 1}</span>`;
                btn.onclick = () => {
                    currentQuestionIndex = index;
                    loadQuiz();
                    closeQuestionsModal();
                };
                grid.appendChild(btn);
            });

            document.getElementById('questionsModal').style.display = 'block';
        }

        function closeQuestionsModal() {
            document.getElementById('questionsModal').style.display = 'none';
        }

        // وضع علامة للمراجعة
        function toggleMarkForReview() {
            const index = markedQuestions.indexOf(currentQuestionIndex);
            const btn = document.getElementById('mark-review-btn');

            if (index === -1) {
                markedQuestions.push(currentQuestionIndex);
                btn.innerHTML = '<i class="fas fa-flag"></i> إزالة العلامة';
                btn.style.background = 'var(--tertiary-gradient)';
            } else {
                markedQuestions.splice(index, 1);
                btn.innerHTML = '<i class="fas fa-flag"></i> وضع علامة';
                btn.style.background = 'var(--secondary-gradient)';
            }
            
            loadQuiz();
        }

        // فتح نافذة الدرجات الحالية
        function openCurrentScoreModal() {
            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const totalQuestions = questions.length;
            const percentage = totalQuestions > 0 ? ((score.correct / totalQuestions) * 100).toFixed(2) : 0;
            
            const circle = document.getElementById('score-circle-fill');
            const text = document.getElementById('score-percentage');
            const circumference = 440;
            const offset = circumference - (percentage / 100) * circumference;
            
            circle.style.strokeDashoffset = offset;
            text.textContent = `${percentage}%`;
            
            document.getElementById('current-score-details').innerHTML = 
                `<strong>الدرجة:</strong> ${score.correct} من ${totalQuestions}`;
            document.getElementById('current-correct-details').innerHTML = 
                `<strong>الصحيحة:</strong> ${score.correct}`;
            document.getElementById('current-progress-details').innerHTML = 
                `<strong>التقدم:</strong> ${answeredCount} من ${totalQuestions}`;
            document.getElementById('current-batch-details').innerHTML = 
                `<strong>الدفعة:</strong> ${currentBatch} | <strong>الإجمالي:</strong> ${totalQuestionsGenerated}`;
            
            document.getElementById('currentScoreModal').style.display = 'block';
        }

        function closeCurrentScoreModal() {
            document.getElementById('currentScoreModal').style.display = 'none';
        }

        // حساب الدرجات
        function calculateScore() {
            let totalCorrect = 0;
            userAnswers.forEach((answer, index) => {
                if (answer === shuffledQuestions[index]?.answer) {
                    totalCorrect++;
                }
            });

            const total = questions.length;
            const percentage = total > 0 ? ((totalCorrect / total) * 100).toFixed(2) : 0;

            let evaluation = "";
            let evaluationIcon = "";
            if (percentage >= 90) {
                evaluation = "ممتاز";
                evaluationIcon = "🌟";
            } else if (percentage >= 80) {
                evaluation = "جيد جداً";
                evaluationIcon = "🔵";
            } else if (percentage >= 70) {
                evaluation = "جيد";
                evaluationIcon = "🟢";
            } else if (percentage >= 60) {
                evaluation = "مقبول";
                evaluationIcon = "🟡";
            } else {
                evaluation = "يحتاج تحسين";
                evaluationIcon = "⚠️";
            }

            return {
                correct: totalCorrect,
                total: total,
                percentage: parseFloat(percentage),
                evaluation: evaluation,
                evaluationIcon: evaluationIcon
            };
        }

        // إضافة المزيد من الأسئلة
        async function addMoreQuestions() {
            if (!pdfFile || !pdfContext) {
                showError('لم يتم تحميل ملف PDF');
                return;
            }

            if (!apiKey) {
                showError('الرجاء إدخال مفتاح API');
                return;
            }

            currentBatch++;
            const numQuestions = document.getElementById('num-questions').value;
            const questionType = document.getElementById('question-type').value;
            
            document.getElementById('loading').style.display = 'block';
            document.getElementById('loading-details').textContent = 
                `جارٍ توليد الدفعة ${currentBatch} (${numQuestions} أسئلة)...`;

            try {
                const prompt = `لدي بالفعل ${totalQuestionsGenerated} سؤالاً من هذا المحتوى.
الرجاء إنشاء ${numQuestions} أسئلة إضافية جديدة ومختلفة.

محتوى PDF:
${pdfContext.substring(0, 7000)}

أنواع الأسئلة المطلوبة: ${questionType}

التنسيق المطلوب:
{
  "questions": [
    {
      "id": ${totalQuestionsGenerated + 1},
      "q": "نص السؤال",
      "options": ["خيار 1", "خيار 2", "خيار 3", "خيار 4"],
      "answer": 0,
      "explanations": {
        "correct": "شرح",
        "wrong1": "شرح",
        "wrong2": "شرح",
        "wrong3": "شرح"
      },
      "source": "المصدر",
      "batch": ${currentBatch},
      "questionType": "${questionType}",
      "category": "التصنيف"
    }
  ]
}`;

                const response = await fetch(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{
                                text: prompt
                            }]
                        }],
                        generationConfig: {
                            temperature: 0.8,
                            topK: 40,
                            topP: 0.95,
                            maxOutputTokens: 4096,
                        }
                    })
                });

                if (!response.ok) {
                    throw new Error(`خطأ: ${response.status}`);
                }

                const data = await response.json();
                const responseText = data.candidates[0].content.parts[0].text;
                const jsonMatch = responseText.match(/\{[\s\S]*\}/);
                
                if (!jsonMatch) {
                    throw new Error('تعذر استخراج البيانات');
                }

                const newQuizData = JSON.parse(jsonMatch[0]);
                
                if (!newQuizData.questions || !Array.isArray(newQuizData.questions)) {
                    throw new Error('لم يتم توليد الأسئلة');
                }

                // التحقق من عدم التكرار
                const uniqueNewQuestions = newQuizData.questions.filter(newQ => {
                    return !existingQuestions.some(existingQ => 
                        existingQ.q === newQ.q
                    );
                });

                if (uniqueNewQuestions.length === 0) {
                    throw new Error('الأسئلة مكررة');
                }

                // إضافة الأسئلة الجديدة
                questions = [...questions, ...uniqueNewQuestions];
                existingQuestions = questions;
                allQuestionsHistory = [...allQuestionsHistory, ...uniqueNewQuestions];
                totalQuestionsGenerated += uniqueNewQuestions.length;

                // تحديث واجهة المستخدم
                const currentTitle = document.getElementById('current-quiz-title');
                currentTitle.textContent = `${pdfFile.name.replace('.pdf', '')} - ${totalQuestionsGenerated} سؤالاً`;

                // إعادة تهيئة متغيرات المستخدم للأسئلة الجديدة فقط
                userAnswers = [...userAnswers, ...Array(uniqueNewQuestions.length).fill(null)];
                answerLocked = [...answerLocked, ...Array(uniqueNewQuestions.length).fill(false)];
                
                // إعادة خلط جميع الأسئلة
                shuffledQuestions = questions.map(q => shuffleOptions(q));

                // إعادة تحميل الاختبار
                if (document.getElementById('quiz-section').style.display !== 'none') {
                    loadQuiz();
                }

                // تحديث وقت الاختبار
                timeLeft = questions.length * 60;
                updateTimerDisplay();

                showSuccessMessage(`تم إضافة ${uniqueNewQuestions.length} سؤالاً في الدفعة ${currentBatch}!`);

            } catch (error) {
                showError(`خطأ: ${error.message}`);
                console.error('Error:', error);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        // إضافة أسئلة بعد الانتهاء من الاختبار
        function addMoreQuestionsAfterTest() {
            document.getElementById('result-box').style.display = 'none';
            document.getElementById('quiz-section').style.display = 'block';
            document.getElementById('add-more-section').style.display = 'block';
            loadQuiz();
            showSuccessMessage('يمكنك إضافة المزيد من الأسئلة!');
        }

        // إنهاء الاختبار
        function finishQuiz() {
            clearInterval(timerInterval);

            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;

            // عرض النتائج
            document.getElementById("result-box").style.display = "block";
            document.getElementById("result").innerHTML = `${score.evaluationIcon} النتيجة: ${score.correct} من ${score.total}`;
            document.getElementById("percentage").innerHTML = `النسبة: ${score.percentage}%`;
            document.getElementById("evaluation").innerHTML = `التقييم: ${score.evaluation}`;

            // إخفاء الاختبار
            document.getElementById("quiz").style.display = "none";
            document.getElementById("quiz-section").style.display = "none";

            // عرض النتائج المتقدمة
            document.getElementById('advanced-results').style.display = 'block';
            
            // تحديث الإحصائيات
            updateAdvancedStats(score);
        }

        // تحديث الإحصائيات المتقدمة
        function updateAdvancedStats(score) {
            const statsContainer = document.getElementById('stats-overview');
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const unansweredCount = questions.length - answeredCount;
            const markedCount = markedQuestions.length;
            
            statsContainer.innerHTML = `
                <div class="stat-card">
                    <div class="stat-value">${score.correct}/${score.total}</div>
                    <div class="stat-label">الدرجة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${score.percentage}%</div>
                    <div class="stat-label">النسبة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${answeredCount}</div>
                    <div class="stat-label">تم الإجابة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${unansweredCount}</div>
                    <div class="stat-label">لم تتم الإجابة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${markedCount}</div>
                    <div class="stat-label">معلمة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${currentBatch}</div>
                    <div class="stat-label">الدفعات</div>
                </div>
            `;
        }

        // الرجوع إلى الإعدادات
        function backToSetup() {
            questions = [];
            userAnswers = [];
            answerLocked = [];
            shuffledQuestions = [];
            currentQuestionIndex = 0;
            markedQuestions = [];
            existingQuestions = [];
            currentBatch = 1;
            totalQuestionsGenerated = 0;
            allQuestionsHistory = [];
            pdfContext = "";
            
            removePDF();
            
            document.getElementById('result-box').style.display = 'none';
            document.getElementById('advanced-results').style.display = 'none';
            document.getElementById('setup-section').style.display = 'block';
            document.getElementById('quiz-section').style.display = 'none';
            document.getElementById('add-more-section').style.display = 'none';
            
            document.getElementById('quiz-title').value = '';
            document.getElementById('quiz-topic').value = '';
            document.getElementById('api-key').value = '';
        }

        // إعادة تشغيل الاختبار
        function restartQuiz() {
            userAnswers = Array(questions.length).fill(null);
            answerLocked = Array(questions.length).fill(false);
            shuffledQuestions = questions.map(q => shuffleOptions(q));
            timeLeft = questions.length * 60;
            currentQuestionIndex = 0;
            markedQuestions = [];

            document.getElementById("quiz").style.display = "block";
            document.getElementById("quiz-section").style.display = "block";
            document.getElementById("result-box").style.display = "none";
            document.getElementById('advanced-results').style.display = 'none';
            document.getElementById('add-more-section').style.display = 'block';

            clearInterval(timerInterval);
            startTimer();
            loadQuiz();
        }

        // إنشاء تقرير PDF
        function generatePDF() {
            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            doc.setR2L(true);
            
            doc.setFontSize(24);
            doc.setTextColor(26, 95, 122);
            doc.text(currentQuizTitle, 105, 20, null, null, 'center');
            
            doc.setFontSize(16);
            doc.setTextColor(21, 152, 149);
            doc.text('تقرير نتائج الاختبار', 105, 30, null, null, 'center');
            
            doc.setFontSize(12);
            doc.setTextColor(100, 100, 100);
            doc.text(`تاريخ: ${new Date().toLocaleDateString('ar-SA')}`, 105, 40, null, null, 'center');
            
            doc.setFontSize(18);
            doc.setTextColor(30, 30, 30);
            doc.text('النتائج', 20, 60);
            
            doc.setFontSize(14);
            doc.text(`الدرجة: ${score.correct} من ${score.total}`, 20, 75);
            doc.text(`النسبة: ${score.percentage}%`, 20, 85);
            doc.text(`التقييم: ${score.evaluation}`, 20, 95);
            doc.text(`المجاب: ${answeredCount} من ${questions.length}`, 20, 105);
            doc.text(`الدفعات: ${currentBatch}`, 20, 115);
            doc.text(`الإجمالي: ${totalQuestionsGenerated}`, 20, 125);
            
            doc.save(`نتيجة-${currentQuizTitle.replace(/\s+/g, '-')}.pdf`);
            
            showSuccessMessage('تم إنشاء تقرير PDF!');
        }

        // التهيئة الأولية
        window.onload = function() {
            checkDarkModePreference();
            
            const dropZone = document.querySelector('.file-upload-label');
            
            dropZone.addEventListener('dragover', (e) => {
                e.preventDefault();
                dropZone.style.background = 'rgba(21, 152, 149, 0.2)';
                dropZone.style.borderColor = 'var(--accent-glow)';
            });
            
            dropZone.addEventListener('dragleave', () => {
                dropZone.style.background = 'rgba(21, 152, 149, 0.05)';
                dropZone.style.borderColor = 'var(--accent)';
            });
            
            dropZone.addEventListener('drop', (e) => {
                e.preventDefault();
                dropZone.style.background = 'rgba(21, 152, 149, 0.05)';
                dropZone.style.borderColor = 'var(--accent)';
                
                const file = e.dataTransfer.files[0];
                if (file && file.type === 'application/pdf') {
                    const event = {
                        target: {
                            files: [file]
                        }
                    };
                    handlePDFUpload(event);
                } else {
                    showError('الرجاء رفع ملف PDF فقط');
                }
            });

            document.getElementById('api-key').addEventListener('input', function() {
                if (this.value.trim()) {
                    this.style.borderColor = 'var(--secondary)';
                }
            });
        }

        // إغلاق النوافذ المنبثقة
        window.onclick = function(event) {
            const currentScoreModal = document.getElementById('currentScoreModal');
            const questionsModal = document.getElementById('questionsModal');
            
            if (event.target === currentScoreModal) {
                closeCurrentScoreModal();
            }
            if (event.target === questionsModal) {
                closeQuestionsModal();
            }
        }
    </script>
</body>
</html>