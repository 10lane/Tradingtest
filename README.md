<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil Trading - Questionnaire Psychologique</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-primary: #0a0e1a;
            --bg-secondary: #141827;
            --bg-card: #1a1f35;
            --accent-gold: #f4b942;
            --accent-blue: #3b82f6;
            --accent-red: #ef4444;
            --accent-green: #10b981;
            --text-primary: #ffffff;
            --text-secondary: #94a3b8;
            --border: rgba(255, 255, 255, 0.1);
        }

        body {
            font-family: 'Space Mono', monospace;
            background: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(circle at 20% 30%, rgba(244, 185, 66, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(59, 130, 246, 0.08) 0%, transparent 50%);
            pointer-events: none;
            z-index: 0;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }

        .header {
            text-align: center;
            margin-bottom: 60px;
            animation: fadeInDown 0.8s ease-out;
        }

        .logo {
            font-family: 'Syne', sans-serif;
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--accent-gold) 0%, var(--accent-blue) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
            letter-spacing: -2px;
        }

        .subtitle {
            font-size: 1.1rem;
            color: var(--text-secondary);
            font-weight: 400;
        }

        .progress-container {
            background: var(--bg-secondary);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 40px;
            border: 1px solid var(--border);
            animation: fadeIn 0.8s ease-out 0.2s both;
        }

        .progress-text {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            font-size: 0.9rem;
            color: var(--text-secondary);
        }

        .progress-bar-bg {
            height: 8px;
            background: var(--bg-card);
            border-radius: 20px;
            overflow: hidden;
            position: relative;
        }

        .progress-bar-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--accent-gold), var(--accent-blue));
            border-radius: 20px;
            transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 0 20px rgba(244, 185, 66, 0.4);
        }

        .question-card {
            background: var(--bg-secondary);
            border-radius: 20px;
            padding: 40px;
            border: 1px solid var(--border);
            margin-bottom: 30px;
            animation: slideInUp 0.6s ease-out;
            position: relative;
            overflow: hidden;
        }

        .question-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--accent-gold), var(--accent-blue));
        }

        .question-number {
            display: inline-block;
            background: var(--bg-card);
            color: var(--accent-gold);
            padding: 8px 18px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 700;
            margin-bottom: 20px;
            border: 1px solid var(--border);
        }

        .question-text {
            font-family: 'Syne', sans-serif;
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 30px;
            color: var(--text-primary);
            line-height: 1.4;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .option {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 15px;
            padding: 20px 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 15px;
            position: relative;
        }

        .option:hover {
            border-color: var(--accent-gold);
            background: rgba(244, 185, 66, 0.05);
            transform: translateX(5px);
        }

        .option.selected {
            border-color: var(--accent-gold);
            background: rgba(244, 185, 66, 0.1);
            box-shadow: 0 0 20px rgba(244, 185, 66, 0.2);
        }

        .option-letter {
            width: 45px;
            height: 45px;
            border-radius: 12px;
            background: var(--bg-secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 1.1rem;
            color: var(--text-secondary);
            flex-shrink: 0;
            border: 1px solid var(--border);
        }

        .option.selected .option-letter {
            background: var(--accent-gold);
            color: var(--bg-primary);
            border-color: var(--accent-gold);
        }

        .option-text {
            flex: 1;
            font-size: 1rem;
        }

        .navigation {
            display: flex;
            justify-content: space-between;
            gap: 20px;
            margin-top: 40px;
        }

        .btn {
            padding: 18px 35px;
            border: none;
            border-radius: 15px;
            font-family: 'Space Mono', monospace;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--accent-gold), #ffd369);
            color: var(--bg-primary);
            flex: 1;
        }

        .btn-primary:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(244, 185, 66, 0.4);
        }

        .btn-primary:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn-secondary {
            background: var(--bg-card);
            color: var(--text-primary);
            border: 2px solid var(--border);
        }

        .btn-secondary:hover {
            border-color: var(--accent-gold);
            background: rgba(244, 185, 66, 0.05);
        }

        .result-card {
            background: var(--bg-secondary);
            border-radius: 20px;
            padding: 50px;
            border: 1px solid var(--border);
            text-align: center;
            animation: fadeIn 0.8s ease-out;
        }

        .result-score {
            font-family: 'Syne', sans-serif;
            font-size: 5rem;
            font-weight: 800;
            margin: 30px 0;
            background: linear-gradient(135deg, var(--accent-gold), var(--accent-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .result-badge {
            display: inline-block;
            padding: 12px 30px;
            border-radius: 30px;
            font-weight: 700;
            margin-bottom: 20px;
            font-size: 1.1rem;
        }

        .badge-red {
            background: rgba(239, 68, 68, 0.2);
            color: var(--accent-red);
            border: 2px solid var(--accent-red);
        }

        .badge-orange {
            background: rgba(251, 146, 60, 0.2);
            color: #fb923c;
            border: 2px solid #fb923c;
        }

        .badge-green {
            background: rgba(16, 185, 129, 0.2);
            color: var(--accent-green);
            border: 2px solid var(--accent-green);
        }

        .badge-blue {
            background: rgba(59, 130, 246, 0.2);
            color: var(--accent-blue);
            border: 2px solid var(--accent-blue);
        }

        .result-title {
            font-family: 'Syne', sans-serif;
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 30px;
        }

        .result-content {
            text-align: left;
            background: var(--bg-card);
            padding: 35px;
            border-radius: 15px;
            margin-top: 30px;
            border: 1px solid var(--border);
        }

        .result-section {
            margin-bottom: 25px;
        }

        .result-section:last-child {
            margin-bottom: 0;
        }

        .result-section-title {
            font-weight: 700;
            color: var(--accent-gold);
            margin-bottom: 10px;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .result-section-content {
            color: var(--text-secondary);
            line-height: 1.8;
        }

        .result-disclaimer {
            margin-top: 30px;
            padding: 25px;
            background: rgba(244, 185, 66, 0.05);
            border-radius: 15px;
            border: 1px solid rgba(244, 185, 66, 0.2);
            font-size: 0.95rem;
            color: var(--text-secondary);
            line-height: 1.8;
        }

        .btn-restart {
            margin-top: 30px;
            background: var(--bg-card);
            color: var(--text-primary);
            border: 2px solid var(--accent-gold);
        }

        .btn-restart:hover {
            background: rgba(244, 185, 66, 0.1);
            transform: translateY(-2px);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 768px) {
            .logo {
                font-size: 2rem;
            }

            .question-card {
                padding: 25px;
            }

            .question-text {
                font-size: 1.2rem;
            }

            .result-card {
                padding: 30px 20px;
            }

            .result-score {
                font-size: 3.5rem;
            }

            .result-title {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        const questions = [
            {
                id: 1,
                text: "Combien de temps peux-tu rester devant un graphique sans trader ?",
                options: [
                    { letter: "A", text: "Moins de 10 minutes", points: 1 },
                    { letter: "B", text: "10 à 30 minutes", points: 2 },
                    { letter: "C", text: "30 à 60 minutes", points: 3 },
                    { letter: "D", text: "Plus d'1 heure", points: 4 }
                ]
            },
            {
                id: 2,
                text: "Préfères-tu attendre une opportunité claire ou entrer rapidement ?",
                options: [
                    { letter: "A", text: "Entrer rapidement", points: 1 },
                    { letter: "B", text: "Dépend du contexte", points: 2 },
                    { letter: "C", text: "Attendre une confirmation", points: 3 },
                    { letter: "D", text: "Attendre longtemps", points: 4 }
                ]
            },
            {
                id: 3,
                text: "Après un trade perdant, quelle est ta réaction ?",
                options: [
                    { letter: "A", text: "Reprendre un trade rapidement", points: 1 },
                    { letter: "B", text: "Réduire légèrement le risque", points: 2 },
                    { letter: "C", text: "Faire une pause", points: 3 },
                    { letter: "D", text: "Analyser avant toute décision", points: 4 }
                ]
            },
            {
                id: 4,
                text: "Une série de pertes te pousse à :",
                options: [
                    { letter: "A", text: "Augmenter le risque", points: 1 },
                    { letter: "B", text: "Continuer normalement", points: 2 },
                    { letter: "C", text: "Réduire les trades", points: 3 },
                    { letter: "D", text: "Arrêter temporairement", points: 4 }
                ]
            },
            {
                id: 5,
                text: "As-tu déjà enfreint ton plan volontairement ?",
                options: [
                    { letter: "A", text: "Très souvent", points: 1 },
                    { letter: "B", text: "Parfois", points: 2 },
                    { letter: "C", text: "Rarement", points: 3 },
                    { letter: "D", text: "Presque jamais", points: 4 }
                ]
            },
            {
                id: 6,
                text: "Que ressens-tu face à des règles strictes ?",
                options: [
                    { letter: "A", text: "Frustration", points: 1 },
                    { letter: "B", text: "Neutralité", points: 2 },
                    { letter: "C", text: "Sécurité", points: 3 },
                    { letter: "D", text: "Confort", points: 4 }
                ]
            },
            {
                id: 7,
                text: "Quand le marché va contre toi :",
                options: [
                    { letter: "A", text: "Urgence", points: 1 },
                    { letter: "B", text: "Nervosité", points: 2 },
                    { letter: "C", text: "Concentration", points: 3 },
                    { letter: "D", text: "Détachement", points: 4 }
                ]
            },
            {
                id: 8,
                text: "Ton niveau de stress en trading est :",
                options: [
                    { letter: "A", text: "Très élevé", points: 1 },
                    { letter: "B", text: "Variable", points: 2 },
                    { letter: "C", text: "Modéré", points: 3 },
                    { letter: "D", text: "Faible", points: 4 }
                ]
            },
            {
                id: 9,
                text: "Tu préfères :",
                options: [
                    { letter: "A", text: "Beaucoup d'actions", points: 1 },
                    { letter: "B", text: "Quelques opportunités", points: 2 },
                    { letter: "C", text: "Peu mais précises", points: 3 },
                    { letter: "D", text: "Très peu de décisions", points: 4 }
                ]
            },
            {
                id: 10,
                text: "Horizon de trading préféré :",
                options: [
                    { letter: "A", text: "Minutes", points: 1 },
                    { letter: "B", text: "Intra-day", points: 2 },
                    { letter: "C", text: "Plusieurs heures", points: 3 },
                    { letter: "D", text: "Plusieurs jours", points: 4 }
                ]
            },
            {
                id: 11,
                text: "Tu te considères comme :",
                options: [
                    { letter: "A", text: "Impulsif", points: 1 },
                    { letter: "B", text: "Réactif", points: 2 },
                    { letter: "C", text: "Réfléchi", points: 3 },
                    { letter: "D", text: "Très patient", points: 4 }
                ]
            },
            {
                id: 12,
                text: "Ton objectif principal :",
                options: [
                    { letter: "A", text: "L'action", points: 1 },
                    { letter: "B", text: "Gains rapides", points: 2 },
                    { letter: "C", text: "Régularité", points: 3 },
                    { letter: "D", text: "Stabilité long terme", points: 4 }
                ]
            }
        ];

        function getProfileResult(score) {
            if (score >= 12 && score <= 20) {
                return {
                    badge: "Profil Impulsif",
                    badgeClass: "badge-red",
                    title: "🔴 Profil Impulsif",
                    style: "Day trading très encadré",
                    interdiction: "Scalping libre, levier élevé",
                    recommendations: "Votre profil psychologique montre une tendance à l'action rapide et à l'impulsivité. Il est crucial d'adopter un cadre strict avec des règles précises pour canaliser cette énergie de manière productive."
                };
            } else if (score >= 21 && score <= 30) {
                return {
                    badge: "Profil Intermédiaire",
                    badgeClass: "badge-orange",
                    title: "🟠 Profil Intermédiaire",
                    style: "Day trading M15–H1",
                    focus: "Règles, patience, max trades/jour",
                    recommendations: "Vous disposez d'un équilibre entre action et réflexion. En développant votre patience et en respectant des limites claires, vous pouvez devenir un trader performant sur des timeframes moyens."
                };
            } else if (score >= 31 && score <= 40) {
                return {
                    badge: "Profil Rationnel",
                    badgeClass: "badge-green",
                    title: "🟢 Profil Rationnel",
                    style: "SMC / ICT",
                    focus: "Trading mécanique, journal obligatoire",
                    recommendations: "Votre approche réfléchie et méthodique est idéale pour les stratégies avancées. En maintenant une discipline stricte et en documentant chaque trade, vous maximiserez vos chances de succès."
                };
            } else {
                return {
                    badge: "Profil Patient",
                    badgeClass: "badge-blue",
                    title: "🔵 Profil Patient",
                    style: "Swing trading",
                    timeframes: "H4–Daily",
                    recommendations: "Votre patience exceptionnelle et votre détachement émotionnel sont des atouts majeurs. Le swing trading sur des timeframes longs vous permettra d'exploiter pleinement ces qualités."
                };
            }
        }

        function TradingQuiz() {
            const [currentQuestion, setCurr
