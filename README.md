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
            --summary-blue: #2196F3;
            --summary-blue-glow: #64B5F6;
            --flashcard-purple: #9C27B0;
            --flashcard-purple-glow: #BA68C8;
            --islamic-green: #228B22;
            --islamic-blue: #1A5F7A;
            --islamic-gold: #D4AF37;
            --islamic-teal: #159895;

            --primary-gradient: linear-gradient(135deg, var(--primary) 0%, var(--primary-glow) 50%, var(--primary-light) 100%);
            --accent-gradient: linear-gradient(135deg, var(--accent) 0%, var(--accent-glow) 50%, var(--islamic-teal) 100%);
            --secondary-gradient: linear-gradient(135deg, var(--secondary) 0%, var(--secondary-glow) 50%, var(--islamic-green) 100%);
            --tertiary-gradient: linear-gradient(135deg, var(--tertiary) 0%, var(--tertiary-glow) 50%, var(--islamic-gold) 100%);
            --summary-gradient: linear-gradient(135deg, var(--summary-blue) 0%, var(--summary-blue-glow) 50%, var(--accent-light) 100%);
            --flashcard-gradient: linear-gradient(135deg, var(--flashcard-purple) 0%, var(--flashcard-purple-glow) 50%, var(--primary-light) 100%);
            --islamic-gradient: linear-gradient(135deg, var(--islamic-blue) 0%, var(--islamic-teal) 50%, var(--islamic-green) 100%);

            --glow-primary: 0 0 20px rgba(26, 95, 122, 0.7), 0 0 40px rgba(26, 95, 122, 0.5), 0 0 60px rgba(26, 95, 122, 0.3);
            --glow-accent: 0 0 20px rgba(21, 152, 149, 0.7), 0 0 40px rgba(21, 152, 149, 0.5), 0 0 60px rgba(21, 152, 149, 0.3);
            --glow-secondary: 0 0 20px rgba(76, 175, 80, 0.7), 0 0 40px rgba(76, 175, 80, 0.5), 0 0 60px rgba(76, 175, 80, 0.3);
            --glow-tertiary: 0 0 20px rgba(255, 152, 0, 0.7), 0 0 40px rgba(255, 152, 0, 0.5), 0 0 60px rgba(255, 152, 0, 0.3);
            --glow-summary: 0 0 20px rgba(33, 150, 243, 0.7), 0 0 40px rgba(33, 150, 243, 0.5), 0 0 60px rgba(33, 150, 243, 0.3);
            --glow-flashcard: 0 0 20px rgba(156, 39, 176, 0.7), 0 0 40px rgba(156, 39, 176, 0.5), 0 0 60px rgba(156, 39, 176, 0.3);
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
            align-items: center;
        }

        .theme-btn, .lang-btn, .sound-btn {
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

        .theme-btn:hover, .lang-btn:hover, .sound-btn:hover {
            background: rgba(26, 95, 122, 0.3);
            transform: translateY(-3px);
            box-shadow: 0 0 25px rgba(26, 95, 122, 0.5);
            border-color: rgba(255, 255, 255, 0.5);
        }

        .lang-btn.active {
            background: var(--accent-gradient);
            border-color: var(--accent);
        }

        .sound-btn.muted {
            background: rgba(239, 68, 68, 0.2);
            border-color: rgba(239, 68, 68, 0.3);
        }

        .sound-btn.muted i {
            color: #ef4444;
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
            max-width: 1200px;
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

        /* PDF Details Section */
        .pdf-details-section {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            border: 2px dashed var(--border);
            display: none;
        }

        .pdf-details-section.active {
            display: block;
            animation: slideDown 0.5s ease;
        }

        .pdf-details-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .pdf-details-tab {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }

        .pdf-details-tab:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-3px);
        }

        .pdf-details-tab.active {
            background: rgba(26, 95, 122, 0.3);
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(21, 152, 149, 0.3);
        }

        .pdf-details-content {
            display: none;
        }

        .pdf-details-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        .details-input-group {
            margin: 15px 0;
        }

        .details-input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--text);
        }

        .details-input {
            width: 100%;
            padding: 12px 18px;
            border: 2px solid var(--border);
            border-radius: 10px;
            font-size: 1rem;
            background: var(--card-bg);
            color: var(--text);
            transition: all 0.3s ease;
        }

        .details-input:focus {
            outline: none;
            border-color: var(--accent);
        }

        .page-range-inputs {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .page-range-inputs input {
            flex: 1;
        }

        .page-range-separator {
            color: var(--light-text);
            font-weight: bold;
        }

        .topics-textarea {
            min-height: 120px;
            resize: vertical;
        }

        .hint-text {
            font-size: 0.85rem;
            color: var(--light-text);
            margin-top: 8px;
            font-style: italic;
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

        .btn-summary {
            background: var(--summary-gradient);
            color: white;
            box-shadow: var(--glow-summary), 0 8px 25px rgba(33, 150, 243, 0.4);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .btn-flashcard {
            background: var(--flashcard-gradient);
            color: white;
            box-shadow: var(--glow-flashcard), 0 8px 25px rgba(156, 39, 176, 0.4);
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

        .btn-summary:hover {
            box-shadow: var(--glow-summary), 0 15px 40px rgba(33, 150, 243, 0.6);
        }

        .btn-flashcard:hover {
            box-shadow: var(--glow-flashcard), 0 15px 40px rgba(156, 39, 176, 0.6);
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
        #quiz-section, #summary-section, #flashcards-section {
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

        /* Option Feedback */
        .option-feedback {
            display: none;
            padding: 15px;
            margin-top: 10px;
            border-radius: 10px;
            font-size: 0.9rem;
            animation: slideDown 0.3s ease;
        }

        .option-feedback.correct {
            background: rgba(76, 175, 80, 0.1);
            border-right: 4px solid var(--secondary);
        }

        .option-feedback.incorrect {
            background: rgba(239, 68, 68, 0.1);
            border-right: 4px solid #ef4444;
        }

        .option-feedback.show {
            display: block;
        }

        /* Instant Review */
        .instant-review {
            background: rgba(255, 193, 7, 0.1);
            border: 2px solid #ffc107;
            border-radius: 15px;
            padding: 20px;
            margin-top: 20px;
            display: none;
        }

        .instant-review.show {
            display: block;
            animation: slideDown 0.5s ease;
        }

        .instant-review-title {
            font-weight: bold;
            color: #ffc107;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .instant-review-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }

        .review-option {
            flex: 1;
            min-width: 200px;
            padding: 12px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .review-option.correct {
            background: rgba(76, 175, 80, 0.1);
            border-color: var(--secondary);
        }

        .review-option.incorrect {
            background: rgba(239, 68, 68, 0.1);
            border-color: #ef4444;
        }

        .review-option-text {
            font-weight: 500;
            margin-bottom: 5px;
        }

        .review-option-feedback {
            font-size: 0.85rem;
            opacity: 0.9;
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

        /* Summary Section Styles */
        .summary-content {
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

        .summary-content::before {
            content: "";
            position: absolute;
            top: 0;
            right: 0;
            width: 100%;
            height: 5px;
            background: var(--summary-gradient);
        }

        .summary-title {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--summary-blue);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .summary-section {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid var(--border);
        }

        .summary-section:last-child {
            border-bottom: none;
        }

        .summary-section-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--text);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .summary-point {
            margin-bottom: 10px;
            padding-right: 15px;
            position: relative;
        }

        .summary-point:before {
            content: "•";
            position: absolute;
            right: 0;
            color: var(--summary-blue);
            font-weight: bold;
        }

        .summary-note {
            background: rgba(33, 150, 243, 0.1);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            border-right: 3px solid var(--summary-blue);
        }

        /* Flashcards Section Styles */
        .flashcard-container {
            perspective: 1000px;
            width: 100%;
            height: 400px;
            margin: 20px auto;
        }

        .flashcard {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
        }

        .flashcard.flipped {
            transform: rotateY(180deg);
        }

        .flashcard-front, .flashcard-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 30px;
            text-align: center;
        }

        .flashcard-front {
            background: var(--card-bg);
            border: 2px solid var(--flashcard-purple);
            box-shadow: 0 10px 30px rgba(156, 39, 176, 0.2);
        }

        .flashcard-back {
            background: var(--card-bg);
            border: 2px solid var(--summary-blue);
            box-shadow: 0 10px 30px rgba(33, 150, 243, 0.2);
            transform: rotateY(180deg);
        }

        .flashcard-icon {
            font-size: 3rem;
            color: var(--flashcard-purple);
            margin-bottom: 20px;
        }

        .flashcard-content {
            font-size: 1.3rem;
            line-height: 1.6;
            color: var(--text);
            max-width: 800px;
        }

        .flashcard-index {
            position: absolute;
            top: 15px;
            left: 15px;
            background: var(--flashcard-gradient);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .flashcard-category {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(156, 39, 176, 0.1);
            color: var(--flashcard-purple);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
        }

        .flashcard-controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .flashcard-progress {
            display: flex;
            align-items: center;
            gap: 15px;
            margin: 20px 0;
            background: rgba(156, 39, 176, 0.1);
            padding: 15px;
            border-radius: 15px;
        }

        .progress-label {
            font-weight: 600;
            color: var(--flashcard-purple);
        }

        .flashcard-stats {
            display: flex;
            gap: 20px;
            margin: 20px 0;
            flex-wrap: wrap;
            justify-content: center;
        }

        .flashcard-stat {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            min-width: 150px;
        }

        .flashcard-stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--flashcard-purple);
            margin-bottom: 5px;
        }

        .flashcard-stat-label {
            font-size: 0.9rem;
            color: var(--light-text);
        }

        /* Mastery Level Indicators */
        .mastery-level {
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.9rem;
            font-weight: 600;
            display: inline-block;
            margin-left: 10px;
        }

        .mastery-beginner {
            background: rgba(239, 68, 68, 0.1);
            color: #dc2626;
        }

        .mastery-intermediate {
            background: rgba(255, 152, 0, 0.1);
            color: #f59e0b;
        }

        .mastery-advanced {
            background: rgba(76, 175, 80, 0.1);
            color: #4CAF50;
        }

        .mastery-expert {
            background: rgba(156, 39, 176, 0.1);
            color: var(--flashcard-purple);
        }

        /* Flashcard Actions */
        .flashcard-actions {
            position: absolute;
            bottom: 15px;
            right: 15px;
            display: flex;
            gap: 10px;
        }

        .flashcard-action-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .flashcard-action-btn:hover {
            background: var(--flashcard-purple);
            color: white;
            transform: translateY(-3px);
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

            .card, .question-box, .summary-content {
                padding: 25px;
            }

            .flashcard-container {
                height: 300px;
            }

            .flashcard-content {
                font-size: 1.1rem;
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

            .instant-review-options {
                flex-direction: column;
            }
            
            .review-option {
                min-width: 100%;
            }

            .page-range-inputs {
                flex-direction: column;
                gap: 10px;
            }

            .page-range-separator {
                display: none;
            }

            .pdf-details-tabs {
                flex-direction: column;
            }

            .flashcard-controls {
                flex-direction: column;
                align-items: center;
            }
            
            .flashcard-stat {
                min-width: 120px;
            }
        }

        /* Sound Animation */
        .sound-wave {
            display: inline-block;
            margin-left: 8px;
        }

        .sound-wave span {
            display: inline-block;
            width: 3px;
            height: 10px;
            background: var(--secondary);
            margin: 0 1px;
            border-radius: 2px;
            animation: soundWave 1.2s infinite ease-in-out;
        }

        .sound-wave span:nth-child(2) {
            animation-delay: 0.1s;
        }

        .sound-wave span:nth-child(3) {
            animation-delay: 0.2s;
        }

        .sound-wave span:nth-child(4) {
            animation-delay: 0.3s;
        }

        @keyframes soundWave {
            0%, 100% {
                transform: scaleY(1);
            }
            50% {
                transform: scaleY(2);
            }
        }

        .sound-btn.muted .sound-wave span {
            background: #ef4444;
            animation: none;
            transform: scaleY(0.5);
        }

        /* Content Sections */
        .content-section {
            margin: 20px 0;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            border: 1px solid var(--border);
        }

        .content-section h3 {
            color: var(--text);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* Output Container */
        .output-container {
            margin-top: 30px;
            padding: 25px;
            background: var(--card-bg);
            border-radius: 20px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            max-height: 600px;
            overflow-y: auto;
        }

        .output-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border);
        }

        .output-title {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--text);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .copy-btn {
            background: var(--accent-gradient);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 5px;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(21, 152, 149, 0.3);
        }

        .copy-btn.copied {
            background: var(--secondary-gradient);
        }

        /* Navigation Dots */
        .navigation-dots {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 20px 0;
        }

        .nav-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: var(--border);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nav-dot.active {
            background: var(--accent);
            transform: scale(1.2);
        }

        /* Tab Content */
        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        /* Summary Types */
        .summary-type-selector {
            display: flex;
            gap: 15px;
            margin: 15px 0;
            flex-wrap: wrap;
        }

        .summary-type {
            flex: 1;
            min-width: 200px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            border: 2px solid transparent;
        }

        .summary-type:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-3px);
        }

        .summary-type.active {
            background: rgba(33, 150, 243, 0.2);
            border-color: var(--summary-blue);
            box-shadow: 0 0 20px rgba(33, 150, 243, 0.3);
        }

        .summary-type-icon {
            font-size: 2rem;
            color: var(--summary-blue);
            margin-bottom: 10px;
        }

        .summary-type-title {
            font-weight: 700;
            color: var(--text);
            margin-bottom: 5px;
        }

        .summary-type-desc {
            color: var(--light-text);
            font-size: 0.9rem;
        }
        
        /* Summary Hierarchy Styles */
        .summary-hierarchy {
            direction: rtl;
            text-align: right;
        }
        
        .summary-main-title {
            color: var(--primary);
            font-size: 1.8rem;
            font-weight: 800;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 3px solid var(--accent);
            text-align: center;
        }
        
        .summary-chapter {
            background: rgba(26, 95, 122, 0.05);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            border: 2px solid rgba(26, 95, 122, 0.1);
        }
        
        .summary-chapter-title {
            color: var(--primary);
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 20px;
            padding-right: 15px;
            border-right: 4px solid var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .summary-section {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            border: 1px solid rgba(21, 152, 149, 0.1);
        }
        
        .summary-section-title {
            color: var(--accent);
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 15px;
            padding-right: 15px;
            border-right: 3px solid var(--accent);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .summary-subsection {
            margin-bottom: 15px;
            padding-right: 20px;
        }
        
        .summary-subsection-title {
            color: var(--summary-blue);
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 10px;
            padding-right: 15px;
            border-right: 2px solid var(--summary-blue);
        }
        
        .summary-points {
            list-style: none;
            padding-right: 30px;
            margin-top: 10px;
        }
        
        .summary-point {
            margin-bottom: 12px;
            padding-right: 20px;
            position: relative;
            line-height: 1.7;
            color: var(--text);
        }
        
        .summary-point:before {
            content: "•";
            position: absolute;
            right: 0;
            color: var(--secondary);
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .summary-key-concept {
            background: rgba(76, 175, 80, 0.05);
            border-right: 4px solid var(--secondary);
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            font-weight: 500;
        }
        
        .summary-definition {
            background: rgba(33, 150, 243, 0.05);
            border-right: 4px solid var(--summary-blue);
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
        }
        
        .summary-note {
            background: rgba(255, 152, 0, 0.05);
            border-right: 4px solid var(--tertiary);
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            font-style: italic;
        }
        
        .summary-important {
            background: rgba(156, 39, 176, 0.05);
            border-right: 4px solid var(--flashcard-purple);
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            font-weight: bold;
        }
        
        /* English mode for summary hierarchy */
        body.english-mode .summary-hierarchy {
            direction: ltr;
            text-align: left;
        }
        
        body.english-mode .summary-chapter-title {
            padding-left: 15px;
            padding-right: 0;
            border-left: 4px solid var(--primary);
            border-right: none;
        }
        
        body.english-mode .summary-section-title {
            padding-left: 15px;
            padding-right: 0;
            border-left: 3px solid var(--accent);
            border-right: none;
        }
        
        body.english-mode .summary-subsection-title {
            padding-left: 15px;
            padding-right: 0;
            border-left: 2px solid var(--summary-blue);
            border-right: none;
        }
        
        body.english-mode .summary-points {
            padding-left: 30px;
            padding-right: 0;
        }
        
        body.english-mode .summary-point {
            padding-left: 20px;
            padding-right: 0;
        }
        
        body.english-mode .summary-point:before {
            left: 0;
            right: auto;
        }
        
        body.english-mode .summary-key-concept,
        body.english-mode .summary-definition,
        body.english-mode .summary-note,
        body.english-mode .summary-important {
            border-left: 4px solid;
            border-right: none;
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
                <button class="sound-btn" id="soundBtn" onclick="toggleSound()">
                    <i class="fas fa-volume-up"></i>
                    <div class="sound-wave">
                        <span></span>
                        <span></span>
                        <span></span>
                        <span></span>
                    </div>
                </button>
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
                <p class="hero-subtitle" id="hero-subtitle">أنشئ اختبارات وملخصات وبطاقات تعليمية باستخدام الذكاء الاصطناعي</p>
                
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
                        <div class="method-desc" id="image-desc">تحميل صورة وتوليد محتوى باستخدام الذكاء الاصطناعي</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('pdf')" id="pdf-tab">
                        <div class="method-icon">
                            <i class="fas fa-file-pdf"></i>
                        </div>
                        <div class="method-title" id="pdf-title">رفع ملف PDF</div>
                        <div class="method-desc" id="pdf-desc">تحميل ملف وتوليد محتوى باستخدام الذكاء الاصطناعي</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('summarize')" id="summarize-tab">
                        <div class="method-icon">
                            <i class="fas fa-file-alt"></i>
                        </div>
                        <div class="method-title" id="summarize-title">تلخيص المحتوى</div>
                        <div class="method-desc" id="summarize-desc">تلخيص النصوص والملفات بأسلوبين مختلفين</div>
                    </div>
                    <div class="method-tab" onclick="selectMethod('flashcards')" id="flashcards-tab">
                        <div class="method-icon">
                            <i class="fas fa-layer-group"></i>
                        </div>
                        <div class="method-title" id="flashcards-title">بطاقات تعليمية</div>
                        <div class="method-desc" id="flashcards-desc">إنشاء بطاقات تعليمية تفاعلية للمراجعة</div>
                    </div>
                </div>

                <!-- اختيار لغة المحتوى -->
                <div id="content-language-section">
                    <div class="input-group">
                        <label><i class="fas fa-globe"></i> <span id="language-label">اختر لغة المحتوى</span></label>
                        <div class="language-selector">
                            <div class="language-option active" onclick="selectContentLanguage('ar')" id="arabic-language">
                                <div class="language-flag">🇸🇦</div>
                                <div class="language-name" id="arabic-language-name">العربية</div>
                                <div class="language-desc" id="arabic-language-desc">محتوى باللغة العربية</div>
                            </div>
                            <div class="language-option" onclick="selectContentLanguage('en')" id="english-language">
                                <div class="language-flag">🇺🇸</div>
                                <div class="language-name" id="english-language-name">English</div>
                                <div class="language-desc" id="english-language-desc">Content in English</div>
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

                <!-- قسم الإدخال اليدوي (للاستخدام في الاختبارات فقط) -->
                <div id="manual-section">
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
                            <option value="25">25 أسئلة</option>
                            <option value="30">30 أسئلة</option>
                            <option value="35">35 أسئلة</option>
                            <option value="40">40 أسئلة</option>
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
                                <p id="image-analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الصورة وتوليد المحتوى</p>
                            </div>
                            <div id="image-preview-container" class="image-preview-container">
                                <img id="preview-image" class="image-preview" alt="معاينة الصورة">
                            </div>
                            <button class="remove-file-btn" onclick="removeImage()" id="remove-image-btn">
                                <i class="fas fa-trash"></i> <span id="remove-image-text">إزالة الصورة</span>
                            </button>
                        </div>
                    </div>

                    <!-- خيارات إضافية حسب الطريقة -->
                    <div id="image-quiz-options" style="display: none;">
                        <div class="question-type-selector">
                            <div class="input-group">
                                <label><i class="fas fa-list-check"></i> <span>اختر نوع الأسئلة المطلوبة</span></label>
                                <div class="question-type-options">
                                    <div class="question-type-option active" onclick="toggleQuestionType('multipleChoice')" id="image-multiple-choice-option">
                                        <input type="checkbox" id="imageMultipleChoiceCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-check-circle"></i>
                                        </div>
                                        <div class="question-type-name">أسئلة اختيار متعدد</div>
                                    </div>
                                    <div class="question-type-option active" onclick="toggleQuestionType('trueFalse')" id="image-true-false-option">
                                        <input type="checkbox" id="imageTrueFalseCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-balance-scale"></i>
                                        </div>
                                        <div class="question-type-name">أسئلة (صح/ خطأ)</div>
                                    </div>
                                    <div class="question-type-option active" onclick="toggleQuestionType('fillBlank')" id="image-fill-blank-option">
                                        <input type="checkbox" id="imageFillBlankCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-pen-to-square"></i>
                                        </div>
                                        <div class="question-type-name">املأ الفراغ</div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="input-group">
                            <label for="num-questions-image"><i class="fas fa-question-circle"></i> <span id="num-questions-label-image">عدد الأسئلة المطلوبة</span></label>
                            <select id="num-questions-image" class="input-field">
                                <option value="5">5 أسئلة</option>
                                <option value="10" selected>10 أسئلة</option>
                                <option value="15">15 أسئلة</option>
                                <option value="20">20 أسئلة</option>
                                <option value="25">25 أسئلة</option>
                                <option value="30">30 أسئلة</option>
                                <option value="35">35 أسئلة</option>
                                <option value="40">40 أسئلة</option>
                            </select>
                        </div>
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
                                الحد الأقصى لحجم الملف: 100MB
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
                                <p id="analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الملف وتوليد المحتوى</p>
                            </div>
                            <button class="remove-file-btn" onclick="removePDF()" id="remove-file-btn">
                                <i class="fas fa-trash"></i> <span id="remove-file-text">إزالة الملف</span>
                            </button>
                        </div>
                    </div>

                    <!-- قسم تفاصيل PDF -->
                    <div class="pdf-details-section" id="pdf-details-section">
                        <h4 style="color: var(--text); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                            <i class="fas fa-filter"></i> <span id="pdf-details-title">تحديد تفاصيل المحتوى</span>
                        </h4>
                        <p style="color: var(--light-text); margin-bottom: 20px; font-size: 0.95rem;" id="pdf-details-subtitle">
                            يمكنك تحديد نطاق محدد من الملف لتحليله. اترك الحقول فارغة لتحليل الملف بالكامل.
                        </p>
                        
                        <div class="pdf-details-tabs">
                            <div class="pdf-details-tab active" onclick="selectPDFDetailsTab('pages')" id="pages-tab">
                                <i class="fas fa-file"></i> <span id="pages-tab-text">الصفحات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('units')" id="units-tab">
                                <i class="fas fa-layer-group"></i> <span id="units-tab-text">الوحدات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('topics')" id="topics-tab">
                                <i class="fas fa-tags"></i> <span id="topics-tab-text">المواضيع</span>
                            </div>
                        </div>
                        
                        <!-- محتوى الصفحات -->
                        <div class="pdf-details-content active" id="pages-content">
                            <div class="details-input-group">
                                <label for="page-range"><i class="fas fa-arrows-alt-h"></i> <span id="page-range-label">نطاق الصفحات</span></label>
                                <div class="page-range-inputs">
                                    <input type="number" id="start-page" class="details-input" placeholder="الصفحة الأولى" min="1">
                                    <div class="page-range-separator">إلى</div>
                                    <input type="number" id="end-page" class="details-input" placeholder="الصفحة الأخيرة">
                                </div>
                                <p class="hint-text" id="page-range-hint">
                                    اترك الحقول فارغة لتحليل جميع الصفحات. أدخل أرقام الصفحات فقط.
                                </p>
                            </div>
                            
                            <div class="details-input-group">
                                <label for="specific-pages"><i class="fas fa-hashtag"></i> <span id="specific-pages-label">صفحات محددة</span></label>
                                <input type="text" id="specific-pages" class="details-input" 
                                       placeholder="مثال: 1,3,5-8,10,12-15">
                                <p class="hint-text" id="specific-pages-hint">
                                    يمكنك تحديد صفحات محددة باستخدام الفواصل والفواصل المنقوطة للنطاقات.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى الوحدات -->
                        <div class="pdf-details-content" id="units-content">
                            <div class="details-input-group">
                                <label for="units-list"><i class="fas fa-list-ol"></i> <span id="units-list-label">الوحدات المطلوبة</span></label>
                                <textarea id="units-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- الوحدة الأولى: المدخل إلى علم الفقه
- الوحدة الثانية: أحكام الطهارة
- الوحدة الثالثة: أحكام الصلاة
- الوحدة الرابعة: أحكام الصيام"></textarea>
                                <p class="hint-text" id="units-list-hint">
                                    اذكر العناوين الرئيسية للوحدات أو الفصول التي تريد التركيز عليها.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى المواضيع -->
                        <div class="pdf-details-content" id="topics-content">
                            <div class="details-input-group">
                                <label for="topics-list"><i class="fas fa-tags"></i> <span id="topics-list-label">المواضيع المطلوبة</span></label>
                                <textarea id="topics-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- تعريف الصلاة وأركانها
- شروط الصلاة
- مكروهات الصلاة
- مبطلات الصلاة
- صلاة الجماعة
- صلاة المريض"></textarea>
                                <p class="hint-text" id="topics-list-hint">
                                    اذكر المواضيع أو المفاهيم المحددة التي تريد التركيز عليها في التحليل.
                                </p>
                            </div>
                        </div>
                    </div>

                    <!-- خيارات إضافية حسب الطريقة -->
                    <div id="pdf-quiz-options" style="display: none;">
                        <div class="question-type-selector">
                            <div class="input-group">
                                <label><i class="fas fa-list-check"></i> <span>اختر نوع الأسئلة المطلوبة</span></label>
                                <div class="question-type-options">
                                    <div class="question-type-option active" onclick="toggleQuestionType('multipleChoice')" id="pdf-multiple-choice-option">
                                        <input type="checkbox" id="pdfMultipleChoiceCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-check-circle"></i>
                                        </div>
                                        <div class="question-type-name">أسئلة اختيار متعدد</div>
                                    </div>
                                    <div class="question-type-option active" onclick="toggleQuestionType('trueFalse')" id="pdf-true-false-option">
                                        <input type="checkbox" id="pdfTrueFalseCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-balance-scale"></i>
                                        </div>
                                        <div class="question-type-name">أسئلة (صح/ خطأ)</div>
                                    </div>
                                    <div class="question-type-option active" onclick="toggleQuestionType('fillBlank')" id="pdf-fill-blank-option">
                                        <input type="checkbox" id="pdfFillBlankCheckbox" checked>
                                        <div class="question-type-icon">
                                            <i class="fas fa-pen-to-square"></i>
                                        </div>
                                        <div class="question-type-name">املأ الفراغ</div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="input-group">
                            <label for="num-questions-pdf"><i class="fas fa-question-circle"></i> <span id="num-questions-label-pdf">عدد الأسئلة المطلوبة</span></label>
                            <select id="num-questions-pdf" class="input-field">
                                <option value="5">5 أسئلة</option>
                                <option value="10" selected>10 أسئلة</option>
                                <option value="15">15 أسئلة</option>
                                <option value="20">20 أسئلة</option>
                                <option value="25">25 أسئلة</option>
                                <option value="30">30 أسئلة</option>
                                <option value="35">35 أسئلة</option>
                                <option value="40">40 أسئلة</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- قسم تلخيص المحتوى -->
                <div id="summarize-section" style="display: none;">
                    <div class="file-upload-container">
                        <label for="summary-file" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <h4 id="summary-upload-title">انقر لرفع ملف للتلخيص</h4>
                            <p id="summary-upload-subtitle">أو اسحب وأفلت الملف هنا</p>
                            <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;" id="summary-upload-size">
                                الأنواع المسموحة: PDF, TXT, DOC, DOCX, JPG, PNG
                            </p>
                        </label>
                        <input type="file" id="summary-file" class="file-input" accept=".pdf,.txt,.doc,.docx,.jpg,.jpeg,.png" onchange="handleSummaryUpload(event)">
                        
                        <div class="file-preview" id="summary-preview">
                            <div class="file-info">
                                <div class="file-icon">
                                    <i class="fas fa-file-alt"></i>
                                </div>
                                <div class="file-details">
                                    <h5 id="summary-filename"></h5>
                                    <p id="summary-filesize"></p>
                                </div>
                            </div>
                            <div class="analysis-status" id="summary-analysis-status">
                                <i class="fas fa-robot"></i>
                                <p id="summary-analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الملف وإنشاء التلخيص</p>
                            </div>
                            <button class="remove-file-btn" onclick="removeSummaryFile()" id="remove-summary-btn">
                                <i class="fas fa-trash"></i> <span id="remove-summary-text">إزالة الملف</span>
                            </button>
                        </div>
                    </div>

                    <!-- نفس قسم تفاصيل PDF -->
                    <div class="pdf-details-section" id="summary-details-section">
                        <h4 style="color: var(--text); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                            <i class="fas fa-filter"></i> <span>تحديد تفاصيل المحتوى</span>
                        </h4>
                        <p style="color: var(--light-text); margin-bottom: 20px; font-size: 0.95rem;">
                            يمكنك تحديد نطاق محدد من الملف لتحليله. اترك الحقول فارغة لتحليل الملف بالكامل.
                        </p>
                        
                        <div class="pdf-details-tabs">
                            <div class="pdf-details-tab active" onclick="selectPDFDetailsTab('pages')" id="summary-pages-tab">
                                <i class="fas fa-file"></i> <span>الصفحات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('units')" id="summary-units-tab">
                                <i class="fas fa-layer-group"></i> <span>الوحدات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('topics')" id="summary-topics-tab">
                                <i class="fas fa-tags"></i> <span>المواضيع</span>
                            </div>
                        </div>
                        
                        <!-- محتوى الصفحات -->
                        <div class="pdf-details-content active" id="summary-pages-content">
                            <div class="details-input-group">
                                <label for="summary-start-page"><i class="fas fa-arrows-alt-h"></i> <span>نطاق الصفحات</span></label>
                                <div class="page-range-inputs">
                                    <input type="number" id="summary-start-page" class="details-input" placeholder="الصفحة الأولى" min="1">
                                    <div class="page-range-separator">إلى</div>
                                    <input type="number" id="summary-end-page" class="details-input" placeholder="الصفحة الأخيرة">
                                </div>
                                <p class="hint-text">
                                    اترك الحقول فارغة لتحليل جميع الصفحات. أدخل أرقام الصفحات فقط.
                                </p>
                            </div>
                            
                            <div class="details-input-group">
                                <label for="summary-specific-pages"><i class="fas fa-hashtag"></i> <span>صفحات محددة</span></label>
                                <input type="text" id="summary-specific-pages" class="details-input" 
                                       placeholder="مثال: 1,3,5-8,10,12-15">
                                <p class="hint-text">
                                    يمكنك تحديد صفحات محددة باستخدام الفواصل والفواصل المنقوطة للنطاقات.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى الوحدات -->
                        <div class="pdf-details-content" id="summary-units-content">
                            <div class="details-input-group">
                                <label for="summary-units-list"><i class="fas fa-list-ol"></i> <span>الوحدات المطلوبة</span></label>
                                <textarea id="summary-units-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- الوحدة الأولى: المدخل إلى علم الفقه
- الوحدة الثانية: أحكام الطهارة
- الوحدة الثالثة: أحكام الصلاة
- الوحدة الرابعة: أحكام الصيام"></textarea>
                                <p class="hint-text">
                                    اذكر العناوين الرئيسية للوحدات أو الفصول التي تريد التركيز عليها.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى المواضيع -->
                        <div class="pdf-details-content" id="summary-topics-content">
                            <div class="details-input-group">
                                <label for="summary-topics-list"><i class="fas fa-tags"></i> <span>المواضيع المطلوبة</span></label>
                                <textarea id="summary-topics-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- تعريف الصلاة وأركانها
- شروط الصلاة
- مكروهات الصلاة
- مبطلات الصلاة
- صلاة الجماعة
- صلاة المريض"></textarea>
                                <p class="hint-text">
                                    اذكر المواضيع أو المفاهيم المحددة التي تريد التركيز عليها في التحليل.
                                </p>
                            </div>
                        </div>
                    </div>

                    <div class="input-group">
                        <label><i class="fas fa-chart-pie"></i> <span id="summary-type-label">نوع التلخيص</span></label>
                        <div class="summary-type-selector">
                            <div class="summary-type active" onclick="selectSummaryType('detailed')" id="detailed-summary">
                                <div class="summary-type-icon">
                                    <i class="fas fa-file-alt"></i>
                                </div>
                                <div class="summary-type-title" id="detailed-summary-name">تفاصيل عميقة</div>
                                <div class="summary-type-desc" id="detailed-summary-desc">تلخيص مفصل مع جميع النقاط الرئيسية</div>
                            </div>
                            <div class="summary-type" onclick="selectSummaryType('quick')" id="quick-summary">
                                <div class="summary-type-icon">
                                    <i class="fas fa-bolt"></i>
                                </div>
                                <div class="summary-type-title" id="quick-summary-name">ملخص سريع</div>
                                <div class="summary-type-desc" id="quick-summary-desc">نقاط رئيسية مركزة وسريعة القراءة</div>
                            </div>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="summary-length"><i class="fas fa-ruler"></i> <span id="summary-length-label">طول التلخيص</span></label>
                        <select id="summary-length" class="input-field">
                            <option value="short">مختصر (نقاط رئيسية)</option>
                            <option value="medium" selected>متوسط (متوازن)</option>
                            <option value="long">مفصل (شامل)</option>
                        </select>
                    </div>
                </div>

                <!-- قسم البطاقات التعليمية -->
                <div id="flashcards-section" style="display: none;">
                    <div class="file-upload-container">
                        <label for="flashcards-file" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <h4 id="flashcards-upload-title">انقر لرفع ملف للبطاقات التعليمية</h4>
                            <p id="flashcards-upload-subtitle">أو اسحب وأفلت الملف هنا</p>
                            <p style="font-size: 0.8rem; color: var(--light-text); margin-top: 10px;" id="flashcards-upload-size">
                                الأنواع المسموحة: PDF, TXT, DOC, DOCX, JPG, PNG
                            </p>
                        </label>
                        <input type="file" id="flashcards-file" class="file-input" accept=".pdf,.txt,.doc,.docx,.jpg,.jpeg,.png" onchange="handleFlashcardsUpload(event)">
                        
                        <div class="file-preview" id="flashcards-preview">
                            <div class="file-info">
                                <div class="file-icon">
                                    <i class="fas fa-layer-group"></i>
                                </div>
                                <div class="file-details">
                                    <h5 id="flashcards-filename"></h5>
                                    <p id="flashcards-filesize"></p>
                                </div>
                            </div>
                            <div class="analysis-status" id="flashcards-analysis-status">
                                <i class="fas fa-robot"></i>
                                <p id="flashcards-analysis-status-text">سيقوم الذكاء الاصطناعي بتحليل الملف وإنشاء البطاقات التعليمية</p>
                            </div>
                            <button class="remove-file-btn" onclick="removeFlashcardsFile()" id="remove-flashcards-btn">
                                <i class="fas fa-trash"></i> <span id="remove-flashcards-text">إزالة الملف</span>
                            </button>
                        </div>
                    </div>

                    <!-- نفس قسم تفاصيل PDF -->
                    <div class="pdf-details-section" id="flashcards-details-section">
                        <h4 style="color: var(--text); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                            <i class="fas fa-filter"></i> <span>تحديد تفاصيل المحتوى</span>
                        </h4>
                        <p style="color: var(--light-text); margin-bottom: 20px; font-size: 0.95rem;">
                            يمكنك تحديد نطاق محدد من الملف لتحليله. اترك الحقول فارغة لتحليل الملف بالكامل.
                        </p>
                        
                        <div class="pdf-details-tabs">
                            <div class="pdf-details-tab active" onclick="selectPDFDetailsTab('pages')" id="flashcards-pages-tab">
                                <i class="fas fa-file"></i> <span>الصفحات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('units')" id="flashcards-units-tab">
                                <i class="fas fa-layer-group"></i> <span>الوحدات</span>
                            </div>
                            <div class="pdf-details-tab" onclick="selectPDFDetailsTab('topics')" id="flashcards-topics-tab">
                                <i class="fas fa-tags"></i> <span>المواضيع</span>
                            </div>
                        </div>
                        
                        <!-- محتوى الصفحات -->
                        <div class="pdf-details-content active" id="flashcards-pages-content">
                            <div class="details-input-group">
                                <label for="flashcards-start-page"><i class="fas fa-arrows-alt-h"></i> <span>نطاق الصفحات</span></label>
                                <div class="page-range-inputs">
                                    <input type="number" id="flashcards-start-page" class="details-input" placeholder="الصفحة الأولى" min="1">
                                    <div class="page-range-separator">إلى</div>
                                    <input type="number" id="flashcards-end-page" class="details-input" placeholder="الصفحة الأخيرة">
                                </div>
                                <p class="hint-text">
                                    اترك الحقول فارغة لتحليل جميع الصفحات. أدخل أرقام الصفحات فقط.
                                </p>
                            </div>
                            
                            <div class="details-input-group">
                                <label for="flashcards-specific-pages"><i class="fas fa-hashtag"></i> <span>صفحات محددة</span></label>
                                <input type="text" id="flashcards-specific-pages" class="details-input" 
                                       placeholder="مثال: 1,3,5-8,10,12-15">
                                <p class="hint-text">
                                    يمكنك تحديد صفحات محددة باستخدام الفواصل والفواصل المنقوطة للنطاقات.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى الوحدات -->
                        <div class="pdf-details-content" id="flashcards-units-content">
                            <div class="details-input-group">
                                <label for="flashcards-units-list"><i class="fas fa-list-ol"></i> <span>الوحدات المطلوبة</span></label>
                                <textarea id="flashcards-units-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- الوحدة الأولى: المدخل إلى علم الفقه
- الوحدة الثانية: أحكام الطهارة
- الوحدة الثالثة: أحكام الصلاة
- الوحدة الرابعة: أحكام الصيام"></textarea>
                                <p class="hint-text">
                                    اذكر العناوين الرئيسية للوحدات أو الفصول التي تريد التركيز عليها.
                                </p>
                            </div>
                        </div>
                        
                        <!-- محتوى المواضيع -->
                        <div class="pdf-details-content" id="flashcards-topics-content">
                            <div class="details-input-group">
                                <label for="flashcards-topics-list"><i class="fas fa-tags"></i> <span>المواضيع المطلوبة</span></label>
                                <textarea id="flashcards-topics-list" class="details-input topics-textarea" 
                                          placeholder="مثال: 
- تعريف الصلاة وأركانها
- شروط الصلاة
- مكروهات الصلاة
- مبطلات الصلاة
- صلاة الجماعة
- صلاة المريض"></textarea>
                                <p class="hint-text">
                                    اذكر المواضيع أو المفاهيم المحددة التي تريد التركيز عليها في التحليل.
                                </p>
                            </div>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="num-flashcards"><i class="fas fa-layer-group"></i> <span id="num-flashcards-label">عدد البطاقات التعليمية</span></label>
                        <select id="num-flashcards" class="input-field">
                            <option value="10">10 بطاقات</option>
                            <option value="20" selected>20 بطاقة</option>
                            <option value="30">30 بطاقة</option>
                            <option value="40">40 بطاقة</option>
                            <option value="50">50 بطاقة</option>
                        </select>
                    </div>

                    <div class="input-group">
                        <label><i class="fas fa-brain"></i> <span id="flashcard-type-label">نوع البطاقات</span></label>
                        <div class="summary-type-selector">
                            <div class="summary-type active" onclick="selectFlashcardType('concepts')" id="concepts-flashcards">
                                <div class="summary-type-icon">
                                    <i class="fas fa-lightbulb"></i>
                                </div>
                                <div class="summary-type-title" id="concepts-flashcards-name">المفاهيم الأساسية</div>
                                <div class="summary-type-desc" id="concepts-flashcards-desc">بطاقات تركز على التعريفات والمفاهيم</div>
                            </div>
                            <div class="summary-type" onclick="selectFlashcardType('qa')" id="qa-flashcards">
                                <div class="summary-type-icon">
                                    <i class="fas fa-question-circle"></i>
                                </div>
                                <div class="summary-type-title" id="qa-flashcards-name">أسئلة وأجوبة</div>
                                <div class="summary-type-desc" id="qa-flashcards-desc">بطاقات بصيغة سؤال وجواب</div>
                            </div>
                        </div>
                    </div>

                    <div class="input-group">
                        <label for="flashcard-difficulty"><i class="fas fa-signal"></i> <span id="flashcard-difficulty-label">مستوى الصعوبة</span></label>
                        <select id="flashcard-difficulty" class="input-field">
                            <option value="easy">سهل (مبتدئ)</option>
                            <option value="medium" selected>متوسط (متقدم)</option>
                            <option value="hard">صعب (خبير)</option>
                            <option value="mixed">مختلط (جميع المستويات)</option>
                        </select>
                    </div>
                </div>

                <!-- زر التوليد -->
                <button class="btn btn-islamic" onclick="generateContent()" style="width: 100%; margin-top: 20px;" id="generate-btn">
                    <i class="fas fa-robot"></i> <span id="generate-text">توليد المحتوى باستخدام الذكاء الاصطناعي</span>
                </button>

                <div class="loading" id="loading">
                    <div class="loader"></div>
                    <p id="loading-text">جارٍ توليد المحتوى باستخدام الذكاء الاصطناعي...</p>
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

        <!-- Summary Section (Hidden Initially) -->
        <section id="summary-section" style="display: none;">
            <div class="output-container">
                <div class="output-header">
                    <div class="output-title">
                        <i class="fas fa-file-alt"></i>
                        <span id="summary-output-title">ملخص المحتوى</span>
                    </div>
                    <button class="copy-btn" onclick="copyToClipboard('summary-content')" id="copy-summary-btn">
                        <i class="fas fa-copy"></i>
                        <span id="copy-summary-text">نسخ الملخص</span>
                    </button>
                </div>
                <div id="summary-content" class="summary-hierarchy"></div>
            </div>

            <div class="navigation" style="margin-top: 30px;">
                <button class="btn btn-secondary" onclick="backToSetup()" id="back-summary-btn">
                    <i class="fas fa-arrow-right"></i>
                    <span id="back-summary-text">العودة للقائمة الرئيسية</span>
                </button>
                <button class="btn btn-summary" onclick="downloadSummary()" id="download-summary-btn">
                    <i class="fas fa-download"></i>
                    <span id="download-summary-text">تحميل الملخص</span>
                </button>
            </div>
        </section>

        <!-- Flashcards Section (Hidden Initially) -->
        <section id="flashcards-section-main" style="display: none;">
            <div class="flashcard-stats">
                <div class="flashcard-stat">
                    <div class="flashcard-stat-value" id="current-card">1</div>
                    <div class="flashcard-stat-label" id="total-cards-label">من إجمالي</div>
                </div>
                <div class="flashcard-stat">
                    <div class="flashcard-stat-value" id="mastered-cards">0</div>
                    <div class="flashcard-stat-label" id="mastered-label">تم إتقانها</div>
                </div>
                <div class="flashcard-stat">
                    <div class="flashcard-stat-value" id="review-cards">0</div>
                    <div class="flashcard-stat-label" id="review-label">تحتاج مراجعة</div>
                </div>
                <div class="flashcard-stat">
                    <div class="flashcard-stat-value" id="mastery-percentage">0%</div>
                    <div class="flashcard-stat-label" id="mastery-label">نسبة الإتقان</div>
                </div>
            </div>

            <div class="flashcard-container">
                <div class="flashcard" id="flashcard" onclick="flipCard()">
                    <div class="flashcard-front">
                        <div class="flashcard-icon">
                            <i class="fas fa-lightbulb"></i>
                        </div>
                        <div class="flashcard-content" id="flashcard-front-content"></div>
                        <div class="flashcard-index" id="flashcard-index">1</div>
                        <div class="flashcard-category" id="flashcard-category">مفهوم</div>
                        <div class="flashcard-actions">
                            <div class="flashcard-action-btn" onclick="markAsMastered(event)">
                                <i class="fas fa-check"></i>
                            </div>
                            <div class="flashcard-action-btn" onclick="markForReview(event)">
                                <i class="fas fa-flag"></i>
                            </div>
                        </div>
                    </div>
                    <div class="flashcard-back">
                        <div class="flashcard-icon">
                            <i class="fas fa-book"></i>
                        </div>
                        <div class="flashcard-content" id="flashcard-back-content"></div>
                        <div class="flashcard-index" id="flashcard-back-index">1</div>
                        <div class="flashcard-category" id="flashcard-back-category">مفهوم</div>
                        <div class="mastery-level" id="mastery-level">مبتدئ</div>
                        <div class="flashcard-actions">
                            <div class="flashcard-action-btn" onclick="markAsMastered(event)">
                                <i class="fas fa-check"></i>
                            </div>
                            <div class="flashcard-action-btn" onclick="markForReview(event)">
                                <i class="fas fa-flag"></i>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="flashcard-controls">
                <button class="btn btn-flashcard" onclick="previousCard()" id="prev-card-btn">
                    <i class="fas fa-arrow-right"></i>
                    <span id="prev-card-text">البطاقة السابقة</span>
                </button>
                <button class="btn btn-secondary" onclick="flipCard()" id="flip-card-btn">
                    <i class="fas fa-sync-alt"></i>
                    <span id="flip-card-text">قلب البطاقة</span>
                </button>
                <button class="btn btn-flashcard" onclick="nextCard()" id="next-card-btn">
                    <span id="next-card-text">البطاقة التالية</span>
                    <i class="fas fa-arrow-left"></i>
                </button>
            </div>

            <div class="flashcard-progress">
                <div class="progress-bar" style="flex: 1; height: 10px;">
                    <div class="progress" id="flashcard-progress" style="background: var(--flashcard-gradient);"></div>
                </div>
                <div class="progress-label" id="progress-text">التقدم: 0%</div>
            </div>

            <div class="navigation-dots" id="flashcard-dots"></div>

            <div class="navigation" style="margin-top: 30px;">
                <button class="btn btn-secondary" onclick="backToSetup()" id="back-flashcards-btn">
                    <i class="fas fa-arrow-right"></i>
                    <span id="back-flashcards-text">العودة للقائمة الرئيسية</span>
                </button>
                <button class="btn btn-flashcard" onclick="restartFlashcards()" id="restart-flashcards-btn">
                    <i class="fas fa-redo"></i>
                    <span id="restart-flashcards-text">إعادة البدء</span>
                </button>
                <button class="btn btn-primary" onclick="downloadFlashcards()" id="download-flashcards-btn">
                    <i class="fas fa-download"></i>
                    <span id="download-flashcards-text">تحميل البطاقات</span>
                </button>
            </div>
        </section>

        <!-- Final Results (for quizzes only) -->
        <div id="result-box" class="card" style="display: none;">
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

    <!-- Audio Elements -->
    <audio id="correctSound" preload="auto">
        <source src="https://media.vocaroo.com/mp3/19lcrilHKuHR" type="audio/mpeg">
    </audio>
    <audio id="wrongSound" preload="auto">
        <source src="https://www.soundjay.com/buttons/button-3.mp3" type="audio/mpeg">
    </audio>
    <audio id="flipSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-page-flip-914.mp3" type="audio/mpeg">
    </audio>

    <script>
        // ==================== المتغيرات العامة ====================
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
        let summaryFile = null;
        let flashcardsFile = null;
        let currentMethod = "manual";
        let existingQuestions = [];
        let currentBatch = 1;
        let totalQuestionsGenerated = 0;
        let currentLanguage = "ar";
        let isAPIKeyValid = false;
        let contentLanguage = "ar";
        let soundEnabled = true;
        let summaryType = "detailed";
        let flashcardType = "concepts";
        
        // أنواع الأسئلة المختارة
        let selectedQuestionTypes = {
            multipleChoice: true,
            trueFalse: true,
            fillBlank: true
        };

        // بيانات البطاقات التعليمية
        let flashcards = [];
        let currentFlashcardIndex = 0;
        let masteredFlashcards = new Set();
        let reviewFlashcards = new Set();

        // إضافة متغيرات جديدة للتحكم في الطلبات
        let lastRequestTime = 0;
        const MIN_REQUEST_INTERVAL = 3000; // 3 ثانية بين الطلبات
        let retryCount = 0;
        const MAX_RETRIES = 3;
        const REQUEST_TIMEOUT = 60000; // 60 ثانية timeout

        // تحديد نموذج Gemini المستخدم
        const GEMINI_MODEL = "gemini-2.5-flash-lite";
        const GEMINI_API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-lite:generateContent";

        // ==================== نصوص اللغة العربية ====================
        const arabicTexts = {
            "hero-title": "نظام الاختبارات الذكي التفاعلي",
            "hero-subtitle": "أنشئ اختبارات وملخصات وبطاقات تعليمية باستخدام الذكاء الاصطناعي",
            "manual-title": "إدخال يدوي",
            "manual-desc": "أدخل عنوان وموضوع الاختبار",
            "image-title": "رفع صورة",
            "image-desc": "تحميل صورة وتوليد محتوى باستخدام الذكاء الاصطناعي",
            "pdf-title": "رفع ملف PDF",
            "pdf-desc": "تحميل ملف وتوليد محتوى باستخدام الذكاء الاصطناعي",
            "summarize-title": "تلخيص المحتوى",
            "summarize-desc": "تلخيص النصوص والملفات بأسلوبين مختلفين",
            "flashcards-title": "بطاقات تعليمية",
            "flashcards-desc": "إنشاء بطاقات تعليمية تفاعلية للمراجعة",
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
            "upload-size": "الحد الأقصى لحجم الملف: 100MB",
            "remove-file-text": "إزالة الملف",
            "summary-upload-title": "انقر لرفع ملف للتلخيص",
            "summary-upload-subtitle": "أو اسحب وأفلت الملف هنا",
            "summary-upload-size": "الأنواع المسموحة: PDF, TXT, DOC, DOCX, JPG, PNG",
            "remove-summary-text": "إزالة الملف",
            "flashcards-upload-title": "انقر لرفع ملف للبطاقات التعليمية",
            "flashcards-upload-subtitle": "أو اسحب وأفلت الملف هنا",
            "flashcards-upload-size": "الأنواع المسموحة: PDF, TXT, DOC, DOCX, JPG, PNG",
            "remove-flashcards-text": "إزالة الملف",
            "num-questions-label-manual": "عدد الأسئلة المطلوبة",
            "num-questions-label-image": "عدد الأسئلة المطلوبة",
            "num-questions-label-pdf": "عدد الأسئلة المطلوبة",
            "num-flashcards-label": "عدد البطاقات التعليمية",
            "question-type-label-main": "اختر نوع الأسئلة المطلوبة",
            "multiple-choice-text": "أسئلة اختيار متعدد",
            "true-false-text": "أسئلة (صح/ خطأ)",
            "fill-blank-text": "املأ الفراغ",
            "question-type-desc": "يمكنك اختيار جميع أنواع الأسئلة أو اختيار نوع واحد فقط",
            "generate-text": "توليد المحتوى باستخدام الذكاء الاصطناعي",
            "loading-text": "جارٍ توليد المحتوى باستخدام الذكاء الاصطناعي...",
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
            "analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الملف وتوليد المحتوى",
            "image-analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الصورة وتوليد المحتوى",
            "summary-analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الملف وإنشاء التلخيص",
            "flashcards-analysis-status-text": "سيقوم الذكاء الاصطناعي بتحليل الملف وإنشاء البطاقات التعليمية",
            "language-label": "اختر لغة المحتوى",
            "arabic-language-name": "العربية",
            "arabic-language-desc": "محتوى باللغة العربية",
            "english-language-name": "English",
            "english-language-desc": "Content in English",
            "instant-review-title": "مراجعة فورية لجميع الخيارات",
            "instant-review-trigger": "انقر هنا لعرض مراجعة فورية لجميع الخيارات",
            "pdf-details-title": "تحديد تفاصيل المحتوى",
            "pdf-details-subtitle": "يمكنك تحديد نطاق محدد من الملف لتحليله. اترك الحقول فارغة لتحليل الملف بالكامل.",
            "pages-tab-text": "الصفحات",
            "units-tab-text": "الوحدات",
            "topics-tab-text": "المواضيع",
            "page-range-label": "نطاق الصفحات",
            "page-range-hint": "اترك الحقول فارغة لتحليل جميع الصفحات. أدخل أرقام الصفحات فقط.",
            "specific-pages-label": "صفحات محددة",
            "specific-pages-hint": "يمكنك تحديد صفحات محددة باستخدام الفواصل والفواصل المنقوطة للنطاقات.",
            "units-list-label": "الوحدات المطلوبة",
            "units-list-hint": "اذكر العناوين الرئيسية للوحدات أو الفصول التي تريد التركيز عليها.",
            "topics-list-label": "المواضيع المطلوبة",
            "topics-list-hint": "اذكر المواضيع أو المفاهيم المحددة التي تريد التركيز عليها في التحليل.",
            "summary-type-label": "نوع التلخيص",
            "detailed-summary-name": "تفاصيل عميقة",
            "detailed-summary-desc": "تلخيص مفصل مع جميع النقاط الرئيسية",
            "quick-summary-name": "ملخص سريع",
            "quick-summary-desc": "نقاط رئيسية مركزة وسريعة القراءة",
            "summary-length-label": "طول التلخيص",
            "summary-output-title": "ملخص المحتوى",
            "copy-summary-text": "نسخ الملخص",
            "back-summary-text": "العودة للقائمة الرئيسية",
            "download-summary-text": "تحميل الملخص",
            "flashcard-type-label": "نوع البطاقات",
            "concepts-flashcards-name": "المفاهيم الأساسية",
            "concepts-flashcards-desc": "بطاقات تركز على التعريفات والمفاهيم",
            "qa-flashcards-name": "أسئلة وأجوبة",
            "qa-flashcards-desc": "بطاقات بصيغة سؤال وجواب",
            "flashcard-difficulty-label": "مستوى الصعوبة",
            "total-cards-label": "من إجمالي",
            "mastered-label": "تم إتقانها",
            "review-label": "تحتاج مراجعة",
            "mastery-label": "نسبة الإتقان",
            "prev-card-text": "البطاقة السابقة",
            "flip-card-text": "قلب البطاقة",
            "next-card-text": "البطاقة التالية",
            "progress-text": "التقدم",
            "back-flashcards-text": "العودة للقائمة الرئيسية",
            "restart-flashcards-text": "إعادة البدء",
            "download-flashcards-text": "تحميل البطاقات"
        };

        // ==================== نصوص اللغة الإنجليزية ====================
        const englishTexts = {
            "hero-title": "Smart Interactive Quiz System",
            "hero-subtitle": "Create quizzes, summaries, and flashcards using AI",
            "manual-title": "Manual Input",
            "manual-desc": "Enter quiz title and topic",
            "image-title": "Upload Image",
            "image-desc": "Upload image and generate content using AI",
            "pdf-title": "Upload PDF File",
            "pdf-desc": "Upload file and generate content using AI",
            "summarize-title": "Content Summary",
            "summarize-desc": "Summarize texts and files in two different styles",
            "flashcards-title": "Flashcards",
            "flashcards-desc": "Create interactive flashcards for review",
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
            "upload-size": "Max file size: 100MB",
            "remove-file-text": "Remove File",
            "summary-upload-title": "Click to Upload File for Summary",
            "summary-upload-subtitle": "or drag and drop file here",
            "summary-upload-size": "Allowed types: PDF, TXT, DOC, DOCX, JPG, PNG",
            "remove-summary-text": "Remove File",
            "flashcards-upload-title": "Click to Upload File for Flashcards",
            "flashcards-upload-subtitle": "or drag and drop file here",
            "flashcards-upload-size": "Allowed types: PDF, TXT, DOC, DOCX, JPG, PNG",
            "remove-flashcards-text": "Remove File",
            "num-questions-label-manual": "Number of Questions",
            "num-questions-label-image": "Number of Questions",
            "num-questions-label-pdf": "Number of Questions",
            "num-flashcards-label": "Number of Flashcards",
            "question-type-label-main": "Select Question Types",
            "multiple-choice-text": "Multiple Choice Questions",
            "true-false-text": "True/False Questions",
            "fill-blank-text": "Fill in the Blank",
            "question-type-desc": "You can select all question types or only one type",
            "generate-text": "Generate Content with AI",
            "loading-text": "Generating content using AI...",
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
            "analysis-status-text": "AI will analyze the file and generate content",
            "image-analysis-status-text": "AI will analyze the image and generate content",
            "summary-analysis-status-text": "AI will analyze the file and create summary",
            "flashcards-analysis-status-text": "AI will analyze the file and create flashcards",
            "language-label": "Choose Content Language",
            "arabic-language-name": "Arabic",
            "arabic-language-desc": "Content in Arabic",
            "english-language-name": "English",
            "english-language-desc": "Content in English",
            "instant-review-title": "Instant Review for All Options",
            "instant-review-trigger": "Click here to show instant review for all options",
            "pdf-details-title": "Specify Content Details",
            "pdf-details-subtitle": "You can specify a specific range from the file to analyze. Leave fields empty to analyze the entire file.",
            "pages-tab-text": "Pages",
            "units-tab-text": "Units",
            "topics-tab-text": "Topics",
            "page-range-label": "Page Range",
            "page-range-hint": "Leave fields empty to analyze all pages. Enter page numbers only.",
            "specific-pages-label": "Specific Pages",
            "specific-pages-hint": "You can specify specific pages using commas and hyphens for ranges.",
            "units-list-label": "Required Units",
            "units-list-hint": "List the main headings of units or chapters you want to focus on.",
            "topics-list-label": "Required Topics",
            "topics-list-hint": "List the specific topics or concepts you want to focus on in the analysis.",
            "summary-type-label": "Summary Type",
            "detailed-summary-name": "Details and In-depth",
            "detailed-summary-desc": "Detailed summary with all key points",
            "quick-summary-name": "Quick and Concise",
            "quick-summary-desc": "Focused key points for quick reading",
            "summary-length-label": "Summary Length",
            "summary-output-title": "Content Summary",
            "copy-summary-text": "Copy Summary",
            "back-summary-text": "Back to Main Menu",
            "download-summary-text": "Download Summary",
            "flashcard-type-label": "Flashcard Type",
            "concepts-flashcards-name": "Basic Concepts",
            "concepts-flashcards-desc": "Flashcards focusing on definitions and concepts",
            "qa-flashcards-name": "Q&A Format",
            "qa-flashcards-desc": "Flashcards in question and answer format",
            "flashcard-difficulty-label": "Difficulty Level",
            "total-cards-label": "of Total",
            "mastered-label": "Mastered",
            "review-label": "Need Review",
            "mastery-label": "Mastery Percentage",
            "prev-card-text": "Previous Card",
            "flip-card-text": "Flip Card",
            "next-card-text": "Next Card",
            "progress-text": "Progress",
            "back-flashcards-text": "Back to Main Menu",
            "restart-flashcards-text": "Restart",
            "download-flashcards-text": "Download Flashcards"
        };

        // ==================== دوال تأخير وإعادة المحاولة ====================
        function delayBetweenRequests() {
            const now = Date.now();
            const timeSinceLastRequest = now - lastRequestTime;
            
            if (timeSinceLastRequest < MIN_REQUEST_INTERVAL) {
                const delayTime = MIN_REQUEST_INTERVAL - timeSinceLastRequest;
                return new Promise(resolve => setTimeout(resolve, delayTime));
            }
            
            lastRequestTime = now;
            return Promise.resolve();
        }

        async function makeAPIRequest(url, options, retryNumber = 0) {
            await delayBetweenRequests();
            
            try {
                // إضافة timeout للطلب
                const controller = new AbortController();
                const timeoutId = setTimeout(() => controller.abort(), REQUEST_TIMEOUT);
                
                const response = await fetch(url, {
                    ...options,
                    signal: controller.signal
                });
                
                clearTimeout(timeoutId);
                
                if (response.status === 429) {
                    // Too Many Requests - انتظر ثم حاول مرة أخرى
                    const retryAfter = response.headers.get('Retry-After') || 5;
                    const waitTime = parseInt(retryAfter) * 1000;
                    
                    if (retryNumber < MAX_RETRIES) {
                        document.getElementById('loading-details').textContent = 
                            currentLanguage === 'ar' ?
                            `محاولة ${retryNumber + 1}/${MAX_RETRIES} - الانتظار ${retryAfter} ثانية...` :
                            `Retry ${retryNumber + 1}/${MAX_RETRIES} - Waiting ${retryAfter} seconds...`;
                        
                        await new Promise(resolve => setTimeout(resolve, waitTime));
                        return makeAPIRequest(url, options, retryNumber + 1);
                    } else {
                        throw new Error(currentLanguage === 'ar' ?
                            'تم تجاوز الحد الأقصى للطلبات. حاول مرة أخرى بعد قليل.' :
                            'Rate limit exceeded. Please try again later.');
                    }
                }
                
                if (!response.ok) {
                    const errorData = await response.json().catch(() => ({}));
                    throw new Error(`HTTP ${response.status}: ${errorData.error?.message || response.statusText}`);
                }
                
                return await response.json();
            } catch (error) {
                if (error.name === 'AbortError') {
                    throw new Error(currentLanguage === 'ar' ?
                        'انتهت مهلة الطلب. تحقق من اتصالك بالإنترنت وحاول مرة أخرى.' :
                        'Request timeout. Check your internet connection and try again.');
                }
                
                if (retryNumber < MAX_RETRIES) {
                    const waitTime = 2000 * Math.pow(2, retryNumber); // Exponential backoff
                    document.getElementById('loading-details').textContent = 
                        currentLanguage === 'ar' ?
                        `محاولة ${retryNumber + 1}/${MAX_RETRIES} - الانتظار ${waitTime/1000} ثانية...` :
                        `Retry ${retryNumber + 1}/${MAX_RETRIES} - Waiting ${waitTime/1000} seconds...`;
                    
                    await new Promise(resolve => setTimeout(resolve, waitTime));
                    return makeAPIRequest(url, options, retryNumber + 1);
                } else {
                    throw error;
                }
            }
        }

        // ==================== وظائف اللغة ====================
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
            
            // إذا كان هناك محتوى معروض، إعادة تحميله
            if (document.getElementById('quiz-section').style.display !== 'none') {
                loadQuiz();
            } else if (document.getElementById('summary-section').style.display !== 'none') {
                // إعادة تحميل الملخص إذا كان معروضاً
                const summaryContent = document.getElementById('summary-content').innerHTML;
                document.getElementById('summary-content').innerHTML = summaryContent; // إعادة التنسيق
            } else if (document.getElementById('flashcards-section-main').style.display !== 'none') {
                loadFlashcard(currentFlashcardIndex);
            }
        }

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
                document.getElementById('units-list').placeholder = `Example:
- Unit 1: Introduction to Islamic Jurisprudence
- Unit 2: Rules of Purification
- Unit 3: Rules of Prayer
- Unit 4: Rules of Fasting`;
                document.getElementById('topics-list').placeholder = `Example:
- Definition and pillars of prayer
- Conditions of prayer
- Disliked acts in prayer
- Invalidators of prayer
- Congregational prayer
- Prayer for the sick`;
                document.getElementById('specific-pages').placeholder = "Example: 1,3,5-8,10,12-15";
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
                document.getElementById('units-list').placeholder = `مثال: 
- الوحدة الأولى: المدخل إلى علم الفقه
- الوحدة الثانية: أحكام الطهارة
- الوحدة الثالثة: أحكام الصلاة
- الوحدة الرابعة: أحكام الصيام`;
                document.getElementById('topics-list').placeholder = `مثال: 
- تعريف الصلاة وأركانها
- شروط الصلاة
- مكروهات الصلاة
- مبطلات الصلاة
- صلاة الجماعة
- صلاة المريض`;
                document.getElementById('specific-pages').placeholder = "مثال: 1,3,5-8,10,12-15";
            }
        }

        function updateDropdownOptions(lang) {
            const options = lang === 'en' ? {
                questions: [
                    {value: "5", text: "5 questions"},
                    {value: "10", text: "10 questions"},
                    {value: "15", text: "15 questions"},
                    {value: "20", text: "20 questions"},
                    {value: "25", text: "25 questions"},
                    {value: "30", text: "30 questions"},
                    {value: "35", text: "35 questions"},
                    {value: "40", text: "40 questions"}
                ],
                flashcards: [
                    {value: "10", text: "10 flashcards"},
                    {value: "20", text: "20 flashcards"},
                    {value: "30", text: "30 flashcards"},
                    {value: "40", text: "40 flashcards"},
                    {value: "50", text: "50 flashcards"}
                ],
                summaryLength: [
                    {value: "short", text: "Brief (key points)"},
                    {value: "medium", text: "Medium (balanced)"},
                    {value: "long", text: "Detailed (comprehensive)"}
                ],
                difficulty: [
                    {value: "easy", text: "Easy (beginner)"},
                    {value: "medium", text: "Medium (advanced)"},
                    {value: "hard", text: "Hard (expert)"},
                    {value: "mixed", text: "Mixed (all levels)"}
                ]
            } : {
                questions: [
                    {value: "5", text: "5 أسئلة"},
                    {value: "10", text: "10 أسئلة"},
                    {value: "15", text: "15 أسئلة"},
                    {value: "20", text: "20 أسئلة"},
                    {value: "25", text: "25 أسئلة"},
                    {value: "30", text: "30 أسئلة"},
                    {value: "35", text: "35 أسئلة"},
                    {value: "40", text: "40 أسئلة"}
                ],
                flashcards: [
                    {value: "10", text: "10 بطاقات"},
                    {value: "20", text: "20 بطاقة"},
                    {value: "30", text: "30 بطاقة"},
                    {value: "40", text: "40 بطاقة"},
                    {value: "50", text: "50 بطاقة"}
                ],
                summaryLength: [
                    {value: "short", text: "مختصر (نقاط رئيسية)"},
                    {value: "medium", text: "متوسط (متوازن)"},
                    {value: "long", text: "مفصل (شامل)"}
                ],
                difficulty: [
                    {value: "easy", text: "سهل (مبتدئ)"},
                    {value: "medium", text: "متوسط (متقدم)"},
                    {value: "hard", text: "صعب (خبير)"},
                    {value: "mixed", text: "مختلط (جميع المستويات)"}
                ]
            };

            // تحديث قوائم الأسئلة
            ['manual', 'image', 'pdf'].forEach(type => {
                const element = document.getElementById(`num-questions-${type}`);
                if (element) {
                    element.innerHTML = options.questions.map(opt => 
                        `<option value="${opt.value}" ${opt.value === "10" ? "selected" : ""}>${opt.text}</option>`
                    ).join('');
                }
            });

            // تحديث قائمة البطاقات التعليمية
            const flashcardsElement = document.getElementById('num-flashcards');
            if (flashcardsElement) {
                flashcardsElement.innerHTML = options.flashcards.map(opt => 
                    `<option value="${opt.value}" ${opt.value === "20" ? "selected" : ""}>${opt.text}</option>`
                ).join('');
            }

            // تحديث قائمة طول التلخيص
            const summaryLengthElement = document.getElementById('summary-length');
            if (summaryLengthElement) {
                summaryLengthElement.innerHTML = options.summaryLength.map(opt => 
                    `<option value="${opt.value}" ${opt.value === "medium" ? "selected" : ""}>${opt.text}</option>`
                ).join('');
            }

            // تحديث قائمة مستوى الصعوبة
            const difficultyElement = document.getElementById('flashcard-difficulty');
            if (difficultyElement) {
                difficultyElement.innerHTML = options.difficulty.map(opt => 
                    `<option value="${opt.value}" ${opt.value === "medium" ? "selected" : ""}>${opt.text}</option>`
                ).join('');
            }
        }

        // ==================== وظائف الطريقة المختارة ====================
        function selectMethod(method) {
            currentMethod = method;
            
            // تحديث التبويبات
            document.getElementById('manual-tab').classList.remove('active');
            document.getElementById('image-tab').classList.remove('active');
            document.getElementById('pdf-tab').classList.remove('active');
            document.getElementById('summarize-tab').classList.remove('active');
            document.getElementById('flashcards-tab').classList.remove('active');
            document.getElementById(`${method}-tab`).classList.add('active');
            
            // إظهار/إخفاء الأقسام
            document.getElementById('manual-section').style.display = method === 'manual' ? 'block' : 'none';
            document.getElementById('image-section').style.display = method === 'image' ? 'block' : 'none';
            document.getElementById('pdf-section').style.display = method === 'pdf' ? 'block' : 'none';
            document.getElementById('summarize-section').style.display = method === 'summarize' ? 'block' : 'none';
            document.getElementById('flashcards-section').style.display = method === 'flashcards' ? 'block' : 'none';
            
            // إظهار/إخفاء خيارات إضافية
            if (method === 'image' || method === 'pdf') {
                const quizOptionsId = `${method}-quiz-options`;
                document.getElementById(quizOptionsId).style.display = 'block';
            }
            
            // إظهار أو إخفاء قسم تفاصيل PDF
            const detailsSectionId = `${method}-details-section`;
            const detailsSection = document.getElementById(detailsSectionId);
            if (detailsSection && (method === 'pdf' || method === 'summarize' || method === 'flashcards')) {
                if ((method === 'pdf' && pdfFile) || (method === 'summarize' && summaryFile) || (method === 'flashcards' && flashcardsFile)) {
                    detailsSection.classList.add('active');
                }
            }
            
            // تحديث نص زر التوليد
            const generateBtn = document.getElementById('generate-btn');
            const generateText = document.getElementById('generate-text');
            if (method === 'summarize') {
                generateText.textContent = currentLanguage === 'ar' ? 'توليد الملخص باستخدام الذكاء الاصطناعي' : 'Generate Summary with AI';
            } else if (method === 'flashcards') {
                generateText.textContent = currentLanguage === 'ar' ? 'توليد البطاقات التعليمية باستخدام الذكاء الاصطناعي' : 'Generate Flashcards with AI';
            } else if (method === 'manual') {
                generateText.textContent = currentLanguage === 'ar' ? 'توليد اختبار باستخدام الذكاء الاصطناعي' : 'Generate Quiz with AI';
            } else {
                generateText.textContent = currentLanguage === 'ar' ? 'توليد المحتوى باستخدام الذكاء الاصطناعي' : 'Generate Content with AI';
            }
        }

        function selectContentLanguage(lang) {
            contentLanguage = lang;
            
            document.getElementById('arabic-language').classList.remove('active');
            document.getElementById('english-language').classList.remove('active');
            
            document.getElementById(`${lang}-language`).classList.add('active');
        }

        function selectPDFDetailsTab(tab) {
            // إزالة النشاط من جميع التبويبات
            document.querySelectorAll('.pdf-details-tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.pdf-details-content').forEach(c => c.classList.remove('active'));
            
            // إضافة النشاط للتبويب المحدد
            const tabId = currentMethod === 'summarize' ? `summary-${tab}-tab` : 
                         currentMethod === 'flashcards' ? `flashcards-${tab}-tab` : `${tab}-tab`;
            const contentId = currentMethod === 'summarize' ? `summary-${tab}-content` : 
                            currentMethod === 'flashcards' ? `flashcards-${tab}-content` : `${tab}-content`;
            
            document.getElementById(tabId).classList.add('active');
            document.getElementById(contentId).classList.add('active');
        }

        function selectSummaryType(type) {
            summaryType = type;
            
            document.getElementById('detailed-summary').classList.remove('active');
            document.getElementById('quick-summary').classList.remove('active');
            
            document.getElementById(`${type}-summary`).classList.add('active');
        }

        function selectFlashcardType(type) {
            flashcardType = type;
            
            document.getElementById('concepts-flashcards').classList.remove('active');
            document.getElementById('qa-flashcards').classList.remove('active');
            
            document.getElementById(`${type}-flashcards`).classList.add('active');
        }

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

        // ==================== وظائف الواجهة ====================
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
            
            // التحقق من تفضيل الصوت
            const soundPref = localStorage.getItem('soundEnabled');
            if (soundPref !== null) {
                soundEnabled = soundPref === 'true';
                updateSoundButton();
            }
        }

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

        function toggleSound() {
            soundEnabled = !soundEnabled;
            localStorage.setItem('soundEnabled', soundEnabled);
            updateSoundButton();
            
            // تشغيل صوت تجريبي عند تشغيل الصوت
            if (soundEnabled) {
                playSound('correct');
            }
        }

        function updateSoundButton() {
            const soundBtn = document.getElementById('soundBtn');
            const icon = soundBtn.querySelector('i');
            const wave = soundBtn.querySelector('.sound-wave');
            
            if (soundEnabled) {
                soundBtn.classList.remove('muted');
                icon.classList.remove('fa-volume-mute');
                icon.classList.add('fa-volume-up');
                wave.style.display = 'inline-block';
            } else {
                soundBtn.classList.add('muted');
                icon.classList.remove('fa-volume-up');
                icon.classList.add('fa-volume-mute');
                wave.style.display = 'inline-block';
            }
        }

        function playSound(type) {
            if (!soundEnabled) return;
            
            const audio = document.getElementById(`${type}Sound`);
            if (audio) {
                audio.currentTime = 0;
                audio.play().catch(e => console.log("Error playing sound:", e));
            }
        }

        // ==================== وظائف API ====================
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

        // ==================== وظائف رفع الملفات ====================
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
                'تم رفع الصورة بنجاح!' : 
                'Image uploaded successfully!');
        }

        function removeImage() {
            imageFile = null;
            document.getElementById('image-file').value = "";
            document.getElementById('image-preview').classList.remove('active');
            document.getElementById('image-preview-container').style.display = 'none';
        }

        async function handlePDFUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            if (file.type !== 'application/pdf') {
                showError(currentLanguage === 'ar' ? 'الرجاء رفع ملف PDF فقط' : 'Please upload PDF files only');
                return;
            }

            if (file.size > 100 * 1024 * 1024) {
                showError(currentLanguage === 'ar' ? 'حجم الملف كبير جداً. الحد الأقصى 100MB' : 'File too large. Maximum size: 100MB');
                return;
            }

            pdfFile = file;

            document.getElementById('pdf-filename').textContent = file.name;
            document.getElementById('pdf-filesize').textContent = currentLanguage === 'ar' ? 
                `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB` : 
                `Size: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            
            document.getElementById('pdf-preview').classList.add('active');
            document.getElementById('pdf-details-section').classList.add('active');
            
            showSuccessMessage(currentLanguage === 'ar' ? 
                'تم رفع الملف بنجاح!' : 
                'File uploaded successfully!');
        }

        function removePDF() {
            pdfFile = null;
            document.getElementById('pdf-file').value = "";
            document.getElementById('pdf-preview').classList.remove('active');
            document.getElementById('pdf-details-section').classList.remove('active');
            existingQuestions = [];
            currentBatch = 1;
            totalQuestionsGenerated = 0;
        }

        async function handleSummaryUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const validTypes = ['application/pdf', 'text/plain', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document', 'image/jpeg', 'image/jpg', 'image/png'];
            if (!validTypes.includes(file.type)) {
                showError(currentLanguage === 'ar' ? 'الرجاء رفع ملف صالح (PDF, TXT, DOC, DOCX, JPG, PNG)' : 'Please upload valid file (PDF, TXT, DOC, DOCX, JPG, PNG)');
                return;
            }

            if (file.size > 100 * 1024 * 1024) {
                showError(currentLanguage === 'ar' ? 'حجم الملف كبير جداً. الحد الأقصى 100MB' : 'File too large. Maximum size: 100MB');
                return;
            }

            summaryFile = file;

            document.getElementById('summary-filename').textContent = file.name;
            document.getElementById('summary-filesize').textContent = currentLanguage === 'ar' ? 
                `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB` : 
                `Size: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            
            document.getElementById('summary-preview').classList.add('active');
            document.getElementById('summary-details-section').classList.add('active');
            
            showSuccessMessage(currentLanguage === 'ar' ? 
                'تم رفع الملف بنجاح!' : 
                'File uploaded successfully!');
        }

        function removeSummaryFile() {
            summaryFile = null;
            document.getElementById('summary-file').value = "";
            document.getElementById('summary-preview').classList.remove('active');
            document.getElementById('summary-details-section').classList.remove('active');
        }

        async function handleFlashcardsUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const validTypes = ['application/pdf', 'text/plain', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document', 'image/jpeg', 'image/jpg', 'image/png'];
            if (!validTypes.includes(file.type)) {
                showError(currentLanguage === 'ar' ? 'الرجاء رفع ملف صالح (PDF, TXT, DOC, DOCX, JPG, PNG)' : 'Please upload valid file (PDF, TXT, DOC, DOCX, JPG, PNG)');
                return;
            }

            if (file.size > 100 * 1024 * 1024) {
                showError(currentLanguage === 'ar' ? 'حجم الملف كبير جداً. الحد الأقصى 100MB' : 'File too large. Maximum size: 100MB');
                return;
            }

            flashcardsFile = file;

            document.getElementById('flashcards-filename').textContent = file.name;
            document.getElementById('flashcards-filesize').textContent = currentLanguage === 'ar' ? 
                `الحجم: ${(file.size / 1024 / 1024).toFixed(2)} MB` : 
                `Size: ${(file.size / 1024 / 1024).toFixed(2)} MB`;
            
            document.getElementById('flashcards-preview').classList.add('active');
            document.getElementById('flashcards-details-section').classList.add('active');
            
            showSuccessMessage(currentLanguage === 'ar' ? 
                'تم رفع الملف بنجاح!' : 
                'File uploaded successfully!');
        }

        function removeFlashcardsFile() {
            flashcardsFile = null;
            document.getElementById('flashcards-file').value = "";
            document.getElementById('flashcards-preview').classList.remove('active');
            document.getElementById('flashcards-details-section').classList.remove('active');
        }

        // ==================== وظائف تفاصيل PDF ====================
        function getPDFDetails() {
            const prefix = currentMethod === 'summarize' ? 'summary-' : 
                          currentMethod === 'flashcards' ? 'flashcards-' : '';
            
            return {
                pages: {
                    startPage: document.getElementById(`${prefix}start-page`)?.value.trim() || '',
                    endPage: document.getElementById(`${prefix}end-page`)?.value.trim() || '',
                    specificPages: document.getElementById(`${prefix}specific-pages`)?.value.trim() || ''
                },
                units: document.getElementById(`${prefix}units-list`)?.value.trim() || '',
                topics: document.getElementById(`${prefix}topics-list`)?.value.trim() || ''
            };
        }

        function validatePDFDetails(details) {
            const errors = [];
            
            if (details.pages.startPage && details.pages.endPage) {
                const start = parseInt(details.pages.startPage);
                const end = parseInt(details.pages.endPage);
                
                if (isNaN(start) || isNaN(end)) {
                    errors.push(currentLanguage === 'ar' ? 
                        'أرقام الصفحات غير صالحة' : 
                        'Invalid page numbers');
                } else if (start > end) {
                    errors.push(currentLanguage === 'ar' ? 
                        'الصفحة الأولى يجب أن تكون أقل من الصفحة الأخيرة' : 
                        'Start page must be less than end page');
                } else if (start < 1) {
                    errors.push(currentLanguage === 'ar' ? 
                        'الصفحة الأولى يجب أن تكون على الأقل 1' : 
                        'Start page must be at least 1');
                }
            }
            
            if (details.pages.specificPages) {
                const pagesRegex = /^[0-9\-, ]+$/;
                if (!pagesRegex.test(details.pages.specificPages)) {
                    errors.push(currentLanguage === 'ar' ? 
                        'تنسيق الصفحات المحددة غير صالح' : 
                        'Invalid specific pages format');
                }
            }
            
            return errors;
        }

        function generatePDFDetailsInstructions(details, languageCode) {
            let instructions = '';
            
            if (languageCode === 'en') {
                instructions = "IMPORTANT: You MUST focus ONLY on the following specified content. Ignore all other content.\n\n";
                
                // إضافة تعليمات الصفحات
                if (details.pages.startPage || details.pages.endPage || details.pages.specificPages) {
                    instructions += "PAGE RANGE INSTRUCTIONS:\n";
                    instructions += "You are REQUIRED to analyze ONLY these pages:\n";
                    
                    if (details.pages.startPage && details.pages.endPage) {
                        instructions += `- STRICTLY analyze ONLY pages ${details.pages.startPage} to ${details.pages.endPage}\n`;
                    } else if (details.pages.startPage) {
                        instructions += `- Start from page ${details.pages.startPage} and include all pages after it\n`;
                    } else if (details.pages.endPage) {
                        instructions += `- Analyze up to page ${details.pages.endPage} only\n`;
                    }
                    
                    if (details.pages.specificPages) {
                        instructions += `- Specifically analyze ONLY these exact pages: ${details.pages.specificPages}\n`;
                    }
                    
                    instructions += "- DO NOT analyze any content outside these specified pages\n";
                    instructions += "- IGNORE all text, images, and information from other pages\n\n";
                }
                
                // إضافة تعليمات الوحدات
                if (details.units) {
                    instructions += "SPECIFIC UNITS/CHAPTERS INSTRUCTIONS:\n";
                    instructions += "You MUST focus ONLY on these specific units/chapters:\n";
                    
                    const units = details.units.split('\n').filter(line => line.trim());
                    units.forEach(unit => {
                        instructions += `- ${unit.trim()}\n`;
                    });
                    
                    instructions += "- If a unit/chapter is NOT listed above, DO NOT include any content from it\n";
                    instructions += "- Extract content ONLY from the specified units/chapters\n";
                    instructions += "- Ignore all other units and chapters\n\n";
                }
                
                // إضافة تعليمات المواضيع
                if (details.topics) {
                    instructions += "SPECIFIC TOPICS/CONCEPTS INSTRUCTIONS:\n";
                    instructions += "You MUST focus ONLY on these specific topics:\n";
                    
                    const topics = details.topics.split('\n').filter(line => line.trim());
                    topics.forEach(topic => {
                        instructions += `- ${topic.trim()}\n`;
                    });
                    
                    instructions += "- DO NOT create content about any topics not listed above\n";
                    instructions += "- Each item MUST relate directly to at least one of these topics\n";
                    instructions += "- Filter out all unrelated concepts and information\n\n";
                }
                
                instructions += "CRITICAL REQUIREMENTS:\n";
                instructions += "1. Generate content ONLY from the specified content above\n";
                instructions += "2. If no content is specified, analyze the ENTIRE document\n";
                instructions += "3. DO NOT include content based on content outside the specified range\n";
                instructions += "4. If you cannot find the specified content, state that clearly\n";
                instructions += "5. Prioritize accuracy over quantity when content is limited\n";
                
            } else {
                instructions = "هام جداً: يجب أن تركز فقط على المحتوى المحدد التالي. تجاهل جميع المحتويات الأخرى.\n\n";
                
                // إضافة تعليمات الصفحات
                if (details.pages.startPage || details.pages.endPage || details.pages.specificPages) {
                    instructions += "تعليمات نطاق الصفحات:\n";
                    instructions += "يجب عليك تحليل هذه الصفحات فقط:\n";
                    
                    if (details.pages.startPage && details.pages.endPage) {
                        instructions += `- حلل صفحات ${details.pages.startPage} إلى ${details.pages.endPage} فقط\n`;
                    } else if (details.pages.startPage) {
                        instructions += `- ابدأ من الصفحة ${details.pages.startPage} وتابع جميع الصفحات بعدها\n`;
                    } else if (details.pages.endPage) {
                        instructions += `- حلل حتى الصفحة ${details.pages.endPage} فقط\n`;
                    }
                    
                    if (details.pages.specificPages) {
                        instructions += `- ركز تحديداً على هذه الصفحات بالضبط: ${details.pages.specificPages}\n`;
                    }
                    
                    instructions += "- لا تحلل أي محتوى خارج هذه الصفحات المحددة\n";
                    instructions += "- تجاهل كل النصوص والصور والمعلومات من الصفحات الأخرى\n\n";
                }
                
                // إضافة تعليمات الوحدات
                if (details.units) {
                    instructions += "تعليمات الوحدات/الفصول المحددة:\n";
                    instructions += "يجب أن تركز فقط على هذه الوحدات/الفصول المحددة:\n";
                    
                    const units = details.units.split('\n').filter(line => line.trim());
                    units.forEach(unit => {
                        instructions += `- ${unit.trim()}\n`;
                    });
                    
                    instructions += "- إذا لم تكن الوحدة/الفصل مدرجة أعلاه، لا تدرج أي محتوى منها\n";
                    instructions += "- استخرج المحتوى فقط من الوحدات/الفصول المحددة\n";
                    instructions += "- تجاهل جميع الوحدات والفصول الأخرى\n\n";
                }
                
                // إضافة تعليمات المواضيع
                if (details.topics) {
                    instructions += "تعليمات المواضيع/المفاهيم المحددة:\n";
                    instructions += "يجب أن تركز فقط على هذه المواضيع المحددة:\n";
                    
                    const topics = details.topics.split('\n').filter(line => line.trim());
                    topics.forEach(topic => {
                        instructions += `- ${topic.trim()}\n`;
                    });
                    
                    instructions += "- لا تنشئ محتوى عن أي مواضيع غير مدرجة أعلاه\n";
                    instructions += "- يجب أن يرتبط كل عنصر مباشرة بواحد على الأقل من هذه المواضيع\n";
                    instructions += "- استبعد جميع المفاهيم والمعلومات غير المرتبطة\n\n";
                }
                
                instructions += "متطلبات حاسمة:\n";
                instructions += "1. أنشئ محتوى فقط من المحتوى المحدد أعلاه\n";
                instructions += "2. إذا لم يتم تحديد محتوى، حلل المستند بالكامل\n";
                instructions += "3. لا تدرج محتوى مبنياً على محتوى خارج النطاق المحدد\n";
                instructions += "4. إذا لم تجد المحتوى المحدد، صرح بذلك بوضوح\n";
                instructions += "5. ركز على الدقة بدلاً من الكمية عندما يكون المحتوى محدوداً\n";
            }
            
            return instructions;
        }

        // ==================== وظائف الرسائل ====================
        function showError(message) {
            const errorDiv = document.getElementById('error-message');
            errorDiv.innerHTML = `<i class="fas fa-exclamation-triangle"></i> ${message}`;
            errorDiv.style.display = 'block';
            
            setTimeout(() => {
                errorDiv.style.display = 'none';
            }, 5000);
        }

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

        // ==================== وظائف المحتوى ====================
        async function generateContent() {
            if (!isAPIKeyValid) {
                showError(currentLanguage === 'ar' ? 
                    'الرجاء التحقق من صحة مفتاح API أولاً' : 
                    'Please verify your API key first');
                return;
            }

            // إعادة تعيين عدد المحاولات
            retryCount = 0;
            lastRequestTime = 0;

            if (currentMethod === 'manual' || currentMethod === 'image' || currentMethod === 'pdf') {
                await generateQuiz();
            } else if (currentMethod === 'summarize') {
                await generateSummary();
            } else if (currentMethod === 'flashcards') {
                await generateFlashcards();
            }
        }

        async function generateQuiz() {
            // التحقق من وجود الملفات المطلوبة
            if ((currentMethod === 'image' && !imageFile) || 
                (currentMethod === 'pdf' && !pdfFile)) {
                showError(currentLanguage === 'ar' ? 
                    'الرجاء رفع الملف المطلوب أولاً' : 
                    'Please upload the required file first');
                return;
            }

            if (currentMethod === 'manual') {
                const quizTitleInput = document.getElementById('quiz-title').value.trim();
                const quizTopicInput = document.getElementById('quiz-topic').value.trim();

                if (!quizTitleInput) {
                    showError(currentLanguage === 'ar' ? 'الرجاء إدخال عنوان للاختبار' : 'Please enter quiz title');
                    return;
                }

                if (!quizTopicInput) {
                    showError(currentLanguage === 'ar' ? 'الرجاء إدخال تفاصيل الموضوع' : 'Please enter topic details');
                    return;
                }
            }

            // الحصول على عدد الأسئلة المطلوب
            const numQuestions = parseInt(document.getElementById(`num-questions-${currentMethod}`).value);
            
            // تحسين الأداء: تقليل حجم الاستجابة للأسئلة الكثيرة
            const maxTokens = numQuestions > 20 ? 6144 : numQuestions > 15 ? 4096 : 2048;
            
            // إعداد واجهة التحميل
            document.getElementById('loading').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
            document.getElementById('loading-details').textContent = currentLanguage === 'ar' ?
                `جارٍ توليد ${numQuestions} سؤالاً...` :
                `Generating ${numQuestions} questions...`;

            try {
                let prompt = '';
                let requestBody = {};
                
                if (currentMethod === 'manual') {
                    const quizTitle = document.getElementById('quiz-title').value.trim();
                    const quizTopic = document.getElementById('quiz-topic').value.trim();
                    
                    prompt = generateQuizPrompt(quizTitle, quizTopic, numQuestions, contentLanguage);
                    requestBody = {
                        contents: [{
                            parts: [{ text: prompt }]
                        }],
                        generationConfig: {
                            temperature: 0.7,
                            topK: 40,
                            topP: 0.95,
                            maxOutputTokens: maxTokens,
                        }
                    };
                } else if (currentMethod === 'image') {
                    const imageBase64 = await convertFileToBase64(imageFile);
                    prompt = generateImageQuizPrompt(numQuestions, contentLanguage);
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
                            maxOutputTokens: maxTokens,
                        }
                    };
                } else if (currentMethod === 'pdf') {
                    const pdfBase64 = await convertFileToBase64(pdfFile);
                    const pdfDetails = getPDFDetails();
                    const validationErrors = validatePDFDetails(pdfDetails);
                    
                    if (validationErrors.length > 0) {
                        showError(validationErrors.join(', '));
                        return;
                    }
                    
                    prompt = generatePDFQuizPrompt(numQuestions, contentLanguage, pdfDetails);
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
                            maxOutputTokens: maxTokens,
                        }
                    };
                }

                // استخدام دالة makeAPIRequest الجديدة
                const data = await makeAPIRequest(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(requestBody)
                });

                const responseText = data.candidates[0].content.parts[0].text;
                
                // تحسين استخراج JSON من الاستجابة
                const jsonMatch = extractJSONFromText(responseText);
                if (!jsonMatch) {
                    console.error("Full response:", responseText);
                    throw new Error(currentLanguage === 'ar' ? 
                        'تعذر استخراج البيانات من استجابة الذكاء الاصطناعي' : 
                        'Could not extract data from AI response');
                }

                let quizData;
                try {
                    quizData = JSON.parse(jsonMatch);
                } catch (error) {
                    console.error("JSON parsing error:", error);
                    console.error("JSON string:", jsonMatch);
                    
                    // محاولة إصلاح JSON
                    const cleanedJson = jsonMatch
                        .replace(/'/g, '"') // استبدال علامات التنصيص المفردة
                        .replace(/(\w+):/g, '"$1":') // إضافة علامات تنصيص للمفاتيح
                        .replace(/,\s*}/g, '}') // إزالة الفواصل الزائدة قبل الأقواس
                        .replace(/,\s*]/g, ']') // إزالة الفواصل الزائدة قبل الأقواس المعقوفة
                        .replace(/\n/g, ' ') // إزالة الأسطر الجديدة
                        .replace(/\s+/g, ' '); // إزالة المسافات الزائدة
                    
                    try {
                        quizData = JSON.parse(cleanedJson);
                    } catch (e) {
                        console.error("Cleaned JSON parsing error:", e);
                        throw new Error(currentLanguage === 'ar' ? 
                            'خطأ في معالجة البيانات. حاول تقليل عدد الأسئلة.' : 
                            'Data processing error. Try reducing the number of questions.');
                    }
                }
                
                if (!quizData.questions || !Array.isArray(quizData.questions)) {
                    throw new Error(currentLanguage === 'ar' ? 
                        'لم يتم العثور على أسئلة في الاستجابة' : 
                        'No questions found in response');
                }

                // معالجة الأسئلة
                questions = quizData.questions.map((q, index) => ({
                    ...q,
                    id: q.id || index + 1,
                    type: q.type || "multiple_choice"
                }));
                
                existingQuestions = questions;
                totalQuestionsGenerated = questions.length;
                userAnswers = Array(questions.length).fill(null);
                answerLocked = Array(questions.length).fill(false);
                shuffledQuestions = questions.map(q => shuffleOptions(q));
                timeLeft = Math.max(questions.length * 60, 600);
                currentQuestionIndex = 0;
                markedQuestions = [];

                // إعداد العنوان
                currentQuizTitle = currentMethod === 'manual' ? 
                    document.getElementById('quiz-title').value.trim() :
                    (currentMethod === 'image' ? imageFile.name.replace(/\.[^/.]+$/, '') : 
                     pdfFile.name.replace('.pdf', '')) + (currentLanguage === 'ar' ? ' - اختبار' : ' - Quiz');
                
                document.getElementById('main-title').textContent = currentQuizTitle;
                document.getElementById('current-quiz-title').textContent = currentQuizTitle;

                // إخفاء قسم الإعداد وإظهار قسم الاختبار
                document.getElementById('setup-section').style.display = 'none';
                document.getElementById('quiz-section').style.display = 'block';

                // بدء المؤقت وتحميل الاختبار
                clearInterval(timerInterval);
                startTimer();
                loadQuiz();

                showSuccessMessage(currentLanguage === 'ar' ?
                    `تم توليد ${questions.length} سؤالاً بنجاح!` :
                    `Successfully generated ${questions.length} questions!`);

            } catch (error) {
                console.error('Error in generateQuiz:', error);
                showError(currentLanguage === 'ar' ? 
                    `حدث خطأ: ${error.message}` : 
                    `Error: ${error.message}`);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        async function generateSummary() {
            if (!summaryFile) {
                showError(currentLanguage === 'ar' ? 
                    'الرجاء رفع ملف للتلخيص أولاً' : 
                    'Please upload a file for summarization first');
                return;
            }

            // إعداد واجهة التحميل
            document.getElementById('loading').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
            document.getElementById('loading-details').textContent = currentLanguage === 'ar' ?
                'جارٍ إنشاء الملخص...' :
                'Creating summary...';

            try {
                const fileBase64 = await convertFileToBase64(summaryFile);
                const pdfDetails = getPDFDetails();
                const validationErrors = validatePDFDetails(pdfDetails);
                
                if (validationErrors.length > 0) {
                    showError(validationErrors.join(', '));
                    return;
                }
                
                const prompt = generateSummaryPrompt(contentLanguage, summaryType, pdfDetails);
                const mimeType = summaryFile.type === 'application/pdf' ? 'application/pdf' : 
                                summaryFile.type.startsWith('image/') ? summaryFile.type : 'text/plain';
                
                const maxTokens = summaryType === 'detailed' ? 4096 : 2048;
                
                const requestBody = {
                    contents: [{
                        parts: [
                            { text: prompt },
                            {
                                inline_data: {
                                    mime_type: mimeType,
                                    data: fileBase64
                                }
                            }
                        ]
                    }],
                    generationConfig: {
                        temperature: 0.7,
                        topK: 40,
                        topP: 0.95,
                        maxOutputTokens: maxTokens,
                    }
                };

                // استخدام دالة makeAPIRequest الجديدة
                const data = await makeAPIRequest(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(requestBody)
                });

                const summaryText = data.candidates[0].content.parts[0].text;
                
                // إظهار الملخص
                document.getElementById('setup-section').style.display = 'none';
                document.getElementById('summary-section').style.display = 'block';
                document.getElementById('summary-content').innerHTML = formatSummary(summaryText, contentLanguage);

                showSuccessMessage(currentLanguage === 'ar' ?
                    'تم إنشاء الملخص بنجاح!' :
                    'Summary created successfully!');

            } catch (error) {
                console.error('Error in generateSummary:', error);
                showError(currentLanguage === 'ar' ? 
                    `حدث خطأ: ${error.message}` : 
                    `Error: ${error.message}`);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        async function generateFlashcards() {
            if (!flashcardsFile) {
                showError(currentLanguage === 'ar' ? 
                    'الرجاء رفع ملف للبطاقات التعليمية أولاً' : 
                    'Please upload a file for flashcards first');
                return;
            }

            // إعداد واجهة التحميل
            document.getElementById('loading').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
            document.getElementById('loading-details').textContent = currentLanguage === 'ar' ?
                'جارٍ إنشاء البطاقات التعليمية...' :
                'Creating flashcards...';

            try {
                const numFlashcards = parseInt(document.getElementById('num-flashcards').value);
                const difficulty = document.getElementById('flashcard-difficulty').value;
                const fileBase64 = await convertFileToBase64(flashcardsFile);
                const pdfDetails = getPDFDetails();
                const validationErrors = validatePDFDetails(pdfDetails);
                
                if (validationErrors.length > 0) {
                    showError(validationErrors.join(', '));
                    return;
                }
                
                const prompt = generateFlashcardsPrompt(numFlashcards, contentLanguage, flashcardType, difficulty, pdfDetails);
                const mimeType = flashcardsFile.type === 'application/pdf' ? 'application/pdf' : 
                                flashcardsFile.type.startsWith('image/') ? flashcardsFile.type : 'text/plain';
                
                const requestBody = {
                    contents: [{
                        parts: [
                            { text: prompt },
                            {
                                inline_data: {
                                    mime_type: mimeType,
                                    data: fileBase64
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

                // استخدام دالة makeAPIRequest الجديدة
                const data = await makeAPIRequest(`${GEMINI_API_URL}?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(requestBody)
                });

                const responseText = data.candidates[0].content.parts[0].text;
                
                // استخراج JSON من الاستجابة
                const jsonMatch = extractJSONFromText(responseText);
                if (!jsonMatch) {
                    throw new Error(currentLanguage === 'ar' ? 
                        'تعذر استخراج البيانات من استجابة الذكاء الاصطناعي' : 
                        'Could not extract data from AI response');
                }

                let flashcardsData;
                try {
                    flashcardsData = JSON.parse(jsonMatch);
                } catch (error) {
                    const cleanedJson = jsonMatch
                        .replace(/```json\n?|\n?```/g, '')
                        .replace(/'/g, '"')
                        .replace(/(\w+):/g, '"$1":')
                        .replace(/,\s*}/g, '}')
                        .replace(/,\s*]/g, ']')
                        .replace(/\n/g, ' ')
                        .replace(/\s+/g, ' ');
                    
                    flashcardsData = JSON.parse(cleanedJson);
                }
                
                if (!flashcardsData.flashcards || !Array.isArray(flashcardsData.flashcards)) {
                    throw new Error(currentLanguage === 'ar' ? 
                        'لم يتم العثور على بطاقات في الاستجابة' : 
                        'No flashcards found in response');
                }

                // معالجة البطاقات
                flashcards = flashcardsData.flashcards.map((card, index) => ({
                    ...card,
                    id: card.id || index + 1,
                    mastered: false,
                    needsReview: false,
                    category: card.category || "general",
                    difficulty: card.difficulty || "medium"
                }));
                
                currentFlashcardIndex = 0;
                masteredFlashcards.clear();
                reviewFlashcards.clear();

                // إظهار قسم البطاقات التعليمية
                document.getElementById('setup-section').style.display = 'none';
                document.getElementById('flashcards-section-main').style.display = 'block';
                
                // تحميل البطاقة الأولى
                loadFlashcard(currentFlashcardIndex);
                updateFlashcardStats();
                updateNavigationDots();

                showSuccessMessage(currentLanguage === 'ar' ?
                    `تم إنشاء ${flashcards.length} بطاقة تعليمية بنجاح!` :
                    `Successfully created ${flashcards.length} flashcards!`);

            } catch (error) {
                console.error('Error in generateFlashcards:', error);
                showError(currentLanguage === 'ar' ? 
                    `حدث خطأ: ${error.message}` : 
                    `Error: ${error.message}`);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }

        // دالة مساعدة لاستخراج JSON من النص
        function extractJSONFromText(text) {
            // محاولة العثور على JSON في النص
            const jsonPatterns = [
                /\{[\s\S]*"flashcards"[\s\S]*\}/,
                /\{[\s\S]*"questions"[\s\S]*\}/,
                /\{[\s\S]*\}/,
                /\[[\s\S]*\]/
            ];
            
            for (const pattern of jsonPatterns) {
                const match = text.match(pattern);
                if (match) {
                    return match[0];
                }
            }
            
            // إذا لم يتم العثور، محاولة العثور على جزء JSON
            const startIndex = text.indexOf('{');
            const endIndex = text.lastIndexOf('}');
            
            if (startIndex !== -1 && endIndex !== -1 && endIndex > startIndex) {
                return text.substring(startIndex, endIndex + 1);
            }
            
            return null;
        }

        // ==================== وظائف توليد النصوص ====================
        function generateQuizPrompt(title, topic, numQuestions, language) {
            const selectedTypesText = getSelectedQuestionTypesText(language);
            const questionFormats = getQuestionFormats(language);
            
            if (language === 'en') {
                return `Please generate exactly ${numQuestions} questions about: "${title}"
                
Topic details: ${topic}

Question types to include: ${selectedTypesText}

IMPORTANT: 
- Keep the response minimal and focused
- Use very brief explanations (max 10-15 words)
- Generate concise questions and options
- Ensure JSON is valid and properly formatted

CRITICAL: For large question sets (more than 15 questions):
- Use minimal text for explanations
- Keep options short
- Prioritize clarity over verbosity

Please follow this JSON format EXACTLY:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "Brief question text?",
      "options": ["A", "B", "C", "D"],
      "answer": 0,
      "explanations": {
        "correct": "Very brief explanation",
        "option0": "Short feedback A",
        "option1": "Short feedback B", 
        "option2": "Short feedback C",
        "option3": "Short feedback D"
      }
    }
  ]
}`;
            } else {
                return `يرجى إنشاء بالضبط ${numQuestions} سؤالاً حول: "${title}"
                
تفاصيل الموضوع: ${topic}

أنواع الأسئلة المطلوبة: ${selectedTypesText}

هام جداً:
- حافظ على الاستجابة مركزة ومختصرة
- استخدم شروحات موجزة جداً (10-15 كلمة كحد أقصى)
- أنشئ أسئلة وخيارات مركزة
- تأكد من أن JSON صالح ومنسق بشكل صحيح

مهم جداً: لمجموعات الأسئلة الكبيرة (أكثر من 15 سؤال):
- استخدم نصاً محدوداً للشروحات
- حافظ على الخيارات قصيرة
- ركز على الوضوح بدلاً من التفصيل المفرط

الرجاء الالتزام بتنسيق JSON التالي بالضبط:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "نص سؤال موجز؟",
      "options": ["أ", "ب", "ج", "د"],
      "answer": 0,
      "explanations": {
        "correct": "شرح موجز جداً",
        "option0": "تغذية راجعة قصيرة أ",
        "option1": "تغذية راجعة قصيرة ب",
        "option2": "تغذية راجعة قصيرة ج",
        "option3": "تغذية راجعة قصيرة د"
      }
    }
  ]
}`;
            }
        }

        function generateImageQuizPrompt(numQuestions, language) {
            const selectedTypesText = getSelectedQuestionTypesText(language);
            const questionFormats = getQuestionFormats(language);
            
            if (language === 'en') {
                return `Please generate exactly ${numQuestions} questions based on the text in the provided image.

Question types to include: ${selectedTypesText}

Extract key information from the image and create clear, concise questions.
Keep JSON response minimal and focused.

CRITICAL: For large question sets (more than 15 questions):
- Use minimal text for explanations
- Keep options short
- Extract only essential information from image

Please follow this JSON format EXACTLY:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "Brief question?",
      "options": ["A", "B", "C", "D"],
      "answer": 0,
      "explanations": {
        "correct": "Very brief",
        "option0": "Short",
        "option1": "Short", 
        "option2": "Short",
        "option3": "Short"
      }
    }
  ]
}`;
            } else {
                return `يرجى إنشاء بالضبط ${numQuestions} سؤالاً بناءً على النص في الصورة المرفوعة.

أنواع الأسئلة المطلوبة: ${selectedTypesText}

استخرج المعلومات الرئيسية من الصورة وأنشئ أسئلة واضحة ومركزة.
حافظ على استجابة JSON بسيطة ومركزة.

مهم جداً: لمجموعات الأسئلة الكبيرة (أكثر من 15 سؤال):
- استخدم نصاً محدوداً للشروحات
- حافظ على الخيارات قصيرة
- استخرج فقط المعلومات الأساسية من الصورة

الرجاء الالتزام بتنسيق JSON التالي بالضبط:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "سؤال موجز؟",
      "options": ["أ", "ب", "ج", "د"],
      "answer": 0,
      "explanations": {
        "correct": "موجز جداً",
        "option0": "قصير",
        "option1": "قصير",
        "option2": "قصير",
        "option3": "قصير"
      }
    }
  ]
}`;
            }
        }

        function generatePDFQuizPrompt(numQuestions, language, pdfDetails) {
            const selectedTypesText = getSelectedQuestionTypesText(language);
            const pdfDetailsInstructions = generatePDFDetailsInstructions(pdfDetails, language);
            
            if (language === 'en') {
                return `Please generate exactly ${numQuestions} questions based on the content of the PDF file.

