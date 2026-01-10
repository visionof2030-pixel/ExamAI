<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام الاختبارات الذكي - AI Powered PDF/Image Reader</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
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

        body.english-mode {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            direction: ltr;
        }

        /* Header */
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

        .developer-credit {
            font-size: 0.8rem;
            color: var(--accent-light);
            text-align: center;
            margin-top: 5px;
            font-family: 'Arial', sans-serif;
            letter-spacing: 1px;
            opacity: 0.9;
            font-style: italic;
        }

        .header-actions {
            display: flex;
            gap: 10px;
        }

        .theme-btn, .lang-btn {
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

        .theme-btn:hover, .lang-btn:hover {
            background: rgba(26, 95, 122, 0.3);
            transform: translateY(-3px);
            box-shadow: 0 0 25px rgba(26, 95, 122, 0.5);
            border-color: rgba(255, 255, 255, 0.5);
        }

        .lang-btn.active {
            background: var(--accent-gradient);
            border-color: var(--accent);
        }

        .language-switcher {
            position: fixed;
            top: 90px;
            left: 20px;
            z-index: 1000;
            display: flex;
            gap: 10px;
        }

        .lang-btn {
            padding: 8px 15px;
            font-size: 0.9rem;
        }

        main {
            max-width: 1000px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* Hero Section */
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

        /* Cards */
        .card {
            background: var(--card-bg);
            backdrop-filter: blur(30px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
            transition: all 0.4s ease;
            border: 1px solid var(--border);
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

        /* Forms */
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

        .input-with-btn {
            display: flex;
            gap: 10px;
        }

        .input-with-btn .input-field {
            flex: 1;
        }

        /* API Key */
        .api-key-status {
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-top: 10px;
            display: none;
        }

        .api-key-status.valid {
            background: rgba(76, 175, 80, 0.1);
            color: #4CAF50;
            border: 1px solid #4CAF50;
        }

        .api-key-status.invalid {
            background: rgba(220, 38, 38, 0.1);
            color: #dc2626;
            border: 1px solid #dc2626;
        }

        .verify-btn {
            padding: 0 20px;
            white-space: nowrap;
        }

        /* File Upload */
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

        /* Image Preview */
        .image-preview-container {
            margin-top: 15px;
            text-align: center;
        }

        .image-preview {
            max-width: 100%;
            max-height: 300px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            margin-top: 10px;
        }

        /* Method Selector */
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

        /* Language Selector */
        .language-selector {
            display: flex;
            gap: 15px;
            margin: 15px 0;
            flex-wrap: wrap;
        }

        .language-option {
            flex: 1;
            min-width: 150px;
            padding: 15px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            border: 2px solid transparent;
        }

        .language-option:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-3px);
        }

        .language-option.active {
            background: rgba(26, 95, 122, 0.3);
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.3);
        }

        .language-flag {
            font-size: 1.5rem;
            margin-bottom: 8px;
        }

        .language-name {
            font-weight: 600;
            color: var(--text);
            font-size: 1rem;
        }

        .language-desc {
            color: var(--light-text);
            font-size: 0.8rem;
            margin-top: 5px;
        }

        /* Buttons */
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

        /* API Info */
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

        /* Loading */
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

        /* Error Message */
        .error-message {
            background: linear-gradient(135deg, rgba(220, 38, 38, 0.1), rgba(239, 68, 68, 0.1));
            border: 2px solid #ef4444;
            color: #dc2626;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            display: none;
        }

        /* Success Message */
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

        /* Quiz Section */
        #quiz-section {
            display: none;
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

        /* Progress Bar */
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

        /* Question Box */
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

        /* Options */
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
            background: linear-gradient(135deg, rgba(239, 68, 68, 0.1), rgba(220, 38, 38, 0.1));
            border: 2px solid #ef4444;
            box-shadow: 0 0 15px rgba(239, 68, 68, 0.3);
            animation: wrongShake 0.5s ease;
        }

        @keyframes wrongShake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .options label.wrong-answer::before {
            width: 6px;
            background: linear-gradient(135deg, #ef4444, #dc2626);
        }

        /* Explanation */
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

        /* Controls */
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

        /* Navigation */
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
            gap: 20px;
        }

        /* Results */
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

        /* Stats */
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

        .source-info {
            background: rgba(21, 152, 149, 0.1);
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 0.85rem;
            color: var(--light-text);
            margin-top: 10px;
            border-right: 3px solid var(--accent);
        }

        /* Modals */
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

        /* Add More Section */
        .add-more-section {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            background: rgba(255, 152, 0, 0.1);
            border-radius: 15px;
            border: 2px dashed var(--tertiary);
            display: none;
        }

        /* Stats Overview */
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

        /* Smart Suggestions */
        .smart-suggestions {
            background: rgba(76, 175, 80, 0.1);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            border-right: 4px solid var(--secondary);
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

        /* Questions Grid */
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

        /* English Mode Styles */
        body.english-mode .question-box,
        body.english-mode .card,
        body.english-mode .modal-content {
            text-align: left;
        }

        body.english-mode .question-number {
            justify-content: flex-start;
        }

        body.english-mode .options label {
            text-align: left;
        }

        body.english-mode .options input[type="radio"] {
            margin-right: 12px;
            margin-left: 0;
        }

        body.english-mode .navigation {
            flex-direction: row-reverse;
        }

        body.english-mode .close-modal {
            float: right;
        }

        body.english-mode .method-selector {
            flex-direction: row;
        }

        body.english-mode .method-tab {
            text-align: left;
        }

        body.english-mode .score-details {
            text-align: left;
        }

        body.english-mode .quiz-info {
            text-align: center;
        }

        body.english-mode .batch-indicator,
        body.english-mode .category-badge {
            margin-left: 10px;
            margin-right: 0;
        }

        body.english-mode .suggestions-list {
            padding-left: 20px;
            padding-right: 0;
        }

        body.english-mode .suggestions-list li:before {
            left: -20px;
            right: auto;
        }

        body.english-mode .question-status-grid-modal {
            text-align: center;
        }

        body.english-mode .source-info {
            border-left: 3px solid var(--accent);
            border-right: none;
        }

        /* PDF Analysis Status */
        .analysis-status {
            background: rgba(255, 193, 7, 0.1);
            border: 2px solid #ffc107;
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            text-align: center;
        }

        .analysis-status i {
            color: #ffc107;
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        /* Image Upload Section */
        .image-upload-section {
            margin: 20px 0;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            border: 2px dashed var(--border);
        }

        .image-upload-section h4 {
            color: var(--text);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* Question Type Selector */
        .question-type-selector {
            margin: 20px 0;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            border: 1px solid var(--border);
        }

        .question-type-options {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
        }

        .question-type-option {
            flex: 1;
            min-width: 150px;
            padding: 15px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            border: 2px solid transparent;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .question-type-option:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-3px);
        }

        .question-type-option.active {
            background: rgba(26, 95, 122, 0.3);
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.3);
        }

        .question-type-option input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .question-type-icon {
            font-size: 1.2rem;
            color: var(--accent);
        }

        .question-type-name {
            font-weight: 600;
            color: var(--text);
            font-size: 1rem;
        }

        /* Responsive */
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

            .developer-credit {
                font-size: 0.7rem;
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

            .language-switcher {
                position: static;
                justify-content: center;
                margin-bottom: 20px;
            }

            .input-with-btn {
                flex-direction: column;
            }

            .input-with-btn .btn {
                width: 100%;
            }

            .language-selector {
                flex-direction: column;
            }
            
            .language-option {
                min-width: 100%;
            }

            .question-type-options {
                flex-direction: column;
            }
            
            .question-type-option {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <!-- Language Switcher -->
    <div class="language-switcher">
        <button class="lang-btn active" onclick="switchLanguage('ar')">
            <i class="fas fa-language"></i> العربية
        </button>
        <button class="lang-btn" onclick="switchLanguage('en')">
            <i class="fas fa-language"></i> English
        </button>
    </div>

    <!-- Header -->
    <header>
        <div class="header-container">
            <div class="title-section">
                <h1 id="main-title">نظام الاختبارات الذكي</h1>
                <div class="developer-credit">تنفيذ المعلم فهد الخالدي</div>
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
                <h1 class="hero-title" id="hero-title">نظام الاختبارات الذكي التفاعلي</h1>
                <p class="hero-subtitle" id="hero-subtitle">أنشئ اختبارات مخصصة في أي مجال باستخدام الذكاء الاصطناعي</p>
                
                <!-- طريقة الاختيار -->
                <div class="method-selector">
                    <div class="method-tab active" onclick="selectMethod('manual')" id="manual-tab">
                        <div class="method-icon">
                            <i class="fas fa-keyboard"></i>
                        </div>
                        <div class="method-title" id="manual-title">إدخال يدوي</div>
                        <div class="method-desc" id="manual-desc">أدخل عنوان وموضوع الاختبار</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('image')" id="image-tab">
                        <div class="method-icon">
                            <i class="fas fa-image"></i>
                        </div>
                        <div class="method-title" id="image-title">رفع صورة</div>
                        <div class="method-desc" id="image-desc">تحميل صورة وتوليد أسئلة باستخدام الذكاء الاصطناعي</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('pdf')" id="pdf-tab">
                        <div class="method-icon">
                            <i class="fas fa-file-pdf"></i>
                        </div>
                        <div class="method-title" id="pdf-title">رفع ملف PDF</div>
                        <div class="method-desc" id="pdf-desc">تحميل ملف وتوليد أسئلة باستخدام الذكاء الاصطناعي</div>
                    </div>
                </div>

                <!-- اختيار لغة الاختبار -->
                <div id="quiz-language-section">
                    <div class="input-group">
                        <label><i class="fas fa-globe"></i> <span id="language-label">اختر لغة الاختبار</span></label>
                        <div class="language-selector">
                            <div class="language-option active" onclick="selectQuizLanguage('ar')" id="arabic-language">
                                <div class="language-flag">🇸🇦</div>
                                <div class="language-name" id="arabic-language-name">العربية</div>
                                <div class="language-desc" id="arabic-language-desc">أسئلة باللغة العربية</div>
                            </div>
                            <div class="language-option" onclick="selectQuizLanguage('en')" id="english-language">
                                <div class="language-flag">🇺🇸</div>
                                <div class="language-name" id="english-language-name">English</div>
                                <div class="language-desc" id="english-language-desc">Questions in English</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- قسم مفتاح API -->
                <div class="api-key-section">
                    <div class="input-group">
                        <label for="api-key"><i class="fas fa-key"></i> <span id="api-key-label">مفتاح Google Gemini API</span></label>
                        <div class="input-with-btn">
                            <input type="password" id="api-key" class="input-field" 
                                   placeholder="أدخل مفتاح API الخاص بك هنا">
                            <button class="btn btn-primary verify-btn" onclick="verifyAPIKey()" id="verify-btn">
                                <i class="fas fa-check"></i> <span id="verify-text">تحقق</span>
                            </button>
                        </div>
                        <div class="api-key-status" id="api-key-status"></div>
                        <div class="api-info">
                            <p><i class="fas fa-info-circle"></i> <span id="api-info-text">للحصول على مفتاح API:</span></p>
                            <ol id="api-steps" style="margin-right: 20px; margin-top: 10px;">
                                <li>اذهب إلى <a href="https://makersuite.google.com/app/apikey" target="_blank">Google AI Studio</a></li>
                                <li>سجل الدخول بحساب Google</li>
                                <li>أنشئ مفتاح API جديد</li>
                                <li>انسخ المفتاح وألصقه هنا</li>
                            </ol>
                            <p style="margin-top: 10px; color: var(--accent);">
                                <i class="fas fa-lightbulb"></i> <span id="api-model-text">يستخدم النظام نموذج:</span> <strong>Gemini 2.5 Flash Lite</strong>
                            </p>
                        </div>
                    </div>
                </div>

                <!-- قسم اختيار نوع الأسئلة -->
                <div class="question-type-selector">
                    <div class="input-group">
                        <label><i class="fas fa-list-check"></i> <span id="question-type-label-main">اختر نوع الأسئلة المطلوبة</span></label>
                        <div class="question-type-options">
                            <div class="question-type-option active" onclick="toggleQuestionType('multipleChoice')" id="multiple-choice-option">
                                <input type="checkbox" id="multipleChoiceCheckbox" checked>
                                <div class="question-type-icon">
                                    <i class="fas fa-check-circle"></i>
                                </div>
                                <div class="question-type-name" id="multiple-choice-text">أسئلة اختيار متعدد</div>
                            </div>
                            <div class="question-type-option active" onclick="toggleQuestionType('trueFalse')" id="true-false-option">
                                <input type="checkbox" id="trueFalseCheckbox" checked>
                                <div class="question-type-icon">
                                    <i class="fas fa-balance-scale"></i>
                                </div>
                                <div class="question-type-name" id="true-false-text">أسئلة (صح/ خطأ)</div>
                            </div>
                            <div class="question-type-option active" onclick="toggleQuestionType('fillBlank')" id="fill-blank-option">
                                <input type="checkbox" id="fillBlankCheckbox" checked>
                                <div class="question-type-icon">
                                    <i class="fas fa-pen-to-square"></i>
                                </div>
                                <div class="question-type-name" id="fill-blank-text">املأ الفراغ</div>
                            </div>
                        </div>
                        <p style="margin-top: 15px; color: var(--light-text); font-size: 0.9rem; text-align: center;" id="question-type-desc">
                            يمكنك اختيار جميع أنواع الأسئلة أو اختيار نوع واحد فقط
                        </p>
                    </div>
                </div>

                <!-- قسم الإدخال اليدوي -->
                <div id="manual-section">
                    <div class="input-group">
                        <label for="quiz-title"><i class="fas fa-heading"></i> <span id="quiz-title-label">عنوان الاختبار</span></label>
                        <input type="text" id="quiz-title" class="input-field" 
                               placeholder="مثال: الفقه الإسلامي - أحكام الصلاة">
                    </div>

                    <div class="input-group">
                        <label for="quiz-topic"><i class="fas fa-book"></i> <span id="quiz-topic-label">تفاصيل الموضوع</span></label>
                        <textarea id="quiz-topic" class="input-field" rows="3" 
                                  placeholder="اكتب تفاصيل الموضوع الذي تريد اختباره..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="num-questions-manual"><i class="fas fa-question-circle"></i> <span id="num-questions-label-manual">عدد الأسئلة المطلوبة</span></label>
                        <select id="num-questions-manual" class="input-field">
                            <option value="5">5 أسئلة</option>
                            <option value="10" selected>10 أسئلة</option>
                            <option value="15">15 أسئلة</option>
                            <option value="20">20 أسئلة</option>
                        </select>
                    </div>
                </div>

                <!-- قسم رفع صورة -->
                <div id="image-section" style="display: none;">
                    <div class="file-upload-container">
                        <label for="image-file" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <h4 id="image-upload-title">انقر لرفع صورة</h4>
                            <p id="image-upload-subtitle">أو اسحب وأفلت الصورة هنا</p>
                            <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;" id="image-upload-size">
                                الأنواع المسموحة: JPG, PNG, GIF, WEBP
                            </p>
                        </label>
                        <input type="file" id="image-file" class="file-input" accept=".jpg,.jpeg,.png,.gif,.webp" onchange="handleImageUpload(event)">
                        
                        <div class="file-preview" id="image-preview">
                            <div class="file-info">
                                <div class="file-icon">
                                    <i class="fas fa-image"></i>
                                </div>
                                <div class="file-details">
                                    <h5 id="image-filename"></h5>
                                    <p id="image-filesize"></p>
                                </div>
                            </div>
                            <div class="analysis-status" id="image-analysis-status">
                                <i class="fas fa-robot"></i>
                                <p id="image-analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الصورة وتوليد الأسئلة</p>
                            </div>
                            <div id="image-preview-container" class="image-preview-container">
                                <img id="preview-image" class="image-preview" alt="معاينة الصورة">
                            </div>
                            <button class="remove-file-btn" onclick="removeImage()" id="remove-image-btn">
                                <i class="fas fa-trash"></i> <span id="remove-image-text">إزالة الصورة</span>
                            </button>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="num-questions-image"><i class="fas fa-question-circle"></i> <span id="num-questions-label-image">عدد الأسئلة المطلوبة</span></label>
                        <select id="num-questions-image" class="input-field">
                            <option value="5">5 أسئلة</option>
                            <option value="10" selected>10 أسئلة</option>
                            <option value="15">15 أسئلة</option>
                            <option value="20">20 أسئلة</option>
                        </select>
                    </div>
                </div>

                <!-- قسم رفع ملف PDF -->
                <div id="pdf-section" style="display: none;">
                    <div class="file-upload-container">
                        <label for="pdf-file" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <h4 id="upload-title">انقر لرفع ملف PDF</h4>
                            <p id="upload-subtitle">أو اسحب وأفلت الملف هنا</p>
                            <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;" id="upload-size">
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
                                </div>
                            </div>
                            <div class="analysis-status" id="analysis-status">
                                <i class="fas fa-robot"></i>
                                <p id="analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الملف وتوليد الأسئلة</p>
                            </div>
                            <button class="remove-file-btn" onclick="removePDF()" id="remove-file-btn">
                                <i class="fas fa-trash"></i> <span id="remove-file-text">إزالة الملف</span>
                            </button>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="num-questions-pdf"><i class="fas fa-question-circle"></i> <span id="num-questions-label-pdf">عدد الأسئلة المطلوبة</span></label>
                        <select id="num-questions-pdf" class="input-field">
                            <option value="5">5 أسئلة</option>
                            <option value="10" selected>10 أسئلة</option>
                            <option value="15">15 أسئلة</option>
                            <option value="20">20 أسئلة</option>
                        </select>
                    </div>
                </div>

                <!-- زر التوليد -->
                <button class="btn btn-islamic" onclick="generateQuiz()" style="width: 100%; margin-top: 20px;" id="generate-btn">
                    <i class="fas fa-robot"></i> <span id="generate-text">توليد اختبار باستخدام الذكاء الاصطناعي</span>
                </button>

                <div class="loading" id="loading">
                    <div class="loader"></div>
                    <p id="loading-text">جارٍ توليد الأسئلة باستخدام الذكاء الاصطناعي...</p>
                    <p style="font-size: 0.9rem; opacity: 0.7;" id="loading-details"></p>
                </div>

                <div class="error-message" id="error-message"></div>
            </div>
        </section>

        <!-- Quiz Section (Hidden Initially) -->
        <section id="quiz-section" style="display: none;">
            <h2 class="current-quiz-title" id="current-quiz-title"></h2>
            
            <!-- Progress Bar -->
            <div class="progress-bar">
                <div class="progress" id="progress"></div>
            </div>

            <!-- Quiz Container -->
            <div id="quiz"></div>

            <!-- Controls -->
            <div class="controls">
                <div class="quiz-info" id="quiz-info"></div>
                <div id="timer">⏱️ <span id="time-display">10:00</span></div>
                <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                    <button class="btn btn-primary" onclick="openQuestionsModal()" id="questions-list-btn">
                        <i class="fas fa-list"></i>
                        <span id="questions-list-text">قائمة الأسئلة</span>
                    </button>
                    <button class="btn btn-warning" onclick="toggleMarkForReview()" id="mark-review-btn">
                        <i class="fas fa-flag"></i>
                        <span id="mark-review-text">وضع علامة للمراجعة</span>
                    </button>
                    <button class="btn btn-islamic" onclick="finishQuiz()" id="finish-quiz-btn">
                        <i class="fas fa-flag-checkered"></i>
                        <span id="finish-quiz-text">إنهاء الاختبار</span>
                    </button>
                    <button class="btn btn-secondary" onclick="openCurrentScoreModal()" id="current-score-btn">
                        <i class="fas fa-chart-bar"></i>
                        <span id="current-score-text">الدرجات الحالية</span>
                    </button>
                </div>
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

                <!-- قسم العودة للقائمة الرئيسية -->
                <div class="share-results" style="margin-top: 30px;">
                    <h4 style="color: var(--text); margin-bottom: 20px;">
                        <i class="fas fa-home"></i> <span id="return-title">العودة للقائمة الرئيسية</span>
                    </h4>
                    <div class="share-buttons" style="display: flex; gap: 15px; flex-wrap: wrap;">
                        <button class="btn btn-success" onclick="backToSetup()" id="return-main-btn">
                            <i class="fas fa-home"></i> <span id="return-main-text">العودة للقائمة الرئيسية</span>
                        </button>
                        <button class="btn btn-secondary" onclick="restartQuiz()" id="restart-quiz-btn">
                            <i class="fas fa-redo"></i> <span id="restart-quiz-text">إعادة الاختبار</span>
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
                <h3><i class="fas fa-chart-bar"></i> <span id="current-score-modal-title">الدرجات الحالية</span></h3>
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
                <h3><i class="fas fa-th-list"></i> <span id="questions-modal-title">قائمة الأسئلة</span></h3>
            </div>
            <div id="questions-grid-modal"></div>
            <button class="btn btn-primary" onclick="closeQuestionsModal()" style="margin-top:20px; width: 100%;" id="close-questions-btn">
                <i class="fas fa-times"></i>
                <span id="close-questions-text">إغلاق القائمة</span>
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
        let currentQuizTitle = "";
        let apiKey = "";
        let pdfFile = null;
        let imageFile = null;
        let currentMethod = "manual";
        let existingQuestions = [];
        let currentBatch = 1;
        let totalQuestionsGenerated = 0;
        let currentLanguage = "ar";
        let isAPIKeyValid = false;
        let quizLanguage = "ar";
        
        // أنواع الأسئلة المختارة
        let selectedQuestionTypes = {
            multipleChoice: true,
            trueFalse: true,
            fillBlank: true
        };

        // تحديد نموذج Gemini المستخدم
        const GEMINI_MODEL = "gemini-2.5-flash-lite";
        const GEMINI_API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-lite:generateContent";

        // نصوص اللغة العربية
        const arabicTexts = {
            "hero-title": "نظام الاختبارات الذكي التفاعلي",
            "hero-subtitle": "أنشئ اختبارات مخصصة في أي مجال باستخدام الذكاء الاصطناعي",
            "manual-title": "إدخال يدوي",
            "manual-desc": "أدخل عنوان وموضوع الاختبار",
            "image-title": "رفع صورة",
            "image-desc": "تحميل صورة وتوليد أسئلة باستخدام الذكاء الاصطناعي",
            "pdf-title": "رفع ملف PDF",
            "pdf-desc": "تحميل ملف وتوليد أسئلة باستخدام الذكاء الاصطناعي",
            "api-key-label": "مفتاح Google Gemini API",
            "verify-text": "تحقق",
            "api-info-text": "للحصول على مفتاح API:",
            "api-model-text": "يستخدم النظام نموذج:",
            "quiz-title-label": "عنوان الاختبار",
            "quiz-topic-label": "تفاصيل الموضوع",
            "image-upload-title": "انقر لرفع صورة",
            "image-upload-subtitle": "أو اسحب وأفلت الصورة هنا",
            "image-upload-size": "الأنواع المسموحة: JPG, PNG, GIF, WEBP",
            "remove-image-text": "إزالة الصورة",
            "upload-title": "انقر لرفع ملف PDF",
            "upload-subtitle": "أو اسحب وأفلت الملف هنا",
            "upload-size": "الحد الأقصى لحجم الملف: 10MB",
            "remove-file-text": "إزالة الملف",
            "num-questions-label-manual": "عدد الأسئلة المطلوبة",
            "num-questions-label-image": "عدد الأسئلة المطلوبة",
            "num-questions-label-pdf": "عدد الأسئلة المطلوبة",
            "question-type-label-main": "اختر نوع الأسئلة المطلوبة",
            "multiple-choice-text": "أسئلة اختيار متعدد",
            "true-false-text": "أسئلة (صح/ خطأ)",
            "fill-blank-text": "املأ الفراغ",
            "question-type-desc": "يمكنك اختيار جميع أنواع الأسئلة أو اختيار نوع واحد فقط",
            "generate-text": "توليد اختبار باستخدام الذكاء الاصطناعي",
            "loading-text": "جارٍ توليد الأسئلة باستخدام الذكاء الاصطناعي...",
            "questions-list-text": "قائمة الأسئلة",
            "mark-review-text": "وضع علامة للمراجعة",
            "finish-quiz-text": "إنهاء الاختبار",
            "current-score-text": "الدرجات الحالية",
            "report-title": "تقرير النتائج",
            "restart-quiz-text": "إعادة الاختبار",
            "return-title": "العودة للقائمة الرئيسية",
            "return-main-text": "العودة للقائمة الرئيسية",
            "current-score-modal-title": "الدرجات الحالية",
            "questions-modal-title": "قائمة الأسئلة",
            "close-questions-text": "إغلاق القائمة",
            "analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الملف وتوليد الأسئلة",
            "image-analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الصورة وتوليد الأسئلة",
            "language-label": "اختر لغة الاختبار",
            "arabic-language-name": "العربية",
            "arabic-language-desc": "أسئلة باللغة العربية",
            "english-language-name": "English",
            "english-language-desc": "Questions in English"
        };

        // نصوص اللغة الإنجليزية
        const englishTexts = {
            "hero-title": "Smart Interactive Quiz System",
            "hero-subtitle": "Create customized quizzes in any field using AI",
            "manual-title": "Manual Input",
            "manual-desc": "Enter quiz title and topic",
            "image-title": "Upload Image",
            "image-desc": "Upload image and generate questions using AI",
            "pdf-title": "Upload PDF File",
            "pdf-desc": "Upload file and generate questions using AI",
            "api-key-label": "Google Gemini API Key",
            "verify-text": "Verify",
            "api-info-text": "To get API key:",
            "api-model-text": "System uses model:",
            "quiz-title-label": "Quiz Title",
            "quiz-topic-label": "Topic Details",
            "image-upload-title": "Click to Upload Image",
            "image-upload-subtitle": "or drag and drop image here",
            "image-upload-size": "Allowed types: JPG, PNG, GIF, WEBP",
            "remove-image-text": "Remove Image",
            "upload-title": "Click to Upload PDF",
            "upload-subtitle": "or drag and drop file here",
            "upload-size": "Max file size: 10MB",
            "remove-file-text": "Remove File",
            "num-questions-label-manual": "Number of Questions",
            "num-questions-label-image": "Number of Questions",
            "num-questions-label-pdf": "Number of Questions",
            "question-type-label-main": "Select Question Types",
            "multiple-choice-text": "Multiple Choice Questions",
            "true-false-text": "True/False Questions",
            "fill-blank-text": "Fill in the Blank",
            "question-type-desc": "You can select all question types or only one type",
            "generate-text": "Generate Quiz with AI",
            "loading-text": "Generating questions using AI...",
            "questions-list-text": "Questions List",
            "mark-review-text": "Mark for Review",
            "finish-quiz-text": "Finish Quiz",
            "current-score-text": "Current Score",
            "report-title": "Results Report",
            "restart-quiz-text": "Restart Quiz",
            "return-title": "Return to Main Menu",
            "return-main-text": "Return to Main Menu",
            "current-score-modal-title": "Current Score",
            "questions-modal-title": "Questions List",
            "close-questions-text": "Close List",
            "analysis-status-text": "AI will analyze the file and generate questions",
            "image-analysis-status-text": "AI will analyze the image and generate questions",
            "language-label": "Choose Quiz Language",
            "arabic-language-name": "Arabic",
            "arabic-language-desc": "Questions in Arabic",
            "english-language-name": "English",
            "english-language-desc": "Questions in English"
        };

        // تحويل اللغة
        function switchLanguage(lang) {
            currentLanguage = lang;
            
            // تحديث أزرار اللغة
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelector(`.lang-btn[onclick="switchLanguage('${lang}')"]`).classList.add('active');
            
            // تغيير اتجاه الصفحة
            if (lang === 'en') {
                document.body.classList.add('english-mode');
                document.documentElement.setAttribute('dir', 'ltr');
                document.documentElement.setAttribute('lang', 'en');
            } else {
                document.body.classList.remove('english-mode');
                document.documentElement.setAttribute('dir', 'rtl');
                document.documentElement.setAttribute('lang', 'ar');
            }
            
            // تحديث النصوص
            updateTexts(lang);
            
            // تحديث نصوص الحقول النصية
            updatePlaceholders(lang);
            
            // إذا كان هناك اختبار معروض، إعادة تحميله
            if (document.getElementById('quiz-section').style.display !== 'none') {
                loadQuiz();
            }
        }

        // تحديث النصوص
        function updateTexts(lang) {
            const texts = lang === 'ar' ? arabicTexts : englishTexts;
            
            for (const [key, value] of Object.entries(texts)) {
                const element = document.getElementById(key);
                if (element) {
                    element.textContent = value;
                }
            }
            
            // تحديث خيارات القائمة المنسدلة
            updateDropdownOptions(lang);
        }

        // تحديث النصوص التوضيحية
        function updatePlaceholders(lang) {
            const apiSteps = document.getElementById('api-steps');
            if (lang === 'en') {
                apiSteps.innerHTML = `
                    <li>Go to <a href="https://makersuite.google.com/app/apikey" target="_blank">Google AI Studio</a></li>
                    <li>Sign in with Google account</li>
                    <li>Create a new API key</li>
                    <li>Copy and paste the key here</li>
                `;
                
                document.getElementById('quiz-title').placeholder = "Example: Islamic Jurisprudence - Prayer Rules";
                document.getElementById('quiz-topic').placeholder = "Write details about the topic you want to test...";
                document.getElementById('api-key').placeholder = "Enter your API key here";
            } else {
                apiSteps.innerHTML = `
                    <li>اذهب إلى <a href="https://makersuite.google.com/app/apikey" target="_blank">Google AI Studio</a></li>
                    <li>سجل الدخول بحساب Google</li>
                    <li>أنشئ مفتاح API جديد</li>
                    <li>انسخ المفتاح وألصقه هنا</li>
                `;
                
                document.getElementById('quiz-title').placeholder = "مثال: الفقه الإسلامي - أحكام الصلاة";
                document.getElementById('quiz-topic').placeholder = "اكتب تفاصيل الموضوع الذي تريد اختباره...";
                document.getElementById('api-key').placeholder = "أدخل مفتاح API الخاص بك هنا";
            }
        }

        // تحديث خيارات القوائم المنسدلة
        function updateDropdownOptions(lang) {
            if (lang === 'en') {
                document.getElementById('num-questions-manual').innerHTML = `
                    <option value="5">5 questions</option>
                    <option value="10" selected>10 questions</option>
                    <option value="15">15 questions</option>
                    <option value="20">20 questions</option>
                `;
                
                document.getElementById('num-questions-image').innerHTML = `
                    <option value="5">5 questions</option>
                    <option value="10" selected>10 questions</option>
                    <option value="15">15 questions</option>
                    <option value="20">20 questions</option>
                `;
                
                document.getElementById('num-questions-pdf').innerHTML = `
                    <option value="5">5 questions</option>
                    <option value="10" selected>10 questions</option>
                    <option value="15">15 questions</option>
                    <option value="20">20 questions</option>
                `;
            } else {
                document.getElementById('num-questions-manual').innerHTML = `
                    <option value="5">5 أسئلة</option>
                    <option value="10" selected>10 أسئلة</option>
                    <option value="15">15 أسئلة</option>
                    <option value="20">20 أسئلة</option>
                `;
                
                document.getElementById('num-questions-image').innerHTML = `
                    <option value="5">5 أسئلة</option>
                    <option value="10" selected>10 أسئلة</option>
                    <option value="15">15 أسئلة</option>
                    <option value="20">20 أسئلة</option>
                `;
                
                document.getElementById('num-questions-pdf').innerHTML = `
                    <option value="5">5 أسئلة</option>
                    <option value="10" selected>10 أسئلة</option>
                    <option value="15">15 أسئلة</option>
                    <option value="20">20 أسئلة</option>
                `;
            }
        }

        // اختيار طريقة الاختبار
        function selectMethod(method) {
            currentMethod = method;
            
            document.getElementById('manual-tab').classList.remove('active');
            document.getElementById('image-tab').classList.remove('active');
            document.getElementById('pdf-tab').classList.remove('active');
            document.getElementById(`${method}-tab`).classList.add('active');
            
            document.getElementById('manual-section').style.display = method === 'manual' ? 'block' : 'none';
            document.getElementById('image-section').style.display = method === 'image' ? 'block' : 'none';
            document.getElementById('pdf-section').style.display = method === 'pdf' ? 'block' : 'none';
        }

        // اختيار لغة الاختبار
        function selectQuizLanguage(lang) {
            quizLanguage = lang;
            
            document.getElementById('arabic-language').classList.remove('active');
            document.getElementById('english-language').classList.remove('active');
            
            document.getElementById(`${lang}-language`).classList.add('active');
        }

        // تبديل نوع السؤال
        function toggleQuestionType(type) {
            selectedQuestionTypes[type] = !selectedQuestionTypes[type];
            const checkbox = document.getElementById(`${type}Checkbox`);
            const option = document.getElementById(`${type.replace(/([A-Z])/g, '-$1').toLowerCase()}-option`);
            
            checkbox.checked = selectedQuestionTypes[type];
            
            if (selectedQuestionTypes[type]) {
                option.classList.add('active');
            } else {
                option.classList.remove('active');
            }
            
            // التأكد من اختيار نوع واحد على الأقل
            const hasSelectedType = Object.values(selectedQuestionTypes).some(value => value);
            if (!hasSelectedType) {
                selectedQuestionTypes[type] = true;
                checkbox.checked = true;
                option.classList.add('active');
                
                showError(currentLanguage === 'ar' ? 
                    'يجب اختيار نوع واحد على الأقل من الأسئلة' : 
                    'You must select at least one question type');
            }
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

        // التحقق من مفتاح API
        async function verifyAPIKey() {
            const apiKeyInput = document.getElementById('api-key').value.trim();
            
            if (!apiKeyInput) {
                showError(currentLanguage === 'ar' ? 'الرجاء إدخال مفتاح API' : 'Please enter API key');
                return;
            }

            const statusDiv = document.getElementById('api-key-status');
            const verifyBtn = document.getElementById('verify-btn');
            
            statusDiv.className = 'api-key-status';
            statusDiv.style.display = 'flex';
            statusDiv.innerHTML = `<i class="fas fa-spinner fa-spin"></i> ${currentLanguage === 'ar' ? 'جارٍ التحقق...' : 'Verifying...'}`;
            
            verifyBtn.disabled = true;
            verifyBtn.innerHTML = `<i class="fas fa-spinner fa-spin"></i> ${currentLanguage === 'ar' ? 'جارٍ التحقق...' : 'Verifying...'}`;

            try {
                const response = await fetch(`${GEMINI_API_URL}?key=${apiKeyInput}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{
                                text: "Test API key"
                            }]
                        }],
                        generationConfig: {
                            maxOutputTokens: 10,
                        }
                    })
                });

                if (response.ok) {
                    isAPIKeyValid = true;
                    apiKey = apiKeyInput;
                    
                    statusDiv.className = 'api-key-status valid';
                    statusDiv.innerHTML = `<i class="fas fa-check-circle"></i> ${currentLanguage === 'ar' ? '✓ مفتاح API صالح' : '✓ API Key is valid'}`;
                    
                    showSuccessMessage(currentLanguage === 'ar' ? 'تم التحقق من المفتاح بنجاح!' : 'API key verified successfully!');
                } else {
                    throw new Error('Invalid API key');
                }
            } catch (error) {
                isAPIKeyValid = false;
                
                statusDiv.className = 'api-key-status invalid';
                statusDiv.innerHTML = `<i class="fas fa-times-circle"></i> ${currentLanguage === 'ar' ? '✗ مفتاح API غير صالح' : '✗ API Key is invalid'}`;
                
                showError(currentLanguage === 'ar' ? 'مفتاح API غير صالح' : 'Invalid API key');
            } finally {
                verifyBtn.disabled = false;
                verifyBtn.innerHTML = `<i class="fas fa-check"></i> ${currentLanguage === 'ar' ? 'تحقق' : 'Verify'}`;
            }
        }

        // التعامل مع رفع صورة
        async function handleImageUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const validTypes = ['image/jpeg', 'image/jpg', 'image/png', 'image/gif', 'image/webp'];
            if (!validTypes.includes(file.type)) {
                showError(currentLanguage === 'ar' ? 'الرجاء رفع صورة صالحة (JPG, PNG, GIF, WEBP)' : 'Please upload valid image (JPG, PNG, GIF, WEBP)');
                return;
            }

            if (file.size > 10 * 1024 * 1024) {
                showError(currentLanguage === 'ar' ? 'حجم الصورة كبير جداً. الحد الأقصى 10MB' : 'Image too large. Maximum size: 10MB');
                return;
            }

            imageFile = file;

            // عرض معلومات الصورة
            document.getElementById('image-filename').textContent = file.name;
            document.getElementById('image-filesize').textContent = currentLanguage === 'ar' ? 
                `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB` : 
                `Size: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            
            document.getElementById('image-preview').classList.add('active');
            
            // عرض معاينة الصورة
            const reader = new FileReader();
            reader.onload = function(e) {
                document.getElementById('preview-image').src = e.target.result;
                document.getElementById('image-preview-container').style.display = 'block';
            };
            reader.readAsDataURL(file);
            
            showSuccessMessage(currentLanguage === 'ar' ? 
                'تم رفع الصورة بنجاح! قم بتوليد الأسئلة الآن.' : 
                'Image uploaded successfully! Generate questions now.');
        }

        // إزالة الصورة
        function removeImage() {
            imageFile = null;
            document.getElementById('image-file').value = "";
            document.getElementById('image-preview').classList.remove('active');
            document.getElementById('image-preview-container').style.display = 'none';
        }

        // التعامل مع رفع ملف PDF
        async function handlePDFUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            if (file.type !== 'application/pdf') {
                showError(currentLanguage === 'ar' ? 'الرجاء رفع ملف PDF فقط' : 'Please upload PDF files only');
                return;
            }

            if (file.size > 10 * 1024 * 1024) {
                showError(currentLanguage === 'ar' ? 'حجم الملف كبير جداً. الحد الأقصى 10MB' : 'File too large. Maximum size: 10MB');
                return;
            }

            pdfFile = file;

            document.getElementById('pdf-filename').textContent = file.name;
            document.getElementById('pdf-filesize').textContent = currentLanguage === 'ar' ? 
                `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB` : 
                `Size: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            
            document.getElementById('pdf-preview').classList.add('active');
            
            showSuccessMessage(currentLanguage === 'ar' ? 
                'تم رفع الملف بنجاح! قم بتوليد الأسئلة الآن.' : 
                'File uploaded successfully! Generate questions now.');
        }

        // إزالة ملف PDF
        function removePDF() {
            pdfFile = null;
            document.getElementById('pdf-file').value = "";
            document.getElementById('pdf-preview').classList.remove('active');
            existingQuestions = [];
            currentBatch = 1;
            totalQuestionsGenerated = 0;
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

        // الحصول على التوجيهات بناءً على اللغة المختارة
        function getLanguageInstructions(targetLanguage) {
            if (targetLanguage === 'en') {
                return {
                    promptPrefix: "Please generate questions in English based on the provided content.",
                    formatInstructions: "All questions, options, and explanations must be in English.",
                    responseLanguage: "English",
                    languageCode: "en"
                };
            } else {
                return {
                    promptPrefix: "يرجى إنشاء أسئلة باللغة العربية بناءً على المحتوى المقدم.",
                    formatInstructions: "يجب أن تكون جميع الأسئلة والخيارات والشروح باللغة العربية.",
                    responseLanguage: "Arabic",
                    languageCode: "ar"
                };
            }
        }

        // تحويل الملفات إلى Base64
        async function convertFileToBase64(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result.split(',')[1]);
                reader.onerror = reject;
                reader.readAsDataURL(file);
            });
        }

        // الحصول على أنواع الأسئلة المختارة كنص
        function getSelectedQuestionTypesText(languageCode) {
            const selectedTypes = [];
            
            if (selectedQuestionTypes.multipleChoice) {
                selectedTypes.push(languageCode === 'en' ? 'multiple choice' : 'اختيار متعدد');
            }
            if (selectedQuestionTypes.trueFalse) {
                selectedTypes.push(languageCode === 'en' ? 'true/false' : 'صح/خطأ');
            }
            if (selectedQuestionTypes.fillBlank) {
                selectedTypes.push(languageCode === 'en' ? 'fill in the blank' : 'املأ الفراغ');
            }
            
            if (languageCode === 'en') {
                return selectedTypes.join(', ');
            } else {
                return selectedTypes.join('، ');
            }
        }

        // الحصول على نموذج JSON بناءً على أنواع الأسئلة المختارة - مُحدَّث لتشمل التغذية الراجعة لجميع الخيارات
        function getQuestionFormats(languageCode) {
            const formats = [];
            
            if (selectedQuestionTypes.multipleChoice) {
                if (languageCode === 'en') {
                    formats.push(`{
      "id": 1,
      "type": "multiple_choice",
      "q": "Question text here",
      "options": ["Option 1", "Option 2", "Option 3", "Option 4"],
      "answer": 0,
      "explanations": {
        "correct": "Explanation of why this option is correct",
        "option0": "Feedback for option 1",
        "option1": "Feedback for option 2", 
        "option2": "Feedback for option 3",
        "option3": "Feedback for option 4"
      }
    }`);
                } else {
                    formats.push(`{
      "id": 1,
      "type": "multiple_choice",
      "q": "نص السؤال هنا",
      "options": ["الخيار الأول", "الخيار الثاني", "الخيار الثالث", "الخيار الرابع"],
      "answer": 0,
      "explanations": {
        "correct": "شرح لماذا هذا الخيار صحيح",
        "option0": "تغذية راجعة للخيار الأول",
        "option1": "تغذية راجعة للخيار الثاني",
        "option2": "تغذية راجعة للخيار الثالث",
        "option3": "تغذية راجعة للخيار الرابع"
      }
    }`);
                }
            }
            
            if (selectedQuestionTypes.trueFalse) {
                if (languageCode === 'en') {
                    formats.push(`{
      "id": 2,
      "type": "true_false",
      "q": "Statement here",
      "options": ["True", "False"],
      "answer": 0,
      "explanations": {
        "correct": "Explanation why it's true/false",
        "option0": "Feedback for True option",
        "option1": "Feedback for False option"
      }
    }`);
                } else {
                    formats.push(`{
      "id": 2,
      "type": "true_false",
      "q": "الجملة هنا",
      "options": ["صح", "خطأ"],
      "answer": 0,
      "explanations": {
        "correct": "شرح لماذا هي صح/خطأ",
        "option0": "تغذية راجعة لخيار صح",
        "option1": "تغذية راجعة لخيار خطأ"
      }
    }`);
                }
            }
            
            if (selectedQuestionTypes.fillBlank) {
                if (languageCode === 'en') {
                    formats.push(`{
      "id": 3,
      "type": "fill_blank",
      "q": "Complete the sentence: The capital of France is _____",
      "answer": "Paris",
      "explanations": {
        "correct": "Paris is the capital of France. Other possible answers might include: 'Paris, France' or 'The capital is Paris'.",
        "common_mistakes": ["London", "Berlin", "Madrid"],
        "mistake_feedback": {
          "London": "London is the capital of the United Kingdom, not France",
          "Berlin": "Berlin is the capital of Germany",
          "Madrid": "Madrid is the capital of Spain"
        }
      }
    }`);
                } else {
                    formats.push(`{
      "id": 3,
      "type": "fill_blank",
      "q": "أكمل الجملة: عاصمة فرنسا هي _____",
      "answer": "باريس",
      "explanations": {
        "correct": "باريس هي عاصمة فرنسا. إجابات أخرى محتملة: 'باريس، فرنسا' أو 'العاصمة هي باريس'.",
        "common_mistakes": ["لندن", "برلين", "مدريد"],
        "mistake_feedback": {
          "لندن": "لندن هي عاصمة المملكة المتحدة، وليست فرنسا",
          "برلين": "برلين هي عاصمة ألمانيا",
          "مدريد": "مدريد هي عاصمة إسبانيا"
        }
      }
    }`);
                }
            }
            
            return formats;
        }

        // توليد الاختبار باستخدام الذكاء الاصطناعي - مع تحسين البرومبت ليشمل التغذية الراجعة لجميع الخيارات
        async function generateQuiz() {
            if (!isAPIKeyValid) {
                showError(currentLanguage === 'ar' ? 
                    'الرجاء التحقق من صحة مفتاح API أولاً' : 
                    'Please verify your API key first');
                return;
            }

            let prompt = '';
            let title = '';
            let requestBody = {};
            const languageInstructions = getLanguageInstructions(quizLanguage);
            const selectedTypesText = getSelectedQuestionTypesText(languageInstructions.languageCode);
            const questionFormats = getQuestionFormats(languageInstructions.languageCode);

            // برومبت محسّن مع تأكيد على التغذية الراجعة لجميع الخيارات
            const feedbackInstruction = languageInstructions.languageCode === 'en' 
                ? `CRITICAL REQUIREMENT: For each question, you MUST provide detailed feedback for EVERY option, not just the correct answer. For multiple choice questions, provide feedback for option0, option1, option2, option3. For true/false questions, provide feedback for both True and False options. For fill-in-the-blank questions, include common mistakes and feedback for each mistake. This is essential for the learning experience.`
                : `متطلب مهم جداً: لكل سؤال، يجب أن تقدم تغذية راجعة مفصلة لكل الخيارات، وليس فقط للإجابة الصحيحة. بالنسبة لأسئلة الاختيار المتعدد، قدم تغذية راجعة لـ option0, option1, option2, option3. بالنسبة لأسئلة صح/خطأ، قدم تغذية راجعة لكلا الخيارين. بالنسبة لأسئلة املأ الفراغ، أضف الأخطاء الشائعة وتغذية راجعة لكل خطأ. هذا ضروري لتجربة التعلم.`;

            if (currentMethod === 'manual') {
                const quizTitleInput = document.getElementById('quiz-title').value.trim();
                const quizTopicInput = document.getElementById('quiz-topic').value.trim();
                const numQuestions = document.getElementById('num-questions-manual').value;

                if (!quizTitleInput) {
                    showError(currentLanguage === 'ar' ? 'الرجاء إدخال عنوان للاختبار' : 'Please enter quiz title');
                    return;
                }

                if (!quizTopicInput) {
                    showError(currentLanguage === 'ar' ? 'الرجاء إدخال تفاصيل الموضوع' : 'Please enter topic details');
                    return;
                }

                title = quizTitleInput;
                
                if (languageInstructions.languageCode === 'en') {
                    prompt = `${languageInstructions.promptPrefix}

Topic: ${quizTitleInput}
Details: ${quizTopicInput}

I want a quiz with ${numQuestions} questions of the following types: ${selectedTypesText}.

${feedbackInstruction}

IMPORTANT: Generate a mix of the selected question types. For example, if multiple types are selected, include questions from each type.

${languageInstructions.formatInstructions}

Please follow this JSON format:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                } else {
                    prompt = `${languageInstructions.promptPrefix}

الموضوع: ${quizTitleInput}
التفاصيل: ${quizTopicInput}

أرغب في اختبار مكون من ${numQuestions} أسئلة من الأنواع التالية: ${selectedTypesText}.

${feedbackInstruction}

مهم: قم بإنشاء مزيج من أنواع الأسئلة المختارة. على سبيل المثال، إذا تم اختيار أنواع متعددة، قم بتضمين أسئلة من كل نوع.

${languageInstructions.formatInstructions}

الرجاء الالتزام بتنسيق JSON التالي:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                }

                requestBody = {
                    contents: [{
                        parts: [{ text: prompt }]
                    }],
                    generationConfig: {
                        temperature: 0.7,
                        topK: 40,
                        topP: 0.95,
                        maxOutputTokens: 4096,
                    }
                };

            } else if (currentMethod === 'image') {
                if (!imageFile) {
                    showError(currentLanguage === 'ar' ? 'الرجاء رفع صورة أولاً' : 'Please upload image first');
                    return;
                }

                const numQuestions = document.getElementById('num-questions-image').value;
                title = `${imageFile.name.replace(/\.[^/.]+$/, '')} - ${currentLanguage === 'ar' ? 'اختبار' : 'Quiz'}`;
                
                if (languageInstructions.languageCode === 'en') {
                    prompt = `${languageInstructions.promptPrefix}

I need ${numQuestions} questions based on the text in the provided image.

Question types to include: ${selectedTypesText}

${feedbackInstruction}

IMPORTANT: Analyze the text in the image and generate questions based on the content. Generate a mix of the selected question types.

${languageInstructions.formatInstructions}

Required JSON format:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                } else {
                    prompt = `${languageInstructions.promptPrefix}

أحتاج إلى ${numQuestions} أسئلة بناءً على النص في الصورة المرفوعة.

أنواع الأسئلة المطلوبة: ${selectedTypesText}

${feedbackInstruction}

مهم: قم بتحليل النص في الصورة وإنشاء أسئلة بناءً على المحتوى. قم بإنشاء مزيج من أنواع الأسئلة المختارة.

${languageInstructions.formatInstructions}

تنسيق JSON المطلوب:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                }

                // تحويل الصورة إلى Base64
                const imageBase64 = await convertFileToBase64(imageFile);

                requestBody = {
                    contents: [{
                        parts: [
                            { text: prompt },
                            {
                                inline_data: {
                                    mime_type: imageFile.type,
                                    data: imageBase64
                                }
                            }
                        ]
                    }],
                    generationConfig: {
                        temperature: 0.7,
                        topK: 40,
                        topP: 0.95,
                        maxOutputTokens: 4096,
                    }
                };

            } else if (currentMethod === 'pdf') {
                if (!pdfFile) {
                    showError(currentLanguage === 'ar' ? 'الرجاء رفع ملف PDF أولاً' : 'Please upload PDF file first');
                    return;
                }

                const numQuestions = document.getElementById('num-questions-pdf').value;
                title = `${pdfFile.name.replace('.pdf', '')} - ${currentLanguage === 'ar' ? 'اختبار' : 'Quiz'}`;
                
                if (languageInstructions.languageCode === 'en') {
                    prompt = `${languageInstructions.promptPrefix}

I need ${numQuestions} questions based on the content of the PDF file.

Question types to include: ${selectedTypesText}

${feedbackInstruction}

IMPORTANT: Analyze the PDF content and generate questions based on the text. Generate a mix of the selected question types.

${languageInstructions.formatInstructions}

Required JSON format:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                } else {
                    prompt = `${languageInstructions.promptPrefix}

أحتاج إلى ${numQuestions} أسئلة بناءً على محتوى ملف PDF.

أنواع الأسئلة المطلوبة: ${selectedTypesText}

${feedbackInstruction}

مهم: قم بتحليل محتوى PDF وإنشاء أسئلة بناءً على النص. قم بإنشاء مزيج من أنواع الأسئلة المختارة.

${languageInstructions.formatInstructions}

تنسيق JSON المطلوب:

{
  "questions": [
${questionFormats.join(',\n')}
  ]
}`;
                }

                // تحويل PDF إلى Base64
                const pdfBase64 = await convertFileToBase64(pdfFile);

                requestBody = {
                    contents: [{
                        parts: [
                            { text: prompt },
                            {
                                inline_data: {
                                    mime_type: "application/pdf",
                                    data: pdfBase64
                                }
                            }
                        ]
                    }],
                    generationConfig: {
                        temperature: 0.7,
                        topK: 40,
                        topP: 0.95,
                        maxOutputTokens: 4096,
                    }
                };
            }

            currentQuizTitle = title;
            document.getElementById('main-title').textContent = currentQuizTitle;
            document.getElementById('current-quiz-title').textContent = currentQuizTitle;

            document.getElementById('loading').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
            
            const numQuestions = currentMethod === 'manual' 
                ? document.getElementById('num-questions-manual').value 
                : currentMethod === 'image'
                ? document.getElementById('num-questions-image').value
                : document.getElementById('num-questions-pdf').value;
            
            document.getElementById('loading-details').textContent = currentLanguage === 'ar' ?
                `جارٍ توليد ${numQuestions} سؤالاً باستخدام الذكاء الاصطناعي...` :
                `Generating ${numQuestions} questions using AI...`;

            try {
                const response = await fetch(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(requestBody)
                });

                if (!response.ok) {
                    const errorText = await response.text();
                    throw new Error(`API Error: ${response.status} - ${errorText}`);
                }

                const data = await response.json();
                
                if (!data.candidates || !data.candidates[0] || !data.candidates[0].content || !data.candidates[0].content.parts[0]) {
                    throw new Error('Invalid API response');
                }

                const responseText = data.candidates[0].content.parts[0].text;
                console.log('API Response:', responseText.substring(0, 500));
                
                // استخراج JSON من الاستجابة
                const jsonMatch = responseText.match(/\{[\s\S]*\}/);
                if (!jsonMatch) {
                    throw new Error(currentLanguage === 'ar' ? 
                        'تعذر استخراج البيانات من استجابة الذكاء الاصطناعي' : 
                        'Could not extract data from AI response');
                }

                let quizData;
                try {
                    quizData = JSON.parse(jsonMatch[0]);
                } catch (parseError) {
                    console.error('JSON Parse Error:', parseError);
                    throw new Error(currentLanguage === 'ar' ? 
                        'خطأ في تحليل استجابة الذكاء الاصطناعي' : 
                        'Error parsing AI response');
                }
                
                if (!quizData.questions || !Array.isArray(quizData.questions)) {
                    throw new Error(currentLanguage === 'ar' ? 
                        'لم يتم العثور على أسئلة في الاستجابة' : 
                        'No questions found in response');
                }

                questions = quizData.questions;
                existingQuestions = questions;
                totalQuestionsGenerated = questions.length;
                
                userAnswers = Array(questions.length).fill(null);
                answerLocked = Array(questions.length).fill(false);
                shuffledQuestions = questions.map(q => shuffleOptions(q));
                timeLeft = questions.length * 60;
                currentQuestionIndex = 0;
                markedQuestions = [];

                document.getElementById('setup-section').style.display = 'none';
                document.getElementById('quiz-section').style.display = 'block';

                clearInterval(timerInterval);
                startTimer();
                loadQuiz();

                showSuccessMessage(currentLanguage === 'ar' ?
                    `تم توليد ${questions.length} سؤالاً بنجاح!` :
                    `Successfully generated ${questions.length} questions!`);

            } catch (error) {
                showError(currentLanguage === 'ar' ? 
                    `حدث خطأ: ${error.message}` : 
                    `Error: ${error.message}`);
                console.error('Error:', error);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        // دالة لترتيب الخيارات بشكل عشوائي
        function shuffleOptions(question) {
            if (question.type === 'fill_blank') {
                return question; // لا تحتاج أسئلة املأ الفراغ إلى خلط
            }
            
            const options = [...question.options];
            const answer = question.answer;
            
            const shuffledIndices = [...Array(options.length).keys()];
            for (let i = shuffledIndices.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffledIndices[i], shuffledIndices[j]] = [shuffledIndices[j], shuffledIndices[i]];
            }
            
            const shuffledOptions = shuffledIndices.map(idx => options[idx]);
            const newAnswer = shuffledIndices.indexOf(answer);
            
            // إعادة ترتيب الشروح وفقاً للترتيب الجديد
            const shuffledExplanations = { ...question.explanations };
            if (shuffledExplanations.option0 || shuffledExplanations.option1 || 
                shuffledExplanations.option2 || shuffledExplanations.option3) {
                for (let i = 0; i < shuffledIndices.length; i++) {
                    const originalIndex = shuffledIndices[i];
                    shuffledExplanations[`option${i}`] = question.explanations[`option${originalIndex}`] || '';
                }
            }
            
            return {
                ...question,
                options: shuffledOptions,
                answer: newAnswer,
                explanations: shuffledExplanations
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

            const questionLanguage = detectTextLanguage(question.q);
            
            let questionNumberText = questionLanguage === 'en' 
                ? `Question ${currentQuestionIndex + 1} of ${questions.length}`
                : `السؤال ${currentQuestionIndex + 1} من ${questions.length}`;
                
            let lockedText = questionLanguage === 'en' ? 'Locked' : 'مقفل';
            let markedText = questionLanguage === 'en' ? 'Flagged' : 'معلمة';
            
            let totalQuestionsText = questionLanguage === 'en' ? 'Total Questions' : 'إجمالي الأسئلة';
            let answeredText = questionLanguage === 'en' ? 'Answered' : 'تم الإجابة';
            let flaggedText = questionLanguage === 'en' ? 'Flagged' : 'معلمة';

            let html = `
            <div class="question-box">
                <div class="question-number">
                    <i class="fas fa-question-circle"></i>
                    ${questionNumberText}
                    ${question.type === 'multiple_choice' ? `<span class="category-badge">${questionLanguage === 'en' ? 'Multiple Choice' : 'اختيار متعدد'}</span>` : ''}
                    ${question.type === 'true_false' ? `<span class="category-badge">${questionLanguage === 'en' ? 'True/False' : 'صح/خطأ'}</span>` : ''}
                    ${question.type === 'fill_blank' ? `<span class="category-badge">${questionLanguage === 'en' ? 'Fill in Blank' : 'املأ الفراغ'}</span>` : ''}
                    ${isLocked ? `<span style="color: var(--accent); margin-right: 10px;"><i class="fas fa-lock"></i> ${lockedText}</span>` : ''}
                    ${markedQuestions.includes(currentQuestionIndex) ? `<span style="background: var(--tertiary-gradient); color: white; padding: 5px 10px; border-radius: 10px; font-size: 0.8rem; margin-right: 10px;"><i class="fas fa-flag"></i> ${markedText}</span>` : ''}
                </div>
                
                <div class="quiz-stats">
                    <span><i class="fas fa-layer-group"></i> ${totalQuestionsText}: ${questions.length}</span>
                    <span><i class="fas fa-question"></i> ${answeredText}: ${userAnswers.filter(a => a !== null).length}</span>
                    <span><i class="fas fa-flag"></i> ${flaggedText}: ${markedQuestions.length}</span>
                </div>
                
                <div class="question-text">${question.q}</div>
            `;

            if (question.type !== 'fill_blank') {
                html += `<div class="options">`;
                
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
                
                html += `</div>`;
            } else {
                // سؤال املأ الفراغ
                html += `
                <div class="options">
                    <label style="flex-direction: column; align-items: flex-start;">
                        <span style="margin-bottom: 10px; font-weight: bold;">${questionLanguage === 'en' ? 'Your Answer:' : 'إجابتك:'}</span>
                        <input type="text" id="fillBlankAnswer" class="input-field" style="width: 100%;" 
                               placeholder="${questionLanguage === 'en' ? 'Type your answer here...' : 'اكتب إجابتك هنا...'}" 
                               ${isLocked ? 'disabled' : ''}
                               value="${userAnswers[currentQuestionIndex] || ''}"
                               onchange="selectFillBlankAnswer(this.value)">
                    </label>
                </div>
                `;
            }

            let previousText, nextText, previousIcon, nextIcon;
            
            if (questionLanguage === 'en') {
                previousText = 'Previous';
                nextText = 'Next';
                previousIcon = 'fa-arrow-left';
                nextIcon = 'fa-arrow-right';
            } else {
                previousText = 'السابق';
                nextText = 'التالي';
                previousIcon = 'fa-arrow-right';
                nextIcon = 'fa-arrow-left';
            }

            html += `
                <div id="explanation" class="explanation"></div>
            </div>
            <div class="navigation">
                <button class="btn btn-secondary" onclick="previousQuestion()" ${currentQuestionIndex === 0 ? 'disabled' : ''}>
                    <i class="fas ${previousIcon}"></i> ${previousText}
                </button>
                <button class="btn btn-primary" onclick="nextQuestion()" ${currentQuestionIndex === questions.length - 1 ? 'disabled' : ''}>
                    ${nextText} <i class="fas ${nextIcon}"></i>
                </button>
            </div>
            `;

            quizDiv.innerHTML = html;

            // تحديث شريط التقدم
            const progress = document.getElementById('progress');
            progress.style.width = questions.length > 0 ? `${((currentQuestionIndex + 1) / questions.length) * 100}%` : '0%';

            // تحديث معلومات الاختبار
            let quizInfoText = questionLanguage === 'en'
                ? `Question ${currentQuestionIndex + 1} of ${questions.length} | Answered: ${userAnswers.filter(a => a !== null).length} | Flagged: ${markedQuestions.length}`
                : `السؤال ${currentQuestionIndex + 1} من ${questions.length} | تم الإجابة: ${userAnswers.filter(a => a !== null).length} | معلمة: ${markedQuestions.length}`;
            
            document.getElementById('quiz-info').innerHTML = quizInfoText;

            // تحديث زر وضع العلامة
            const markBtn = document.getElementById('mark-review-btn');
            if (markedQuestions.includes(currentQuestionIndex)) {
                markBtn.innerHTML = questionLanguage === 'en'
                    ? '<i class="fas fa-flag"></i> Remove Flag'
                    : '<i class="fas fa-flag"></i> إزالة العلامة';
                markBtn.style.background = 'var(--tertiary-gradient)';
            } else {
                markBtn.innerHTML = questionLanguage === 'en'
                    ? '<i class="fas fa-flag"></i> Mark for Review'
                    : '<i class="fas fa-flag"></i> وضع علامة';
                markBtn.style.background = 'var(--secondary-gradient)';
            }

            // عرض الشرح إذا كان المستخدم قد أجاب على السؤال
            if (userAnswers[currentQuestionIndex] !== null) {
                showExplanation();
            }
            
            // التحقق إذا كان هذا آخر سؤال وتمت الإجابة عليه
            checkIfLastQuestionAnswered();
        }

        // اختيار إجابة
        function selectAnswer(answerIndex) {
            if (answerLocked[currentQuestionIndex]) {
                return;
            }
            
            userAnswers[currentQuestionIndex] = answerIndex;
            answerLocked[currentQuestionIndex] = true;

            const radioInputs = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
            radioInputs.forEach(input => {
                input.disabled = true;
            });

            const labels = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
            labels.forEach(input => {
                input.closest('label').classList.add('locked');
            });

            showExplanation();
            checkIfLastQuestionAnswered();
        }

        // اختيار إجابة لسؤال املأ الفراغ
        function selectFillBlankAnswer(value) {
            if (answerLocked[currentQuestionIndex]) {
                return;
            }
            
            userAnswers[currentQuestionIndex] = value;
            answerLocked[currentQuestionIndex] = true;

            document.getElementById('fillBlankAnswer').disabled = true;
            showExplanation();
            checkIfLastQuestionAnswered();
        }

        // التحقق مما إذا كان آخر سؤال تمت الإجابة عليه
        function checkIfLastQuestionAnswered() {
            const allAnswered = userAnswers.every(answer => answer !== null);
            const lastQuestionIndex = questions.length - 1;
            const isLastQuestion = currentQuestionIndex === lastQuestionIndex;
            const lastQuestionAnswered = userAnswers[lastQuestionIndex] !== null;
            
            // إذا كان هذا هو السؤال الأخير وتمت الإجابة عليه، إنهاء الاختبار تلقائياً
            if (isLastQuestion && lastQuestionAnswered) {
                setTimeout(() => {
                    if (currentLanguage === 'ar') {
                        showSuccessMessage('تمت الإجابة على جميع الأسئلة! جاري إنهاء الاختبار...');
                    } else {
                        showSuccessMessage('All questions answered! Finishing quiz...');
                    }
                    
                    setTimeout(() => {
                        finishQuiz();
                    }, 2000);
                }, 1000);
            }
        }

        // عرض الشرح
        function showExplanation() {
            const question = shuffledQuestions[currentQuestionIndex];
            const explanationDiv = document.getElementById("explanation");
            const userAnswer = userAnswers[currentQuestionIndex];

            if (userAnswer !== null) {
                explanationDiv.style.display = "block";

                const questionLanguage = detectTextLanguage(question.q);
                
                let correctText = questionLanguage === 'en' ? 'Correct answer!' : 'إجابة صحيحة!';
                let wrongText = questionLanguage === 'en' ? 'Wrong answer' : 'إجابة خاطئة';
                let correctAnswerText = questionLanguage === 'en' ? 'Correct answer' : 'الإجابة الصحيحة';
                let explanationText = questionLanguage === 'en' ? 'Feedback' : 'التغذية الراجعة';
                let yourAnswerText = questionLanguage === 'en' ? 'Your answer' : 'إجابتك';

                let resultHTML = "";
                let isCorrect = false;

                if (question.type === 'fill_blank') {
                    // مقارنة نصية لأسئلة املأ الفراغ
                    const userAnswerStr = userAnswer.toString().toLowerCase().trim();
                    const correctAnswerStr = question.answer.toString().toLowerCase().trim();
                    
                    // مقارنة مرنة للنصوص
                    isCorrect = userAnswerStr === correctAnswerStr || 
                               Math.abs(userAnswerStr.length - correctAnswerStr.length) < 3;
                    
                    if (isCorrect) {
                        resultHTML = `<p style="color: var(--secondary);"><i class="fas fa-check-circle"></i> ${correctText}</p>`;
                    } else {
                        resultHTML = `
                        <p style="color: #dc2626;"><i class="fas fa-times-circle"></i> ${wrongText}</p>
                        <p style="color: var(--secondary);">${correctAnswerText}: ${question.answer}</p>
                        `;
                    }
                    
                    // عرض التغذية الراجعة المناسبة
                    if (isCorrect && question.explanations && question.explanations.correct) {
                        resultHTML += `
                        <div style="margin-top: 15px; padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px;">
                            <strong>📚 ${explanationText}:</strong><br>
                            ${question.explanations.correct}
                        </div>
                        `;
                    } else if (!isCorrect && question.explanations && question.explanations.mistake_feedback) {
                        // البحث عن تغذية راجعة للخطأ المحدد
                        const userAnswerLower = userAnswer.toString().toLowerCase().trim();
                        let foundFeedback = '';
                        
                        for (const [mistake, feedback] of Object.entries(question.explanations.mistake_feedback)) {
                            if (mistake.toLowerCase().trim() === userAnswerLower) {
                                foundFeedback = feedback;
                                break;
                            }
                        }
                        
                        if (foundFeedback) {
                            resultHTML += `
                            <div style="margin-top: 15px; padding: 10px; background: rgba(239, 68, 68, 0.1); border-radius: 8px;">
                                <strong>📚 ${explanationText}:</strong><br>
                                ${foundFeedback}
                            </div>
                            `;
                        } else if (question.explanations.correct) {
                            resultHTML += `
                            <div style="margin-top: 15px; padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px;">
                                <strong>📚 ${explanationText}:</strong><br>
                                ${question.explanations.correct}
                            </div>
                            `;
                        }
                    }
                } else {
                    if (userAnswer === question.answer) {
                        resultHTML = `<p style="color: var(--secondary);"><i class="fas fa-check-circle"></i> ${correctText}</p>`;
                        isCorrect = true;
                    } else {
                        resultHTML = `
                        <p style="color: #dc2626;"><i class="fas fa-times-circle"></i> ${wrongText}</p>
                        <p style="color: var(--secondary);">${correctAnswerText}: ${question.options[question.answer]}</p>
                        `;
                    }
                    
                    // عرض التغذية الراجعة لجميع الخيارات
                    if (question.explanations) {
                        resultHTML += `
                        <div style="margin-top: 15px;">
                            <strong>📚 ${explanationText}:</strong><br><br>
                        `;
                        
                        // التغذية الراجعة للخيار الصحيح
                        if (question.explanations.correct) {
                            resultHTML += `
                            <div style="padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px; margin-bottom: 8px;">
                                <strong>✅ ${correctAnswerText}:</strong> ${question.explanations.correct}
                            </div>
                            `;
                        }
                        
                        // التغذية الراجعة للخيار الذي اختاره المستخدم
                        const userChoiceText = questionLanguage === 'en' ? 'Your choice' : 'اختيارك';
                        if (question.explanations[`option${userAnswer}`]) {
                            const bgColor = isCorrect ? 'rgba(76, 175, 80, 0.1)' : 'rgba(239, 68, 68, 0.1)';
                            const icon = isCorrect ? '✅' : '❌';
                            resultHTML += `
                            <div style="padding: 10px; background: ${bgColor}; border-radius: 8px; margin-bottom: 8px;">
                                <strong>${icon} ${yourAnswerText}:</strong> ${question.explanations[`option${userAnswer}`]}
                            </div>
                            `;
                        }
                        
                        resultHTML += `</div>`;
                    }
                }

                explanationDiv.innerHTML = resultHTML;
            }
        }

        // الانتقال إلى السؤال التالي
        function nextQuestion() {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                loadQuiz();
            } else {
                // إذا كان هذا هو السؤال الأخير، التحقق مما إذا تمت الإجابة عليه
                if (userAnswers[currentQuestionIndex] !== null) {
                    finishQuiz();
                }
            }
        }

        // الانتقال إلى السؤال السابق
        function previousQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                loadQuiz();
            }
        }

        // اكتشاف لغة النص
        function detectTextLanguage(text) {
            if (!text) return quizLanguage === 'en' ? 'en' : 'ar';
            
            const arabicChars = text.match(/[؀-ۿ]/g) || [];
            const englishChars = text.match(/[a-zA-Z]/g) || [];
            
            if (englishChars.length > arabicChars.length) {
                return 'en';
            }
            return 'ar';
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
                btn.innerHTML = currentLanguage === 'ar' ? 
                    '<i class="fas fa-flag"></i> إزالة العلامة' : 
                    '<i class="fas fa-flag"></i> Remove Flag';
                btn.style.background = 'var(--tertiary-gradient)';
            } else {
                markedQuestions.splice(index, 1);
                btn.innerHTML = currentLanguage === 'ar' ? 
                    '<i class="fas fa-flag"></i> وضع علامة' : 
                    '<i class="fas fa-flag"></i> Mark for Review';
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
            
            let scoreText = currentLanguage === 'ar' ? 'الدرجة' : 'Score';
            let correctText = currentLanguage === 'ar' ? 'الصحيحة' : 'Correct';
            let progressText = currentLanguage === 'ar' ? 'التقدم' : 'Progress';
            let totalText = currentLanguage === 'ar' ? 'الإجمالي' : 'Total';
            
            document.getElementById('current-score-details').innerHTML = 
                `<strong>${scoreText}:</strong> ${score.correct} ${currentLanguage === 'ar' ? 'من' : 'of'} ${totalQuestions}`;
            document.getElementById('current-correct-details').innerHTML = 
                `<strong>${correctText}:</strong> ${score.correct}`;
            document.getElementById('current-progress-details').innerHTML = 
                `<strong>${progressText}:</strong> ${answeredCount} ${currentLanguage === 'ar' ? 'من' : 'of'} ${totalQuestions}`;
            document.getElementById('current-batch-details').innerHTML = 
                `<strong>${totalText}:</strong> ${totalQuestionsGenerated}`;
            
            document.getElementById('currentScoreModal').style.display = 'block';
        }

        function closeCurrentScoreModal() {
            document.getElementById('currentScoreModal').style.display = 'none';
        }

        // حساب الدرجات
        function calculateScore() {
            let totalCorrect = 0;
            
            userAnswers.forEach((answer, index) => {
                const question = shuffledQuestions[index];
                
                if (question.type === 'fill_blank') {
                    // مقارنة نصية لأسئلة املأ الفراغ
                    if (answer) {
                        const userAnswerStr = answer.toString().toLowerCase().trim();
                        const correctAnswerStr = question.answer.toString().toLowerCase().trim();
                        
                        if (userAnswerStr === correctAnswerStr || 
                            Math.abs(userAnswerStr.length - correctAnswerStr.length) < 3) {
                            totalCorrect++;
                        }
                    }
                } else {
                    if (answer === question.answer) {
                        totalCorrect++;
                    }
                }
            });

            const total = questions.length;
            const percentage = total > 0 ? ((totalCorrect / total) * 100).toFixed(2) : 0;

            let evaluation = "";
            let evaluationIcon = "";
            
            if (currentLanguage === 'ar') {
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
            } else {
                if (percentage >= 90) {
                    evaluation = "Excellent";
                    evaluationIcon = "🌟";
                } else if (percentage >= 80) {
                    evaluation = "Very Good";
                    evaluationIcon = "🔵";
                } else if (percentage >= 70) {
                    evaluation = "Good";
                    evaluationIcon = "🟢";
                } else if (percentage >= 60) {
                    evaluation = "Acceptable";
                    evaluationIcon = "🟡";
                } else {
                    evaluation = "Needs Improvement";
                    evaluationIcon = "⚠️";
                }
            }

            return {
                correct: totalCorrect,
                total: total,
                percentage: parseFloat(percentage),
                evaluation: evaluation,
                evaluationIcon: evaluationIcon
            };
        }

        // إنهاء الاختبار
        function finishQuiz() {
            clearInterval(timerInterval);

            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;

            document.getElementById("result-box").style.display = "block";
            
            let resultText = currentLanguage === 'ar' ? 'النتيجة' : 'Result';
            let percentageText = currentLanguage === 'ar' ? 'النسبة' : 'Percentage';
            let evaluationText = currentLanguage === 'ar' ? 'التقييم' : 'Evaluation';
            
            document.getElementById("result").innerHTML = `${score.evaluationIcon} ${resultText}: ${score.correct} ${currentLanguage === 'ar' ? 'من' : 'of'} ${score.total}`;
            document.getElementById("percentage").innerHTML = `${percentageText}: ${score.percentage}%`;
            document.getElementById("evaluation").innerHTML = `${evaluationText}: ${score.evaluation}`;

            document.getElementById("quiz").style.display = "none";
            document.getElementById("quiz-section").style.display = "none";

            document.getElementById('advanced-results').style.display = 'block';
            
            updateAdvancedStats(score);
        }

        // تحديث الإحصائيات المتقدمة
        function updateAdvancedStats(score) {
            const statsContainer = document.getElementById('stats-overview');
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const unansweredCount = questions.length - answeredCount;
            const markedCount = markedQuestions.length;
            
            let scoreText = currentLanguage === 'ar' ? 'الدرجة' : 'Score';
            let percentageText = currentLanguage === 'ar' ? 'النسبة' : 'Percentage';
            let answeredText = currentLanguage === 'ar' ? 'تم الإجابة' : 'Answered';
            let unansweredText = currentLanguage === 'ar' ? 'لم تتم الإجابة' : 'Unanswered';
            let flaggedText = currentLanguage === 'ar' ? 'معلمة' : 'Flagged';
            
            statsContainer.innerHTML = `
                <div class="stat-card">
                    <div class="stat-value">${score.correct}/${score.total}</div>
                    <div class="stat-label">${scoreText}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${score.percentage}%</div>
                    <div class="stat-label">${percentageText}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${answeredCount}</div>
                    <div class="stat-label">${answeredText}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${unansweredCount}</div>
                    <div class="stat-label">${unansweredText}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${markedCount}</div>
                    <div class="stat-label">${flaggedText}</div>
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
            
            if (pdfFile) {
                removePDF();
            }
            
            if (imageFile) {
                removeImage();
            }
            
            document.getElementById('result-box').style.display = 'none';
            document.getElementById('advanced-results').style.display = 'none';
            document.getElementById('setup-section').style.display = 'block';
            document.getElementById('quiz-section').style.display = 'none';
            
            document.getElementById('quiz-title').value = '';
            document.getElementById('quiz-topic').value = '';
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

            clearInterval(timerInterval);
            startTimer();
            loadQuiz();
        }

        // التهيئة الأولية
        window.onload = function() {
            checkDarkModePreference();
            
            const dropZones = document.querySelectorAll('.file-upload-label');
            
            dropZones.forEach(dropZone => {
                dropZone.addEventListener('dragover', (e) => {
                    e.preventDefault();
                    dropZone.style.background = 'rgba(21, 152, 149, 0.2)';
                    dropZone.style.borderColor = 'var(--accent-glow)';
                });
                
                dropZone.addEventListener('dragleave', () => {
                    dropZone.style.background = 'rgba(21, 152, 149, 0.05)';
                    dropZone.style.borderColor = 'var(--accent)';
                });
            });

            document.getElementById('api-key').addEventListener('input', function() {
                if (this.value.trim()) {
                    this.style.borderColor = 'var(--secondary)';
                    document.getElementById('api-key-status').style.display = 'none';
                    isAPIKeyValid = false;
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