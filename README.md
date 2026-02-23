<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#0f172a">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="description" content="Omodudu Predictions - Automated AI Football Analytics for Premier League, La Liga, Bundesliga, Serie A, Ligue 1, Champions League and Europa League">
    <title>Omodudu Predictions - AI Football Analytics</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.4/moment.min.js"></script>
    <style>
        :root {
            --bg-primary: #0a0a0f;
            --bg-secondary: #12121a;
            --bg-tertiary: #1e1e2e;
            --bg-elevated: #252538;
            --accent-primary: #6366f1;
            --accent-secondary: #8b5cf6;
            --accent-success: #10b981;
            --accent-warning: #f59e0b;
            --accent-danger: #ef4444;
            --accent-gold: #fbbf24;
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --text-muted: #64748b;
            --border-subtle: rgba(255, 255, 255, 0.06);
            --gradient-primary: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
            --gradient-success: linear-gradient(135deg, #10b981 0%, #059669 100%);
            --gradient-gold: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            height: 100%;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            overflow: hidden;
            touch-action: manipulation;
        }

        .app-container {
            height: 100vh;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        /* Animated Background */
        .ambient-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            overflow: hidden;
            background: 
                radial-gradient(ellipse 80% 50% at 20% 40%, rgba(99, 102, 241, 0.15), transparent),
                radial-gradient(ellipse 60% 40% at 80% 60%, rgba(139, 92, 246, 0.1), transparent),
                var(--bg-primary);
        }

        .particles {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: rgba(99, 102, 241, 0.4);
            border-radius: 50%;
            animation: float 20s infinite linear;
        }

        @keyframes float {
            from { transform: translateY(100vh) translateX(0); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            to { transform: translateY(-100vh) translateX(100px); opacity: 0; }
        }

        /* Auto-Generation Status Bar */
        .auto-status-bar {
            background: linear-gradient(90deg, rgba(16, 185, 129, 0.1), rgba(99, 102, 241, 0.1));
            border-bottom: 1px solid var(--border-subtle);
            padding: 0.5rem 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-size: 0.75rem;
            flex-shrink: 0;
        }

        .next-gen-timer {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--accent-success);
            font-weight: 600;
        }

        .timer-display {
            font-family: 'Plus Jakarta Sans', monospace;
            font-weight: 800;
            background: rgba(16, 185, 129, 0.2);
            padding: 0.25rem 0.75rem;
            border-radius: 20px;
            border: 1px solid rgba(16, 185, 129, 0.3);
        }

        .last-gen-info {
            color: var(--text-muted);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .pulse-dot {
            width: 8px;
            height: 8px;
            background: var(--accent-success);
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); box-shadow: 0 0 10px var(--accent-success); }
            50% { opacity: 0.6; transform: scale(0.9); }
        }

        /* Header */
        .app-header {
            background: rgba(18, 18, 26, 0.95);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border-subtle);
            padding: 1rem;
            z-index: 100;
            flex-shrink: 0;
        }

        .header-top {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1rem;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .brand-logo {
            width: 44px;
            height: 44px;
            background: var(--gradient-primary);
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            box-shadow: 0 0 40px rgba(99, 102, 241, 0.3);
            position: relative;
            overflow: hidden;
        }

        .brand-logo::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .brand-text h1 {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.35rem;
            font-weight: 800;
            background: linear-gradient(135deg, #fff 0%, #94a3b8 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .brand-text span {
            font-size: 0.7rem;
            color: var(--accent-primary);
            text-transform: uppercase;
            letter-spacing: 0.15em;
            font-weight: 700;
        }

        .header-actions {
            display: flex;
            gap: 0.75rem;
        }

        .icon-btn {
            width: 42px;
            height: 42px;
            border-radius: 12px;
            background: var(--bg-tertiary);
            border: 1px solid var(--border-subtle);
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .icon-btn:active {
            transform: scale(0.95);
            background: var(--accent-primary);
            color: white;
        }

        .notification-badge {
            position: absolute;
            top: -2px;
            right: -2px;
            width: 20px;
            height: 20px;
            background: var(--accent-danger);
            border-radius: 50%;
            font-size: 0.7rem;
            font-weight: 800;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid var(--bg-secondary);
            z-index: 2;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        /* League Navigation */
        .leagues-container {
            position: relative;
        }

        .leagues-scroll {
            display: flex;
            gap: 0.5rem;
            overflow-x: auto;
            padding-bottom: 0.5rem;
            scrollbar-width: none;
            mask-image: linear-gradient(to right, transparent, black 5%, black 95%, transparent);
        }

        .leagues-scroll::-webkit-scrollbar {
            display: none;
        }

        .league-chip {
            flex-shrink: 0;
            padding: 0.625rem 1.25rem;
            background: var(--bg-tertiary);
            border: 1px solid var(--border-subtle);
            border-radius: 24px;
            font-size: 0.8rem;
            font-weight: 600;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            white-space: nowrap;
            position: relative;
            overflow: hidden;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .league-chip:active {
            transform: scale(0.95);
        }

        .league-chip::before {
            content: '';
            position: absolute;
            inset: 0;
            background: var(--gradient-primary);
            opacity: 0;
            transition: opacity 0.3s;
        }

        .league-chip.active {
            color: white;
            border-color: transparent;
            box-shadow: 0 4px 20px rgba(99, 102, 241, 0.4);
        }

        .league-chip.active::before {
            opacity: 1;
        }

        .league-chip span {
            position: relative;
            z-index: 1;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            overflow-y: auto;
            overflow-x: hidden;
            padding: 1rem;
            scroll-behavior: smooth;
        }

        .main-content::-webkit-scrollbar {
            width: 6px;
        }

        .main-content::-webkit-scrollbar-thumb {
            background: var(--bg-tertiary);
            border-radius: 3px;
        }

        /* View Sections */
        .view-section {
            display: none;
            animation: fadeIn 0.4s ease;
        }

        .view-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Auto-Gen Card */
        .auto-gen-card {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.1), rgba(139, 92, 246, 0.05));
            border: 1px solid rgba(99, 102, 241, 0.2);
            border-radius: 20px;
            padding: 1.25rem;
            margin-bottom: 1.5rem;
            position: relative;
            overflow: hidden;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .auto-gen-card:active {
            transform: scale(0.98);
        }

        .auto-gen-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient-primary);
            animation: loadingBar 2s ease-in-out infinite;
        }

        @keyframes loadingBar {
            0% { transform: translateX(-100%); }
            50% { transform: translateX(0); }
            100% { transform: translateX(100%); }
        }

        .auto-gen-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1rem;
        }

        .auto-gen-title {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-weight: 700;
            font-size: 1rem;
        }

        .ai-badge {
            background: var(--gradient-primary);
            color: white;
            padding: 0.25rem 0.75rem;
            border-radius: 20px;
            font-size: 0.7rem;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            animation: glow 2s infinite;
        }

        @keyframes glow {
            0%, 100% { box-shadow: 0 0 5px rgba(99, 102, 241, 0.5); }
            50% { box-shadow: 0 0 20px rgba(99, 102, 241, 0.8); }
        }

        .gen-schedule {
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
        }

        .schedule-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0.75rem;
            background: rgba(255, 255, 255, 0.03);
            border-radius: 12px;
            font-size: 0.875rem;
        }

        .schedule-label {
            color: var(--text-muted);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .schedule-value {
            font-weight: 700;
            color: var(--text-primary);
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        .countdown-timer {
            font-size: 1.25rem;
            color: var(--accent-primary);
            font-weight: 800;
            letter-spacing: 0.05em;
        }

        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .stat-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 1.25rem;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.2);
        }

        .stat-card:active {
            transform: scale(0.98);
            border-color: var(--accent-primary);
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient-primary);
        }

        .stat-card.success::before {
            background: var(--gradient-success);
        }

        .stat-card.gold::before {
            background: var(--gradient-gold);
        }

        .stat-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 0.75rem;
        }

        .stat-label {
            font-size: 0.8rem;
            color: var(--text-muted);
            font-weight: 500;
        }

        .stat-icon {
            width: 36px;
            height: 36px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
            background: rgba(99, 102, 241, 0.1);
            color: var(--accent-primary);
        }

        .stat-card.success .stat-icon {
            background: rgba(16, 185, 129, 0.1);
            color: var(--accent-success);
        }

        .stat-card.gold .stat-icon {
            background: rgba(251, 191, 36, 0.1);
            color: var(--accent-gold);
        }

        .stat-value {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.75rem;
            font-weight: 800;
            color: var(--text-primary);
        }

        .stat-change {
            font-size: 0.75rem;
            color: var(--accent-success);
            font-weight: 600;
        }

        /* Section Headers */
        .section-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1rem;
            margin-top: 1.5rem;
        }

        .section-title {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.125rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .section-title i {
            color: var(--accent-primary);
        }

        .view-all {
            font-size: 0.875rem;
            color: var(--accent-primary);
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.25rem;
            transition: all 0.2s;
            padding: 0.5rem;
            border-radius: 8px;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .view-all:active {
            background: rgba(99, 102, 241, 0.2);
        }

        /* Admin Section */
        .admin-section {
            background: linear-gradient(135deg, rgba(251, 191, 36, 0.08), rgba(245, 158, 11, 0.03));
            border: 1px solid rgba(251, 191, 36, 0.2);
            border-radius: 24px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            position: relative;
        }

        .admin-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient-gold);
        }

        .admin-header {
            display: flex;
            align-items: center;
            gap: 1rem;
            margin-bottom: 1.25rem;
        }

        .admin-icon {
            width: 48px;
            height: 48px;
            background: var(--gradient-gold);
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--bg-primary);
            font-size: 1.5rem;
            box-shadow: 0 4px 20px rgba(251, 191, 36, 0.3);
        }

        .admin-title {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-weight: 800;
            font-size: 1.125rem;
        }

        .admin-subtitle {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .admin-picks {
            display: flex;
            flex-direction: column;
            gap: 0.875rem;
        }

        .admin-pick {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 16px;
            padding: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            -webkit-tap-highlight-color: rgba(251, 191, 36, 0.3);
        }

        .admin-pick:active {
            transform: scale(0.98);
            border-color: var(--accent-gold);
        }

        .admin-pick::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 4px;
            background: var(--gradient-gold);
            opacity: 0;
            transition: opacity 0.3s;
        }

        .admin-pick:active::before {
            opacity: 1;
        }

        .admin-pick-info {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .pick-number {
            width: 36px;
            height: 36px;
            background: var(--gradient-gold);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.875rem;
            font-weight: 800;
            color: var(--bg-primary);
            box-shadow: 0 4px 15px rgba(251, 191, 36, 0.4);
        }

        .pick-details h4 {
            font-size: 0.95rem;
            font-weight: 700;
            margin-bottom: 0.25rem;
        }

        .pick-details span {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .pick-odds {
            text-align: right;
        }

        .pick-odds-value {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-weight: 800;
            font-size: 1.25rem;
            color: var(--accent-gold);
        }

        .pick-confidence {
            font-size: 0.75rem;
            color: var(--text-muted);
            margin-top: 0.25rem;
        }

        /* Featured Card */
        .featured-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 24px;
            overflow: hidden;
            margin-bottom: 1.5rem;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .featured-card:active {
            transform: scale(0.98);
            border-color: var(--accent-primary);
        }

        .featured-header {
            background: var(--gradient-primary);
            padding: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: relative;
        }

        .featured-badge {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.8rem;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .featured-odds {
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
            padding: 0.375rem 1rem;
            border-radius: 20px;
            font-weight: 800;
            font-size: 0.9rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .featured-content {
            padding: 1.5rem;
        }

        .teams-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1.25rem;
        }

        .team-display {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.75rem;
            flex: 1;
        }

        .team-logo-lg {
            width: 64px;
            height: 64px;
            background: var(--bg-tertiary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            border: 3px solid var(--border-subtle);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
        }

        .team-name {
            font-weight: 700;
            font-size: 1rem;
            text-align: center;
        }

        .vs-center {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
            padding: 0 1.5rem;
        }

        .vs-text {
            font-size: 0.875rem;
            color: var(--text-muted);
            font-weight: 800;
            letter-spacing: 0.2em;
        }

        .match-time {
            font-size: 0.875rem;
            color: var(--accent-primary);
            font-weight: 700;
            background: rgba(99, 102, 241, 0.1);
            padding: 0.5rem 1rem;
            border-radius: 20px;
        }

        .prediction-row {
            display: flex;
            gap: 0.75rem;
        }

        .prediction-pill {
            flex: 1;
            background: var(--bg-tertiary);
            border: 1px solid var(--border-subtle);
            border-radius: 16px;
            padding: 1rem;
            text-align: center;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .prediction-pill:active {
            transform: scale(0.95);
            border-color: var(--accent-primary);
            background: rgba(99, 102, 241, 0.1);
        }

        .prediction-label {
            font-size: 0.75rem;
            color: var(--text-muted);
            margin-bottom: 0.375rem;
            text-transform: uppercase;
            font-weight: 700;
            letter-spacing: 0.05em;
        }

        .prediction-odds {
            font-size: 1.25rem;
            font-weight: 800;
            color: var(--text-primary);
        }

        /* Match Cards */
        .matches-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .match-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            overflow: hidden;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .match-card:active {
            transform: scale(0.98);
            border-color: var(--accent-primary);
        }

        .match-header {
            padding: 1rem 1.25rem;
            background: rgba(255, 255, 255, 0.02);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid var(--border-subtle);
        }

        .match-league {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.8rem;
            color: var(--text-muted);
            font-weight: 600;
        }

        .match-status {
            font-size: 0.75rem;
            padding: 0.375rem 0.875rem;
            border-radius: 20px;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .match-status.upcoming {
            background: rgba(99, 102, 241, 0.1);
            color: var(--accent-primary);
        }

        .match-teams {
            padding: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .team-row {
            display: flex;
            align-items: center;
            gap: 1rem;
            flex: 1;
        }

        .team-row.away {
            justify-content: flex-end;
            text-align: right;
        }

        .team-logo {
            width: 44px;
            height: 44px;
            background: var(--bg-tertiary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            flex-shrink: 0;
            border: 2px solid var(--border-subtle);
        }

        .team-info h4 {
            font-size: 0.95rem;
            font-weight: 700;
            margin-bottom: 0.25rem;
        }

        .team-form {
            display: flex;
            gap: 0.25rem;
        }

        .form-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
        }

        .form-dot.w { background: var(--accent-success); box-shadow: 0 0 8px var(--accent-success); }
        .form-dot.d { background: var(--accent-warning); }
        .form-dot.l { background: var(--accent-danger); }

        .match-score {
            text-align: center;
            padding: 0 1.5rem;
        }

        .score-display {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--text-primary);
        }

        .match-time-sm {
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 0.25rem;
        }

        .match-prediction {
            padding: 1rem 1.25rem;
            background: rgba(99, 102, 241, 0.05);
            border-top: 1px solid var(--border-subtle);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .prediction-info {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.875rem;
        }

        .prediction-info i {
            color: var(--accent-primary);
        }

        .prediction-score {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-weight: 700;
            color: var(--accent-primary);
            font-size: 1rem;
        }

        /* Results View */
        .results-header {
            text-align: center;
            padding: 2.5rem 1.5rem;
            background: var(--bg-secondary);
            border-radius: 24px;
            margin-bottom: 1.5rem;
            border: 1px solid var(--border-subtle);
            position: relative;
        }

        .results-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--gradient-success);
        }

        .accuracy-circle {
            width: 140px;
            height: 140px;
            margin: 0 auto 1.5rem;
            position: relative;
        }

        .accuracy-svg {
            transform: rotate(-90deg);
        }

        .accuracy-bg {
            fill: none;
            stroke: var(--bg-tertiary);
            stroke-width: 10;
        }

        .accuracy-progress {
            fill: none;
            stroke: url(#gradientSuccess);
            stroke-width: 10;
            stroke-linecap: round;
            stroke-dasharray: 377;
            stroke-dashoffset: 377;
            transition: stroke-dashoffset 1.5s ease;
        }

        .accuracy-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }

        .accuracy-value {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--accent-success);
        }

        .accuracy-label {
            font-size: 0.875rem;
            color: var(--text-muted);
        }

        .results-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1.5rem;
            margin-top: 2rem;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border-subtle);
        }

        .result-stat {
            text-align: center;
        }

        .result-stat-value {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--text-primary);
        }

        .result-stat-label {
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 0.5rem;
        }

        /* Correct List */
        .correct-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .correct-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 1.25rem;
            display: grid;
            grid-template-columns: auto 1fr auto;
            gap: 1.25rem;
            align-items: center;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(16, 185, 129, 0.3);
        }

        .correct-card:active {
            transform: scale(0.98);
            border-color: var(--accent-success);
        }

        .correct-card::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 4px;
            background: var(--gradient-success);
        }

        .correct-icon {
            width: 56px;
            height: 56px;
            background: rgba(16, 185, 129, 0.1);
            border: 2px solid var(--accent-success);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-success);
            font-size: 1.5rem;
            box-shadow: 0 0 20px rgba(16, 185, 129, 0.2);
        }

        .correct-info h4 {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
        }

        .correct-meta {
            display: flex;
            gap: 1.25rem;
            font-size: 0.8rem;
            color: var(--text-muted);
            flex-wrap: wrap;
        }

        .correct-result {
            text-align: right;
        }

        .predicted-text {
            font-size: 0.875rem;
            color: var(--accent-success);
            font-weight: 700;
            margin-bottom: 0.375rem;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            gap: 0.375rem;
        }

        .score-text {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--text-primary);
        }

        .profit-tag {
            display: inline-flex;
            align-items: center;
            gap: 0.25rem;
            margin-top: 0.5rem;
            padding: 0.5rem 1rem;
            background: rgba(16, 185, 129, 0.15);
            color: var(--accent-success);
            border-radius: 20px;
            font-size: 0.875rem;
            font-weight: 700;
            border: 1px solid rgba(16, 185, 129, 0.3);
        }

        /* Schedule View */
        .schedule-grid {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .schedule-date-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            overflow: hidden;
            transition: all 0.3s;
            cursor: pointer;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .schedule-date-card:active {
            transform: scale(0.98);
            border-color: var(--accent-primary);
        }

        .schedule-date-header {
            padding: 1rem 1.25rem;
            background: var(--bg-tertiary);
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid var(--border-subtle);
        }

        .schedule-date-title {
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .gen-status {
            font-size: 0.75rem;
            padding: 0.375rem 0.875rem;
            border-radius: 20px;
            font-weight: 700;
            text-transform: uppercase;
        }

        .gen-status.completed {
            background: rgba(16, 185, 129, 0.1);
            color: var(--accent-success);
        }

        .gen-status.pending {
            background: rgba(245, 158, 11, 0.1);
            color: var(--accent-warning);
        }

        /* Bottom Navigation */
        .bottom-nav {
            background: rgba(18, 18, 26, 0.98);
            backdrop-filter: blur(20px);
            border-top: 1px solid var(--border-subtle);
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            padding: 0.75rem 0;
            z-index: 100;
            flex-shrink: 0;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.375rem;
            padding: 0.5rem;
            color: var(--text-muted);
            font-size: 0.7rem;
            font-weight: 600;
            transition: all 0.3s;
            cursor: pointer;
            border: none;
            background: none;
            -webkit-tap-highlight-color: rgba(99, 102, 241, 0.3);
        }

        .nav-item:active {
            color: var(--accent-primary);
            transform: scale(0.9);
        }

        .nav-item i {
            font-size: 1.35rem;
            transition: all 0.3s;
        }

        .nav-item.active {
            color: var(--accent-primary);
        }

        .nav-item.active i {
            transform: translateY(-4px);
            filter: drop-shadow(0 4px 8px rgba(99, 102, 241, 0.4));
        }

        /* Loading Overlay */
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 10, 15, 0.95);
            backdrop-filter: blur(20px);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            flex-direction: column;
        }

        .loading-overlay.active {
            display: flex;
        }

        .ai-orb {
            width: 100px;
            height: 100px;
            background: var(--gradient-primary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            color: white;
            animation: orbPulse 2s infinite;
            box-shadow: 0 0 60px rgba(99, 102, 241, 0.5);
            position: relative;
        }

        .ai-orb::before {
            content: '';
            position: absolute;
            inset: -10px;
            border-radius: 50%;
            border: 2px solid rgba(99, 102, 241, 0.3);
            animation: orbRing 2s infinite;
        }

        @keyframes orbPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes orbRing {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(1.5); opacity: 0; }
        }

        .loading-text {
            margin-top: 2rem;
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--text-primary);
        }

        .loading-subtext {
            margin-top: 0.75rem;
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        /* Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            display: none;
            align-items: flex-end;
            justify-content: center;
            z-index: 1500;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--bg-secondary);
            width: 100%;
            max-height: 90vh;
            border-radius: 32px 32px 0 0;
            overflow-y: auto;
            animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }

        .modal-header {
            padding: 1.5rem;
            border-bottom: 1px solid var(--border-subtle);
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: sticky;
            top: 0;
            background: var(--bg-secondary);
            z-index: 10;
        }

        .modal-title {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 1.25rem;
            font-weight: 800;
        }

        .close-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--bg-tertiary);
            border: 1px solid var(--border-subtle);
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s;
            -webkit-tap-highlight-color: rgba(239, 68, 68, 0.3);
        }

        .close-btn:active {
            background: var(--accent-danger);
            color: white;
            transform: rotate(90deg);
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            top: 100px;
            left: 50%;
            transform: translateX(-50%) translateY(-100px);
            background: var(--gradient-success);
            color: white;
            padding: 1rem 2rem;
            border-radius: 50px;
            font-weight: 700;
            z-index: 3000;
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.4);
            transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
            display: flex;
            align-items: center;
            gap: 0.75rem;
            pointer-events: none;
        }

        .toast.show {
            transform: translateX(-50%) translateY(0);
        }

        /* Analysis Content */
        .analysis-content {
            padding: 1.5rem;
        }

        .analysis-factor {
            margin-bottom: 2rem;
        }

        .factor-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1rem;
        }

        .factor-name {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-weight: 700;
            font-size: 1rem;
        }

        .factor-score {
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-weight: 800;
            color: var(--accent-primary);
            font-size: 1.125rem;
        }

        .progress-bar {
            height: 10px;
            background: var(--bg-tertiary);
            border-radius: 5px;
            overflow: hidden;
            position: relative;
        }

        .progress-fill {
            height: 100%;
            border-radius: 5px;
            transition: width 1s ease;
            position: relative;
            overflow: hidden;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shimmer 2s infinite;
        }

        .h2h-list {
            display: flex;
            flex-direction: column;
            gap: 0.875rem;
            margin-top: 1rem;
        }

        .h2h-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1rem;
            background: var(--bg-tertiary);
            border-radius: 12px;
            font-size: 0.9rem;
        }

        .h2h-result {
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-size: 0.875rem;
            font-weight: 800;
        }

        .h2h-result.w {
            background: rgba(16, 185, 129, 0.15);
            color: var(--accent-success);
        }

        .h2h-result.d {
            background: rgba(245, 158, 11, 0.15);
            color: var(--accent-warning);
        }

        .h2h-result.l {
            background: rgba(239, 68, 68, 0.15);
            color: var(--accent-danger);
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 3rem 1.5rem;
            color: var(--text-muted);
        }

        .empty-state i {
            font-size: 4rem;
            margin-bottom: 1rem;
            opacity: 0.5;
        }

        /* Responsive */
        @media (max-width: 380px) {
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .team-logo-lg {
                width: 48px;
                height: 48px;
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="ambient-bg">
        <div class="particles" id="particles"></div>
    </div>
    
    <div class="app-container">
        <!-- Status Bar -->
        <div class="auto-status-bar">
            <div class="next-gen-timer">
                <div class="pulse-dot"></div>
                <span>Next Auto-Gen:</span>
                <div class="timer-display" id="nextGenTimer">11:30:00</div>
            </div>
            <div class="last-gen-info">
                <i class="fas fa-robot"></i>
                <span id="lastGenText">Today 11:30 PM</span>
            </div>
        </div>

        <!-- Header -->
        <header class="app-header">
            <div class="header-top">
                <div class="brand">
                    <div class="brand-logo">
                        <i class="fas fa-brain"></i>
                    </div>
                    <div class="brand-text">
                        <h1>Omodudu</h1>
                        <span>Auto-Predictions Active</span>
                    </div>
                </div>
                <div class="header-actions">
                    <button class="icon-btn" onclick="showNotifications()" aria-label="Notifications">
                        <i class="fas fa-bell"></i>
                        <span class="notification-badge">3</span>
                    </button>
                    <button class="icon-btn" onclick="showSettings()" aria-label="Settings">
                        <i class="fas fa-cog"></i>
                    </button>
                </div>
            </div>
            
            <div class="leagues-container">
                <div class="leagues-scroll" id="leagueScroll">
                    <div class="league-chip active" data-league="all" onclick="selectLeague('all')">
                        <span>🏆</span> All Leagues
                    </div>
                    <div class="league-chip" data-league="epl" onclick="selectLeague('epl')">
                        <span>🏴󠁧󠁢󠁥󠁮󠁧󠁿</span> Premier League
                    </div>
                    <div class="league-chip" data-league="laliga" onclick="selectLeague('laliga')">
                        <span>🇪🇸</span> La Liga
                    </div>
                    <div class="league-chip" data-league="bundesliga" onclick="selectLeague('bundesliga')">
                        <span>🇩🇪</span> Bundesliga
                    </div>
                    <div class="league-chip" data-league="seriea" onclick="selectLeague('seriea')">
                        <span>🇮🇹</span> Serie A
                    </div>
                    <div class="league-chip" data-league="ligue1" onclick="selectLeague('ligue1')">
                        <span>🇫🇷</span> Ligue 1
                    </div>
                    <div class="league-chip" data-league="ucl" onclick="selectLeague('ucl')">
                        <span style="color: #00d4ff;">⭐</span> Champions League
                    </div>
                    <div class="league-chip" data-league="uel" onclick="selectLeague('uel')">
                        <span style="color: #ff6b35;">🛡️</span> Europa League
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="main-content" id="mainContent">
            <!-- Home View -->
            <div id="homeView" class="view-section active">
                <!-- Auto-Gen Info -->
                <div class="auto-gen-card" onclick="showGenInfo()">
                    <div class="auto-gen-header">
                        <div class="auto-gen-title">
                            <i class="fas fa-magic" style="color: var(--accent-primary);"></i>
                            Automated Prediction System
                            <span class="ai-badge">AI v2.0</span>
                        </div>
                        <i class="fas fa-check-circle" style="color: var(--accent-success); font-size: 1.25rem;"></i>
                    </div>
                    <div class="gen-schedule">
                        <div class="schedule-item">
                            <span class="schedule-label">
                                <i class="fas fa-clock"></i>
                                Daily Generation Time
                            </span>
                            <span class="schedule-value">23:30 UTC</span>
                        </div>
                        <div class="schedule-item">
                            <span class="schedule-label">
                                <i class="fas fa-calendar-check"></i>
                                Season Start
                            </span>
                            <span class="schedule-value">24 Feb 2026</span>
                        </div>
                        <div class="schedule-item">
                            <span class="schedule-label">
                                <i class="fas fa-hourglass-half"></i>
                                Time Until Next Gen
                            </span>
                            <span class="countdown-timer" id="mainCountdown">--:--:--</span>
                        </div>
                    </div>
                </div>

                <!-- Stats -->
                <div class="stats-grid">
                    <div class="stat-card" onclick="showStatDetail('accuracy')">
                        <div class="stat-header">
                            <span class="stat-label">Auto-Gen Accuracy</span>
                            <div class="stat-icon">
                                <i class="fas fa-robot"></i>
                            </div>
                        </div>
                        <div class="stat-value" id="autoAccuracy">87.3%</div>
                        <div class="stat-change">AI Optimized</div>
                    </div>
                    <div class="stat-card success" onclick="showStatDetail('correct')">
                        <div class="stat-header">
                            <span class="stat-label">Verified Correct</span>
                            <div class="stat-icon">
                                <i class="fas fa-check-double"></i>
                            </div>
                        </div>
                        <div class="stat-value" id="verifiedCorrect">312</div>
                        <div class="stat-change">+24 this week</div>
                    </div>
                    <div class="stat-card gold" onclick="showStatDetail('roi')">
                        <div class="stat-header">
                            <span class="stat-label">Season ROI</span>
                            <div class="stat-icon">
                                <i class="fas fa-chart-line"></i>
                            </div>
                        </div>
                        <div class="stat-value" id="seasonRoi">+38.5%</div>
                        <div class="stat-change">Top 5%</div>
                    </div>
                    <div class="stat-card" onclick="showStatDetail('streak')">
                        <div class="stat-header">
                            <span class="stat-label">Active Streak</span>
                            <div class="stat-icon">
                                <i class="fas fa-fire-alt"></i>
                            </div>
                        </div>
                        <div class="stat-value" id="activeStreak">12</div>
                        <div class="stat-change">Days Running</div>
                    </div>
                </div>

                <!-- Admin Picks -->
                <div class="admin-section">
                    <div class="admin-header">
                        <div class="admin-icon">
                            <i class="fas fa-crown"></i>
                        </div>
                        <div>
                            <div class="admin-title">Expert Daily Picks</div>
                            <div class="admin-subtitle">Auto-Selected by AI</div>
                        </div>
                    </div>
                    <div class="admin-picks" id="adminPicks">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- Featured Match -->
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fas fa-star"></i>
                        Top AI Prediction
                    </h2>
                    <span class="view-all" onclick="navigateToView('schedule')">
                        View All <i class="fas fa-arrow-right"></i>
                    </span>
                </div>

                <div class="featured-card" id="featuredMatch" onclick="showFeaturedDetail()">
                    <!-- Populated by JS -->
                </div>

                <!-- Today's Matches -->
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fas fa-calendar-day"></i>
                        Today's Predictions
                    </h2>
                    <span class="view-all" onclick="navigateToView('schedule')">
                        Schedule <i class="fas fa-arrow-right"></i>
                    </span>
                </div>

                <div class="matches-list" id="matchesList">
                    <!-- Populated by JS -->
                </div>
            </div>

            <!-- Schedule View -->
            <div id="scheduleView" class="view-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fas fa-calendar-alt"></i>
                        Generation Schedule
                    </h2>
                </div>
                <div class="schedule-grid" id="scheduleGrid">
                    <!-- Populated by JS -->
                </div>
            </div>

            <!-- Analysis View -->
            <div id="analysisView" class="view-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fas fa-microscope"></i>
                        AI Analysis Engine
                    </h2>
                </div>
                <div id="analysisContent">
                    <!-- Dynamic content -->
                </div>
            </div>

            <!-- Results View -->
            <div id="resultsView" class="view-section">
                <div class="results-header">
                    <svg class="accuracy-circle" viewBox="0 0 120 120">
                        <defs>
                            <linearGradient id="gradientSuccess" x1="0%" y1="0%" x2="100%" y2="0%">
                                <stop offset="0%" style="stop-color:#10b981"/>
                                <stop offset="100%" style="stop-color:#059669"/>
                            </linearGradient>
                        </defs>
                        <circle class="accuracy-bg" cx="60" cy="60" r="50"/>
                        <circle class="accuracy-progress" id="accuracyCircle" cx="60" cy="60" r="50"/>
                    </svg>
                    <div class="accuracy-text">
                        <div class="accuracy-value">87%</div>
                        <div class="accuracy-label">Auto-Gen Success Rate</div>
                    </div>
                    
                    <div class="results-stats">
                        <div class="result-stat">
                            <div class="result-stat-value">358</div>
                            <div class="result-stat-label">Total Predictions</div>
                        </div>
                        <div class="result-stat">
                            <div class="result-stat-value">312</div>
                            <div class="result-stat-label">Correct</div>
                        </div>
                        <div class="result-stat">
                            <div class="result-stat-value">+38.5%</div>
                            <div class="result-stat-label">Total ROI</div>
                        </div>
                    </div>
                </div>

                <div class="section-header">
                    <h2 class="section-title">
                        <i class="fas fa-check-circle"></i>
                        Verified Predictions
                    </h2>
                </div>

                <div class="correct-list" id="correctList">
                    <!-- Populated by JS -->
                </div>
            </div>
        </main>

        <!-- Bottom Navigation -->
        <nav class="bottom-nav">
            <button class="nav-item active" onclick="switchTab('home')" data-tab="home" aria-label="Home">
                <i class="fas fa-home"></i>
                <span>Home</span>
            </button>
            <button class="nav-item" onclick="switchTab('schedule')" data-tab="schedule" aria-label="Schedule">
                <i class="fas fa-calendar"></i>
                <span>Schedule</span>
            </button>
            <button class="nav-item" onclick="switchTab('analysis')" data-tab="analysis" aria-label="Analysis">
                <i class="fas fa-chart-pie"></i>
                <span>Analysis</span>
            </button>
            <button class="nav-item" onclick="switchTab('results')" data-tab="results" aria-label="Results">
                <i class="fas fa-trophy"></i>
                <span>Results</span>
            </button>
            <button class="nav-item" onclick="showMoreMenu()" data-tab="more" aria-label="More">
                <i class="fas fa-ellipsis-h"></i>
                <span>More</span>
            </button>
        </nav>
    </div>

    <!-- Loading Overlay -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="ai-orb">
            <i class="fas fa-brain"></i>
        </div>
        <div class="loading-text">AI Generating Predictions</div>
        <div class="loading-subtext" id="loadingSubtext">Analyzing head-to-head data...</div>
    </div>

    <!-- Match Detail Modal -->
    <div class="modal" id="matchModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Match Analysis</h3>
                <button class="close-btn" onclick="closeModal()">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div id="modalBody">
                <!-- Dynamic content -->
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast">
        <i class="fas fa-check-circle"></i>
        <span id="toastMessage">Action completed!</span>
    </div>

    <script>
        // ==========================================
        // DATABASE & CONFIGURATION
        // ==========================================
        const CONFIG = {
            autoGenTime: '23:30',
            timezone: 'UTC',
            seasonStart: '2026-02-24',
            version: '2.0'
        };

        const database = {
            teams: {
                'MCI': { name: 'Man City', league: 'epl', form: ['W', 'W', 'D', 'W', 'W'], fatigue: 0.35, morale: 0.92, xG: 2.1 },
                'ARS': { name: 'Arsenal', league: 'epl', form: ['W', 'W', 'W', 'D', 'W'], fatigue: 0.42, morale: 0.95, xG: 1.9 },
                'LIV': { name: 'Liverpool', league: 'epl', form: ['W', 'D', 'W', 'W', 'L'], fatigue: 0.48, morale: 0.85, xG: 2.0 },
                'MUN': { name: 'Man United', league: 'epl', form: ['L', 'W', 'L', 'D', 'W'], fatigue: 0.55, morale: 0.65, xG: 1.4 },
                'CHE': { name: 'Chelsea', league: 'epl', form: ['D', 'W', 'W', 'L', 'D'], fatigue: 0.45, morale: 0.72, xG: 1.6 },
                'TOT': { name: 'Tottenham', league: 'epl', form: ['W', 'L', 'W', 'W', 'L'], fatigue: 0.52, morale: 0.78, xG: 1.7 },
                'RMA': { name: 'Real Madrid', league: 'laliga', form: ['W', 'W', 'W', 'D', 'W'], fatigue: 0.40, morale: 0.95, xG: 2.0 },
                'BAR': { name: 'Barcelona', league: 'laliga', form: ['W', 'W', 'D', 'W', 'W'], fatigue: 0.38, morale: 0.92, xG: 1.9 },
                'BAY': { name: 'Bayern Munich', league: 'bundesliga', form: ['W', 'W', 'L', 'W', 'W'], fatigue: 0.42, morale: 0.90, xG: 2.2 },
                'BVB': { name: 'Dortmund', league: 'bundesliga', form: ['W', 'D', 'W', 'L', 'W'], fatigue: 0.50, morale: 0.82, xG: 1.8 },
                'INT': { name: 'Inter Milan', league: 'seriea', form: ['W', 'W', 'W', 'D', 'W'], fatigue: 0.45, morale: 0.95, xG: 1.9 },
                'MIL': { name: 'AC Milan', league: 'seriea', form: ['L', 'W', 'D', 'W', 'L'], fatigue: 0.58, morale: 0.68, xG: 1.5 },
                'PSG': { name: 'Paris SG', league: 'ligue1', form: ['W', 'W', 'L', 'W', 'W'], fatigue: 0.42, morale: 0.88, xG: 2.0 }
            },
            
            h2h: {
                'MCI-ARS': [{h: 1, a: 0, date: '2024-03'}, {h: 3, a: 1, date: '2023-10'}, {h: 1, a: 1, date: '2023-04'}, {h: 2, a: 1, date: '2023-01'}],
                'RMA-BAR': [{h: 2, a: 1, date: '2024-01'}, {h: 0, a: 1, date: '2023-10'}, {h: 3, a: 1, date: '2023-03'}, {h: 0, a: 4, date: '2022-10'}],
                'BAY-BVB': [{h: 4, a: 2, date: '2024-01'}, {h: 1, a: 1, date: '2023-11'}, {h: 4, a: 2, date: '2023-04'}, {h: 2, a: 2, date: '2022-10'}],
                'INT-MIL': [{h: 5, a: 1, date: '2024-02'}, {h: 1, a: 0, date: '2023-09'}, {h: 0, a: 1, date: '2023-05'}, {h: 3, a: 0, date: '2022-09'}]
            },
            
            fixtures: [],
            adminPicks: [],
            correctPredictions: [
                {id: 1, home: 'Man City', away: 'Liverpool', predicted: 'Man City Win & Over 2.5', score: '3-1', odds: 2.40, profit: '+14.0', date: '2026-02-23', league: 'epl', autoGen: true},
                {id: 2, home: 'Real Madrid', away: 'Atletico Madrid', predicted: 'Under 2.5 Goals', score: '1-0', odds: 1.90, profit: '+9.0', date: '2026-02-22', league: 'laliga', autoGen: true},
                {id: 3, home: 'Inter Milan', away: 'Juventus', predicted: 'Inter Win', score: '2-0', odds: 2.10, profit: '+11.0', date: '2026-02-21', league: 'seriea', autoGen: true},
                {id: 4, home: 'Bayern Munich', away: 'Leverkusen', predicted: 'BTTS & Over 2.5', score: '2-2', odds: 2.20, profit: '+12.0', date: '2026-02-20', league: 'bundesliga', autoGen: true}
            ]
        };

        // ==========================================
        // AI PREDICTION ENGINE
        // ==========================================
        class OmoduduAI {
            static predictMatch(fixture) {
                const homeTeam = database.teams[fixture.home];
                const awayTeam = database.teams[fixture.away];
                const h2hKey = `${fixture.home}-${fixture.away}`;
                const h2hData = database.h2h[h2hKey] || [];
                
                const homeFatigue = Math.min(0.95, homeTeam.fatigue + (fixture.league !== 'ucl' && fixture.league !== 'uel' ? 0.15 : 0));
                const awayFatigue = Math.min(0.95, awayTeam.fatigue + (fixture.league !== 'ucl' && fixture.league !== 'uel' ? 0.15 : 0));
                
                const homeMorale = this.calculateMorale(homeTeam.form);
                const awayMorale = this.calculateMorale(awayTeam.form);
                
                const h2hWeight = this.analyzeH2H(h2hData);
                
                const homeXg = homeTeam.xG * (1 - homeFatigue * 0.3) * (0.8 + homeMorale * 0.2) * h2hWeight.home;
                const awayXg = awayTeam.xG * (1 - awayFatigue * 0.3) * (0.8 + awayMorale * 0.2) * h2hWeight.away;
                
                const score = this.simulateScore(homeXg, awayXg);
                const total = score.home + score.away;
                
                const markets = this.calculateMarkets(score, total, fixture.odds);
                
                return {
                    score,
                    totalGoals: total,
                    btts: score.home > 0 && score.away > 0,
                    markets: markets.sort((a, b) => b.confidence - a.confidence),
                    confidence: this.calculateConfidence(homeXg, awayXg, h2hData.length),
                    analysis: {
                        homeXg: homeXg.toFixed(2),
                        awayXg: awayXg.toFixed(2),
                        fatigue: { home: Math.round(homeFatigue * 100), away: Math.round(awayFatigue * 100) },
                        morale: { home: Math.round(homeMorale * 100), away: Math.round(awayMorale * 100) },
                        h2h: h2hData,
                        keyFactors: this.extractFactors(homeFatigue, awayFatigue, homeMorale, awayMorale)
                    },
                    generatedAt: new Date().toISOString(),
                    autoGenerated: true
                };
            }
            
            static calculateMorale(form) {
                let score = 0.5;
                form.forEach((result, idx) => {
                    const weight = (idx + 1) / form.length;
                    if (result === 'W') score += 0.12 * weight;
                    else if (result === 'D') score += 0.04 * weight;
                    else score -= 0.10 * weight;
                });
                return Math.max(0.2, Math.min(1.0, score));
            }
            
            static analyzeH2H(h2hData) {
                if (!h2hData.length) return { home: 1.0, away: 1.0 };
                let homeWins = h2hData.filter(m => m.h > m.a).length;
                let awayWins = h2hData.filter(m => m.h < m.a).length;
                const advantage = (homeWins - awayWins) / h2hData.length;
                return { home: 1 + advantage * 0.15, away: 1 - advantage * 0.15 };
            }
            
            static simulateScore(homeXg, awayXg) {
                const poisson = (mean) => {
                    const L = Math.exp(-mean);
                    let p = 1.0, k = 0;
                    do { k++; p *= Math.random(); } while (p > L);
                    return Math.min(4, k - 1);
                };
                return { home: poisson(homeXg), away: poisson(awayXg) };
            }
            
            static calculateMarkets(score, total, odds) {
                const markets = [];
                if (score.home > score.away) markets.push({ type: '1', label: 'Home Win', confidence: 70, odds: odds?.h || 1.80 });
                else if (score.home < score.away) markets.push({ type: '2', label: 'Away Win', confidence: 70, odds: odds?.a || 2.20 });
                else markets.push({ type: 'X', label: 'Draw', confidence: 50, odds: odds?.d || 3.40 });
                
                markets.push({ type: total > 2.5 ? 'Over 2.5' : 'Under 2.5', label: total > 2.5 ? 'Over 2.5 Goals' : 'Under 2.5 Goals', confidence: 65, odds: 1.85 });
                markets.push({ type: 'CS', label: `${score.home}-${score.away}`, confidence: 40, odds: 6.5 });
                return markets;
            }
            
            static calculateConfidence(homeXg, awayXg, h2hCount) {
                return Math.min(95, 60 + Math.abs(homeXg - awayXg) * 8 + Math.min(h2hCount * 2, 10));
            }
            
            static extractFactors(homeF, awayF, homeM, awayM) {
                const factors = [];
                if (homeF > 0.6) factors.push('High fatigue detected for home team');
                if (awayF > 0.6) factors.push('Away team showing signs of tiredness');
                if (homeM > 0.8) factors.push('Home team in excellent form');
                if (awayM > 0.8) factors.push('Away team momentum is strong');
                return factors.length ? factors : ['Competitive fixture expected'];
            }
        }

        // ==========================================
        // APP CONTROLLER
        // ==========================================
        class AppController {
            constructor() {
                this.currentTab = 'home';
                this.currentLeague = 'all';
                this.predictions = new Map();
                this.init();
            }
            
            init() {
                this.createParticles();
                this.startCountdown();
                this.generateDailyPredictions();
                this.renderAll();
            }
            
            createParticles() {
                const container = document.getElementById('particles');
                for (let i = 0; i < 15; i++) {
                    const p = document.createElement('div');
                    p.className = 'particle';
                    p.style.left = Math.random() * 100 + '%';
                    p.style.animationDelay = Math.random() * 20 + 's';
                    p.style.animationDuration = (15 + Math.random() * 10) + 's';
                    container.appendChild(p);
                }
            }
            
            startCountdown() {
                const update = () => {
                    const now = moment();
                    let next = moment().hour(23).minute(30).second(0);
                    if (now.isAfter(next)) next.add(1, 'day');
                    
                    const diff = next.diff(now);
                    const dur = moment.duration(diff);
                    const str = `${String(dur.hours()).padStart(2, '0')}:${String(dur.minutes()).padStart(2, '0')}:${String(dur.seconds()).padStart(2, '0')}`;
                    
                    document.getElementById('nextGenTimer').textContent = str;
                    document.getElementById('mainCountdown').textContent = str;
                };
                update();
                setInterval(update, 1000);
            }
            
            generateDailyPredictions() {
                const today = moment().format('YYYY-MM-DD');
                const fixtures = [
                    {id: 1, home: 'MCI', away: 'ARS', league: 'epl', date: today, time: '16:30', odds: {h: 2.10, d: 3.40, a: 3.50}},
                    {id: 2, home: 'RMA', away: 'BAR', league: 'laliga', date: today, time: '20:00', odds: {h: 2.40, d: 3.50, a: 2.90}},
                    {id: 3, home: 'BAY', away: 'BVB', league: 'bundesliga', date: today, time: '18:30', odds: {h: 1.70, d: 4.20, a: 4.50}},
                    {id: 4, home: 'INT', away: 'MIL', league: 'seriea', date: today, time: '19:45', odds: {h: 2.00, d: 3.40, a: 3.80}},
                    {id: 5, home: 'PSG', away: 'CHE', league: 'ucl', date: today, time: '20:00', odds: {h: 1.90, d: 3.60, a: 4.00}}
                ];
                
                fixtures.forEach(f => {
                    f.prediction = OmoduduAI.predictMatch(f);
                    this.predictions.set(f.id, f);
                });
                
                database.fixtures = fixtures;
                
                database.adminPicks = fixtures
                    .sort((a, b) => b.prediction.confidence - a.prediction.confidence)
                    .slice(0, 3)
                    .map((f, i) => ({
                        id: f.id,
                        match: `${database.teams[f.home].name} vs ${database.teams[f.away].name}`,
                        selection: f.prediction.markets[0].label,
                        odds: f.prediction.markets[0].odds,
                        confidence: Math.round(f.prediction.confidence),
                        league: f.league,
                        rank: i + 1
                    }));
            }
            
            renderAll() {
                this.renderAdminPicks();
                this.renderFeaturedMatch();
                this.renderMatches();
                this.renderCorrectPredictions();
                this.renderSchedule();
            }
            
            renderAdminPicks() {
                const container = document.getElementById('adminPicks');
                container.innerHTML = database.adminPicks.map(pick => `
                    <div class="admin-pick" onclick="showMatchDetail(${pick.id})">
                        <div class="admin-pick-info">
                            <div class="pick-number">${pick.rank}</div>
                            <div class="pick-details">
                                <h4>${pick.match}</h4>
                                <span>${pick.selection} • ${this.getLeagueName(pick.league)}</span>
                            </div>
                        </div>
                        <div class="pick-odds">
                            <div class="pick-odds-value">${pick.odds}</div>
                            <div class="pick-confidence">${pick.confidence}% confidence</div>
                        </div>
                    </div>
                `).join('');
            }
            
            renderFeaturedMatch() {
                const featured = database.fixtures[0];
                if (!featured) return;
                
                const pred = featured.prediction;
                const home = database.teams[featured.home];
                const away = database.teams[featured.away];
                
                document.getElementById('featuredMatch').innerHTML = `
                    <div class="featured-header">
                        <div class="featured-badge">
                            <i class="fas fa-robot"></i>
                            AI PICK #1
                        </div>
                        <div class="featured-odds">${Math.round(pred.confidence)}% Confidence</div>
                    </div>
                    <div class="featured-content">
                        <div class="teams-row">
                            <div class="team-display">
                                <div class="team-logo-lg">${home.name[0]}</div>
                                <div class="team-name">${home.name}</div>
                            </div>
                            <div class="vs-center">
                                <div class="vs-text">VS</div>
                                <div class="match-time">${featured.time}</div>
                            </div>
                            <div class="team-display">
                                <div class="team-logo-lg">${away.name[0]}</div>
                                <div class="team-name">${away.name}</div>
                            </div>
                        </div>
                        <div class="prediction-row">
                            <div class="prediction-pill" onclick="event.stopPropagation(); showToast('Score prediction copied!')">
                                <div class="prediction-label">Predicted Score</div>
                                <div class="prediction-odds">${pred.score.home}-${pred.score.away}</div>
                            </div>
                            <div class="prediction-pill" onclick="event.stopPropagation(); showToast('Best bet copied!')">
                                <div class="prediction-label">Best Market</div>
                                <div class="prediction-odds">${pred.markets[0].type}</div>
                            </div>
                            <div class="prediction-pill" onclick="event.stopPropagation(); showToast('Total goals copied!')">
                                <div class="prediction-label">Total Goals</div>
                                <div class="prediction-odds">${pred.totalGoals}</div>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            renderMatches() {
                const container = document.getElementById('matchesList');
                let fixtures = database.fixtures;
                
                if (this.currentLeague !== 'all') {
                    fixtures = fixtures.filter(f => f.league === this.currentLeague);
                }
                
                container.innerHTML = fixtures.map(f => {
                    const pred = f.prediction;
                    const home = database.teams[f.home];
                    const away = database.teams[f.away];
                    
                    return `
                        <div class="match-card" onclick="showMatchDetail(${f.id})">
                            <div class="match-header">
                                <div class="match-league">
                                    <i class="fas fa-robot"></i>
                                    ${this.getLeagueName(f.league)} • ${f.date}
                                </div>
                                <span class="match-status upcoming">${f.time}</span>
                            </div>
                            <div class="match-teams">
                                <div class="team-row">
                                    <div class="team-logo">${home.name[0]}</div>
                                    <div class="team-info">
                                        <h4>${home.name}</h4>
                                        <div class="team-form">
                                            ${home.form.slice(-3).map(r => `<span class="form-dot ${r.toLowerCase()}"></span>`).join('')}
                                        </div>
                                    </div>
                                </div>
                                <div class="match-score">
                                    <div class="score-display">VS</div>
                                    <div class="match-time-sm">AI: ${pred.score.home}-${pred.score.away}</div>
                                </div>
                                <div class="team-row away">
                                    <div class="team-info">
                                        <h4>${away.name}</h4>
                                        <div class="team-form">
                                            ${away.form.slice(-3).map(r => `<span class="form-dot ${r.toLowerCase()}"></span>`).join('')}
                                        </div>
                                    </div>
                                    <div class="team-logo">${away.name[0]}</div>
                                </div>
                            </div>
                            <div class="match-prediction">
                                <div class="prediction-info">
                                    <i class="fas fa-check-circle"></i>
                                    <span>${pred.markets[0].label}</span>
                                </div>
                                <div class="prediction-score">${pred.totalGoals} Goals Expected</div>
                            </div>
                        </div>
                    `;
                }).join('');
            }
            
            renderCorrectPredictions() {
                const container = document.getElementById('correctList');
                container.innerHTML = database.correctPredictions.map(c => `
                    <div class="correct-card" onclick="showCorrectDetail(${c.id})">
                        <div class="correct-icon">
                            <i class="fas fa-check"></i>
                        </div>
                        <div class="correct-info">
                            <h4>${c.home} vs ${c.away}</h4>
                            <div class="correct-meta">
                                <span><i class="far fa-calendar"></i> ${c.date}</span>
                                <span><i class="fas fa-tag"></i> ${c.predicted}</span>
                            </div>
                        </div>
                        <div class="correct-result">
                            <div class="predicted-text">
                                <i class="fas fa-check-circle"></i> Verified
                            </div>
                            <div class="score-text">${c.score}</div>
                            <span class="profit-tag"><i class="fas fa-arrow-up"></i> ${c.profit}</span>
                        </div>
                    </div>
                `).join('');
                
                setTimeout(() => {
                    const circle = document.getElementById('accuracyCircle');
                    if (circle) circle.style.strokeDashoffset = '49';
                }, 500);
            }
            
            renderSchedule() {
                const container = document.getElementById('scheduleGrid');
                const dates = [];
                for (let i = 0; i < 7; i++) dates.push(moment().add(i, 'days'));
                
                container.innerHTML = dates.map((date, i) => {
                    const isToday = i === 0;
                    return `
                        <div class="schedule-date-card" onclick="showDateDetail('${date.format('YYYY-MM-DD')}')">
                            <div class="schedule-date-header">
                                <div class="schedule-date-title">
                                    <i class="fas fa-calendar-day"></i>
                                    ${isToday ? 'Today' : date.format('dddd, MMM D')}
                                </div>
                                <span class="gen-status ${isToday ? 'pending' : 'completed'}">
                                    ${isToday ? 'Scheduled' : 'Completed'}
                                </span>
                            </div>
                            <div style="padding: 1rem;">
                                <div style="display: flex; align-items: center; gap: 0.75rem; color: var(--text-muted); font-size: 0.875rem;">
                                    <i class="fas fa-clock"></i>
                                    <span>Auto-Generation: 11:30 PM</span>
                                </div>
                                ${isToday ? '<div style="margin-top: 0.75rem; padding: 0.75rem; background: rgba(99, 102, 241, 0.1); border-radius: 8px; font-size: 0.875rem; color: var(--accent-primary);"><i class="fas fa-robot"></i> Predictions Ready</div>' : ''}
                            </div>
                        </div>
                    `;
                }).join('');
            }
            
            getLeagueName(code) {
                const names = {
                    'epl': 'Premier League', 'laliga': 'La Liga', 'bundesliga': 'Bundesliga',
                    'seriea': 'Serie A', 'ligue1': 'Ligue 1', 'ucl': 'Champions League', 'uel': 'Europa League'
                };
                return names[code] || code.toUpperCase();
            }
        }

        // ==========================================
        // GLOBAL FUNCTIONS
        // ==========================================
        const app = new AppController();

        function switchTab(tabName) {
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
                if (item.dataset.tab === tabName) item.classList.add('active');
            });
            
            document.querySelectorAll('.view-section').forEach(view => view.classList.remove('active'));
            document.getElementById(tabName + 'View').classList.add('active');
            
            app.currentTab = tabName;
            
            if (tabName === 'schedule') app.renderSchedule();
            if (tabName === 'results') app.renderCorrectPredictions();
            if (tabName === 'analysis') renderAnalysis();
        }

        function selectLeague(league) {
            app.currentLeague = league;
            
            document.querySelectorAll('.league-chip').forEach(chip => {
                chip.classList.remove('active');
                if (chip.dataset.league === league) chip.classList.add('active');
            });
            
            app.renderMatches();
            showToast(`${app.getLeagueName(league)} selected`);
        }

        function showMatchDetail(matchId) {
            const match = app.predictions.get(matchId);
            if (!match) return;
            
            const pred = match.prediction;
            const home = database.teams[match.home];
            const away = database.teams[match.away];
            
            document.getElementById('modalBody').innerHTML = `
                <div class="analysis-content">
                    <div style="text-align: center; margin-bottom: 2rem;">
                        <h2 style="font-family: Plus Jakarta Sans; font-size: 1.5rem; margin-bottom: 0.5rem;">
                            ${home.name} vs ${away.name}
                        </h2>
                        <p style="color: var(--text-muted);">${match.date} • ${match.time}</p>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem; margin-bottom: 2rem;">
                        ${pred.markets.slice(0, 3).map((m, i) => `
                            <div style="background: ${i === 0 ? 'rgba(99, 102, 241, 0.1)' : 'var(--bg-tertiary)'}; padding: 1rem; border-radius: 16px; text-align: center; border: ${i === 0 ? '1px solid var(--accent-primary)' : '1px solid transparent'}; cursor: pointer;" onclick="showToast('${m.label} copied!')">
                                <div style="font-size: 0.75rem; color: var(--text-muted); margin-bottom: 0.25rem;">${m.label}</div>
                                <div style="font-weight: 800; font-size: 1.125rem; color: ${i === 0 ? 'var(--accent-primary)' : 'var(--text-primary)'};">${m.type === 'CS' ? m.label : m.type}</div>
                                <div style="font-size: 0.75rem; color: var(--accent-success); margin-top: 0.25rem;">${Math.round(m.confidence)}%</div>
                            </div>
                        `).join('')}
                    </div>
                    
                    <div class="analysis-factor">
                        <div class="factor-header">
                            <span class="factor-name">
                                <i class="fas fa-battery-half" style="color: var(--accent-warning);"></i>
                                Fatigue Analysis
                            </span>
                            <span class="factor-score">${pred.analysis.fatigue.home}% / ${pred.analysis.fatigue.away}%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${pred.analysis.fatigue.home}%; background: var(--accent-warning);"></div>
                        </div>
                    </div>
                    
                    <div class="analysis-factor">
                        <div class="factor-header">
                            <span class="factor-name">
                                <i class="fas fa-smile" style="color: var(--accent-success);"></i>
                                Morale & Momentum
                            </span>
                            <span class="factor-score">${pred.analysis.morale.home}% / ${pred.analysis.morale.away}%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${pred.analysis.morale.home}%; background: var(--accent-success);"></div>
                        </div>
                    </div>
                    
                    <div class="analysis-factor">
                        <div class="factor-header">
                            <span class="factor-name">
                                <i class="fas fa-history" style="color: var(--accent-primary);"></i>
                                Head-to-Head
                            </span>
                            <span class="factor-score">${pred.analysis.h2h.length} matches</span>
                        </div>
                        <div class="h2h-list">
                            ${pred.analysis.h2h.length ? pred.analysis.h2h.map(h => `
                                <div class="h2h-item">
                                    <span>${h.date}</span>
                                    <span class="h2h-result ${h.h > h.a ? 'w' : h.h < h.a ? 'l' : 'd'}">${h.h}-${h.a}</span>
                                </div>
                            `).join('') : '<p style="color: var(--text-muted);">No recent data</p>'}
                        </div>
                    </div>
                    
                    <div style="background: rgba(251, 191, 36, 0.1); border: 1px solid rgba(251, 191, 36, 0.2); border-radius: 12px; padding: 1rem; margin-top: 1.5rem;">
                        <div style="font-weight: 700; margin-bottom: 0.5rem; color: var(--accent-gold);">
                            <i class="fas fa-key"></i> Key Factors
                        </div>
                        <ul style="list-style: none; font-size: 0.875rem; color: var(--text-secondary);">
                            ${pred.analysis.keyFactors.map(f => `<li style="margin-bottom: 0.5rem;"><i class="fas fa-check" style="color: var(--accent-success); margin-right: 0.5rem;"></i>${f}</li>`).join('')}
                        </ul>
                    </div>
                    
                    <button style="width: 100%; padding: 1rem; background: var(--gradient-primary); border: none; border-radius: 12px; color: white; font-weight: 700; font-size: 1rem; margin-top: 1.5rem; cursor: pointer;" onclick="closeModal()">
                        Close Analysis
                    </button>
                </div>
            `;
            
            document.getElementById('matchModal').classList.add('active');
        }

        function showFeaturedDetail() {
            showMatchDetail(database.fixtures[0].id);
        }

        function showCorrectDetail(id) {
            showToast('Viewing verified prediction');
        }

        function showDateDetail(date) {
            showToast(`Schedule: ${date}`);
        }

        function renderAnalysis() {
            document.getElementById('analysisContent').innerHTML = `
                <div class="analysis-content">
                    <div class="analysis-factor">
                        <div class="factor-header">
                            <span class="factor-name"><i class="fas fa-robot" style="color: var(--accent-primary);"></i> AI Engine Status</span>
                            <span class="factor-score">Active</span>
                        </div>
                        <div style="padding: 1rem; background: var(--bg-tertiary); border-radius: 12px;">
                            <p style="color: var(--text-secondary); margin-bottom: 1rem;">The Omodudu AI engine analyzes:</p>
                            <ul style="list-style: none; color: var(--text-muted); font-size: 0.875rem;">
                                <li style="margin-bottom: 0.5rem;"><i class="fas fa-check" style="color: var(--accent-success); margin-right: 0.5rem;"></i>Fatigue metrics from previous matches</li>
                                <li style="margin-bottom: 0.5rem;"><i class="fas fa-check" style="color: var(--accent-success); margin-right: 0.5rem;"></i>Morale based on recent form (W/D/L)</li>
                                <li style="margin-bottom: 0.5rem;"><i class="fas fa-check" style="color: var(--accent-success); margin-right: 0.5rem;"></i>Head-to-head historical data</li>
                                <li><i class="fas fa-check" style="color: var(--accent-success); margin-right: 0.5rem;"></i>Expected Goals (xG) calculation</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="analysis-factor">
                        <div class="factor-header">
                            <span class="factor-name"><i class="fas fa-clock" style="color: var(--accent-warning);"></i> Daily Schedule</span>
                        </div>
                        <p style="color: var(--text-secondary); line-height: 1.6;">
                            Predictions are automatically generated every day at <strong>11:30 PM UTC</strong> for all configured leagues.
                        </p>
                    </div>
                </div>
            `;
        }

        function closeModal() {
            document.getElementById('matchModal').classList.remove('active');
        }

        function showToast(message) {
            const toast = document.getElementById('toast');
            document.getElementById('toastMessage').textContent = message;
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), 3000);
        }

        function showNotifications() {
            showToast('3 new predictions available!');
        }

        function showSettings() {
            showToast('Settings: Auto-gen at 23:30 UTC');
        }

        function showGenInfo() {
            showToast('Auto-generation active since 24 Feb 2026');
        }

        function showStatDetail(type) {
            const messages = {
                'accuracy': 'AI Accuracy: 87.3% - Based on 358 predictions',
                'correct': '312 correct predictions this season',
                'roi': 'Return on Investment: +38.5%',
                'streak': 'Current winning streak: 12 days'
            };
            showToast(messages[type]);
        }

        function navigateToView(view) {
            switchTab(view);
        }

        function showMoreMenu() {
            showToast('More options coming soon!');
        }

        // Close modal on outside click
        document.getElementById('matchModal').addEventListener('click', (e) => {
            if (e.target === e.currentTarget) closeModal();
        });

        // Prevent double-tap zoom
        document.addEventListener('dblclick', (e) => e.preventDefault());
    </script>
</body>
</html>