${pdfDetailsInstructions}

Question types to include: ${selectedTypesText}

Generate clear, concise questions that accurately reflect ONLY the specified content.
Keep explanations brief and JSON response minimal.

CRITICAL: For large question sets (more than 15 questions):
- Use minimal text for explanations
- Keep options short
- Focus on key concepts only

Please follow this JSON format EXACTLY:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "Brief question?",
      "options": ["A", "B", "C", "D"],
      "answer": 0,
      "explanations": {
        "correct": "Very brief",
        "option0": "Short",
        "option1": "Short", 
        "option2": "Short",
        "option3": "Short"
      }
    }
  ]
}`;
            } else {
                return `يرجى إنشاء بالضبط ${numQuestions} سؤالاً بناءً على محتوى ملف PDF.

${pdfDetailsInstructions}

أنواع الأسئلة المطلوبة: ${selectedTypesText}

أنشئ أسئلة واضحة ومركزة تعكس بدقة المحتوى المحدد فقط.
حافظ على الشروحات موجزة واستجابة JSON بسيطة.

مهم جداً: لمجموعات الأسئلة الكبيرة (أكثر من 15 سؤال):
- استخدم نصاً محدوداً للشروحات
- حافظ على الخيارات قصيرة
- ركز على المفاهيم الأساسية فقط

