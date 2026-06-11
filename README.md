# luftkoordinator
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luftkoordinering SAR - ACO System</title>
    <link href="https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #005F9E;
            --primary-dark: #003d66;
            --primary-light: #e6f0f7;
            --accent: #F26A36;
            --success: #2ecc71;
            --warning: #f39c12;
            --danger: #e74c3c;
            --bg: #f5f6f7;
            --bg-card: #ffffff;
            --border: #e1e4e8;
            --text-dark: #2C2C2C;
            --text-light: #666666;
            --text-muted: #999999;
        }

        body {
            font-family: 'Source Sans Pro', sans-serif;
            background: var(--bg);
            color: var(--text-dark);
            line-height: 1.6;
        }

        .container {
            max-width: 1600px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
            color: white;
            padding: 50px 40px;
            border-radius: 16px;
            margin-bottom: 30px;
            box-shadow: 0 8px 24px rgba(0, 95, 158, 0.15);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -10%;
            width: 400px;
            height: 400px;
            background: rgba(242, 106, 54, 0.1);
            border-radius: 50%;
            z-index: 0;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: 40px;
            position: relative;
            z-index: 1;
        }

        .header-left h1 {
            font-size: 2.5rem;
            margin-bottom: 8px;
            font-weight: 700;
        }

        .header-left p {
            font-size: 1.05rem;
            opacity: 0.95;
            margin-bottom: 0;
            font-weight: 300;
        }

        .header-status {
            display: flex;
            gap: 16px;
            flex-wrap: wrap;
        }

        .status-item {
            background: rgba(255, 255, 255, 0.12);
            padding: 14px 22px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .status-label {
            opacity: 0.85;
            font-size: 0.8rem;
            display: block;
            margin-bottom: 6px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .status-value {
            font-weight: 700;
            font-size: 1.2rem;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 1fr 360px;
            gap: 24px;
            margin-bottom: 30px;
        }

        .main-content {
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        .sidebar {
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 28px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            padding-bottom: 18px;
            border-bottom: 2px solid var(--primary-light);
        }

        .card h2 {
            font-size: 1.35rem;
            color: var(--primary);
            margin: 0;
            font-weight: 700;
        }

        .card h3 {
            font-size: 1.1rem;
            color: var(--text-dark);
            margin: 24px 0 14px 0;
            font-weight: 600;
        }

        .btn {
            padding: 11px 18px;
            border: none;
            border-radius: 8px;
            font-size: 0.95rem;
            cursor: pointer;
            transition: all 0.2s ease;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-family: 'Source Sans Pro', sans-serif;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--primary-dark);
            box-shadow: 0 4px 12px rgba(0, 95, 158, 0.3);
        }

        .btn-secondary {
            background: var(--bg);
            color: var(--text-dark);
            border: 1.5px solid var(--border);
        }

        .btn-secondary:hover {
            background: #f0f0f0;
        }

        .btn-danger {
            background: var(--danger);
            color: white;
        }

        .btn-danger:hover {
            background: #c0392b;
        }

        .btn-small {
            padding: 7px 14px;
            font-size: 0.85rem;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 18px;
            margin-bottom: 18px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        label {
            font-weight: 600;
            margin-bottom: 8px;
            color: var(--text-dark);
            font-size: 0.95rem;
        }

        input, select, textarea {
            padding: 11px 14px;
            border: 1.5px solid var(--border);
            border-radius: 8px;
            font-family: 'Source Sans Pro', sans-serif;
            font-size: 0.95rem;
            background: white;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 4px var(--primary-light);
        }

        .table-container {
            overflow-x: auto;
            margin-top: 18px;
            border-radius: 10px;
            border: 1px solid var(--border);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.95rem;
        }

        th {
            background: linear-gradient(135deg, var(--primary-light) 0%, rgba(0, 95, 158, 0.05) 100%);
            padding: 14px;
            text-align: left;
            font-weight: 700;
            color: var(--primary);
            border-bottom: 2px solid var(--primary);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }

        td {
            padding: 14px;
            border-bottom: 1px solid var(--border);
        }

        tr:hover {
            background: var(--primary-light);
        }

        .badge {
            display: inline-block;
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            text-align: center;
        }

        .badge-active {
            background: rgba(46, 204, 113, 0.1);
            color: var(--success);
        }

        .badge-standby {
            background: rgba(243, 156, 18, 0.1);
            color: var(--warning);
        }

        .badge-inactive {
            background: rgba(153, 153, 153, 0.1);
            color: var(--text-muted);
        }

        .badge-drone {
            background: rgba(0, 95, 158, 0.1);
            color: var(--primary);
        }

        .badge-helicopter {
            background: rgba(231, 76, 60, 0.1);
            color: var(--danger);
        }

        .badge-plane {
            background: rgba(155, 89, 182, 0.1);
            color: #9b59b6;
        }

        .badge-log-system {
            background: #e2e8f0;
            color: #475569;
            border: 1px solid #cbd5e1;
        }

        .badge-log-manual {
            background: rgba(0, 95, 158, 0.1);
            color: var(--primary);
            border: 1px solid rgba(0, 95, 158, 0.2);
        }

        .alert {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 14px 18px;
            border-radius: 10px;
            margin-bottom: 18px;
            border-left: 4px solid;
            font-size: 0.95rem;
            font-weight: 500;
            z-index: 2000;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .alert-danger {
            background: #ffebee;
            border-color: var(--danger);
            color: #c62828;
        }

        .alert-warning {
            background: #fff3e0;
            border-color: var(--warning);
            color: #e65100;
        }

        .alert-success {
            background: #e8f5e9;
            border-color: var(--success);
            color: #2e7d32;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(4px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--bg-card);
            border-radius: 16px;
            padding: 36px;
            max-width: 600px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 28px;
            padding-bottom: 18px;
            border-bottom: 2px solid var(--primary-light);
        }

        .modal-header h2 {
            margin: 0;
            color: var(--primary);
            font-size: 1.4rem;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 1.6rem;
            cursor: pointer;
            color: var(--text-light);
        }

        .close-btn:hover {
            color: var(--primary);
        }

        .action-btn {
            padding: 10px 16px;
            background: var(--primary-light);
            border: 1.5px solid var(--primary);
            color: var(--primary);
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: 600;
            transition: all 0.2s ease;
            font-family: 'Source Sans Pro', sans-serif;
            width: 100%;
            margin-bottom: 8px;
        }

        .action-btn:hover {
            background: var(--primary);
            color: white;
        }

        .action-btn.danger {
            background: rgba(231, 76, 60, 0.1);
            border-color: var(--danger);
            color: var(--danger);
        }

        .action-btn.danger:hover {
            background: var(--danger);
            color: white;
        }

        .inline-select {
            padding: 7px 10px;
            border: 1.5px solid var(--border);
            border-radius: 6px;
            font-size: 0.9rem;
            font-family: 'Source Sans Pro', sans-serif;
            background: white;
        }

        .inline-input {
            padding: 7px 10px;
            border: 1.5px solid var(--border);
            border-radius: 6px;
            font-size: 0.9rem;
            width: 100%;
            font-family: 'Source Sans Pro', sans-serif;
            background: white;
        }

        .mt-20 { margin-top: 20px; }
        .text-center { text-align: center; }
        .text-muted { color: var(--text-muted); }

        @media (max-width: 1024px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
            .header-content {
                flex-direction: column;
                gap: 20px;
            }
        }
    </style>
</head>
<body>
    <div id="alertsContainer"></div>
    <div class="header">
        <div class="header-content">
            <div class="header-left" style="display:flex; align-items:center; gap:10px;">
                   <img src="https://www.hovedredningssentralen.no/wp-content/uploads/2023/01/hrs-logo-.svg" width="150" height="200" alt="" />
                   <div>
                       <h1>Luftkoordinering</h1>
                       <p>Dette er et uoffisielt hobbyprosjekt for å bistå med koordinering av <br> luftressurser under søk- og redningsoppdrag.</p>
                   </div>
            </div>
            
            <div class="header-status">
                <div class="status-item">
                    <span class="status-label">Antall<BR>Luftfartøy</span>
                    <span class="status-value" id="headerAircraftCount">0</span>
                </div>
                <div class="status-item">
                    <span class="status-label">SAR<BR>TG</span>
                    <span class="status-value" id="headerSarTg">-</span>
                </div>
                <div class="status-item">
                    <span class="status-label">VHF<BR>Frekvens</span>
                    <span class="status-value" id="headerVhf">-</span>
                </div>
                <div class="status-item">
                    <span class="status-label">HRS<BR>Sør-Norge </span>
                    <span class="status-value">51 51 70 00</span>
                </div>
                <div style="text-align: right;">
                    <button class="action-btn" onclick="generateReport()">Generer rapport</button> <br>
                    <button class="action-btn" onclick="exportData()">Eksporter data</button> <br>
                    <button class="action-btn danger" onclick="resetAll()">Nullstill</button>
                </div>
            </div>
        </div>
    </div>

    <div class="container">
        <div class="main-grid">
            <div class="main-content">
              <div class="card">
                    <div class="card-header">
                        <h2>📊 Operasjonsdetaljer</h2>
                        <button class="btn btn-primary" onclick="openActionModal()">⚙️ Rediger</button>
                    </div>
                    <div class="form-row">
                        <div>
                            <label>Område</label>
                            <div style="font-size: 1.15rem; font-weight: 700;" id="displayActionArea">-</div>
                        </div>
                        <div>
                            <label>IPP</label>
                            <div style="font-size: 1.15rem; font-weight: 700;" id="displayIpp">-</div>
                        </div>
                        <div>
                            <label>SAR-TG</label>
                            <div style="font-size: 1.15rem; font-weight: 700;" id="displaySarTg">-</div>
                        </div>
                        <div>
                            <label>VHF Frekvens</label>
                            <div style="font-size: 1.15rem; font-weight: 700;" id="displayVhf">-</div>
                        </div>
                        <div style="grid-column: 1 / -1; margin-top: 10px; border-top: 1px dashed var(--border); padding-top: 10px;">
                            <label>✈️ METAR ENGM</label>
                            <div id="metarContent" style="font-size: 1.1rem; font-weight: 600; font-family: monospace; background: var(--primary-light); padding: 12px; border-radius: 8px; margin-top: 5px; color: var(--primary-dark);">Laster METAR...</div>

                            <label style="display: block; margin-top: 12px;">🌦️ Oversatt METAR</label>
                            <div id="metarTranslation" style="font-size: 1rem; font-weight: 600; background: #f8fafc; padding: 12px; border-radius: 8px; border-left: 4px solid var(--success); margin-top: 5px; color: var(--text-dark);">Venter på METAR...</div>
                        </div>
                        <div style="grid-column: 1 / -1; margin-top: 10px; border-top: 1px dashed var(--border); padding-top: 10px;">
                            <label>⚠️ Begrensninger</label>
                            <div style="font-size: 1.05rem; font-weight: 600; color: #c62828;" id="displayLimitations">-</div>
                        </div>
                        <div style="grid-column: 1 / -1; margin-top: 10px;">
                            <label>ℹ️ Annet / Nyttig info</label>
                            <div style="font-size: 1.05rem; font-weight: 400;" id="displayOther">-</div>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h2>✈️ Luftfartøy</h2>
                        <button class="btn btn-primary" onclick="openAircraftModal()">➕ Legg til</button>
                    </div>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Kallesignal</th>
                                    <th>Type</th>
                                    <th>Pilot</th>
                                    <th style="width: 20%;">Søksområde / Teig</th>
                                    <th>Status</th>
                                    <th style="width: 140px; min-width: 140px;">Høyde (Fot)</th>
                                    <th style="width: 25%;">Kommentar</th>
                                    <th></th>
                                </tr>
                            </thead>
                            <tbody id="aircraftList">
                                <tr><td colspan="8" class="text-center text-muted">Ingen luftfartøy registrert</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h2>📍 Separasjon</h2>
                        <button class="btn btn-primary" onclick="openSeparationModal()">➕ Legg til</button>
                    </div>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Ressurs</th>
                                    <th style="width: 120px;">Status</th>
                                    <th>Type</th>
                                    <th>Beskrivelse</th>
                                    <th></th>
                                </tr>
                            </thead>
                            <tbody id="separationList">
                                <tr><td colspan="5" class="text-center text-muted">Ingen separasjoner definert</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h2>📋 Logg</h2>
                    </div>
                    <div class="form-row">
                        <textarea id="messageInput" placeholder="Skriv manuell loggføring/melding..." rows="2" style="grid-column: 1/-1;"></textarea>
                    </div>
                    <button class="btn btn-primary" onclick="addMessage()">📤 Send</button>
                    <div class="table-container mt-20">
                        <table>
                            <thead>
                                <tr>
                                    <th style="width: 100px;">Tid</th>
                                    <th style="width: 120px;">Type</th>
                                    <th>Melding</th>
                                </tr>
                            </thead>
                            <tbody id="messageList">
                                <tr><td colspan="3" class="text-center text-muted">Ingen meldinger</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <div class="sidebar">
                <iframe width="350" height="450" src="https://live.safesky.app/map?lat=59.9&lng=10.7&zoom=7&metric=feet" frameborder="0"></iframe>
                <iframe width="350" height="450" src="https://embed.windy.com/embed.html?type=map&location=coordinates&metricRain=mm&metricTemp=°C&metricWind=m/s&zoom=7&overlay=rain&product=ecmwf&level=surface&lat=59.9&lon=10.6&message=true" frameborder="0"></iframe>

                <h3>Ullevål Sykehus</h3>
                <img src="https://www.yr.no/webcams/1/2000/enuh/3.jpg" width="350" height="250" alt="" />
                <h3>NLA Lørenskog</h3>
                <img src="https://www.yr.no/webcams/1/2000/lorenskog2/1.jpg" width="350" height="250" alt="" />
            </div>
        </div>
    </div>

    <div id="actionModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Aksjonsdetaljer</h2>
                <button class="close-btn" onclick="closeActionModal()">✕</button>
            </div>
            <div class="form-group">
                <label>Aksjonsområde</label>
                <input type="text" id="actionArea" placeholder="Stedsnavn">
            </div>
            <div class="form-group">
                <label>IPP</label>
                <input type="text" id="ipp" placeholder="Koordinater eller adresse">
            </div>
            <div class="form-group">
                <label>SAR-TG</label>
                <input type="text" id="SarTg" placeholder="f.eks. 01-SAR-1">
            </div>
            <div class="form-group">
                <label>VHF Frekvens</label>
                <input type="text" id="Vhf" placeholder="f.eks. 123.100 MHz">
            </div>
            <div class="form-group">
                <label>Begrensninger (restriksjoner, tidsfrister osv.)</label>
                <textarea id="limitations" placeholder="Begresninger..." rows="2"></textarea>
            </div>
            <div class="form-group">
                <label>Annet (nyttig informasjon)</label>
                <textarea id="other" placeholder="Annen relevant info..." rows="2"></textarea>
            </div>
            <button class="btn btn-primary" onclick="saveAction()" style="width: 100%; margin-top: 24px;">💾 Lagre</button>
        </div>
    </div>

    <div id="aircraftModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="aircraftModalTitle">Registrer Luftfartøy</h2>
                <button class="close-btn" onclick="closeAircraftModal()">✕</button>
            </div>
            <input type="hidden" id="aircraftId">
            <div class="form-group">
                <label>Kallesignal *</label>
                <input type="text" id="callsign" placeholder="f.eks. NF Drone1 eller Heli 3-0">
            </div>
            <div class="form-group">
                <label>Type *</label>
                <select id="aircraftType">
                    <option value="">Velg type</option>
                    <option value="Helikopter">Helikopter</option>
                    <option value="Småfly">Småfly</option>
                    <option value="Drone">Drone</option>
                </select>
            </div>
            <div class="form-group">
                <label>Pilot/Operatør</label>
                <input type="text" id="pilot" placeholder="Navn">
            </div>
            <div class="form-group">
                <label>Søksområde / Teig</label>
                <textarea id="aircraftSearchArea" placeholder="Sektor/Teig" rows="2"></textarea>
            </div>
            <div class="form-row" style="margin-bottom: 0;">
                <div class="form-group">
                    <label>Status</label>
                    <select id="aircraftStatus">
                        <option value="Standby">Standby</option>
                        <option value="Aktiv">Aktiv</option>
                        <option value="Avsluttet">Avsluttet</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Høyde (Fot)</label>
                    <input type="text" id="aircraftHeight" placeholder="f.eks. 500">
                </div>
            </div>
            <div class="form-group">
                <label>Kommentar</label>
                <textarea id="aircraftComment" placeholder="Fritekst..." rows="2"></textarea>
            </div>
            <button class="btn btn-primary" id="aircraftSaveButton" onclick="saveAircraft()" style="width: 100%; margin-top: 24px;">➕ Registrer</button>
        </div>
    </div>
    
    <div id="separationModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="separationModalTitle">Legg til Separasjon</h2>
                <button class="close-btn" onclick="closeSeparationModal()">✕</button>
            </div>
            <input type="hidden" id="separationId">
            <div class="form-group">
                <label>Velg ressurser (velg to eller flere) *</label>
                <div id="sepResourcesContainer" style="max-height: 150px; overflow-y: auto; border: 1px solid var(--border); padding: 10px; border-radius: 8px; background: white; margin-bottom: 10px;">
                </div>
            </div>
            <div class="form-group">
                <label>Type *</label>
                <select id="sepType">
                    <option value="">Velg type</option>
                    <option value="Høyde (ft)">Høyde (ft)</option>
                    <option value="Geografisk">Geografisk</option>
                    <option value="Tid">Tid</option>
                </select>
            </div>
            <div class="form-group">
                <label>Status</label>
                <select id="sepStatus">
                    <option value="Aktiv">Aktiv</option>
                    <option value="Inaktiv">Inaktiv</option>
                </select>
            </div>
            <div class="form-group">
                <label>Beskrivelse *</label>
                <input type="text" id="sepValue" placeholder="f.eks. Drone holder seg vest for elven">
            </div>
            <button class="btn btn-primary" id="separationSaveButton" onclick="saveSeparation()" style="width: 100%; margin-top: 24px;">➕ Lagre</button>
        </div>
    </div>

    <script>
        function escapeHtml(value) {
            return String(value || '')
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }

        function joinNorwegian(parts) {
            const cleanParts = parts.filter(Boolean);
            if (cleanParts.length === 0) return '';
            if (cleanParts.length === 1) return cleanParts[0];
            if (cleanParts.length === 2) return `${cleanParts[0]} og ${cleanParts[1]}`;
            return `${cleanParts.slice(0, -1).join(', ')} og ${cleanParts[cleanParts.length - 1]}`;
        }

        function uniqueValues(values) {
            return [...new Set(values.filter(Boolean))];
        }

        function formatSignedMetarTemperature(value) {
            if (!value) return '';
            return parseInt(value.replace('M', '-'), 10);
        }

        function translateWeatherToken(token) {
            if (!token) return '';

            const descriptors = {
                MI: 'grunn', PR: 'delvis', BC: 'banker av', DR: 'lav drivende', BL: 'blåsende',
                SH: 'byger', TS: 'tordenvær', FZ: 'underkjølt'
            };

            const phenomena = {
                DZ: 'yr', RA: 'regn', SN: 'snø', SG: 'snøkorn', IC: 'iskrystaller',
                PL: 'isnåler', GR: 'hagl', GS: 'småhagl', UP: 'ukjent nedbør',
                BR: 'dis', FG: 'tåke', FU: 'røyk', VA: 'vulkansk aske', DU: 'støv',
                SA: 'sand', HZ: 'tørrdis', PY: 'sjøsprøyt', PO: 'støv-/sandvirvler',
                SQ: 'vindbyger', FC: 'skypumpe/tornado', SS: 'sandstorm', DS: 'støvstorm'
            };

            let working = token.toUpperCase();
            let intensity = '';
            let vicinity = false;

            if (working.startsWith('+')) {
                intensity = 'kraftig ';
                working = working.substring(1);
            } else if (working.startsWith('-')) {
                intensity = 'lett ';
                working = working.substring(1);
            }

            if (working.startsWith('VC')) {
                vicinity = true;
                working = working.substring(2);
            }

            const descriptorWords = [];
            const phenomenonWords = [];

            while (working.length >= 2) {
                const code = working.substring(0, 2);
                if (descriptors[code]) {
                    descriptorWords.push(descriptors[code]);
                    working = working.substring(2);
                } else if (phenomena[code]) {
                    phenomenonWords.push(phenomena[code]);
                    working = working.substring(2);
                } else {
                    return '';
                }
            }

            if (working.length !== 0 || (descriptorWords.length === 0 && phenomenonWords.length === 0)) {
                return '';
            }

            let phrase = '';
            if (descriptorWords.length > 0 && phenomenonWords.length > 0) {
                phrase = `${descriptorWords.join(' og ')} med ${phenomenonWords.join(' og ')}`;
            } else if (descriptorWords.length > 0) {
                phrase = descriptorWords.join(' og ');
            } else {
                phrase = phenomenonWords.join(' og ');
            }

            phrase = intensity + phrase;
            if (vicinity) phrase = `${phrase} i nærheten`;
            return phrase;
        }

        function getLatestMetarFromText(text) {
            if (!text) return '';

            const entries = text
                .replace(/\r/g, '\n')
                .split(/=\s*|\n+/)
                .map(entry => entry.trim())
                .filter(Boolean)
                .map(entry => entry.replace(/^(METAR|SPECI)\s+/i, '').trim())
                .filter(entry => /^ENGM\s+\d{6}Z\b/i.test(entry));

            if (entries.length > 0) {
                return entries[entries.length - 1];
            }

            const matches = text.match(/(?:METAR\s+|SPECI\s+)?ENGM\s+\d{6}Z\b[^=\n\r]*/gi);
            if (matches && matches.length > 0) {
                return matches[matches.length - 1].replace(/^(METAR|SPECI)\s+/i, '').trim();
            }

            return '';
        }

        function parseMetar(metarStr) {
            if (!metarStr || metarStr.includes('Laster') || metarStr.includes('Kunne ikke')) return '';

            const cleaned = metarStr
                .replace(/=$/, '')
                .replace(/^(METAR|SPECI)\s+/i, '')
                .trim();

            const tokens = cleaned.split(/\s+/).filter(Boolean);
            if (tokens.length === 0) return '';

            let station = '';
            let obsTime = '';
            let wind = '';
            let windVariation = '';
            let visibility = '';
            let cavok = false;
            let temperature = '';
            let dewpoint = '';
            let qnh = '';
            let trend = '';
            let inTrendSection = false;
            const weather = [];
            const clouds = [];

            const cloudCoverage = {
                FEW: 'få skyer',
                SCT: 'spredte skyer',
                BKN: 'brutt skydekke',
                OVC: 'overskyet'
            };

            for (const originalToken of tokens) {
                const token = originalToken.toUpperCase();

                if (/^(TEMPO|BECMG|PROB30|PROB40)$/.test(token)) {
                    trend = token === 'TEMPO'
                        ? 'midlertidige endringer er meldt'
                        : token === 'BECMG'
                            ? 'gradvis endring er meldt'
                            : 'sannsynlige endringer er meldt';
                    inTrendSection = true;
                    continue;
                }

                if (token === 'NOSIG') {
                    trend = 'ingen signifikant endring er meldt';
                    continue;
                }

                // Ikke bland varslede TEMPO/BECMG-forhold inn i selve observasjonen.
                if (inTrendSection) continue;

                if (/^[A-Z]{4}$/.test(token) && !station) {
                    station = token;
                    continue;
                }

                const timeMatch = token.match(/^(\d{2})(\d{2})(\d{2})Z$/);
                if (timeMatch) {
                    obsTime = `${timeMatch[2]}:${timeMatch[3]}`;
                    continue;
                }

                const windMatch = token.match(/^([0-9]{3}|VRB)([0-9]{2,3})(G([0-9]{2,3}))?KT$/);
                if (windMatch) {
                    const direction = windMatch[1] === 'VRB' ? 'skiftende retning' : `fra ${windMatch[1]}°`;
                    const knots = parseInt(windMatch[2], 10);
                    const ms = Math.round(knots * 0.51444);
                    wind = `${direction} med ${ms} m/s (${knots} kt)`;

                    if (windMatch[4]) {
                        const gustKnots = parseInt(windMatch[4], 10);
                        const gustMs = Math.round(gustKnots * 0.51444);
                        wind += `, kast opp mot ${gustMs} m/s (${gustKnots} kt)`;
                    }
                    continue;
                }

                const windVariationMatch = token.match(/^(\d{3})V(\d{3})$/);
                if (windVariationMatch) {
                    windVariation = `mellom ${windVariationMatch[1]}° og ${windVariationMatch[2]}°`;
                    continue;
                }

                if (token === 'CAVOK') {
                    cavok = true;
                    visibility = 'over 10 km';
                    clouds.push('ingen signifikante skyer under 5000 fot');
                    continue;
                }

                const visibilityMatch = token.match(/^(\d{4})(N|NE|E|SE|S|SW|W|NW)?$/);
                if (visibilityMatch && !visibility) {
                    const meters = parseInt(visibilityMatch[1], 10);
                    visibility = meters === 9999 ? 'over 10 km' : `${(meters / 1000).toFixed(1)} km`;
                    continue;
                }

                const tempMatch = token.match(/^(M?\d{2})\/(M?\d{2})$/);
                if (tempMatch) {
                    temperature = formatSignedMetarTemperature(tempMatch[1]);
                    dewpoint = formatSignedMetarTemperature(tempMatch[2]);
                    continue;
                }

                const qnhMatch = token.match(/^Q(\d{4})$/);
                if (qnhMatch) {
                    qnh = qnhMatch[1];
                    continue;
                }

                const cloudMatch = token.match(/^(FEW|SCT|BKN|OVC)(\d{3})(CB|TCU)?$/);
                if (cloudMatch) {
                    const heightFeet = parseInt(cloudMatch[2], 10) * 100;
                    const cloudType = cloudMatch[3]
                        ? cloudMatch[3] === 'CB'
                            ? ', cumulonimbus'
                            : ', towering cumulus'
                        : '';
                    clouds.push(`${cloudCoverage[cloudMatch[1]]} på ${heightFeet} fot${cloudType}`);
                    continue;
                }

                if (token === 'NSC' || token === 'NCD' || token === 'SKC' || token === 'CLR') {
                    clouds.push('ingen signifikante skyer');
                    continue;
                }

                const translatedWeather = translateWeatherToken(token);
                if (translatedWeather) {
                    weather.push(translatedWeather);
                }
            }

            const details = [];
            if (wind) details.push(`vinden er ${wind}`);
            if (windVariation) details.push(`vindretningen varierer ${windVariation}`);
            if (visibility) details.push(`sikten er ${visibility}`);
            if (weather.length > 0) details.push(`været er ${uniqueValues(weather).join(', ')}`);
            if (clouds.length > 0 && !cavok) details.push(`skydekke er ${uniqueValues(clouds).join(', ')}`);
            if (clouds.length > 0 && cavok) details.push(uniqueValues(clouds).join(', '));
            if (temperature !== '') {
                details.push(`temperaturen er ${temperature}°C${dewpoint !== '' ? ` og duggpunktet er ${dewpoint}°C` : ''}`);
            }
            if (qnh) details.push(`QNH er ${qnh} hPa`);
            if (trend) details.push(trend);

            if (details.length === 0) {
                return 'METAR funnet, men ingen kjente felt kunne tolkes automatisk.';
            }

            const intro = station
                ? `METAR for ${station}${obsTime ? ` observert kl. ${obsTime} UTC` : ''}:`
                : 'METAR:';

            return `${intro} ${joinNorwegian(details)}.`;
        }

        const ACTION_HISTORY_FIELDS = ['actionArea', 'ipp', 'sarTg', 'vhfFreq', 'limitations', 'other'];
        const ACTION_LABELS = {
            actionArea: 'AKSJONSOMRÅDE',
            ipp: 'IPP',
            sarTg: 'SAR-TG',
            vhfFreq: 'VHF FREKVENS',
            limitations: 'BEGRENSNINGER',
            other: 'ANNET/MERKNADER'
        };
        const AIRCRAFT_HISTORY_FIELDS = ['callsign', 'type', 'pilot', 'searchArea', 'status', 'height', 'comment'];
        const AIRCRAFT_LABELS = {
            callsign: 'Kallesignal',
            type: 'Type',
            pilot: 'Pilot/Operatør',
            searchArea: 'Søksområde/Teig',
            status: 'Status',
            height: 'Flyhøyde',
            comment: 'Kommentar'
        };
        const SEPARATION_HISTORY_FIELDS = ['description', 'status', 'type', 'value'];
        const SEPARATION_LABELS = {
            description: 'Ressurser',
            status: 'Status',
            type: 'Type',
            value: 'Beskrivelse'
        };

        let data = {
            action: { actionArea: '', ipp: '', sarTg: '', vhfFreq: '', limitations: '', other: '' },
            actionHistory: createEmptyHistory(ACTION_HISTORY_FIELDS),
            currentMetar: { time: '', raw: '', translation: '' },
            metarHistory: [],
            aircraft: [],
            separations: [],
            messages: []
        };

        function createEmptyHistory(fields) {
            return fields.reduce((history, field) => {
                history[field] = [];
                return history;
            }, {});
        }

        function ensureHistory(history, fields) {
            const safeHistory = history || {};
            fields.forEach(field => {
                if (!Array.isArray(safeHistory[field])) safeHistory[field] = [];
            });
            return safeHistory;
        }

        function normalizeValue(value) {
            if (value === undefined || value === null || value === '') return '-';
            if (Array.isArray(value)) return value.length ? value.join(' ↔ ') : '-';
            return String(value);
        }

        function recordHistory(history, field, oldValue, newValue) {
            if (!history) return;
            if (!Array.isArray(history[field])) history[field] = [];

            const oldNormalized = normalizeValue(oldValue);
            const newNormalized = normalizeValue(newValue);
            if (oldNormalized === newNormalized) return;

            history[field].push({
                time: new Date().toLocaleString('no-NO'),
                from: oldNormalized,
                to: newNormalized
            });
        }

        function getReportHistoryLines(historyEntries, maxEntries = 6) {
            if (!Array.isArray(historyEntries) || historyEntries.length === 0) return [];
            return historyEntries.slice(-maxEntries).map(entry => {
                const from = normalizeValue(entry.from);
                const to = normalizeValue(entry.to);
                return `    - [${entry.time || '-'}] ${from} ➔ ${to}`;
            });
        }

        function formatReportField(label, currentValue, historyEntries) {
            const currentLine = `${label.padEnd(18)} ${normalizeValue(currentValue)}`;
            const historyLines = getReportHistoryLines(historyEntries);
            if (historyLines.length === 0) return currentLine;
            return `${currentLine}\n  Tidligere endringer:\n${historyLines.join('\n')}`;
        }

        function formatAircraftHistorySection(aircraft) {
            const lines = [];
            AIRCRAFT_HISTORY_FIELDS.forEach(field => {
                const historyLines = getReportHistoryLines(aircraft.history?.[field], 5);
                if (historyLines.length > 0) {
                    lines.push(`  Tidligere ${AIRCRAFT_LABELS[field].toLowerCase()}:`);
                    lines.push(historyLines.join('\n'));
                }
            });
            return lines.length > 0 ? `\n${lines.join('\n')}` : '';
        }

        function formatSeparationHistorySection(separation) {
            const lines = [];
            SEPARATION_HISTORY_FIELDS.forEach(field => {
                const historyLines = getReportHistoryLines(separation.history?.[field], 5);
                if (historyLines.length > 0) {
                    lines.push(`  Tidligere ${SEPARATION_LABELS[field].toLowerCase()}:`);
                    lines.push(historyLines.join('\n'));
                }
            });
            return lines.length > 0 ? `\n${lines.join('\n')}` : '';
        }

        function getAircraftById(id) {
            return data.aircraft.find(a => String(a.id) === String(id));
        }

        function getSeparationById(id) {
            return data.separations.find(s => String(s.id) === String(id));
        }

        function getSeparationResourceIds(separation) {
            if (!separation) return [];
            if (Array.isArray(separation.resources) && separation.resources.length > 0) {
                return separation.resources.map(String);
            }

            // Bakoverkompatibilitet: eldre separasjoner hadde bare tekstbeskrivelse.
            const description = separation.description || '';
            return data.aircraft
                .filter(a => description.includes(a.callsign))
                .map(a => String(a.id));
        }

        function getSeparationDescription(resourceIds) {
            const names = resourceIds
                .map(id => getAircraftById(id))
                .filter(Boolean)
                .map(a => a.callsign);
            return names.length > 0 ? names.join(' ↔ ') : 'Udefinerte ressurser';
        }

        function addToAreaHistory(aircraft, value) {
            const formattedArea = (value || '').trim();
            if (!formattedArea) return;
            if (!Array.isArray(aircraft.areaHistory)) aircraft.areaHistory = [];
            if (!aircraft.areaHistory.includes(formattedArea)) aircraft.areaHistory.push(formattedArea);
        }

        function ensureDataShape() {
            if (!data || typeof data !== 'object') data = {};
            if (!data.action) data.action = {};
            if (data.action.weather !== undefined) delete data.action.weather;
            ACTION_HISTORY_FIELDS.forEach(field => {
                if (data.action[field] === undefined) data.action[field] = '';
            });
            data.actionHistory = ensureHistory(data.actionHistory, ACTION_HISTORY_FIELDS);

            if (!Array.isArray(data.aircraft)) data.aircraft = [];
            data.aircraft.forEach(a => {
                if (!a.id) a.id = Date.now() + Math.floor(Math.random() * 100000);
                if (a.callsign === undefined) a.callsign = '';
                if (a.type === undefined) a.type = '';
                if (a.pilot === undefined) a.pilot = '';
                if (a.searchArea === undefined) a.searchArea = '';
                if (a.status === undefined) a.status = 'Standby';
                if (a.height === undefined || a.height === '') a.height = '-';
                if (a.comment === undefined) a.comment = '';
                if (!Array.isArray(a.areaHistory)) a.areaHistory = a.searchArea ? [a.searchArea] : [];
                a.history = ensureHistory(a.history, AIRCRAFT_HISTORY_FIELDS);
            });

            if (!Array.isArray(data.separations)) data.separations = [];
            data.separations.forEach(s => {
                if (!s.id) s.id = Date.now() + Math.floor(Math.random() * 100000);
                if (s.description === undefined) s.description = '';
                if (s.type === undefined) s.type = '';
                if (s.value === undefined) s.value = '';
                if (s.status === undefined || !['Aktiv', 'Inaktiv'].includes(s.status)) s.status = 'Aktiv';
                if (!Array.isArray(s.resources)) s.resources = getSeparationResourceIds(s);
                s.history = ensureHistory(s.history, SEPARATION_HISTORY_FIELDS);
            });

            if (!Array.isArray(data.messages)) data.messages = [];
            if (!data.currentMetar) data.currentMetar = { time: '', raw: '', translation: '' };
            if (!Array.isArray(data.metarHistory)) data.metarHistory = [];
        }

        function loadData() {
            const saved = localStorage.getItem('luftkoordineringData');
            if (saved) {
                try {
                    data = JSON.parse(saved);
                } catch (e) {
                    console.error('Feil ved lasting:', e);
                }
            }
            ensureDataShape();
            updateUI();
        }

        function saveData() {
            ensureDataShape();
            localStorage.setItem('luftkoordineringData', JSON.stringify(data));
        }

        function showAlert(msg, type = 'success') {
            const container = document.getElementById('alertsContainer');
            const alert = document.createElement('div');
            alert.className = `alert alert-${type}`;
            alert.textContent = msg;
            container.appendChild(alert);
            setTimeout(() => alert.remove(), 3000);
        }

        function logAction(message, isSystem = true) {
            data.messages.push({
                time: new Date().toLocaleTimeString('no-NO'),
                type: isSystem ? 'SYSTEM' : 'MANUELL',
                message: message
            });
            saveData();
        }

        // MODAL FUNCTIONS
        function openActionModal() {
            document.getElementById('actionModal').classList.add('active');
            document.getElementById('actionArea').value = data.action.actionArea || '';
            document.getElementById('ipp').value = data.action.ipp || '';
            document.getElementById('SarTg').value = data.action.sarTg || '';
            document.getElementById('Vhf').value = data.action.vhfFreq || '';
            document.getElementById('limitations').value = data.action.limitations || '';
            document.getElementById('other').value = data.action.other || '';
        }

        function closeActionModal() {
            document.getElementById('actionModal').classList.remove('active');
        }

        function openAircraftModal(id = null) {
            const isEdit = id !== null && id !== undefined;
            const aircraft = isEdit ? getAircraftById(id) : null;

            document.getElementById('aircraftModal').classList.add('active');
            document.getElementById('aircraftModalTitle').textContent = aircraft ? 'Rediger Luftfartøy' : 'Registrer Luftfartøy';
            document.getElementById('aircraftSaveButton').textContent = aircraft ? '💾 Lagre endringer' : '➕ Registrer';
            document.getElementById('aircraftId').value = aircraft ? aircraft.id : '';
            document.getElementById('callsign').value = aircraft ? aircraft.callsign || '' : '';
            document.getElementById('aircraftType').value = aircraft ? aircraft.type || '' : '';
            document.getElementById('pilot').value = aircraft ? aircraft.pilot || '' : '';
            document.getElementById('aircraftSearchArea').value = aircraft ? aircraft.searchArea || '' : '';
            document.getElementById('aircraftStatus').value = aircraft ? aircraft.status || 'Standby' : 'Standby';
            document.getElementById('aircraftHeight').value = aircraft ? aircraft.height || '-' : '-';
            document.getElementById('aircraftComment').value = aircraft ? aircraft.comment || '' : '';
        }

        function closeAircraftModal() {
            document.getElementById('aircraftModal').classList.remove('active');
        }

        function openSeparationModal(id = null) {
            const isEdit = id !== null && id !== undefined;
            const separation = isEdit ? getSeparationById(id) : null;
            const selectedIds = separation ? getSeparationResourceIds(separation) : [];

            document.getElementById('separationModal').classList.add('active');
            document.getElementById('separationModalTitle').textContent = separation ? 'Rediger Separasjon' : 'Legg til Separasjon';
            document.getElementById('separationSaveButton').textContent = separation ? '💾 Lagre endringer' : '➕ Lagre';
            document.getElementById('separationId').value = separation ? separation.id : '';
            document.getElementById('sepType').value = separation ? separation.type || '' : '';
            document.getElementById('sepStatus').value = separation ? separation.status || 'Aktiv' : 'Aktiv';
            document.getElementById('sepValue').value = separation ? separation.value || '' : '';
            
            const container = document.getElementById('sepResourcesContainer');
            if (data.aircraft.length === 0) {
                container.innerHTML = '<span class="text-muted" style="font-size:0.9rem;">Ingen registrerte luftfartøy tilgjengelig.</span>';
                return;
            }
            
            container.innerHTML = data.aircraft.map(a => {
                const idValue = String(a.id);
                const checked = selectedIds.includes(idValue) ? 'checked' : '';
                return `
                    <div style="display: flex; align-items: center; gap: 8px; margin-bottom: 6px;">
                        <input type="checkbox" name="sepAircraftCheck" value="${escapeHtml(idValue)}" id="chk_${escapeHtml(idValue)}" style="width:auto;" ${checked}>
                        <label for="chk_${escapeHtml(idValue)}" style="margin:0; font-weight:400; cursor:pointer;">${escapeHtml(a.callsign)} (${escapeHtml(a.type)})</label>
                    </div>
                `;
            }).join('');
        }

        function closeSeparationModal() {
            document.getElementById('separationModal').classList.remove('active');
        }

        // SAVE FUNCTIONS
        function saveAction() {
            const oldAction = { ...data.action };
            
            const newAction = {
                actionArea: document.getElementById('actionArea').value.trim(),
                ipp: document.getElementById('ipp').value.trim(),
                sarTg: document.getElementById('SarTg').value.trim(),
                vhfFreq: document.getElementById('Vhf').value.trim(),
                limitations: document.getElementById('limitations').value.trim(),
                other: document.getElementById('other').value.trim()
            };

            let changes = [];
            ACTION_HISTORY_FIELDS.forEach(field => {
                if (normalizeValue(oldAction[field]) !== normalizeValue(newAction[field])) {
                    recordHistory(data.actionHistory, field, oldAction[field], newAction[field]);
                    changes.push(`${ACTION_LABELS[field]}: "${normalizeValue(oldAction[field])}" ➔ "${normalizeValue(newAction[field])}"`);
                }
            });

            data.action = newAction;

            if (changes.length > 0) {
                logAction(`Operasjonsdetaljer oppdatert: ${changes.join(', ')}`, true);
            }

            saveData();
            updateUI();
            closeActionModal();
            showAlert('Aksjon lagret!', 'success');
        }

        function saveAircraft() {
            const id = document.getElementById('aircraftId').value;
            const callsign = document.getElementById('callsign').value.trim();
            const type = document.getElementById('aircraftType').value;
            const pilot = document.getElementById('pilot').value.trim();
            const searchArea = document.getElementById('aircraftSearchArea').value.trim();
            const status = document.getElementById('aircraftStatus').value || 'Standby';
            const height = document.getElementById('aircraftHeight').value.trim() || '-';
            const comment = document.getElementById('aircraftComment').value.trim();

            if (!callsign || !type) {
                showAlert('Fyll inn kallesignal og type', 'danger');
                return;
            }

            if (type === 'Drone' && !callsign.toLowerCase().includes('drone')) {
                showAlert('Drone-kallesignal må inneholde ordet "drone"', 'danger');
                return;
            }

            const aircraft = id ? getAircraftById(id) : null;

            if (aircraft) {
                const oldCallsign = aircraft.callsign;
                const updates = { callsign, type, pilot, searchArea, status, height, comment };
                const changes = [];

                AIRCRAFT_HISTORY_FIELDS.forEach(field => {
                    if (normalizeValue(aircraft[field]) !== normalizeValue(updates[field])) {
                        recordHistory(aircraft.history, field, aircraft[field], updates[field]);
                        changes.push(`${AIRCRAFT_LABELS[field]}: "${normalizeValue(aircraft[field])}" ➔ "${normalizeValue(updates[field])}"`);
                        aircraft[field] = updates[field];
                    }
                });

                addToAreaHistory(aircraft, aircraft.searchArea);

                if (changes.length > 0) {
                    logAction(`Luftfartøy oppdatert (${oldCallsign}): ${changes.join(', ')}`, true);
                }

                saveData();
                updateUI();
                closeAircraftModal();
                showAlert('Luftfartøy oppdatert!', 'success');
                return;
            }

            const newAircraft = {
                id: Date.now(),
                callsign,
                type,
                pilot,
                searchArea,
                areaHistory: searchArea ? [searchArea] : [],
                height,
                status,
                comment,
                history: createEmptyHistory(AIRCRAFT_HISTORY_FIELDS)
            };

            data.aircraft.push(newAircraft);
            logAction(`Nytt luftfartøy registrert: ${callsign} (${type})`, true);
            saveData();
            updateUI();
            closeAircraftModal();
            showAlert('Luftfartøy registrert!', 'success');
        }

        function saveSeparation() {
            const id = document.getElementById('separationId').value;
            const type = document.getElementById('sepType').value;
            const status = document.getElementById('sepStatus').value || 'Aktiv';
            const value = document.getElementById('sepValue').value.trim();

            const checkedBoxes = document.querySelectorAll('input[name="sepAircraftCheck"]:checked');
            const selectedResources = Array.from(checkedBoxes).map(cb => cb.value);

            if (selectedResources.length < 2) {
                showAlert('Du må velge minst to ressurser for å opprette en separasjon', 'danger');
                return;
            }
            if (!type || !value) {
                showAlert('Fyll inn alle felt', 'danger');
                return;
            }

            const description = getSeparationDescription(selectedResources);
            const separation = id ? getSeparationById(id) : null;

            if (separation) {
                const oldDescription = separation.description;
                const updates = { description, status, type, value };
                const changes = [];

                SEPARATION_HISTORY_FIELDS.forEach(field => {
                    if (normalizeValue(separation[field]) !== normalizeValue(updates[field])) {
                        recordHistory(separation.history, field, separation[field], updates[field]);
                        changes.push(`${SEPARATION_LABELS[field]}: "${normalizeValue(separation[field])}" ➔ "${normalizeValue(updates[field])}"`);
                        separation[field] = updates[field];
                    }
                });

                separation.resources = selectedResources;

                if (changes.length > 0) {
                    logAction(`Separasjon oppdatert: [${oldDescription}] ${changes.join(', ')}`, true);
                }

                saveData();
                updateUI();
                closeSeparationModal();
                showAlert('Separasjon oppdatert!', 'success');
                return;
            }

            data.separations.push({
                id: Date.now(),
                resources: selectedResources,
                description,
                type,
                status,
                value,
                history: createEmptyHistory(SEPARATION_HISTORY_FIELDS)
            });

            logAction(`Separasjon etablert: [${description}] (${status}) via ${type} på ${value}`, true);
            saveData();
            updateUI();
            closeSeparationModal();
            showAlert('Separasjon lagret!', 'success');
        }

        function addMessage() {
            const message = document.getElementById('messageInput').value.trim();
            if (!message) {
                showAlert('Skriv en melding', 'danger');
                return;
            }

            logAction(message, false);
            document.getElementById('messageInput').value = '';
            updateUI();
            showAlert('Melding sendt!', 'success');
        }

        // INLINE TABLE UPDATES
        function updateAircraftStatus(id, status) {
            const aircraft = getAircraftById(id);
            if (aircraft) {
                const oldStatus = aircraft.status;
                if (normalizeValue(oldStatus) !== normalizeValue(status)) {
                    recordHistory(aircraft.history, 'status', oldStatus, status);
                    aircraft.status = status;
                    logAction(`Status endret for ${aircraft.callsign}: ${normalizeValue(oldStatus)} ➔ ${normalizeValue(status)}`, true);
                    saveData();
                    updateUI();
                }
            }
        }

        function updateAircraftHeight(id, height) {
            const aircraft = getAircraftById(id);
            if (aircraft) {
                const formattedHeight = height.trim() || '-';
                if (normalizeValue(aircraft.height) !== normalizeValue(formattedHeight)) {
                    recordHistory(aircraft.history, 'height', aircraft.height, formattedHeight);
                    aircraft.height = formattedHeight;
                    logAction(`${aircraft.callsign} høyde endret til: ${formattedHeight}`, true);
                    saveData();
                    updateUI();
                }
            }
        }

        function updateAircraftSearchArea(id, searchArea) {
            const aircraft = getAircraftById(id);
            if (aircraft) {
                const formattedArea = searchArea.trim();
                if (normalizeValue(aircraft.searchArea) !== normalizeValue(formattedArea)) {
                    recordHistory(aircraft.history, 'searchArea', aircraft.searchArea, formattedArea);
                    aircraft.searchArea = formattedArea;
                    addToAreaHistory(aircraft, formattedArea);
                    logAction(`${aircraft.callsign} søksområde/teig oppdatert til: "${formattedArea || 'Udefinert'}"`, true);
                    saveData();
                    updateUI();
                }
            }
        }

        function updateAircraftComment(id, comment) {
            const aircraft = getAircraftById(id);
            if (aircraft) {
                const formattedComment = comment.trim();
                if (normalizeValue(aircraft.comment) !== normalizeValue(formattedComment)) {
                    recordHistory(aircraft.history, 'comment', aircraft.comment, formattedComment);
                    aircraft.comment = formattedComment;
                    logAction(`${aircraft.callsign} kommentar oppdatert: "${formattedComment || '-'}"`, true);
                    saveData();
                    updateUI();
                }
            }
        }

        function deleteAircraft(id) {
            const aircraft = getAircraftById(id);
            if (aircraft && confirm('Slett luftfartøy?')) {
                logAction(`Luftfartøy fjernet fra aksjonen: ${aircraft.callsign}`, true);
                data.aircraft = data.aircraft.filter(a => String(a.id) !== String(id));
                saveData();
                updateUI();
                showAlert('Luftfartøy slettet', 'success');
            }
        }

        // FETCH & TRANSLATE METAR FROM MET.NO
        function updateStoredMetar(rawMetar, translation) {
            const oldMetar = data.currentMetar || { raw: '', translation: '' };
            const rawChanged = normalizeValue(oldMetar.raw) !== normalizeValue(rawMetar);
            const translationChanged = normalizeValue(oldMetar.translation) !== normalizeValue(translation);

            if (rawChanged && (oldMetar.raw || oldMetar.translation)) {
                data.metarHistory.push({
                    time: oldMetar.time || new Date().toLocaleString('no-NO'),
                    raw: oldMetar.raw || '-',
                    translation: oldMetar.translation || '-'
                });
                data.metarHistory = data.metarHistory.slice(-50);
            }

            if (rawChanged || translationChanged) {
                data.currentMetar = {
                    time: new Date().toLocaleString('no-NO'),
                    raw: rawMetar || '',
                    translation: translation || ''
                };
                saveData();
            }
        }

        function fetchLatestMetar() {
            fetch('https://api.met.no/weatherapi/tafmetar/1.0/metar.txt?icao=ENGM')
                .then(response => {
                    if (!response.ok) throw new Error('Nettverksfeil');
                    return response.text();
                })
                .then(text => {
                    const rawMetar = getLatestMetarFromText(text);
                    const translationBox = document.getElementById('metarTranslation');

                    if (!rawMetar) {
                        const fallbackText = text.trim() || 'Ingen METAR data tilgjengelig.';
                        document.getElementById('metarContent').textContent = fallbackText;
                        if (translationBox) {
                            translationBox.textContent = 'Fant tekst fra MET.NO, men klarte ikke å identifisere en gyldig ENGM METAR i responsen.';
                        }
                        return;
                    }

                    document.getElementById('metarContent').innerHTML = `<strong>${escapeHtml(rawMetar)}</strong>`;

                    const oversettelse = parseMetar(rawMetar);
                    if (oversettelse) {
                        if (translationBox) {
                            translationBox.textContent = oversettelse;
                        }
                        updateStoredMetar(rawMetar, oversettelse);
                    } else {
                        if (translationBox) {
                            translationBox.textContent = 'METAR ble hentet, men kunne ikke tolkes automatisk.';
                        }
                        updateStoredMetar(rawMetar, 'METAR ble hentet, men kunne ikke tolkes automatisk.');
                    }
                })
                .catch(err => {
                    console.error('Feil ved henting av METAR:', err);
                    document.getElementById('metarContent').innerHTML = '<span style="color: var(--danger); font-size:0.85rem; display:block; margin-bottom: 5px;">Kunne ikke hente automatisk (nettverk/CORS).</span><a href="https://api.met.no/weatherapi/tafmetar/1.0/metar.txt?icao=ENGM" target="_blank" style="color: var(--primary); font-weight:600; font-size: 0.85rem;">Klikk her for å åpne manuelt</a>';
                    const translationBox = document.getElementById('metarTranslation');
                    if (translationBox) {
                        translationBox.textContent = 'Kunne ikke hente METAR. Oversettelse er derfor ikke tilgjengelig.';
                    }
                });
        }

        function updateSeparationStatus(id, status) {
            const sep = getSeparationById(id);
            if (!sep || sep.status === status) return;

            const oldStatus = sep.status || 'Aktiv';
            recordHistory(sep.history, 'status', oldStatus, status);
            sep.status = status;
            logAction(`Status endret for separasjon [${sep.description}]: ${oldStatus} ➔ ${status}`, true);
            saveData();
            updateUI();
        }

        function deleteSeparation(id) {
            const sep = getSeparationById(id);
            if (sep && confirm('Slett separasjon?')) {
                logAction(`Separasjon opphevet: [${sep.description}]`, true);
                data.separations = data.separations.filter(s => String(s.id) !== String(id));
                saveData();
                updateUI();
                showAlert('Separasjon slettet', 'success');
            }
        }

        function resetAll() {
            if (confirm('Er du sikker på at du vil nullstille ALLE data?')) {
                data = {
                    action: { actionArea: '', ipp: '', sarTg: '', vhfFreq: '', limitations: '', other: '' },
                    actionHistory: createEmptyHistory(ACTION_HISTORY_FIELDS),
                    currentMetar: { time: '', raw: '', translation: '' },
                    metarHistory: [],
                    aircraft: [],
                    separations: [],
                    messages: []
                };
                saveData();
                logAction('Systemet ble fullstendig nullstilt.', true);
                updateUI();
                showAlert('Alle data nullstilt!', 'success');
            }
        }

        // UI UPDATES
        function updateUI() {
            ensureDataShape();
            updateHeader();
            updateAircraftTable();
            updateSeparationTable();
            updateMessageTable();
        }

        function updateHeader() {
            document.getElementById('displayActionArea').textContent = data.action.actionArea || '-';
            document.getElementById('displayIpp').textContent = data.action.ipp || '-';
            
            document.getElementById('displaySarTg').textContent = data.action.sarTg || '-';
            document.getElementById('headerSarTg').textContent = data.action.sarTg || '-';
            
            document.getElementById('displayVhf').textContent = data.action.vhfFreq || '-';
            document.getElementById('headerVhf').textContent = data.action.vhfFreq || '-';
            
            document.getElementById('displayLimitations').textContent = data.action.limitations || 'Ingen registrerte begrensninger';
            document.getElementById('displayOther').textContent = data.action.other || '-';
            
            document.getElementById('headerAircraftCount').textContent = data.aircraft.length;
        }

        function updateAircraftTable() {
            const tbody = document.getElementById('aircraftList');
            if (data.aircraft.length === 0) {
                tbody.innerHTML = '<tr><td colspan="8" class="text-center text-muted">Ingen luftfartøy registrert</td></tr>';
                return;
            }

            tbody.innerHTML = data.aircraft.map(a => {
                let typeBadge = escapeHtml(a.type);
                if (a.type === 'Drone') typeBadge = '<span class="badge badge-drone">Drone</span>';
                else if (a.type === 'Helikopter') typeBadge = '<span class="badge badge-helicopter">Helikopter</span>';
                else if (a.type === 'Småfly') typeBadge = '<span class="badge badge-plane">Småfly</span>';

                return `
                    <tr>
                        <td><strong>${escapeHtml(a.callsign)}</strong></td>
                        <td>${typeBadge}</td>
                        <td>${escapeHtml(a.pilot || '-')}</td>
                        <td>
                            <textarea class="inline-input auto-expand" rows="1" 
                                      style="resize: none; width: 100%; min-height: 38px; font-family: inherit; overflow-y: hidden;" 
                                      oninput="this.style.height = 'auto'; this.style.height = this.scrollHeight + 'px';"
                                      onchange="updateAircraftSearchArea(${a.id}, this.value)" 
                                      placeholder="Sektor/Teig">${escapeHtml(a.searchArea || '')}</textarea>
                        </td>
                        <td>
                            <select class="inline-select" onchange="updateAircraftStatus(${a.id}, this.value)">
                                <option value="Standby" ${a.status === 'Standby' ? 'selected' : ''}>Standby</option>
                                <option value="Aktiv" ${a.status === 'Aktiv' ? 'selected' : ''}>Aktiv</option>
                                <option value="Avsluttet" ${a.status === 'Avsluttet' ? 'selected' : ''}>Avsluttet</option>
                            </select>
                        </td>
                        <td style="min-width: 140px;"><input type="text" class="inline-input" style="min-width: 110px; text-align: right;" value="${escapeHtml(a.height)}" onchange="updateAircraftHeight(${a.id}, this.value)" placeholder="ft"></td>
                        <td>
                            <textarea class="inline-input auto-expand" rows="1" 
                                      style="resize: none; width: 100%; min-height: 38px; font-family: inherit; overflow-y: hidden;" 
                                      oninput="this.style.height = 'auto'; this.style.height = this.scrollHeight + 'px';"
                                      onchange="updateAircraftComment(${a.id}, this.value)" 
                                      placeholder="Fritekst...">${escapeHtml(a.comment || '')}</textarea>
                        </td>
                        <td style="white-space: nowrap;">
                            <button class="btn btn-secondary btn-small" onclick="openAircraftModal(${a.id})">Rediger</button>
                            <button class="btn btn-secondary btn-small" onclick="deleteAircraft(${a.id})" style="margin-top: 6px;">Slett</button>
                        </td>
                    </tr>
                `;
            }).join('');

            document.querySelectorAll('.auto-expand').forEach(textarea => {
                textarea.style.height = 'auto';
                textarea.style.height = textarea.scrollHeight + 'px';
            });
        }

        function updateSeparationTable() {
            const tbody = document.getElementById('separationList');
            if (data.separations.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" class="text-center text-muted">Ingen separasjoner definert</td></tr>';
                return;
            }

            tbody.innerHTML = data.separations.map(s => {
                const resourceIds = getSeparationResourceIds(s);
                const currentDescription = resourceIds.length > 0 ? getSeparationDescription(resourceIds) : s.description;
                if (currentDescription && currentDescription !== s.description) s.description = currentDescription;

                return `
                    <tr>
                        <td><strong>${escapeHtml(s.description)}</strong></td>
                        <td>
                            <select class="inline-select" onchange="updateSeparationStatus(${s.id}, this.value)">
                                <option value="Aktiv" ${(s.status || 'Aktiv') === 'Aktiv' ? 'selected' : ''}>Aktiv</option>
                                <option value="Inaktiv" ${s.status === 'Inaktiv' ? 'selected' : ''}>Inaktiv</option>
                            </select>
                        </td>
                        <td>${escapeHtml(s.type)}</td>
                        <td>${escapeHtml(s.value)}</td>
                        <td style="white-space: nowrap;">
                            <button class="btn btn-secondary btn-small" onclick="openSeparationModal(${s.id})">Rediger</button>
                            <button class="btn btn-secondary btn-small" onclick="deleteSeparation(${s.id})" style="margin-top: 6px;">Slett</button>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function updateMessageTable() {
            const tbody = document.getElementById('messageList');
            if (data.messages.length === 0) {
                tbody.innerHTML = '<tr><td colspan="3" class="text-center text-muted">Ingen meldinger</td></tr>';
                return;
            }

            tbody.innerHTML = data.messages.slice().reverse().map(m => {
                const isSystem = m.type === 'SYSTEM';
                const badgeClass = isSystem ? 'badge-log-system' : 'badge-log-manual';
                const textStyle = isSystem ? 'font-style: italic; color: #555;' : 'font-weight: 600; color: #1e293b;';
                
                return `
                    <tr>
                        <td style="font-weight: 700; color: var(--primary); font-size: 0.9rem;">${escapeHtml(m.time)}</td>
                        <td><span class="badge ${badgeClass}" style="width: 100px; display: block;">${escapeHtml(m.type)}</span></td>
                        <td style="${textStyle}">${escapeHtml(m.message)}</td>
                    </tr>
                `;
            }).join('');
        }

        // EXPORT & REPORT
        function exportData() {
            const dataStr = JSON.stringify(data, null, 2);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `SAR-${data.action.actionArea || 'data'}-${new Date().toISOString().split('T')[0]}.json`;
            link.click();
            showAlert('Data eksportert!', 'success');
        }

        function getCurrentMetarForReport() {
            const metarElement = document.getElementById('metarContent');
            const translationElement = document.getElementById('metarTranslation');
            return {
                raw: data.currentMetar?.raw || (metarElement ? metarElement.innerText.replace(/⏱️ Hentet: .*\n?/, '').trim() : '-'),
                translation: data.currentMetar?.translation || (translationElement ? translationElement.innerText.trim() : '-')
            };
        }

        function formatMetarHistoryForReport() {
            if (!Array.isArray(data.metarHistory) || data.metarHistory.length === 0) return '';
            const lines = data.metarHistory.slice(-5).map(entry => `    - [${entry.time || '-'}] ${entry.raw || '-'}\n      ${entry.translation || '-'}`);
            return `\n  Tidligere METAR-er:\n${lines.join('\n')}`;
        }

        function generateReport() {
            ensureDataShape();
            const currentMetar = getCurrentMetarForReport();

            const operationDetails = [
                formatReportField('IPP:', data.action.ipp, data.actionHistory.ipp),
                formatReportField('AKSJONSOMRÅDE:', data.action.actionArea, data.actionHistory.actionArea),
                formatReportField('SAR-TG:', data.action.sarTg, data.actionHistory.sarTg),
                formatReportField('VHF FREKVENS:', data.action.vhfFreq, data.actionHistory.vhfFreq),
                `METAR ENGM:        ${normalizeValue(currentMetar.raw)}${formatMetarHistoryForReport()}`,
                `OVERSATT METAR:    ${normalizeValue(currentMetar.translation)}`,
                formatReportField('BEGRENSNINGER:', data.action.limitations || 'Ingen registrerte begrensninger', data.actionHistory.limitations),
                formatReportField('ANNET/MERKNADER:', data.action.other, data.actionHistory.other)
            ].join('\n');

            const aircraftReportRows = data.aircraft.length === 0
                ? 'Ingen registrerte luftfartøy'
                : data.aircraft.map(a => {
                    const currentArea = a.searchArea || 'Udefinert';
                    const pastAreas = Array.isArray(a.areaHistory) ? a.areaHistory.filter(area => area !== a.searchArea) : [];
                    const areaHistoryText = pastAreas.length > 0 ? `\n  Tidligere søksområder/teiger: ${pastAreas.join(' ➔ ')}` : '';
                    
                    return `• ${a.callsign} [${a.type}]
  Pilot/Operatør:   ${normalizeValue(a.pilot || 'Ukjent')}
  Nåværende område: ${normalizeValue(currentArea)}${areaHistoryText}
  Flyhøyde:         ${normalizeValue(a.height)}
  Siste status:     ${normalizeValue(a.status)}
  Kommentar:        ${normalizeValue(a.comment)}${formatAircraftHistorySection(a)}`;
                }).join('\n\n');

            const separationReportRows = data.separations.length === 0
                ? 'Ingen etablerte separasjoner'
                : data.separations.map(s => {
                    const resourceIds = getSeparationResourceIds(s);
                    const description = resourceIds.length > 0 ? getSeparationDescription(resourceIds) : s.description;
                    return `[${description}]
  Status:      ${normalizeValue(s.status || 'Aktiv')}
  Type:        ${normalizeValue(s.type)}
  Beskrivelse: ${normalizeValue(s.value)}${formatSeparationHistorySection(s)}`;
                }).join('\n\n');

            const report = `SØKSRAPPORT
═══════════════════════════════════════════════════════════

${operationDetails}

───────────────────────────────────────────────────────────
LUFTFARTØY OG HISTORIKK (${data.aircraft.length})
───────────────────────────────────────────────────────────
${aircraftReportRows}

───────────────────────────────────────────────────────────
SEPARASJONER (${data.separations.length})
───────────────────────────────────────────────────────────
${separationReportRows}

───────────────────────────────────────────────────────────
LOGGFØRING (${data.messages.length})
───────────────────────────────────────────────────────────
${data.messages.length === 0 ? 'Ingen loggføringer tilgjengelig' : data.messages.map(m => `[${m.time}] [${m.type}] ${m.message}`).join('\n')}

═══════════════════════════════════════════════════════════
Rapport generert: ${new Date().toLocaleString('no-NO')}
═══════════════════════════════════════════════════════════`;

            const blob = new Blob([report], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `SAR-${data.action.actionArea || 'rapport'}-${new Date().toISOString().split('T')[0]}.txt`;
            link.click();
            showAlert('Rapport generert!', 'success');
        }

        // CLOSE MODALS WITH ESCAPE
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                document.querySelectorAll('.modal.active').forEach(m => m.classList.remove('active'));
            }
        });

        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    modal.classList.remove('active');
                }
            });
        });

        // INITIALIZE
        window.addEventListener('load', () => {
            loadData();
            fetchLatestMetar();
            setInterval(fetchLatestMetar, 600000); // 10 min auto-refresh
        });
    </script>
</body>
</html>
