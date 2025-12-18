<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2048 Mega Grid Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            color: #fff;
        }
        
        .header {
            text-align: center;
            margin-bottom: 20px;
        }
        
        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .subtitle {
            font-size: 1.2em;
            opacity: 0.9;
        }
        
        .controls {
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }
        
        button {
            padding: 12px 24px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        .score-display {
            font-size: 18px;
            font-weight: bold;
        }
        
        .progress-container {
            width: 100%;
            max-width: 900px;
            margin-bottom: 20px;
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }
        
        .progress-label {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 14px;
        }
        
        .progress-bar {
            width: 100%;
            height: 30px;
            background: rgba(0,0,0,0.3);
            border-radius: 15px;
            overflow: hidden;
            position: relative;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4facfe 0%, #00f2fe 100%);
            transition: width 0.5s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 14px;
            color: white;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
            min-width: 50px;
        }
        
        .game-container {
            background: rgba(255,255,255,0.1);
            padding: 10px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            overflow: auto;
            max-width: 95vw;
            max-height: 70vh;
        }
        
        #grid {
            display: grid;
            grid-template-columns: repeat(64, 12px);
            grid-template-rows: repeat(64, 12px);
            gap: 1px;
            background: rgba(0,0,0,0.2);
            padding: 5px;
            border-radius: 10px;
        }
        
        .cell {
            background: rgba(255,255,255,0.2);
            border-radius: 2px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 6px;
            font-weight: bold;
            color: white;
            text-shadow: 0 0 2px rgba(0,0,0,0.5);
            transition: all 0.15s ease;
            cursor: grab;
            user-select: none;
        }
        
        .cell:active {
            cursor: grabbing;
        }
        
        .cell.dragging {
            opacity: 0.5;
            cursor: grabbing;
            transform: scale(1.1);
            z-index: 1000;
        }
        
        .cell.drag-over {
            background: rgba(255,255,255,0.5) !important;
            transform: scale(1.1);
        }
        
        .cell-2 { background: #eee4da; color: #776e65; }
        .cell-4 { background: #ede0c8; color: #776e65; }
        .cell-8 { background: #f2b179; color: #f9f6f2; }
        .cell-16 { background: #f59563; color: #f9f6f2; }
        .cell-32 { background: #f67c5f; color: #f9f6f2; }
        .cell-64 { background: #f65e3b; color: #f9f6f2; }
        .cell-128 { background: #edcf72; color: #f9f6f2; }
        .cell-256 { background: #edcc61; color: #f9f6f2; }
        .cell-512 { background: #edc850; color: #f9f6f2; }
        .cell-1024 { background: #edc53f; color: #f9f6f2; }
        .cell-2048 { background: #edc22e; color: #f9f6f2; }
        .cell-4096 { background: #3c3a32; color: #f9f6f2; }
        .cell-8192 { background: #3c3a32; color: #f9f6f2; }
        .cell-16384 { background: #3c3a32; color: #f9f6f2; }
        .cell-32768 { background: #3c3a32; color: #f9f6f2; }
        .cell-65536 { background: #3c3a32; color: #f9f6f2; }
        .cell-131072 { background: #3c3a32; color: #f9f6f2; }
        .cell-262144 { background: #ff0000; color: #f9f6f2; }
        .cell-524288 { background: #ff0000; color: #f9f6f2; }
        .cell-1048576 { background: #ff0000; color: #f9f6f2; }
        .cell-2097152 { background: #ff0000; color: #f9f6f2; }
        .cell-4194304 { background: #ff0000; color: #f9f6f2; }
        .cell-8388608 { background: #ff0000; color: #f9f6f2; }
        .cell-16777216 { background: #ff0000; color: #f9f6f2; }
        .cell-33554432 { background: #ff0000; color: #f9f6f2; }
        .cell-67108864 { background: #ff0000; color: #f9f6f2; }
        .cell-134217728 { background: #ffd700; color: #000; font-weight: 900; }
        
        .save-indicator {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(0,255,0,0.8);
            padding: 10px 20px;
            border-radius: 5px;
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
        }
        
        .save-indicator.show {
            opacity: 1;
        }
        
        .instructions {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            text-align: center;
            font-size: 14px;
        }
        
        @media (max-width: 768px) {
            h1 { font-size: 1.8em; }
            .subtitle { font-size: 1em; }
            #grid {
                grid-template-columns: repeat(64, 10px);
                grid-template-rows: repeat(64, 10px);
            }
            .cell { font-size: 5px; }
        }
    </style>
</head>
<body>
    <div class="save-indicator" id="saveIndicator">Auto-saved!</div>
    
    <div class="header">
        <h1>2048 Mega Grid</h1>
        <div class="subtitle">64x64 Grid - Goal: 134,217,728</div>
    </div>
    
    <div class="instructions">
        🖱️ Drag tiles to move them | Drop on same number to merge | Use "Add Number 2" button to spawn new tiles
    </div>
    
    <div class="controls">
        <button onclick="game.addTwo()">Add Number 2</button>
        <button onclick="game.newGame()">New Game</button>
        <div class="score-display">Score: <span id="score">0</span></div>
        <div class="score-display">Best: <span id="bestScore">0</span></div>
    </div>
    
    <div class="progress-container">
        <div class="progress-label">
            <span>Progress to 134,217,728</span>
            <span id="progressPercent">0%</span>
        </div>
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill">0%</div>
        </div>
        <div style="margin-top: 10px; font-size: 12px; opacity: 0.8;">
            Highest Tile: <span id="highestTile">0</span>
        </div>
    </div>
    
    <div class="game-container">
        <div id="grid"></div>
    </div>
    
    <script>
        const game = {
            grid: [],
            size: 64,
            score: 0,
            bestScore: 0,
            targetValue: 134217728,
            draggedElement: null,
            draggedRow: null,
            draggedCol: null,
            
            init() {
                this.loadGame();
                this.createGrid();
                this.updateDisplay();
                
                // Auto-save every 5 seconds
                setInterval(() => this.saveGame(), 5000);
            },
            
            createGrid() {
                const gridEl = document.getElementById('grid');
                gridEl.innerHTML = '';
                
                for (let i = 0; i < this.size; i++) {
                    this.grid[i] = this.grid[i] || [];
                    for (let j = 0; j < this.size; j++) {
                        this.grid[i][j] = this.grid[i][j] || 0;
                        const cell = document.createElement('div');
                        cell.className = 'cell';
                        cell.id = `cell-${i}-${j}`;
                        cell.setAttribute('data-row', i);
                        cell.setAttribute('data-col', j);
                        cell.draggable = true;
                        
                        // Drag events
                        cell.addEventListener('dragstart', (e) => this.handleDragStart(e, i, j));
                        cell.addEventListener('dragend', (e) => this.handleDragEnd(e));
                        cell.addEventListener('dragover', (e) => this.handleDragOver(e));
                        cell.addEventListener('dragleave', (e) => this.handleDragLeave(e));
                        cell.addEventListener('drop', (e) => this.handleDrop(e, i, j));
                        
                        gridEl.appendChild(cell);
                    }
                }
                
                // If new game, add two 2s
                if (this.score === 0 && this.getHighestTile() === 0) {
                    this.addTwo();
                    this.addTwo();
                }
                
                this.render();
            },
            
            handleDragStart(e, row, col) {
                if (this.grid[row][col] === 0) {
                    e.preventDefault();
                    return;
                }
                
                this.draggedElement = e.target;
                this.draggedRow = row;
                this.draggedCol = col;
                
                e.target.classList.add('dragging');
                e.dataTransfer.effectAllowed = 'move';
                e.dataTransfer.setData('text/html', e.target.innerHTML);
            },
            
            handleDragEnd(e) {
                e.target.classList.remove('dragging');
            },
            
            handleDragOver(e) {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'move';
                e.target.classList.add('drag-over');
                return false;
            },
            
            handleDragLeave(e) {
                e.target.classList.remove('drag-over');
            },
            
            handleDrop(e, targetRow, targetCol) {
                e.preventDefault();
                e.stopPropagation();
                
                e.target.classList.remove('drag-over');
                
                if (this.draggedRow === null || this.draggedCol === null) return;
                
                const draggedValue = this.grid[this.draggedRow][this.draggedCol];
                const targetValue = this.grid[targetRow][targetCol];
                
                // If dropping on same cell, do nothing
                if (this.draggedRow === targetRow && this.draggedCol === targetCol) {
                    return;
                }
                
                // If target is empty, just move the tile
                if (targetValue === 0) {
                    this.grid[targetRow][targetCol] = draggedValue;
                    this.grid[this.draggedRow][this.draggedCol] = 0;
                    this.render();
                    this.saveGame();
                }
                // If target has same value, merge them
                else if (targetValue === draggedValue) {
                    this.grid[targetRow][targetCol] = draggedValue * 2;
                    this.grid[this.draggedRow][this.draggedCol] = 0;
                    this.score += draggedValue * 2;
                    
                    if (this.score > this.bestScore) {
                        this.bestScore = this.score;
                    }
                    
                    this.render();
                    this.saveGame();
                }
                // Otherwise, swap the tiles
                else {
                    this.grid[targetRow][targetCol] = draggedValue;
                    this.grid[this.draggedRow][this.draggedCol] = targetValue;
                    this.render();
                    this.saveGame();
                }
                
                this.draggedElement = null;
                this.draggedRow = null;
                this.draggedCol = null;
                
                return false;
            },
            
            addTwo() {
                const empty = [];
                for (let i = 0; i < this.size; i++) {
                    for (let j = 0; j < this.size; j++) {
                        if (this.grid[i][j] === 0) {
                            empty.push([i, j]);
                        }
                    }
                }
                
                if (empty.length > 0) {
                    const [row, col] = empty[Math.floor(Math.random() * empty.length)];
                    this.grid[row][col] = 2;
                    this.render();
                    this.saveGame();
                }
            },
            
            render() {
                for (let i = 0; i < this.size; i++) {
                    for (let j = 0; j < this.size; j++) {
                        const cell = document.getElementById(`cell-${i}-${j}`);
                        const value = this.grid[i][j];
                        
                        if (value === 0) {
                            cell.textContent = '';
                            cell.className = 'cell';
                            cell.draggable = false;
                        } else {
                            if (value >= 1000000) {
                                cell.textContent = Math.floor(value/1000000) + 'M';
                            } else if (value >= 1000) {
                                cell.textContent = Math.floor(value/1000) + 'k';
                            } else {
                                cell.textContent = value;
                            }
                            cell.className = `cell cell-${value}`;
                            cell.draggable = true;
                        }
                    }
                }
                this.updateDisplay();
            },
            
            updateDisplay() {
                document.getElementById('score').textContent = this.score.toLocaleString();
                document.getElementById('bestScore').textContent = this.bestScore.toLocaleString();
                
                const highest = this.getHighestTile();
                document.getElementById('highestTile').textContent = highest.toLocaleString();
                
                const progress = Math.min(100, (Math.log2(highest) / Math.log2(this.targetValue)) * 100);
                document.getElementById('progressPercent').textContent = progress.toFixed(2) + '%';
                document.getElementById('progressFill').style.width = progress + '%';
                document.getElementById('progressFill').textContent = progress.toFixed(1) + '%';
            },
            
            getHighestTile() {
                let max = 0;
                for (let i = 0; i < this.size; i++) {
                    for (let j = 0; j < this.size; j++) {
                        if (this.grid[i][j] > max) {
                            max = this.grid[i][j];
                        }
                    }
                }
                return max;
            },
            
            newGame() {
                if (confirm('Start a new game? Current progress will be lost.')) {
                    this.grid = [];
                    this.score = 0;
                    this.createGrid();
                    this.saveGame();
                }
            },
            
            saveGame() {
                const gameState = {
                    grid: this.grid,
                    score: this.score,
                    bestScore: this.bestScore
                };
                
                localStorage.setItem('2048MegaGame', JSON.stringify(gameState));
                
                // Show save indicator
                const indicator = document.getElementById('saveIndicator');
                indicator.classList.add('show');
                setTimeout(() => indicator.classList.remove('show'), 1000);
            },
            
            loadGame() {
                const saved = localStorage.getItem('2048MegaGame');
                if (saved) {
                    try {
                        const gameState = JSON.parse(saved);
                        this.grid = gameState.grid || [];
                        this.score = gameState.score || 0;
                        this.bestScore = gameState.bestScore || 0;
                    } catch (e) {
                        console.error('Error loading game:', e);
                    }
                }
            }
        };
        
        // Initialize game when page loads
        window.onload = () => game.init();
        
        // Save on page unload
        window.onbeforeunload = () => game.saveGame();
    </script>
</body>
</html>