الرجاء الالتزام بتنسيق JSON التالي بالضبط:

{
  "questions": [
    {
      "type": "multiple_choice",
      "q": "سؤال موجز؟",
      "options": ["أ", "ب", "ج", "د"],
      "answer": 0,
      "explanations": {
        "correct": "موجز جداً",
        "option0": "قصير",
        "option1": "قصير",
        "option2": "قصير",
        "option3": "قصير"
      }
    }
  ]
}`;
            }
        }

        function generateSummaryPrompt(language, type, pdfDetails) {
            const summaryLength = document.getElementById('summary-length').value;
            const pdfDetailsInstructions = generatePDFDetailsInstructions(pdfDetails, language);
            
            let lengthInstruction = '';
            if (summaryLength === 'short') {
                lengthInstruction = language === 'en' ? 
                    "Keep the summary brief, focusing only on the most important points (3-5 key points maximum)." :
                    "حافظ على الملخص موجزاً، وركز فقط على النقاط الأهم (3-5 نقاط رئيسية كحد أقصى).";
            } else if (summaryLength === 'long') {
                lengthInstruction = language === 'en' ?
                    "Provide a comprehensive and detailed summary covering all important aspects with hierarchical structure (chapters, sections, subsections)." :
                    "قدم ملخصاً شاملاً ومفصلاً يغطي جميع الجوانب المهمة مع هيكل هرمي (فصول، أقسام، أقسام فرعية).";
            } else {
                lengthInstruction = language === 'en' ?
                    "Provide a balanced summary that covers the main points with clear hierarchy without being too brief or too detailed." :
                    "قدم ملخصاً متوازناً يغطي النقاط الرئيسية مع هيكل واضح دون أن يكون موجزاً جداً أو مفصلاً جداً.";
            }
            
            if (type === 'detailed') {
                if (language === 'en') {
                    return `Please provide a comprehensive hierarchical summary of the document.

