<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Performance Sprint Tracker - Empathy Focus</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 25px;
        }
        h1 {
            margin: 0;
            font-size: 28px;
        }
        .subtitle {
            opacity: 0.9;
            margin-top: 5px;
            font-size: 20px;
            font-weight: 500;
        }
        .subheading {
            opacity: 0.85;
            margin-top: 8px;
            font-size: 14px;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }
        .card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .card h2 {
            margin-top: 0;
            color: #333;
            font-size: 18px;
            border-bottom: 2px solid #667eea;
            padding-bottom: 10px;
        }
        .metric {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #eee;
        }
        .metric:last-child {
            border-bottom: none;
        }
        .metric-label {
            font-weight: 500;
            color: #666;
        }
        .metric-value {
            font-size: 20px;
            font-weight: bold;
        }
        .positive { color: #22c55e; }
        .negative { color: #ef4444; }
        .neutral { color: #f59e0b; }
        .focus { color: #667eea; }
        .progress-bar {
            width: 100%;
            height: 30px;
            background: #e5e5e5;
            border-radius: 15px;
            overflow: hidden;
            margin-top: 10px;
            position: relative;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            transition: width 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            padding-right: 10px;
            color: white;
            font-weight: bold;
        }
        .progress-label {
            position: absolute;
            width: 100%;
            text-align: center;
            line-height: 30px;
            color: #333;
            font-weight: 600;
        }
        .tracking-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        .tracking-table th {
            background: #f8f8f8;
            padding: 10px;
            text-align: left;
            font-weight: 600;
            color: #333;
            border-bottom: 2px solid #ddd;
        }
        .tracking-table td {
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        .day-tracker {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
            margin-top: 15px;
        }
        .day-card {
            background: #f8f8f8;
            border: 2px solid #e5e5e5;
            padding: 12px 8px;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            min-height: 80px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        .day-card.completed {
            background: #22c55e;
            border-color: #16a34a;
            color: white;
        }
        .day-card.partial {
            background: #fbbf24;
            border-color: #f59e0b;
            color: white;
        }
        .day-card.missed {
            background: #ef4444;
            border-color: #dc2626;
            color: white;
        }
        .day-card.weekend {
            background: #f3f4f6;
            border-style: dashed;
        }
        .day-card.weekend.completed {
            background: #22c55e;
            border-style: solid;
        }
        .day-card.weekend.partial {
            background: #fbbf24;
            border-style: solid;
        }
        .day-card.weekend.missed {
            background: #ef4444;
            border-style: solid;
        }
        .day-name {
            font-weight: bold;
            font-size: 11px;
            margin-bottom: 3px;
            text-transform: uppercase;
        }
        .day-score {
            font-size: 20px;
            font-weight: bold;
            margin: 5px 0;
        }
        .day-status {
            font-size: 10px;
            opacity: 0.9;
        }
        .week-label {
            grid-column: span 7;
            text-align: center;
            font-weight: bold;
            color: #667eea;
            margin: 10px 0 5px 0;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .insight {
            background: #f8f9ff;
            border-left: 4px solid #667eea;
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
        }
        .mission-statement {
            background: linear-gradient(135deg, #f8f9ff, #fff);
            border: 2px solid #667eea;
            padding: 20px;
            margin: 20px 0;
            border-radius: 10px;
            text-align: center;
        }
        .mission-statement h3 {
            color: #667eea;
            margin-top: 0;
            margin-bottom: 15px;
            font-size: 16px;
        }
        .mission-statement p {
            color: #333;
            line-height: 1.6;
            margin: 10px 0;
        }
        .method-box {
            background: #fff;
            border: 1px solid #e5e5e5;
            padding: 15px;
            margin-top: 15px;
            border-radius: 8px;
        }
        .method-example {
            font-style: italic;
            color: #666;
            margin: 5px 0;
            padding-left: 20px;
        }
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }
        .alert-critical {
            background: #fef2f2;
            border: 1px solid #fecaca;
            color: #991b1b;
        }
        .alert-success {
            background: #f0fdf4;
            border: 1px solid #bbf7d0;
            color: #14532d;
        }
        .alert-info {
            background: #eff6ff;
            border: 1px solid #bfdbfe;
            color: #1e3a8a;
        }
        .phrase-list {
            background: #fafafa;
            border: 1px solid #e5e5e5;
            border-radius: 8px;
            padding: 15px;
            margin: 10px 0;
        }
        .phrase-item {
            padding: 8px;
            margin: 5px 0;
            background: white;
            border-left: 3px solid #667eea;
            border-radius: 4px;
            font-style: italic;
            font-size: 14px;
        }
        .tally-section {
            background: #f8f9ff;
            border: 2px solid #667eea;
            border-radius: 10px;
            padding: 20px;
            margin: 15px 0;
        }
        .tally-row {
            display: flex;
            align-items: center;
            margin: 15px 0;
            gap: 15px;
        }
        .tally-label {
            font-weight: 600;
            color: #333;
            min-width: 120px;
        }
        .tally-counter {
            display: flex;
            align-items: center;
            gap: 10px;
            flex: 1;
        }
        .tally-btn {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            border: 2px solid #667eea;
            background: white;
            color: #667eea;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }
        .tally-btn:hover {
            background: #667eea;
            color: white;
        }
        .tally-btn:active {
            transform: scale(0.95);
        }
        .tally-display {
            font-size: 24px;
            font-weight: bold;
            min-width: 60px;
            text-align: center;
            color: #667eea;
        }
        .tally-result {
            background: white;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            text-align: center;
        }
        .result-percentage {
            font-size: 36px;
            font-weight: bold;
            margin: 10px 0;
        }
        .result-percentage.success { color: #22c55e; }
        .result-percentage.warning { color: #f59e0b; }
        .result-percentage.danger { color: #ef4444; }
        .big-metric {
            text-align: center;
            padding: 30px;
            background: linear-gradient(135deg, #f8f9ff, #fff);
            border-radius: 10px;
            margin: 20px 0;
        }
        .big-number {
            font-size: 64px;
            font-weight: bold;
            color: #667eea;
            line-height: 1;
        }
        .big-label {
            color: #666;
            margin-top: 10px;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .sprint-timeline {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background: white;
            border-radius: 10px;
            margin: 20px 0;
        }
        .sprint-phase {
            text-align: center;
            flex: 1;
            padding: 15px;
            border-radius: 8px;
            margin: 0 5px;
            font-size: 13px;
        }
        .sprint-phase.active {
            background: #667eea;
            color: white;
        }
        .sprint-phase.completed {
            background: #22c55e;
            color: white;
        }
        .sprint-phase.upcoming {
            background: #f3f4f6;
            color: #9ca3af;
        }
        .checkbox {
            width: 20px;
            height: 20px;
            border: 2px solid #667eea;
            border-radius: 4px;
            display: inline-block;
            cursor: pointer;
            margin-right: 10px;
            vertical-align: middle;
        }
        .checkbox.checked {
            background: #667eea;
            position: relative;
        }
        .checkbox.checked::after {
            content: "✓";
            color: white;
            position: absolute;
            top: -2px;
            left: 3px;
            font-size: 16px;
        }
        .checklist-item {
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }
        .checklist-item:last-child {
            border-bottom: none;
        }
        .input-field {
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
            min-width: 80px;
            transition: border-color 0.2s;
        }
        .input-field:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }
        .input-field.small {
            width: 60px;
            text-align: center;
        }
        .input-field.medium {
            width: 120px;
        }
        .input-field.large {
            width: 100%;
            margin-top: 5px;
        }
        .prep-item {
            padding: 10px;
            background: white;
            border-left: 3px solid #667eea;
            margin: 10px 0;
            border-radius: 5px;
        }
        .reset-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            margin-left: 15px;
        }
        .reset-btn:hover {
            background: #dc2626;
        }
        @media (max-width: 768px) {
            .day-tracker {
                grid-template-columns: repeat(4, 1fr);
            }
            .week-label {
                grid-column: span 4;
            }
            .tally-row {
                flex-direction: column;
                align-items: flex-start;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Performance Tracking Dashboard</h1>
        <div class="subtitle">Sprint #3: Empathy First</div>
        <div class="subheading">Single-Focus Goal Tracking | April 8-21, 2026</div>
    </div>

    <div class="sprint-timeline">
        <div class="sprint-phase completed">
            <strong>Sprint #1</strong><br>
            5As Framework<br>
            ✓ Mastered
        </div>
        <div class="sprint-phase completed">
            <strong>Sprint #2</strong><br>
            5Ws Framework<br>
            ✓ Mastered
        </div>
        <div class="sprint-phase active">
            <strong>Sprint #3</strong><br>
            Empathy First<br>
            In Progress
        </div>
        <div class="sprint-phase upcoming">
            <strong>Sprint #4</strong><br>
            Timeline Precision<br>
            Apr 22
        </div>
        <div class="sprint-phase upcoming">
            <strong>Sprint #5</strong><br>
            Business Discovery<br>
            May 6
        </div>
    </div>

    <div class="grid">
        <div class="card">
            <h2>🎯 Current Focus: ONE GOAL</h2>
            <div class="big-metric">
                <div class="big-number">12%</div>
                <div class="big-label">Current Empathy Usage</div>
            </div>
            <div class="progress-bar">
                <div class="progress-label">Target: 80%</div>
                <div class="progress-fill" style="width: 15%;">
                </div>
            </div>
            <div class="alert alert-critical">
                <strong>Gap Identified:</strong> 88% of Neutral/Frownie ratings lack empathy acknowledgment during constraints
            </div>
        </div>

        <div class="card">
            <h2>🚀 Sprint Mission Statement</h2>
            <div class="mission-statement">
                <h3>MY COMMITMENT TO EMPATHY EXCELLENCE</h3>
                <p><strong>Building on my proven success with 5As and 5Ws frameworks, I'm dedicating two weeks to master empathy in every constraint conversation.</strong></p>
                <p>This sprint targets my #1 opportunity: transforming technical accuracy into human connection. By adding just 5-10 seconds of acknowledgment, I'll convert frustration into understanding.</p>
                
                <div class="method-box">
                    <strong>The "Feel, Felt, Found" Method:</strong><br>
                    A three-step empathy framework that builds instant rapport:<br><br>
                    <strong>FEEL:</strong> "I understand how you feel..."<br>
                    <div class="method-example">Acknowledges their current emotion</div>
                    
                    <strong>FELT:</strong> "Other merchants have felt the same way..."<br>
                    <div class="method-example">Shows they're not alone</div>
                    
                    <strong>FOUND:</strong> "What they've found helpful is..."<br>
                    <div class="method-example">Bridges to the solution</div>
                </div>
            </div>
        </div>
    </div>

    <div class="card">
        <h2>📊 Why This Sprint Matters</h2>
        <div class="insight">
            <strong>The Data Says:</strong><br>
            When you use empathy → 92% Smiley rate<br>
            When you don't → 8% Frownie rate
        </div>
        <div class="metric">
            <span class="metric-label">Potential CSAT Impact</span>
            <span class="metric-value positive">+15%</span>
        </div>
        <div class="metric">
            <span class="metric-label">Neutral Conversion Opportunity</span>
            <span class="metric-value focus">24% → 15%</span>
        </div>
        <div class="metric">
            <span class="metric-label">Time Investment Required</span>
            <span class="metric-value positive">5-10 sec</span>
        </div>
    </div>

    <div class="card">
        <h2>📅 Two-Week Sprint Calendar</h2>
        <div class="day-tracker">
            <div class="week-label">WEEK 1: Build the Habit (April 8-14)</div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">MON</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 8</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">TUE</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 9</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">WED</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 10</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">THU</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 11</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">FRI</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 12</div>
            </div>
            <div class="day-card weekend" onclick="toggleDay(this)">
                <div class="day-name">SAT</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 13</div>
            </div>
            <div class="day-card weekend" onclick="toggleDay(this)">
                <div class="day-name">SUN</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 14</div>
            </div>
            
            <div class="week-label">WEEK 2: Refine & Master (April 15-21)</div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">MON</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 15</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">TUE</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 16</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">WED</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 17</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">THU</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 18</div>
            </div>
            <div class="day-card" onclick="toggleDay(this)">
                <div class="day-name">FRI</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 19</div>
            </div>
            <div class="day-card weekend" onclick="toggleDay(this)">
                <div class="day-name">SAT</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 20</div>
            </div>
            <div class="day-card weekend" onclick="toggleDay(this)">
                <div class="day-name">SUN</div>
                <div class="day-score">--%</div>
                <div class="day-status">Apr 21</div>
            </div>
        </div>
        
        <div class="phrase-list">
            <strong>Daily Practice Phrases (use throughout your shift):</strong>
            <div class="phrase-item">Monday: "I completely understand why that's frustrating..."</div>
            <div class="phrase-item">Tuesday: "I can see how this impacts your business..."</div>
            <div class="phrase-item">Wednesday: "I know this isn't the answer you were hoping for..."</div>
            <div class="phrase-item">Thursday: "I appreciate your patience with this situation..."</div>
            <div class="phrase-item">Friday: "That's a completely reasonable expectation..."</div>
            <div class="phrase-item">Weekend: Mix and match - use what feels most natural</div>
        </div>
    </div>

    <div class="grid">
        <div class="card">
            <h2>✍️ Daily Tracking Sheet</h2>
            
            <div class="prep-item">
                <strong>📝 Daily Prep:</strong> Review today's empathy phrase
            </div>
            
            <div class="tally-section">
                <h3 style="margin-top: 0; color: #667eea;">Today's Live Tally</h3>
                
                <div class="tally-row">
                    <span class="tally-label">Constraints:</span>
                    <div class="tally-counter">
                        <button class="tally-btn" onclick="updateTally('constraints', -1)">-</button>
                        <span class="tally-display" id="constraints-count">0</span>
                        <button class="tally-btn" onclick="updateTally('constraints', 1)">+</button>
                        <button class="reset-btn" onclick="resetTally('constraints')">Reset</button>
                    </div>
                </div>
                
                <div class="tally-row">
                    <span class="tally-label">Empathy Used:</span>
                    <div class="tally-counter">
                        <button class="tally-btn" onclick="updateTally('empathy', -1)">-</button>
                        <span class="tally-display" id="empathy-count">0</span>
                        <button class="tally-btn" onclick="updateTally('empathy', 1)">+</button>
                        <button class="reset-btn" onclick="resetTally('empathy')">Reset</button>
                    </div>
                </div>
                
                <div class="tally-result">
                    <strong>Success Rate</strong>
                    <div class="result-percentage" id="success-rate">--%</div>
                    <div id="rate-message">Start tracking to see your rate</div>
                </div>
            </div>
            
            <div class="prep-item">
                <strong>📊 End of Shift Review:</strong><br>
                Note one win: <input type="text" class="input-field large" placeholder="What went well today?"><br>
                Note one opportunity: <input type="text" class="input-field large" placeholder="What could improve tomorrow?">
            </div>
        </div>

        <div class="card">
            <h2>📈 Weekly Progress Tracking</h2>
            <table class="tracking-table">
                <thead>
                    <tr>
                        <th>Metric</th>
                        <th>Week 1</th>
                        <th>Week 2</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><strong>Days Goal Met (80%+)</strong></td>
                        <td><input type="text" class="input-field small" placeholder="0"> days</td>
                        <td><input type="text" class="input-field small" placeholder="0"> days</td>
                    </tr>
                    <tr>
                        <td><strong>Average Empathy Usage</strong></td>
                        <td><input type="text" class="input-field small" placeholder="0">%</td>
                        <td><input type="text" class="input-field small" placeholder="0">%</td>
                    </tr>
                    <tr>
                        <td><strong>Most Effective Phrase</strong></td>
                        <td colspan="2">
                            <input type="text" class="input-field large" placeholder="Which phrase got the best merchant response?">
                        </td>
                    </tr>
                    <tr>
                        <td><strong>Neutral → Smiley Conversions</strong></td>
                        <td><input type="text" class="input-field small" placeholder="0"> chats</td>
                        <td><input type="text" class="input-field small" placeholder="0"> chats</td>
                    </tr>
                </tbody>
            </table>
            <div class="alert alert-success" style="margin-top: 15px;">
                <strong>Week 1 Goal:</strong> Practice & build the habit (aim for 60%+ average)<br>
                <strong>Week 2 Goal:</strong> Consistency & mastery (hit 80%+ average)
            </div>
        </div>
    </div>

    <div class="card">
        <h2>🎯 Success Criteria & Manager Support</h2>
        <div class="grid">
            <div>
                <div class="alert alert-success">
                    <strong>Sprint Success Looks Like:</strong><br>
                    <span class="checkbox" onclick="toggleCheck(this)"></span>Empathy usage increases from 12% to 80%<br>
                    <span class="checkbox" onclick="toggleCheck(this)"></span>Neutral rate drops by at least 5%<br>
                    <span class="checkbox" onclick="toggleCheck(this)"></span>AHT remains stable (±2 minutes)<br>
                    <span class="checkbox" onclick="toggleCheck(this)"></span>No increase in escalations
                </div>
            </div>
            <div>
                <div class="alert alert-info">
                    <strong>Manager Check-in Checklist:</strong><br>
                    <div class="checklist-item">
                        <span class="checkbox" onclick="toggleCheck(this)"></span>Weekly spot-check of 2-3 constraint conversations
                    </div>
                    <div class="checklist-item">
                        <span class="checkbox" onclick="toggleCheck(this)"></span>Listen for empathy language before policy statements
                    </div>
                    <div class="checklist-item">
                        <span class="checkbox" onclick="toggleCheck(this)"></span>5-minute Friday progress review
                    </div>
                    <div class="checklist-item">
                        <span class="checkbox" onclick="toggleCheck(this)"></span>Shadow one live chat as accountability partner
                    </div>
                    <div class="checklist-item">
                        <span class="checkbox" onclick="toggleCheck(this)"></span>Flag if overcorrecting (too much empathy affecting AHT)
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="card">
        <h2>📅 What's Next: The Master Plan</h2>
        <table class="tracking-table">
            <thead>
                <tr>
                    <th>Sprint</th>
                    <th>Focus</th>
                    <th>Dates</th>
                    <th>Target</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody>
                <tr style="background: #f0fdf4;">
                    <td><strong>Sprint #1</strong></td>
                    <td>5As Framework</td>
                    <td>Completed</td>
                    <td>Master framework</td>
                    <td>✅ Complete</td>
                </tr>
                <tr style="background: #f0fdf4;">
                    <td><strong>Sprint #2</strong></td>
                    <td>5Ws Framework</td>
                    <td>Completed</td>
                    <td>Master framework</td>
                    <td>✅ Complete</td>
                </tr>
                <tr style="background: #f8f9ff;">
                    <td><strong>Sprint #3</strong></td>
                    <td>Empathy First</td>
                    <td>Apr 8-21</td>
                    <td>12% → 80%</td>
                    <td>🔄 In Progress</td>
                </tr>
                <tr>
                    <td><strong>Sprint #4</strong></td>
                    <td>Timeline Precision</td>
                    <td>Apr 22 - May 5</td>
                    <td>45% → 90%</td>
                    <td>📅 Upcoming</td>
                </tr>
                <tr>
                    <td><strong>Sprint #5</strong></td>
                    <td>Business Discovery</td>
                    <td>May 6-19</td>
                    <td>20% → 75%</td>
                    <td>📅 Upcoming</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        // Tally counter functionality
        let tallies = {
            constraints: 0,
            empathy: 0
        };

        function updateTally(type, change) {
            tallies[type] = Math.max(0, tallies[type] + change);
            document.getElementById(`${type}-count`).textContent = tallies[type];
            calculateRate();
        }

        function resetTally(type) {
            tallies[type] = 0;
            document.getElementById(`${type}-count`).textContent = 0;
            calculateRate();
        }

        function calculateRate() {
            const rateDisplay = document.getElementById('success-rate');
            const messageDisplay = document.getElementById('rate-message');
            
            if (tallies.constraints === 0) {
                rateDisplay.textContent = '--%';
                rateDisplay.className = 'result-percentage';
                messageDisplay.textContent = 'Start tracking to see your rate';
            } else {
                const rate = Math.round((tallies.empathy / tallies.constraints) * 100);
                rateDisplay.textContent = rate + '%';
                
                if (rate >= 80) {
                    rateDisplay.className = 'result-percentage success';
                    messageDisplay.textContent = '✅ Goal Met! Keep it up!';
                } else if (rate >= 60) {
                    rateDisplay.className = 'result-percentage warning';
                    messageDisplay.textContent = '📈 Getting there! Push for 80%!';
                } else {
                    rateDisplay.className = 'result-percentage danger';
                    messageDisplay.textContent = '⚡ Focus on empathy for remaining chats';
                }
            }
        }

        // Day card functionality
        function toggleDay(element) {
            if (!element.classList.contains('completed') && !element.classList.contains('partial') && !element.classList.contains('missed')) {
                element.classList.add('completed');
                element.querySelector('.day-score').textContent = '85%';
                element.querySelector('.day-status').textContent = 'Goal Met!';
            } else if (element.classList.contains('completed')) {
                element.classList.remove('completed');
                element.classList.add('partial');
                element.querySelector('.day-score').textContent = '70%';
                element.querySelector('.day-status').textContent = 'Partial';
            } else if (element.classList.contains('partial')) {
                element.classList.remove('partial');
                element.classList.add('missed');
                element.querySelector('.day-score').textContent = '45%';
                element.querySelector('.day-status').textContent = 'Missed';
            } else {
                element.classList.remove('completed', 'partial', 'missed');
                element.querySelector('.day-score').textContent = '--%';
                const dates = ['Apr 8', 'Apr 9', 'Apr 10', 'Apr 11', 'Apr 12', 'Apr 13', 'Apr 14', 
                              'Apr 15', 'Apr 16', 'Apr 17', 'Apr 18', 'Apr 19', 'Apr 20', 'Apr 21'];
                const dayIndex = Array.from(element.parentNode.children).indexOf(element);
                if (dayIndex > 0 && dayIndex <= 7) {
                    element.querySelector('.day-status').textContent = dates[dayIndex - 1];
                } else if (dayIndex > 8 && dayIndex <= 15) {
                    element.querySelector('.day-status').textContent = dates[dayIndex - 2];
                }
            }
        }

        function toggleCheck(element) {
            element.classList.toggle('checked');
        }

        // Save input values to localStorage
        document.querySelectorAll('.input-field').forEach(input => {
            const savedValue = localStorage.getItem(input.placeholder);
            if (savedValue) input.value = savedValue;
            
            input.addEventListener('input', function() {
                localStorage.setItem(this.placeholder, this.value);
            });
        });
    </script>
</body>
</html>
