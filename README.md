<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plano de Corrida - 5km e 10km</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
            font-size: 16px;
        }

        .controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }

        .btn {
            background: white;
            border: none;
            padding: 15px;
            border-radius: 10px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-primary {
            background: #10b981;
            color: white;
        }

        .btn-secondary {
            background: #3b82f6;
            color: white;
        }

        .filter-section {
            background: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .filter-section label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #374151;
        }

        .filter-section select {
            width: 100%;
            padding: 10px;
            border: 2px solid #e5e7eb;
            border-radius: 8px;
            font-size: 14px;
        }

        .stats {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            text-align: center;
        }

        .stat {
            padding: 10px;
        }

        .stat-number {
            font-size: 32px;
            font-weight: bold;
            color: #667eea;
        }

        .stat-label {
            font-size: 12px;
            color: #6b7280;
            margin-top: 5px;
        }

        .workout-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            transition: transform 0.2s;
        }

        .workout-card.completed {
            background: #f0fdf4;
            border: 2px solid #10b981;
        }

        .workout-header {
            display: flex;
            align-items: flex-start;
            margin-bottom: 15px;
        }

        .checkbox-wrapper {
            margin-right: 15px;
            padding-top: 2px;
        }

        .checkbox {
            width: 24px;
            height: 24px;
            cursor: pointer;
            accent-color: #10b981;
        }

        .workout-info {
            flex: 1;
        }

        .workout-meta {
            font-size: 12px;
            color: #6b7280;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .workout-name {
            font-size: 18px;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 8px;
        }

        .workout-description {
            font-size: 14px;
            color: #4b5563;
            line-height: 1.5;
            margin-bottom: 12px;
        }

        .workout-intervals {
            background: #f9fafb;
            border-radius: 8px;
            padding: 12px;
            margin-top: 12px;
        }

        .interval-title {
            font-size: 13px;
            font-weight: 600;
            color: #374151;
            margin-bottom: 8px;
        }

        .interval-item {
            font-size: 12px;
            color: #6b7280;
            padding: 6px 0;
            border-bottom: 1px solid #e5e7eb;
        }

        .interval-item:last-child {
            border-bottom: none;
        }

        .interval-badge {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
            margin-right: 8px;
        }

        .badge-warmup { background: #fef3c7; color: #92400e; }
        .badge-work { background: #fecaca; color: #991b1b; }
        .badge-rest { background: #dbeafe; color: #1e40af; }
        .badge-cooldown { background: #e0e7ff; color: #3730a3; }

        .workout-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
        }

        .btn-small {
            padding: 10px;
            font-size: 13px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s;
        }

        .btn-export {
            background: #3b82f6;
            color: white;
        }

        .btn-details {
            background: #f3f4f6;
            color: #374151;
            border: 1px solid #d1d5db;
        }

        .type-badge {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
            margin-top: 8px;
        }

        .type-easy { background: #dbeafe; color: #1e40af; }
        .type-tempo { background: #fed7aa; color: #9a3412; }
        .type-interval { background: #fecaca; color: #991b1b; }
        .type-long { background: #d1fae5; color: #065f46; }
        .type-recovery { background: #e0e7ff; color: #3730a3; }

        @media (max-width: 600px) {
            .stats {
                grid-template-columns: 1fr;
                gap: 10px;
            }

            .stat-number {
                font-size: 24px;
            }

            .controls {
                grid-template-columns: 1fr;
            }
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            padding: 20px;
            overflow-y: auto;
        }

        .modal-content {
            background: white;
            max-width: 600px;
            margin: 20px auto;
            border-radius: 15px;
            padding: 25px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e5e7eb;
        }

        .modal-title {
            font-size: 20px;
            font-weight: bold;
            color: #1f2937;
        }

        .close-btn {
            background: #f3f4f6;
            border: none;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            color: #6b7280;
        }

        .export-content {
            background: #f9fafb;
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
            font-family: monospace;
            font-size: 12px;
            white-space: pre-wrap;
            max-height: 400px;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏃‍♂️ Plano de Corrida</h1>
            <p>Rumo aos 5km e 10km</p>
        </div>

        <div class="stats">
            <div class="stat">
                <div class="stat-number" id="totalWorkouts">30</div>
                <div class="stat-label">Total de Treinos</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="completedWorkouts">0</div>
                <div class="stat-label">Concluídos</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="progressPercent">0%</div>
                <div class="stat-label">Progresso</div>
            </div>
        </div>

        <div class="controls">
            <button class="btn btn-primary" onclick="exportAllWorkouts()">
                📤 Exportar Todos
            </button>
            <button class="btn btn-secondary" onclick="resetProgress()">
                🔄 Resetar Progresso
            </button>
        </div>

        <div class="filter-section">
            <label for="weekFilter">Filtrar por Semana:</label>
            <select id="weekFilter" onchange="filterWorkouts()">
                <option value="all">Todas as Semanas</option>
            </select>
        </div>

        <div id="workoutsList"></div>
    </div>

    <div id="exportModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Treino Exportado</h3>
                <button class="close-btn" onclick="closeModal()">×</button>
            </div>
            <div id="exportContent"></div>
            <button class="btn btn-primary" style="width: 100%; margin-top: 15px;" onclick="copyToClipboard()">
                📋 Copiar para Área de Transferência
            </button>
        </div>
    </div>

    <script>
        const workouts = [
            {id: 1, week: 1, day: 1, name: "Corrida Fácil - 20min", type: "EASY_RUN", description: "Aquecimento 5min caminhada + 20min corrida leve + 5min volta à calma", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1200, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 2, week: 1, day: 3, name: "Intervalados Curtos", type: "INTERVAL", description: "Aquecimento + 6x (1min rápido / 2min recuperação) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 60, intensity: "HARD"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 3, week: 1, day: 5, name: "Corrida Longa - 25min", type: "LONG_RUN", description: "Corrida contínua em ritmo confortável", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 4, week: 2, day: 1, name: "Corrida Fácil - 25min", type: "EASY_RUN", description: "Aquecimento 5min + 25min corrida leve + 5min volta à calma", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 5, week: 2, day: 3, name: "Fartlek - 30min", type: "INTERVAL", description: "Aquecimento + 20min alternando ritmos (2min rápido / 1min leve) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 60, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 6, week: 2, day: 5, name: "Corrida Longa - 30min", type: "LONG_RUN", description: "Corrida contínua em ritmo confortável", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 7, week: 3, day: 1, name: "Corrida Fácil - 30min", type: "EASY_RUN", description: "Corrida leve e confortável", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 8, week: 3, day: 3, name: "Intervalados 400m", type: "INTERVAL", description: "Aquecimento + 8x 400m (2min intenso / 1min30s recuperação) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 120, intensity: "HARD"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 9, week: 3, day: 5, name: "Corrida Longa - 35min", type: "LONG_RUN", description: "Corrida contínua em ritmo confortável", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 2100, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 10, week: 4, day: 1, name: "Corrida Fácil - 25min", type: "RECOVERY", description: "Semana de recuperação - ritmo leve", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 11, week: 4, day: 3, name: "Corrida Fácil - 20min", type: "RECOVERY", description: "Corrida muito leve - recuperação ativa", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1200, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 12, week: 4, day: 5, name: "Corrida Longa - 30min", type: "LONG_RUN", description: "Corrida leve e relaxada", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 13, week: 5, day: 1, name: "Corrida Fácil - 30min", type: "EASY_RUN", description: "Corrida leve para recuperação", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 14, week: 5, day: 3, name: "Tempo Run - 20min", type: "TEMPO_RUN", description: "Aquecimento + 20min ritmo forte sustentável + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 1200, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 15, week: 5, day: 5, name: "Intervalados 1km", type: "INTERVAL", description: "Aquecimento + 5x 1km (ritmo 5k / 2min recuperação) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 300, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 300, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 300, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 300, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 300, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 16, week: 6, day: 1, name: "Corrida Fácil - 35min", type: "EASY_RUN", description: "Corrida leve", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 2100, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 17, week: 6, day: 3, name: "Intervalados 800m", type: "INTERVAL", description: "Aquecimento + 6x 800m (3min intenso / 90s recuperação) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "REST", duration: 90, intensity: "EASY"}, {type: "WORK", duration: 180, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 18, week: 6, day: 5, name: "Teste 5km", type: "TEMPO_RUN", description: "Aquecimento + 5km em ritmo forte (teste de performance) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "VERY_HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 19, week: 7, day: 1, name: "Corrida Fácil - 40min", type: "EASY_RUN", description: "Começando a aumentar a distância", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 2400, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 20, week: 7, day: 3, name: "Tempo Run - 25min", type: "TEMPO_RUN", description: "Aquecimento + 25min ritmo forte + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 21, week: 7, day: 5, name: "Corrida Longa - 50min", type: "LONG_RUN", description: "Primeira corrida longa de 50 minutos", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 3000, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 22, week: 8, day: 1, name: "Corrida Fácil - 35min", type: "EASY_RUN", description: "Recuperação", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 2100, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 23, week: 8, day: 3, name: "Intervalados 2km", type: "INTERVAL", description: "Aquecimento + 4x 2km (ritmo 10k / 2min recuperação) + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 600, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 600, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 600, intensity: "HARD"}, {type: "REST", duration: 120, intensity: "EASY"}, {type: "WORK", duration: 600, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 24, week: 8, day: 5, name: "Corrida Longa - 55min", type: "LONG_RUN", description: "Aumentando a resistência", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 3300, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 25, week: 9, day: 1, name: "Corrida Fácil - 40min", type: "EASY_RUN", description: "Corrida leve de recuperação", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 2400, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 26, week: 9, day: 3, name: "Tempo Run - 30min", type: "TEMPO_RUN", description: "Aquecimento + 30min ritmo forte + volta à calma", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "HARD"}, {type: "COOLDOWN", duration: 600, intensity: "EASY"}]},
            {id: 27, week: 9, day: 5, name: "Corrida Longa - 60min", type: "LONG_RUN", description: "Maior volume da semana", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 3600, intensity: "MODERATE"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 28, week: 10, day: 1, name: "Corrida Fácil - 30min", type: "RECOVERY", description: "Semana de taper - reduzindo volume", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1800, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 29, week: 10, day: 3, name: "Corrida Fácil - 25min", type: "RECOVERY", description: "Leve com alguns piques curtos", intervals: [{type: "WARMUP", duration: 300, intensity: "EASY"}, {type: "WORK", duration: 1500, intensity: "EASY"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]},
            {id: 30, week: 10, day: 6, name: "PROVA - 10KM", type: "TEMPO_RUN", description: "DIA DA PROVA! Aquecimento leve + 10km + comemoração!", intervals: [{type: "WARMUP", duration: 600, intensity: "EASY"}, {type: "WORK", duration: 3000, intensity: "VERY_HARD"}, {type: "COOLDOWN", duration: 300, intensity: "EASY"}]}
        ];

        let completedWorkouts = JSON.parse(localStorage.getItem('completedWorkouts') || '[]');

        function init() {
            populateWeekFilter();
            renderWorkouts();
            updateStats();
        }

        function populateWeekFilter() {
            const select = document.getElementById('weekFilter');
            const weeks = [...new Set(workouts.map(w => w.week))];
            
            weeks.forEach(week => {
                const option = document.createElement('option');
                option.value = week;
                option.textContent = `Semana ${week}`;
                select.appendChild(option);
            });
        }

        function filterWorkouts() {
            renderWorkouts();
        }

        function render
let filteredWorkouts = workouts;
        if (weekFilter !== 'all') {
            filteredWorkouts = workouts.filter(w => w.week == weekFilter);
        }

        container.innerHTML = filteredWorkouts.map(workout => `
            <div class="workout-card ${completedWorkouts.includes(workout.id) ? 'completed' : ''}">
                <div class="workout-header">
                    <div class="checkbox-wrapper">
                        <input type="checkbox" 
                               class="checkbox" 
                               ${completedWorkouts.includes(workout.id) ? 'checked' : ''}
                               onchange="toggleWorkout(${workout.id})">
                    </div>
                    <div class="workout-info">
                        <div class="workout-meta">Semana ${workout.week} - Dia ${workout.day}</div>
                        <div class="workout-name">${workout.name}</div>
                        <div class="workout-description">${workout.description}</div>
                        <span class="type-badge type-${workout.type.toLowerCase().replace('_', '')}">${getTypeLabel(workout.type)}</span>
                        
                        <div class="workout-intervals">
                            <div class="interval-title">Estrutura do Treino:</div>
                            ${workout.intervals.map(interval => `
                                <div class="interval-item">
                                    <span class="interval-badge badge-${interval.type.toLowerCase()}">${getIntervalLabel(interval.type)}</span>
                                    ${formatDuration(interval.duration)} - ${interval.intensity}
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>
                <div class="workout-actions">
                    <button class="btn-small btn-export" onclick="exportWorkout(${workout.id})">
                        📤 Exportar
                    </button>
                    <button class="btn-small btn-details" onclick="showDetails(${workout.id})">
                        📋 Detalhes
                    </button>
                </div>
            </div>
        `).join('');
    }

    function toggleWorkout(id) {
        const index = completedWorkouts.indexOf(id);
        if (index > -1) {
            completedWorkouts.splice(index, 1);
        } else {
            completedWorkouts.push(id);
        }
        localStorage.setItem('completedWorkouts', JSON.stringify(completedWorkouts));
        renderWorkouts();
        updateStats();
    }

    function updateStats() {
        document.getElementById('totalWorkouts').textContent = workouts.length;
        document.getElementById('completedWorkouts').textContent = completedWorkouts.length;
        const percent = Math.round((completedWorkouts.length / workouts.length) * 100);
        document.getElementById('progressPercent').textContent = percent + '%';
    }

    function formatDuration(seconds) {
        const minutes = Math.floor(seconds / 60);
        const secs = seconds % 60;
        return secs > 0 ? `${minutes}min ${secs}s` : `${minutes}min`;
    }

    function getTypeLabel(type) {
        const labels = {
            'EASY_RUN': 'Corrida Fácil',
            'TEMPO_RUN': 'Tempo Run',
            'INTERVAL': 'Intervalado',
            'LONG_RUN': 'Long Run',
            'RECOVERY': 'Recuperação'
        };
        return labels[type] || type;
    }

    function getIntervalLabel(type) {
        const labels = {
            'WARMUP': 'Aquecimento',
            'WORK': 'Trabalho',
            'REST': 'Recuperação',
            'COOLDOWN': 'Volta à Calma'
        };
        return labels[type] || type;
    }

    function exportWorkout(id) {
        const workout = workouts.find(w => w.id === id);
        const content = generateWorkoutText(workout);
        
        document.getElementById('exportContent').innerHTML = `<div class="export-content">${content}</div>`;
        document.getElementById('exportModal').style.display = 'block';
    }

    function generateWorkoutText(workout) {
        let text = '========================================\n';
        text += `TREINO: ${workout.name}\n`;
        text += `Semana ${workout.week} - Dia ${workout.day}\n`;
        text += '========================================\n\n';
        text += `Descrição: ${workout.description}\n\n`;
        text += 'INTERVALOS:\n';
        text += '----------------------------------------\n\n';
        
        workout.intervals.forEach((interval, index) => {
            text += `${index + 1}. ${getIntervalLabel(interval.type)}\n`;
            text += `   Duração: ${formatDuration(interval.duration)}\n`;
            text += `   Intensidade: ${interval.intensity}\n\n`;
        });
        
        const totalTime = workout.intervals.reduce((sum, i) => sum + i.duration, 0);
        text += '========================================\n';
        text += `Tempo Total: ${formatDuration(totalTime)}\n`;
        text += '========================================';
        
        return text;
    }

    function exportAllWorkouts() {
        let allText = 'PLANO DE CORRIDA COMPLETO - 10 SEMANAS\n';
        allText += 'Rumo aos 5km e 10km\n';
        allText += '========================================\n\n';
        
        workouts.forEach(workout => {
            allText += generateWorkoutText(workout) + '\n\n\n';
        });
        
        const blob = new Blob([allText], { type: 'text/plain' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'plano-corrida-completo.txt';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
        
        alert('✅ Todos os treinos exportados com sucesso!\nArquivo salvo como "plano-corrida-completo.txt"');
    }

    function showDetails(id) {
        exportWorkout(id);
    }

    function closeModal() {
        document.getElementById('exportModal').style.display = 'none';
    }

    function copyToClipboard() {
        const content = document.getElementById('exportContent').textContent;
        navigator.clipboard.writeText(content).then(() => {
            alert('✅ Treino copiado para a área de transferência!');
        });
    }

    function resetProgress() {
        if (confirm('Tem certeza que deseja resetar todo o progresso?')) {
            completedWorkouts = [];
            localStorage.setItem('completedWorkouts', JSON.stringify(completedWorkouts));
            renderWorkouts();
            updateStats();
            alert('✅ Progresso resetado!');
        }
    }

    window.onclick = function(event) {
        const modal = document.getElementById('exportModal');
        if (event.target === modal) {
            closeModal();
        }
    }

    init();
</script>