${pdfDetailsInstructions}

${lengthInstruction}

CRITICAL: Structure the summary hierarchically:
1. Main Title
2. Chapters/Sections
3. Subsections within each chapter
4. Key points under each subsection
5. Important concepts, definitions, and notes

Formatting requirements:
- Use clear hierarchical structure
- Highlight key concepts
- Include important definitions
- Add notes for critical information
- Make it easy to read and navigate`;
                } else {
                    return `يرجى تقديم ملخص هرمي شاملاً للمستند.

${pdfDetailsInstructions}

${lengthInstruction}

مهم جداً: قم بتنظيم الملخص بشكل هرمي:
1. عنوان رئيسي
2. فصول/أقسام
3. أقسام فرعية داخل كل فصل
4. نقاط رئيسية تحت كل قسم فرعي
5. مفاهيم وتعريفات وملاحظات مهمة

متطلبات التنسيق:
- استخدم هيكلاً هرمياً واضحاً
- سلط الضوء على المفاهيم الأساسية
- أدرج التعريفات المهمة
- أضف ملاحظات للمعلومات الحاسمة
- اجعله سهل القراءة والتنقل`;
                }
            } else {
                if (language === 'en') {
                    return `Please provide a quick hierarchical summary of the document.

${pdfDetailsInstructions}

${lengthInstruction}

Focus only on:
1. Most important chapters
2. Key sections within chapters
3. Essential points within sections

Structure hierarchically with clear levels.`;
                } else {
                    return `يرجى تقديم ملخص هرمي سريع للمستند.

${pdfDetailsInstructions}

${lengthInstruction}

ركز فقط على:
1. الفصول الأهم
2. الأقسام الرئيسية داخل الفصول
3. النقاط الأساسية داخل الأقسام

قم بتنظيمها هرمياً بمستويات واضحة.`;
                }
            }
        }

        function generateFlashcardsPrompt(numFlashcards, language, type, difficulty, pdfDetails) {
            const pdfDetailsInstructions = generatePDFDetailsInstructions(pdfDetails, language);
            
            let typeInstruction = '';
            if (type === 'concepts') {
                typeInstruction = language === 'en' ?
                    "Focus on key concepts, definitions, and important terms. Front: concept/term, Back: definition/explanation." :
                    "ركز على المفاهيم الأساسية والتعريفات والمصطلحات المهمة. الوجه: المفهوم/المصطلح، الظهر: التعريف/الشرح.";
            } else {
                typeInstruction = language === 'en' ?
                    "Focus on Q&A format. Front: question, Back: answer with brief explanation." :
                    "ركز على صيغة سؤال وجواب. الوجه: السؤال، الظهر: الإجابة مع شرح موجز.";
            }
            
            let difficultyInstruction = '';
            if (difficulty === 'easy') {
                difficultyInstruction = language === 'en' ?
                    "Focus on basic concepts and definitions suitable for beginners." :
                    "ركز على المفاهيم الأساسية والتعريفات المناسبة للمبتدئين.";
            } else if (difficulty === 'hard') {
                difficultyInstruction = language === 'en' ?
                    "Focus on advanced concepts, complex relationships, and detailed explanations." :
                    "ركز على المفاهيم المتقدمة، والعلاقات المعقدة، والشروحات المفصلة.";
            } else if (difficulty === 'mixed') {
                difficultyInstruction = language === 'en' ?
                    "Include a mix of easy, medium, and hard flashcards." :
                    "اشمل مزيجاً من البطاقات التعليمية السهلة والمتوسطة والصعبة.";
            } else {
                difficultyInstruction = language === 'en' ?
                    "Focus on concepts suitable for intermediate learners." :
                    "ركز على المفاهيم المناسبة للمتعلمين المتوسطين.";
            }
            
            if (language === 'en') {
                return `Create exactly ${numFlashcards} educational flashcards based on the document content.

${pdfDetailsInstructions}

${typeInstruction}

${difficultyInstruction}

IMPORTANT: Return ONLY valid JSON. Do not include any other text.
The JSON MUST have this exact structure:

{
  "flashcards": [
    {
      "front": "Question or concept",
      "back": "Answer or explanation",
      "category": "concepts",
      "difficulty": "medium"
    }
  ]
}

CRITICAL: Ensure the JSON is valid. Use double quotes for all keys and string values.
Generate exactly ${numFlashcards} flashcards.`;
            } else {
                return `أنشئ بالضبط ${numFlashcards} بطاقة تعليمية بناءً على محتوى المستند.

${pdfDetailsInstructions}

${typeInstruction}

${difficultyInstruction}

مهم جداً: أعد فقط JSON صالحاً. لا تدرج أي نص آخر.
يجب أن يكون هيكل JSON بالضبط كما يلي:

{
  "flashcards": [
    {
      "front": "السؤال أو المفهوم",
      "back": "الإجابة أو الشرح",
      "category": "مفاهيم",
      "difficulty": "متوسط"
    }
  ]
}

مهم: تأكد من صحة JSON. استخدم علامات تنصيص مزدوجة لجميع المفاتيح والقيم النصية.
أنشئ بالضبط ${numFlashcards} بطاقة تعليمية.`;
            }
        }

        function getSelectedQuestionTypesText(language) {
            const selectedTypes = [];
            
            if (selectedQuestionTypes.multipleChoice) {
                selectedTypes.push(language === 'en' ? 'multiple choice' : 'اختيار متعدد');
            }
            if (selectedQuestionTypes.trueFalse) {
                selectedTypes.push(language === 'en' ? 'true/false' : 'صح/خطأ');
            }
            if (selectedQuestionTypes.fillBlank) {
                selectedTypes.push(language === 'en' ? 'fill in the blank' : 'املأ الفراغ');
            }
            
            if (language === 'en') {
                return selectedTypes.join(', ');
            } else {
                return selectedTypes.join('، ');
            }
        }

        function getQuestionFormats(language) {
            const formats = [];
            
            if (selectedQuestionTypes.multipleChoice) {
                if (language === 'en') {
                    formats.push(`{
      "type": "multiple_choice",
      "q": "Brief question?",
      "options": ["A", "B", "C", "D"],
      "answer": 0,
      "explanations": {
        "correct": "Very brief explanation",
        "option0": "Short feedback A",
        "option1": "Short feedback B", 
        "option2": "Short feedback C",
        "option3": "Short feedback D"
      }
    }`);
                } else {
                    formats.push(`{
      "type": "multiple_choice",
      "q": "سؤال موجز؟",
      "options": ["أ", "ب", "ج", "د"],
      "answer": 0,
      "explanations": {
        "correct": "شرح موجز جداً",
        "option0": "تغذية راجعة قصيرة أ",
        "option1": "تغذية راجعة قصيرة ب",
        "option2": "تغذية راجعة قصيرة ج",
        "option3": "تغذية راجعة قصيرة د"
      }
    }`);
                }
            }
            
            if (selectedQuestionTypes.trueFalse) {
                if (language === 'en') {
                    formats.push(`{
      "type": "true_false",
      "q": "Statement",
      "options": ["True", "False"],
      "answer": 0,
      "explanations": {
        "correct": "Very brief explanation",
        "option0": "Short feedback True",
        "option1": "Short feedback False"
      }
    }`);
                } else {
                    formats.push(`{
      "type": "true_false",
      "q": "الجملة",
      "options": ["صح", "خطأ"],
      "answer": 0,
      "explanations": {
        "correct": "شرح موجز جداً",
        "option0": "تغذية راجعة قصيرة صح",
        "option1": "تغذية راجعة قصيرة خطأ"
      }
    }`);
                }
            }
            
            if (selectedQuestionTypes.fillBlank) {
                if (language === 'en') {
                    formats.push(`{
      "type": "fill_blank",
      "q": "Complete: The capital of France is _____",
      "answer": "Paris",
      "explanations": {
        "correct": "Brief explanation",
        "common_mistakes": ["London", "Berlin"]
      }
    }`);
                } else {
                    formats.push(`{
      "type": "fill_blank",
      "q": "أكمل: عاصمة فرنسا هي _____",
      "answer": "باريس",
      "explanations": {
        "correct": "شرح موجز",
        "common_mistakes": ["لندن", "برلين"]
      }
    }`);
                }
            }
            
            return formats;
        }

        function formatSummary(summaryText, language) {
            // تحويل النص إلى تنسيق HTML هرمي
            let formattedText = '<div class="summary-hierarchy">';
            
            // إضافة عنوان رئيسي
            formattedText += `<h1 class="summary-main-title">
                <i class="fas fa-book"></i>
                ${currentLanguage === 'ar' ? 'ملخص المحتوى' : 'Content Summary'}
            </h1>`;
            
            // تقسيم النص إلى أقسام
            const lines = summaryText.split('\n').filter(line => line.trim());
            
            let currentChapter = null;
            let currentSection = null;
            let currentSubsection = null;
            let inPointsList = false;
            let currentPoints = [];
            
            for (let i = 0; i < lines.length; i++) {
                const line = lines[i].trim();
                
                // الكشف عن الفصول الرئيسية (مستوى 1)
                if (line.match(/^(الفصل|القسم|الجزء|Chapter|Part|Section)[\s:]+[١-٩0-9IVX]/i) || 
                    line.match(/^[IVX]+\.\s+(.+)$/) ||
                    line.match(/^[١-٩]+\.\s+(.+)$/) ||
                    (line.length < 100 && (line.includes(':') || line.endsWith(':')))) {
                    
                    // إنهاء القسم السابق إذا كان موجوداً
                    if (currentSection && currentPoints.length > 0) {
                        formattedText += '<ul class="summary-points">';
                        currentPoints.forEach(point => {
                            formattedText += `<li class="summary-point">${point}</li>`;
                        });
                        formattedText += '</ul>';
                        currentPoints = [];
                    }
                    
                    if (currentSection) {
                        formattedText += '</div>'; // إغلاق القسم
                        currentSection = null;
                    }
                    
                    if (currentChapter) {
                        formattedText += '</div>'; // إغلاق الفصل
                    }
                    
                    const title = line.replace(/^(الفصل|القسم|الجزء|Chapter|Part|Section)[\s:]+/i, '')
                                     .replace(/^[IVX]+\.\s+/, '')
                                     .replace(/^[١-٩]+\.\s+/, '')
                                     .replace(/:$/, '')
                                     .trim();
                    
                    currentChapter = title;
                    formattedText += `<div class="summary-chapter">
                        <h2 class="summary-chapter-title">
                            <i class="fas fa-bookmark"></i>
                            ${title}
                        </h2>`;
                }
                // الكشف عن الأقسام الفرعية (مستوى 2)
                else if (line.match(/^[A-Z]\.\s+(.+)$/) || 
                        line.match(/^[أ-ي]\.\s+(.+)$/) ||
                        (line.length < 80 && line.includes(':'))) {
                    
                    // إنهاء القائمة السابقة إذا كانت موجودة
                    if (currentPoints.length > 0) {
                        formattedText += '<ul class="summary-points">';
                        currentPoints.forEach(point => {
                            formattedText += `<li class="summary-point">${point}</li>`;
                        });
                        formattedText += '</ul>';
                        currentPoints = [];
                    }
                    
                    if (currentSection) {
                        formattedText += '</div>'; // إغلاق القسم السابق
                    }
                    
                    const sectionTitle = line.replace(/^[A-Z]\.\s+/, '')
                                           .replace(/^[أ-ي]\.\s+/, '')
                                           .replace(/:$/, '')
                                           .trim();
                    
                    currentSection = sectionTitle;
                    formattedText += `<div class="summary-section">
                        <h3 class="summary-section-title">
                            <i class="fas fa-cube"></i>
                            ${sectionTitle}
                        </h3>`;
                }
                // الكشف عن الأقسام الفرعية من المستوى الثالث
                else if (line.match(/^[0-9]+\.[0-9]+\s+(.+)$/) || 
                        line.match(/^[١-٩]+\.[١-٩]+\s+(.+)$/) ||
                        (line.length < 60 && line.includes('-'))) {
                    
                    if (currentPoints.length > 0) {
                        formattedText += '<ul class="summary-points">';
                        currentPoints.forEach(point => {
                            formattedText += `<li class="summary-point">${point}</li>`;
                        });
                        formattedText += '</ul>';
                        currentPoints = [];
                    }
                    
                    const subsectionTitle = line.replace(/^[0-9]+\.[0-9]+\s+/, '')
                                              .replace(/^[١-٩]+\.[١-٩]+\s+/, '')
                                              .trim();
                    
                    currentSubsection = subsectionTitle;
                    formattedText += `<div class="summary-subsection">
                        <h4 class="summary-subsection-title">
                            <i class="fas fa-circle"></i>
                            ${subsectionTitle}
                        </h4>`;
                }
                // الكشف عن النقاط الرئيسية
                else if (line.match(/^[•\-]\s+(.+)$/) || 
                        line.match(/^[٠-٩]+\)\s+(.+)$/) ||
                        line.match(/^[0-9]+\)\s+(.+)$/)) {
                    
                    const point = line.replace(/^[•\-]\s+/, '')
                                    .replace(/^[٠-٩]+\)\s+/, '')
                                    .replace(/^[0-9]+\)\s+/, '')
                                    .trim();
                    
                    currentPoints.push(point);
                }
                // الكشف عن المفاهيم الأساسية
                else if (line.match(/^(مفهوم|تعريف|ملاحظة|هام|Concept|Definition|Note|Important)[\s:]/i)) {
                    
                    if (currentPoints.length > 0) {
                        formattedText += '<ul class="summary-points">';
                        currentPoints.forEach(point => {
                            formattedText += `<li class="summary-point">${point}</li>`;
                        });
                        formattedText += '</ul>';
                        currentPoints = [];
                    }
                    
                    const content = line.replace(/^(مفهوم|تعريف|ملاحظة|هام|Concept|Definition|Note|Important)[\s:]+/i, '').trim();
                    
                    if (line.match(/^مفهوم|^Concept/i)) {
                        formattedText += `<div class="summary-key-concept">
                            <strong><i class="fas fa-lightbulb"></i> ${currentLanguage === 'ar' ? 'مفهوم أساسي:' : 'Key Concept:'}</strong> ${content}
                        </div>`;
                    } else if (line.match(/^تعريف|^Definition/i)) {
                        formattedText += `<div class="summary-definition">
                            <strong><i class="fas fa-book"></i> ${currentLanguage === 'ar' ? 'تعريف:' : 'Definition:'}</strong> ${content}
                        </div>`;
                    } else if (line.match(/^ملاحظة|^Note/i)) {
                        formattedText += `<div class="summary-note">
                            <strong><i class="fas fa-sticky-note"></i> ${currentLanguage === 'ar' ? 'ملاحظة:' : 'Note:'}</strong> ${content}
                        </div>`;
                    } else if (line.match(/^هام|^Important/i)) {
                        formattedText += `<div class="summary-important">
                            <strong><i class="fas fa-exclamation-circle"></i> ${currentLanguage === 'ar' ? 'هام:' : 'Important:'}</strong> ${content}
                        </div>`;
                    }
                }
                // النص العادي (فقرات)
                else if (line.length > 20) {
                    if (currentPoints.length > 0) {
                        formattedText += '<ul class="summary-points">';
                        currentPoints.forEach(point => {
                            formattedText += `<li class="summary-point">${point}</li>`;
                        });
                        formattedText += '</ul>';
                        currentPoints = [];
                    }
                    
                    formattedText += `<p class="summary-paragraph">${line}</p>`;
                }
            }
            
            // إنهاء أي قائمة متبقية
            if (currentPoints.length > 0) {
                formattedText += '<ul class="summary-points">';
                currentPoints.forEach(point => {
                    formattedText += `<li class="summary-point">${point}</li>`;
                });
                formattedText += '</ul>';
            }
            
            // إغلاق الأقسام المفتوحة
            if (currentSubsection) {
                formattedText += '</div>';
            }
            if (currentSection) {
                formattedText += '</div>';
            }
            if (currentChapter) {
                formattedText += '</div>';
            }
            
            formattedText += '</div>';
            
            return formattedText;
        }

        // ==================== وظائف مساعدة ====================
        async function convertFileToBase64(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result.split(',')[1]);
                reader.onerror = reject;
                reader.readAsDataURL(file);
            });
        }

        function shuffleOptions(question) {
            if (question.type === 'fill_blank') {
                return question;
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

        // ==================== وظائف الاختبار ====================
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

        function loadQuiz() {
            const quizDiv = document.getElementById("quiz");
            
            if (shuffledQuestions.length === 0) {
                shuffledQuestions = questions.map(q => shuffleOptions(q));
            }
            
            const question = shuffledQuestions[currentQuestionIndex];
            const isLocked = answerLocked[currentQuestionIndex];

            let questionNumberText = currentLanguage === 'en' 
                ? `Question ${currentQuestionIndex + 1} of ${questions.length}`
                : `السؤال ${currentQuestionIndex + 1} من ${questions.length}`;
                
            let lockedText = currentLanguage === 'en' ? 'Locked' : 'مقفل';
            let markedText = currentLanguage === 'en' ? 'Flagged' : 'معلمة';
            
            let totalQuestionsText = currentLanguage === 'en' ? 'Total Questions' : 'إجمالي الأسئلة';
            let answeredText = currentLanguage === 'en' ? 'Answered' : 'تم الإجابة';
            let flaggedText = currentLanguage === 'en' ? 'Flagged' : 'معلمة';
            let instantReviewText = currentLanguage === 'en' ? 'Instant Review' : 'مراجعة فورية';

            let html = `
            <div class="question-box">
                <div class="question-number">
                    <i class="fas fa-question-circle"></i>
                    ${questionNumberText}
                    ${question.type === 'multiple_choice' ? `<span class="category-badge">${currentLanguage === 'en' ? 'Multiple Choice' : 'اختيار متعدد'}</span>` : ''}
                    ${question.type === 'true_false' ? `<span class="category-badge">${currentLanguage === 'en' ? 'True/False' : 'صح/خطأ'}</span>` : ''}
                    ${question.type === 'fill_blank' ? `<span class="category-badge">${currentLanguage === 'en' ? 'Fill in Blank' : 'املأ الفراغ'}</span>` : ''}
                    ${isLocked ? `<span style="color: var(--accent); margin-right: 10px;"><i class="fas fa-lock"></i> ${lockedText}</span>` : ''}
                    ${markedQuestions.includes(currentQuestionIndex) ? `<span style="background: var(--tertiary-gradient); color: white; padding: 5px 10px; border-radius: 10px; font-size: 0.8rem; margin-right: 10px;"><i class="fas fa-flag"></i> ${markedText}</span>` : ''}
                </div>
                
                <div class="quiz-stats">
                    <span><i class="fas fa-layer-group"></i> ${totalQuestionsText}: ${questions.length}</span>
                    <span><i class="fas fa-question"></i> ${answeredText}: ${userAnswers.filter(a => a !== null).length}</span>
                    <span><i class="fas fa-flag"></i> ${flaggedText}: ${markedQuestions.length}</span>
                </div>`;

            // إضافة معلومات المحتوى المحدد لملفات PDF
            if (currentMethod === 'pdf') {
                const pdfDetails = getPDFDetails();
                const hasSpecifiedContent = pdfDetails.pages.startPage || 
                                           pdfDetails.pages.endPage || 
                                           pdfDetails.pages.specificPages || 
                                           pdfDetails.units || 
                                           pdfDetails.topics;

                if (hasSpecifiedContent) {
                    let contentInfo = '';
                    
                    if (currentLanguage === 'en') {
                        contentInfo = '<div class="source-info">';
                        contentInfo += '<i class="fas fa-filter"></i> <strong>Content Filter Applied:</strong> ';
                        
                        if (pdfDetails.pages.startPage || pdfDetails.pages.endPage || pdfDetails.pages.specificPages) {
                            contentInfo += 'Specific pages';
                        }
                        if (pdfDetails.units) {
                            contentInfo += (contentInfo.includes('pages') ? ', ' : '') + 'Specific units';
                        }
                        if (pdfDetails.topics) {
                            contentInfo += (contentInfo.includes('units') ? ', ' : '') + 'Specific topics';
                        }
                        contentInfo += '</div>';
                    } else {
                        contentInfo = '<div class="source-info">';
                        contentInfo += '<i class="fas fa-filter"></i> <strong>تم تطبيق تصفية المحتوى:</strong> ';
                        
                        if (pdfDetails.pages.startPage || pdfDetails.pages.endPage || pdfDetails.pages.specificPages) {
                            contentInfo += 'صفحات محددة';
                        }
                        if (pdfDetails.units) {
                            contentInfo += (contentInfo.includes('محددة') ? '، ' : '') + 'وحدات محددة';
                        }
                        if (pdfDetails.topics) {
                            contentInfo += (contentInfo.includes('محددة') ? '، ' : '') + 'مواضيع محددة';
                        }
                        contentInfo += '</div>';
                    }
                    
                    html += contentInfo;
                }
            }

            html += `
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
                    
                    <div id="option-feedback-${currentQuestionIndex}-${i}" class="option-feedback" style="display: none;">
                        ${question.explanations && question.explanations[`option${i}`] ? question.explanations[`option${i}`] : ''}
                    </div>
                    `;
                });
                
                html += `</div>`;
            } else {
                html += `
                <div class="options">
                    <label style="flex-direction: column; align-items: flex-start;">
                        <span style="margin-bottom: 10px; font-weight: bold;">${currentLanguage === 'en' ? 'Your Answer:' : 'إجابتك:'}</span>
                        <input type="text" id="fillBlankAnswer" class="input-field" style="width: 100%;" 
                               placeholder="${currentLanguage === 'en' ? 'Type your answer here...' : 'اكتب إجابتك هنا...'}" 
                               ${isLocked ? 'disabled' : ''}
                               value="${userAnswers[currentQuestionIndex] || ''}"
                               onchange="selectFillBlankAnswer(this.value)">
                    </label>
                </div>
                `;
            }

            // إضافة زر المراجعة الفورية
            if (question.type !== 'fill_blank' && question.explanations && Object.keys(question.explanations).length > 0) {
                html += `
                <div class="instant-review" id="instant-review-${currentQuestionIndex}">
                    <div class="instant-review-title">
                        <i class="fas fa-lightbulb"></i>
                        ${instantReviewText}
                    </div>
                    <button class="btn btn-primary" onclick="showInstantReview(${currentQuestionIndex})" style="width: 100%; margin-bottom: 10px;">
                        <i class="fas fa-eye"></i> ${currentLanguage === 'ar' ? 'عرض المراجعة الفورية لجميع الخيارات' : 'Show Instant Review for All Options'}
                    </button>
                    <div id="review-content-${currentQuestionIndex}" style="display: none;">
                        <div class="instant-review-options">
                `;
                
                question.options.forEach((opt, i) => {
                    const isCorrect = i === question.answer;
                    const feedback = question.explanations[`option${i}`] || '';
                    
                    html += `
                    <div class="review-option ${isCorrect ? 'correct' : 'incorrect'}">
                        <div class="review-option-text">
                            <strong>${opt}</strong> 
                            ${isCorrect ? '<span style="color: var(--secondary);"><i class="fas fa-check"></i></span>' : '<span style="color: #ef4444;"><i class="fas fa-times"></i></span>'}
                        </div>
                        <div class="review-option-feedback">
                            ${feedback}
                        </div>
                    </div>
                    `;
                });
                
                html += `
                        </div>
                    </div>
                </div>
                `;
            }

            let previousText, nextText, previousIcon, nextIcon;
            
            if (currentLanguage === 'en') {
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
            let quizInfoText = currentLanguage === 'en'
                ? `Question ${currentQuestionIndex + 1} of ${questions.length} | Answered: ${userAnswers.filter(a => a !== null).length} | Flagged: ${markedQuestions.length}`
                : `السؤال ${currentQuestionIndex + 1} من ${questions.length} | تم الإجابة: ${userAnswers.filter(a => a !== null).length} | معلمة: ${markedQuestions.length}`;
            
            document.getElementById('quiz-info').innerHTML = quizInfoText;

            // تحديث زر وضع العلامة
            const markBtn = document.getElementById('mark-review-btn');
            if (markedQuestions.includes(currentQuestionIndex)) {
                markBtn.innerHTML = currentLanguage === 'en'
                    ? '<i class="fas fa-flag"></i> Remove Flag'
                    : '<i class="fas fa-flag"></i> إزالة العلامة';
                markBtn.style.background = 'var(--tertiary-gradient)';
            } else {
                markBtn.innerHTML = currentLanguage === 'en'
                    ? '<i class="fas fa-flag"></i> Mark for Review'
                    : '<i class="fas fa-flag"></i> وضع علامة';
                markBtn.style.background = 'var(--secondary-gradient)';
            }

            // عرض الشرح إذا كان المستخدم قد أجاب على السؤال
            if (userAnswers[currentQuestionIndex] !== null) {
                showExplanation();
            }
            
            // إظهار المراجعة الفورية إذا تمت الإجابة
            if (answerLocked[currentQuestionIndex] && question.type !== 'fill_blank') {
                const instantReviewDiv = document.getElementById(`instant-review-${currentQuestionIndex}`);
                if (instantReviewDiv) {
                    instantReviewDiv.classList.add('show');
                }
            }
        }

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

            // إظهار التغذية الراجعة للخيار المختار
            const feedbackDiv = document.getElementById(`option-feedback-${currentQuestionIndex}-${answerIndex}`);
            const question = shuffledQuestions[currentQuestionIndex];
            
            if (feedbackDiv && question.explanations && question.explanations[`option${answerIndex}`]) {
                feedbackDiv.className = 'option-feedback';
                feedbackDiv.classList.add(answerIndex === question.answer ? 'correct' : 'incorrect');
                feedbackDiv.classList.add('show');
            }

            // إظهار المراجعة الفورية
            const instantReviewDiv = document.getElementById(`instant-review-${currentQuestionIndex}`);
            if (instantReviewDiv) {
                instantReviewDiv.classList.add('show');
            }

            // تشغيل الصوت المناسب
            if (answerIndex === question.answer) {
                playSound('correct');
            } else {
                playSound('wrong');
            }

            showExplanation();
            checkIfLastQuestionAnswered();
        }

        function selectFillBlankAnswer(value) {
            if (answerLocked[currentQuestionIndex]) {
                return;
            }
            
            userAnswers[currentQuestionIndex] = value;
            answerLocked[currentQuestionIndex] = true;

            document.getElementById('fillBlankAnswer').disabled = true;
            
            const question = shuffledQuestions[currentQuestionIndex];
            const userAnswerStr = value.toString().toLowerCase().trim();
            const correctAnswerStr = question.answer.toString().toLowerCase().trim();
            
            if (userAnswerStr === correctAnswerStr || 
                Math.abs(userAnswerStr.length - correctAnswerStr.length) < 3) {
                playSound('correct');
            } else {
                playSound('wrong');
            }
            
            showExplanation();
            checkIfLastQuestionAnswered();
        }

        function checkIfLastQuestionAnswered() {
            const allAnswered = userAnswers.every(answer => answer !== null);
            const lastQuestionIndex = questions.length - 1;
            const isLastQuestion = currentQuestionIndex === lastQuestionIndex;
            const lastQuestionAnswered = userAnswers[lastQuestionIndex] !== null;
            
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

        function showExplanation() {
            const question = shuffledQuestions[currentQuestionIndex];
            const explanationDiv = document.getElementById("explanation");
            const userAnswer = userAnswers[currentQuestionIndex];

            if (userAnswer !== null) {
                explanationDiv.style.display = "block";

                let correctText = currentLanguage === 'en' ? 'Correct answer!' : 'إجابة صحيحة!';
                let wrongText = currentLanguage === 'en' ? 'Wrong answer' : 'إجابة خاطئة';
                let correctAnswerText = currentLanguage === 'en' ? 'Correct answer' : 'الإجابة الصحيحة';
                let explanationText = currentLanguage === 'en' ? 'Feedback' : 'التغذية الراجعة';
                let yourAnswerText = currentLanguage === 'en' ? 'Your answer' : 'إجابتك';

                let resultHTML = "";
                let isCorrect = false;

                if (question.type === 'fill_blank') {
                    const userAnswerStr = userAnswer.toString().toLowerCase().trim();
                    const correctAnswerStr = question.answer.toString().toLowerCase().trim();
                    
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
                    
                    if (isCorrect && question.explanations && question.explanations.correct) {
                        resultHTML += `
                        <div style="margin-top: 15px; padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px;">
                            <strong>📚 ${explanationText}:</strong><br>
                            ${question.explanations.correct}
                        </div>
                        `;
                    } else if (!isCorrect && question.explanations && question.explanations.mistake_feedback) {
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
                    
                    if (question.explanations) {
                        resultHTML += `
                        <div style="margin-top: 15px;">
                            <strong>📚 ${explanationText}:</strong><br><br>
                        `;
                        
                        if (question.explanations.correct) {
                            resultHTML += `
                            <div style="padding: 10px; background: rgba(76, 175, 80, 0.1); border-radius: 8px; margin-bottom: 8px;">
                                <strong>✅ ${correctAnswerText}:</strong> ${question.explanations.correct}
                            </div>
                            `;
                        }
                        
                        const userChoiceText = currentLanguage === 'en' ? 'Your choice' : 'اختيارك';
                        if (question.explanations[`option${userAnswer}`]) {
                            const bgColor = isCorrect ? 'rgba(76, 175, 80, 0.1)' : 'rgba(239, 68, 68, 0.1)';
                            const icon = isCorrect ? '✅' : '❌';
                            resultHTML += `
                            <div style="padding: 10px; background: ${bgColor}; border-radius: 8px; margin-bottom: 8px;">
                                <strong>${icon} ${userChoiceText}:</strong> ${question.explanations[`option${userAnswer}`]}
                            </div>
                            `;
                        }
                        
                        resultHTML += `</div>`;
                    }
                }

                explanationDiv.innerHTML = resultHTML;
            }
        }

        function nextQuestion() {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                loadQuiz();
            } else {
                if (userAnswers[currentQuestionIndex] !== null) {
                    finishQuiz();
                }
            }
        }

        function previousQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                loadQuiz();
            }
        }

        function showInstantReview(questionIndex) {
            const reviewContent = document.getElementById(`review-content-${questionIndex}`);
            const reviewContainer = document.getElementById(`instant-review-${questionIndex}`);
            
            if (reviewContent.style.display === 'none') {
                reviewContent.style.display = 'block';
                reviewContainer.querySelector('button').innerHTML = currentLanguage === 'ar' ? 
                    '<i class="fas fa-eye-slash"></i> إخفاء المراجعة الفورية' : 
                    '<i class="fas fa-eye-slash"></i> Hide Instant Review';
            } else {
                reviewContent.style.display = 'none';
                reviewContainer.querySelector('button').innerHTML = currentLanguage === 'ar' ? 
                    '<i class="fas fa-eye"></i> عرض المراجعة الفورية لجميع الخيارات' : 
                    '<i class="fas fa-eye"></i> Show Instant Review for All Options';
            }
        }

        // ==================== وظائف البطاقات التعليمية ====================
        function loadFlashcard(index) {
            if (flashcards.length === 0) return;
            
            const card = flashcards[index];
            const flashcardElement = document.getElementById('flashcard');
            
            // إعادة البطاقة إلى وضعها الطبيعي
            flashcardElement.classList.remove('flipped');
            
            // تحديث محتوى الوجه
            document.getElementById('flashcard-front-content').innerHTML = card.front;
            document.getElementById('flashcard-back-content').innerHTML = card.back;
            document.getElementById('flashcard-index').textContent = index + 1;
            document.getElementById('flashcard-back-index').textContent = index + 1;
            
            // تحديث التصنيف
            const categoryText = currentLanguage === 'en' ? 
                card.category.charAt(0).toUpperCase() + card.category.slice(1) :
                getArabicCategory(card.category);
            document.getElementById('flashcard-category').textContent = categoryText;
            document.getElementById('flashcard-back-category').textContent = categoryText;
            
            // تحديث مستوى الإتقان
            const masteryElement = document.getElementById('mastery-level');
            let masteryText = '';
            let masteryClass = '';
            
            if (masteredFlashcards.has(index)) {
                masteryText = currentLanguage === 'en' ? 'Mastered' : 'تم إتقانها';
                masteryClass = 'mastery-expert';
            } else if (reviewFlashcards.has(index)) {
                masteryText = currentLanguage === 'en' ? 'Needs Review' : 'تحتاج مراجعة';
                masteryClass = 'mastery-intermediate';
            } else {
                masteryText = currentLanguage === 'en' ? 'Beginner' : 'مبتدئ';
                masteryClass = 'mastery-beginner';
            }
            
            masteryElement.textContent = masteryText;
            masteryElement.className = `mastery-level ${masteryClass}`;
            
            // تحديث مؤشرات التنقل
            document.getElementById('current-card').textContent = index + 1;
            
            // تحديث شريط التقدم
            const progress = (index / flashcards.length) * 100;
            document.getElementById('flashcard-progress').style.width = `${progress}%`;
            document.getElementById('progress-text').textContent = currentLanguage === 'en' ? 
                `Progress: ${Math.round(progress)}%` : `التقدم: ${Math.round(progress)}%`;
            
            // تحديث زر التنقل السابق/التالي
            document.getElementById('prev-card-btn').disabled = index === 0;
            document.getElementById('next-card-btn').disabled = index === flashcards.length - 1;
        }

        function flipCard() {
            const flashcard = document.getElementById('flashcard');
            flashcard.classList.toggle('flipped');
            playSound('flip');
        }

        function nextCard() {
            if (currentFlashcardIndex < flashcards.length - 1) {
                currentFlashcardIndex++;
                loadFlashcard(currentFlashcardIndex);
                updateNavigationDots();
            }
        }

        function previousCard() {
            if (currentFlashcardIndex > 0) {
                currentFlashcardIndex--;
                loadFlashcard(currentFlashcardIndex);
                updateNavigationDots();
            }
        }

        function markAsMastered(event) {
            event.stopPropagation();
            
            if (masteredFlashcards.has(currentFlashcardIndex)) {
                masteredFlashcards.delete(currentFlashcardIndex);
            } else {
                masteredFlashcards.add(currentFlashcardIndex);
                reviewFlashcards.delete(currentFlashcardIndex);
            }
            
            loadFlashcard(currentFlashcardIndex);
            updateFlashcardStats();
            updateNavigationDots();
        }

        function markForReview(event) {
            event.stopPropagation();
            
            if (reviewFlashcards.has(currentFlashcardIndex)) {
                reviewFlashcards.delete(currentFlashcardIndex);
            } else {
                reviewFlashcards.add(currentFlashcardIndex);
                masteredFlashcards.delete(currentFlashcardIndex);
            }
            
            loadFlashcard(currentFlashcardIndex);
            updateFlashcardStats();
            updateNavigationDots();
        }

        function updateFlashcardStats() {
            const masteredCount = masteredFlashcards.size;
            const reviewCount = reviewFlashcards.size;
            const masteryPercentage = flashcards.length > 0 ? 
                Math.round((masteredCount / flashcards.length) * 100) : 0;
            
            document.getElementById('mastered-cards').textContent = masteredCount;
            document.getElementById('review-cards').textContent = reviewCount;
            document.getElementById('mastery-percentage').textContent = `${masteryPercentage}%`;
        }

        function updateNavigationDots() {
            const dotsContainer = document.getElementById('flashcard-dots');
            dotsContainer.innerHTML = '';
            
            for (let i = 0; i < flashcards.length; i++) {
                const dot = document.createElement('div');
                dot.className = 'nav-dot';
                if (i === currentFlashcardIndex) {
                    dot.classList.add('active');
                }
                
                if (masteredFlashcards.has(i)) {
                    dot.style.background = 'var(--secondary)';
                } else if (reviewFlashcards.has(i)) {
                    dot.style.background = 'var(--tertiary)';
                }
                
                dot.onclick = () => {
                    currentFlashcardIndex = i;
                    loadFlashcard(currentFlashcardIndex);
                    updateNavigationDots();
                };
                
                dotsContainer.appendChild(dot);
            }
        }

        function getArabicCategory(category) {
            switch(category) {
                case 'concepts': return 'مفاهيم';
                case 'definitions': return 'تعريفات';
                case 'qa': return 'سؤال وجواب';
                default: return 'عام';
            }
        }

        function restartFlashcards() {
            currentFlashcardIndex = 0;
            masteredFlashcards.clear();
            reviewFlashcards.clear();
            loadFlashcard(currentFlashcardIndex);
            updateFlashcardStats();
            updateNavigationDots();
        }

        // ==================== وظائف النتائج ====================
        function finishQuiz() {
            clearInterval(timerInterval);

            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;

            document.getElementById("result-box").style.display = "block";
            
            let resultText = currentLanguage === 'en' ? 'Result' : 'النتيجة';
            let percentageText = currentLanguage === 'en' ? 'Percentage' : 'النسبة';
            let evaluationText = currentLanguage === 'en' ? 'Evaluation' : 'التقييم';
            
            document.getElementById("result").innerHTML = `${score.evaluationIcon} ${resultText}: ${score.correct} ${currentLanguage === 'en' ? 'of' : 'من'} ${score.total}`;
            document.getElementById("percentage").innerHTML = `${percentageText}: ${score.percentage}%`;
            document.getElementById("evaluation").innerHTML = `${evaluationText}: ${score.evaluation}`;

            document.getElementById("quiz").style.display = "none";
            document.getElementById("quiz-section").style.display = "none";

            document.getElementById('advanced-results').style.display = 'block';
            updateAdvancedStats(score);
        }

        function calculateScore() {
            let totalCorrect = 0;
            
            userAnswers.forEach((answer, index) => {
                const question = shuffledQuestions[index];
                
                if (question.type === 'fill_blank') {
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

        function updateAdvancedStats(score) {
            const statsContainer = document.getElementById('stats-overview');
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const unansweredCount = questions.length - answeredCount;
            const markedCount = markedQuestions.length;
            
            let scoreText = currentLanguage === 'en' ? 'Score' : 'الدرجة';
            let percentageText = currentLanguage === 'en' ? 'Percentage' : 'النسبة';
            let answeredText = currentLanguage === 'en' ? 'Answered' : 'تم الإجابة';
            let unansweredText = currentLanguage === 'en' ? 'Unanswered' : 'لم تتم الإجابة';
            let flaggedText = currentLanguage === 'en' ? 'Flagged' : 'معلمة';
            
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

        // ==================== وظائف التنقل ====================
        function backToSetup() {
            // إعادة تعيين جميع المتغيرات
            questions = [];
            userAnswers = [];
            answerLocked = [];
            shuffledQuestions = [];
            currentQuestionIndex = 0;
            markedQuestions = [];
            existingQuestions = [];
            currentBatch = 1;
            totalQuestionsGenerated = 0;
            flashcards = [];
            currentFlashcardIndex = 0;
            masteredFlashcards.clear();
            reviewFlashcards.clear();
            retryCount = 0;
            lastRequestTime = 0;
            
            // إزالة الملفات
            if (pdfFile) removePDF();
            if (imageFile) removeImage();
            if (summaryFile) removeSummaryFile();
            if (flashcardsFile) removeFlashcardsFile();
            
            // إعادة تعيين الواجهة
            document.getElementById('result-box').style.display = 'none';
            document.getElementById('advanced-results').style.display = 'none';
            document.getElementById('setup-section').style.display = 'block';
            document.getElementById('quiz-section').style.display = 'none';
            document.getElementById('summary-section').style.display = 'none';
            document.getElementById('flashcards-section-main').style.display = 'none';
            
            // إعادة تعيين الحقول
            document.getElementById('quiz-title').value = '';
            document.getElementById('quiz-topic').value = '';
            document.getElementById('api-key').value = '';
            
            // إعادة تعيين تفاصيل PDF
            const inputs = ['start-page', 'end-page', 'specific-pages', 'units-list', 'topics-list',
                          'summary-start-page', 'summary-end-page', 'summary-specific-pages', 
                          'summary-units-list', 'summary-topics-list',
                          'flashcards-start-page', 'flashcards-end-page', 'flashcards-specific-pages',
                          'flashcards-units-list', 'flashcards-topics-list'];
            
            inputs.forEach(id => {
                const element = document.getElementById(id);
                if (element) element.value = '';
            });
        }

        function restartQuiz() {
            userAnswers = Array(questions.length).fill(null);
            answerLocked = Array(questions.length).fill(false);
            shuffledQuestions = questions.map(q => shuffleOptions(q));
            timeLeft = Math.max(questions.length * 60, 600);
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

        // ==================== وظائف النوافذ المنبثقة ====================
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

        // ==================== وظائف التحميل ====================
        function downloadSummary() {
            const summaryContent = document.getElementById('summary-content').innerText;
            const blob = new Blob([summaryContent], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `summary_${new Date().getTime()}.txt`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        function downloadFlashcards() {
            const flashcardsData = {
                flashcards: flashcards,
                stats: {
                    total: flashcards.length,
                    mastered: masteredFlashcards.size,
                    needsReview: reviewFlashcards.size,
                    masteryPercentage: Math.round((masteredFlashcards.size / flashcards.length) * 100)
                }
            };
            
            const blob = new Blob([JSON.stringify(flashcardsData, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `flashcards_${new Date().getTime()}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        function copyToClipboard(elementId) {
            const element = document.getElementById(elementId);
            const text = element.innerText;
            
            navigator.clipboard.writeText(text).then(() => {
                const copyBtn = document.getElementById(`copy-${elementId}-btn`);
                const originalText = copyBtn.innerHTML;
                copyBtn.innerHTML = currentLanguage === 'ar' ? 
                    '<i class="fas fa-check"></i> تم النسخ!' : 
                    '<i class="fas fa-check"></i> Copied!';
                copyBtn.classList.add('copied');
                
                setTimeout(() => {
                    copyBtn.innerHTML = originalText;
                    copyBtn.classList.remove('copied');
                }, 2000);
            }).catch(err => {
                console.error('Failed to copy: ', err);
            });
        }

        // ==================== التهيئة الأولية ====================
        window.onload = function() {
            checkDarkModePreference();
            
            // إعداد مناطق السحب والإفلات
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

            // إعداد حقل API key
            document.getElementById('api-key').addEventListener('input', function() {
                if (this.value.trim()) {
                    this.style.borderColor = 'var(--secondary)';
                    document.getElementById('api-key-status').style.display = 'none';
                    isAPIKeyValid = false;
                }
            });
            
            // تعيين الصوت الخاطئ افتراضياً
            document.getElementById('wrongSound').src = "https://www.soundjay.com/buttons/button-3.mp3";
        }

        // إغلاق النوافذ المنبثقة عند النقر خارجها
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