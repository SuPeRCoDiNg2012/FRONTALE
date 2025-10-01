<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Pianificatore Allenamenti Orienteering</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f8f9fa;
      color: #2c3e50;
      text-align: center;
      padding: 30px;
      line-height: 1.6;
    }
    
    .container {
      max-width: 900px;
      margin: 0 auto;
    }
    
    h1 {
      font-size: 2.2em;
      margin-bottom: 15px;
      color: #2c3e50;
      font-weight: 300;
    }
    
    h2 {
      font-size: 1.5em;
      margin-bottom: 20px;
      color: #34495e;
      font-weight: 400;
    }
    
    h3 {
      font-size: 1.2em;
      margin-bottom: 15px;
      color: #34495e;
      font-weight: 500;
    }
    
    #info, #countdown {
      font-size: 1.1em;
      margin-bottom: 20px;
      color: #5d6d7e;
    }
    
    #risultato {
      font-size: 1.6em;
      padding: 25px;
      background-color: #ffffff;
      border-radius: 8px;
      display: inline-block;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      margin: 20px auto;
      border-left: 4px solid #3498db;
      min-width: 300px;
      min-height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .torcia {
      color: #c0392b;
      font-weight: 500;
    }
    
    .sole {
      color: #27ae60;
      font-weight: 500;
    }
    
    .nuvoloso {
      color: #f39c12;
      font-weight: 500;
    }
    
    .loading {
      color: #7f8c8d;
      font-style: italic;
    }
    
    footer {
      margin-top: 40px;
      font-size: 0.85em;
      color: #7f8c8d;
    }
    
    footer a {
      color: #3498db;
      text-decoration: none;
    }
    
    footer a:hover {
      text-decoration: underline;
    }

    /* Stili per il pannello impostazioni */
    #impostazioni {
      background-color: #ffffff;
      padding: 25px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      margin: 25px auto;
      text-align: left;
      border: 1px solid #e0e0e0;
    }

    .giorno-configurazione {
      margin: 15px 0;
      padding: 15px;
      border: 1px solid #e0e0e0;
      border-radius: 6px;
      background-color: #fafafa;
    }

    .giorno-header {
      display: flex;
      align-items: center;
      margin-bottom: 12px;
    }

    .giorno-header label {
      flex: 1;
      cursor: pointer;
      font-weight: 500;
      font-size: 1.1em;
    }

    .orari-container {
      display: flex;
      align-items: center;
      gap: 15px;
      flex-wrap: wrap;
    }

    .orario-group {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .orario-group label {
      font-size: 0.9em;
      color: #5d6d7e;
      white-space: nowrap;
    }

    .orario-input {
      padding: 8px;
      border: 1px solid #ddd;
      border-radius: 4px;
      width: 90px;
      font-family: inherit;
      background-color: white;
    }

    .orario-input:disabled {
      background-color: #f5f5f5;
      color: #999;
    }

    #salvaImpostazioni {
      background: #2c3e50;
      color: white;
      border: none;
      padding: 12px 25px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1em;
      margin-top: 20px;
      width: 100%;
      font-family: inherit;
      transition: background-color 0.2s;
    }

    #salvaImpostazioni:hover {
      background: #34495e;
    }

    #toggleImpostazioni {
      background: #3498db;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.95em;
      margin-bottom: 15px;
      font-family: inherit;
      transition: background-color 0.2s;
    }

    #toggleImpostazioni:hover {
      background: #2980b9;
    }

    .istruzioni {
      color: #7f8c8d;
      font-size: 0.9em;
      margin-bottom: 20px;
      font-style: italic;
    }

    .status-box {
      background: #f8f9fa;
      border: 1px solid #e9ecef;
      border-radius: 6px;
      padding: 20px;
      margin: 20px 0;
    }

    .durata-info {
      font-size: 0.85em;
      color: #7f8c8d;
      margin-top: 8px;
      font-style: italic;
    }

    .configurazione-posizione {
      background: #f8f9fa;
      border: 1px solid #e9ecef;
      border-radius: 6px;
      padding: 20px;
      margin: 20px 0;
    }

    .citta-select {
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
      width: 200px;
      font-family: inherit;
      margin-right: 10px;
    }

    .meteo-info {
      font-size: 0.9em;
      margin-top: 10px;
      padding: 10px;
      border-radius: 4px;
      background: #f8f9fa;
    }

    .meteo-sole {
      border-left: 4px solid #27ae60;
    }

    .meteo-nuvoloso {
      border-left: 4px solid #f39c12;
    }

    .meteo-pioggia {
      border-left: 4px solid #3498db;
    }

    .meteo-neve {
      border-left: 4px solid #95a5a6;
    }

    .previsione-giorno {
      font-weight: bold;
      color: #2c3e50;
    }

    @media (max-width: 768px) {
      body {
        padding: 20px;
      }
      
      h1 {
        font-size: 1.8em;
      }
      
      #risultato {
        font-size: 1.3em;
        padding: 20px;
        min-width: 250px;
      }
      
      #impostazioni {
        padding: 20px;
      }
      
      .orari-container {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
      }
      
      .orario-group {
        width: 100%;
        justify-content: space-between;
      }
      
      .orario-input {
        width: 100px;
      }
      
      .citta-select {
        width: 100%;
        margin-bottom: 10px;
      }
    }

    @media (max-width: 480px) {
      .giorno-configurazione {
        padding: 10px;
      }
      
      .orario-group {
        flex-direction: column;
        align-items: flex-start;
      }
      
      .orario-input {
        width: 100%;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Pianificatore Allenamenti Orienteering</h1>
    
    <button id="toggleImpostazioni">Configura Allenamenti</button>
    
    <div id="impostazioni" style="display: none;">
      <h3>Configurazione Giorni e Orari di Allenamento</h3>
      <p class="istruzioni">Seleziona i giorni e imposta gli orari di inizio e fine per ogni allenamento:</p>
      
      <div class="configurazione-posizione">
        <h3>Seleziona la tua città</h3>
        <select id="selezionaCitta" class="citta-select">
          <option value="44.4949,11.3426">Bologna</option>
          <option value="45.4642,9.1900">Milano</option>
          <option value="41.9028,12.4964">Roma</option>
          <option value="45.0703,7.6869">Torino</option>
          <option value="40.8518,14.2681">Napoli</option>
          <option value="43.7696,11.2558">Firenze</option>
          <option value="44.4056,8.9463">Genova</option>
          <option value="38.1157,13.3615">Palermo</option>
          <option value="37.5023,15.0873">Catania</option>
          <option value="46.0667,11.1167">Trento</option>
        </select>
        <div id="info-posizione" class="meteo-info">Posizione selezionata: Bologna</div>
      </div>
      
      <div id="giorni-container">
        <!-- I giorni verranno generati dinamicamente via JavaScript -->
      </div>
      
      <button id="salvaImpostazioni">Salva Configurazione</button>
    </div>

    <div class="status-box">
      <div id="info">Prossimo allenamento: <span id="prossimo"></span></div>
      <div id="countdown">Tempo rimanente: <span id="tempo"></span></div>
      <div id="info-meteo" class="meteo-info"></div>
    </div>

    <div id="risultato" class="loading">Analisi condizioni luminose in corso...</div>

    <footer>
      Dati meteo forniti da <a href="https://open-meteo.com" target="_blank">Open-Meteo</a> e 
      <a href="https://sunrise-sunset.org" target="_blank">Sunrise-Sunset API</a>
    </footer>
  </div>

  <script>
    // Nomi dei giorni in italiano
    const giorniSettimana = [
      'Domenica', 'Lunedì', 'Martedì', 'Mercoledì', 
      'Giovedì', 'Venerdì', 'Sabato'
    ];

    // Coordinate delle città italiane principali
    const cittaItaliane = {
      "Bologna": { lat: 44.4949, lng: 11.3426 },
      "Milano": { lat: 45.4642, lng: 9.1900 },
      "Roma": { lat: 41.9028, lng: 12.4964 },
      "Torino": { lat: 45.0703, lng: 7.6869 },
      "Napoli": { lat: 40.8518, lng: 14.2681 },
      "Firenze": { lat: 43.7696, lng: 11.2558 },
      "Genova": { lat: 44.4056, lng: 8.9463 },
      "Palermo": { lat: 38.1157, lng: 13.3615 },
      "Catania": { lat: 37.5023, lng: 15.0873 },
      "Trento": { lat: 46.0667, lng: 11.1167 }
    };

    // Impostazioni predefinite
    let impostazioniAllenamenti = {
      giorni: [false, false, true, false, true, false, false],
      orariInizio: ['18:30', '18:30', '18:30', '18:30', '18:30', '18:30', '18:30'],
      orariFine: ['20:00', '20:00', '20:00', '20:00', '20:00', '20:00', '20:00'],
      citta: "Bologna",
      lat: 44.4949,
      lng: 11.3426
    };

    // Carica le impostazioni salvate
    function caricaImpostazioni() {
      const salvate = localStorage.getItem('impostazioniAllenamenti');
      if (salvate) {
        const impostazioniParse = JSON.parse(salvate);
        // Mantieni compatibilità con le versioni precedenti
        impostazioniAllenamenti = { ...impostazioniAllenamenti, ...impostazioniParse };
        
        // Aggiorna il selettore della città
        const valoreCitta = `${impostazioniAllenamenti.lat},${impostazioniAllenamenti.lng}`;
        document.getElementById('selezionaCitta').value = valoreCitta;
        document.getElementById('info-posizione').textContent = `Posizione selezionata: ${impostazioniAllenamenti.citta}`;
      }
    }

    // Salva le impostazioni
    function salvaImpostazioni() {
      localStorage.setItem('impostazioniAllenamenti', JSON.stringify(impostazioniAllenamenti));
      alert('Configurazione salvata con successo');
      
      // Chiudi il pannello impostazioni
      document.getElementById('impostazioni').style.display = 'none';
      document.getElementById('toggleImpostazioni').textContent = 'Configura Allenamenti';
      
      // Ricalcola tutto
      controllaTorcia();
    }

    // Calcola la durata in ore tra due orari
    function calcolaDurata(orarioInizio, orarioFine) {
      const [oreInizio, minutiInizio] = orarioInizio.split(':').map(Number);
      const [oreFine, minutiFine] = orarioFine.split(':').map(Number);
      
      const inizioMinuti = oreInizio * 60 + minutiInizio;
      const fineMinuti = oreFine * 60 + minutiFine;
      
      if (fineMinuti <= inizioMinuti) {
        return 0; // Orario non valido
      }
      
      return (fineMinuti - inizioMinuti) / 60;
    }

    // Genera l'interfaccia per selezionare i giorni e gli orari
    function generaInterfacciaGiorni() {
      const container = document.getElementById('giorni-container');
      container.innerHTML = '';

      giorniSettimana.forEach((giorno, index) => {
        const div = document.createElement('div');
        div.className = 'giorno-configurazione';
        
        const durata = calcolaDurata(
          impostazioniAllenamenti.orariInizio[index], 
          impostazioniAllenamenti.orariFine[index]
        );
        
        div.innerHTML = `
          <div class="giorno-header">
            <label>
              <input type="checkbox" id="giorno-${index}" ${impostazioniAllenamenti.giorni[index] ? 'checked' : ''}>
              ${giorno}
            </label>
          </div>
          <div class="orari-container">
            <div class="orario-group">
              <label>Inizio:</label>
              <input type="time" id="inizio-${index}" class="orario-input" 
                     value="${impostazioniAllenamenti.orariInizio[index]}" 
                     ${!impostazioniAllenamenti.giorni[index] ? 'disabled' : ''}>
            </div>
            <div class="orario-group">
              <label>Fine:</label>
              <input type="time" id="fine-${index}" class="orario-input" 
                     value="${impostazioniAllenamenti.orariFine[index]}" 
                     ${!impostazioniAllenamenti.giorni[index] ? 'disabled' : ''}>
            </div>
          </div>
          ${durata > 0 ? `<div class="durata-info">Durata: ${durata.toFixed(1)} ore</div>` : ''}
        `;

        const checkbox = div.querySelector(`#giorno-${index}`);
        const inputInizio = div.querySelector(`#inizio-${index}`);
        const inputFine = div.querySelector(`#fine-${index}`);
        const durataInfo = div.querySelector('.durata-info');
        
        // Aggiorna durata quando cambiano gli orari
        function aggiornaDurata() {
          const nuovaDurata = calcolaDurata(inputInizio.value, inputFine.value);
          if (durataInfo) {
            durataInfo.textContent = nuovaDurata > 0 ? 
              `Durata: ${nuovaDurata.toFixed(1)} ore` : 
              'Orari non validi';
          }
        }
        
        inputInizio.addEventListener('change', aggiornaDurata);
        inputFine.addEventListener('change', aggiornaDurata);
        
        checkbox.addEventListener('change', function() {
          const abilitato = this.checked;
          inputInizio.disabled = !abilitato;
          inputFine.disabled = !abilitato;
          aggiornaDurata();
        });

        container.appendChild(div);
      });
    }

    // Aggiorna le impostazioni dall'interfaccia
    function aggiornaImpostazioniDaUI() {
      // Aggiorna posizione
      const cittaSelezionata = document.getElementById('selezionaCitta').value;
      const [lat, lng] = cittaSelezionata.split(',').map(Number);
      const nomeCitta = document.getElementById('selezionaCitta').options[document.getElementById('selezionaCitta').selectedIndex].text;
      
      impostazioniAllenamenti.lat = lat;
      impostazioniAllenamenti.lng = lng;
      impostazioniAllenamenti.citta = nomeCitta;

      // Aggiorna giorni e orari
      giorniSettimana.forEach((_, index) => {
        const checkbox = document.getElementById(`giorno-${index}`);
        const inputInizio = document.getElementById(`inizio-${index}`);
        const inputFine = document.getElementById(`fine-${index}`);
        
        if (checkbox && inputInizio && inputFine) {
          impostazioniAllenamenti.giorni[index] = checkbox.checked;
          impostazioniAllenamenti.orariInizio[index] = inputInizio.value;
          impostazioniAllenamenti.orariFine[index] = inputFine.value;
        }
      });
    }

    // Ottieni le previsioni meteo per il giorno specifico
    async function ottieniPrevisioniMeteo(dataAllenamento) {
      try {
        // Formatta la data per l'API (YYYY-MM-DD)
        const dataFormattata = dataAllenamento.toISOString().split('T')[0];
        
        const response = await fetch(
          `https://api.open-meteo.com/v1/forecast?latitude=${impostazioniAllenamenti.lat}&longitude=${impostazioniAllenamenti.lng}&daily=weathercode,temperature_2m_max,temperature_2m_min&timezone=Europe/Rome&start_date=${dataFormattata}&end_date=${dataFormattata}`
        );
        
        if (!response.ok) {
          throw new Error('Errore nel recupero previsioni meteo');
        }
        
        const data = await response.json();
        return data;
      } catch (error) {
        console.error('Errore previsioni meteo:', error);
        return null;
      }
    }

    // Aggiorna le informazioni meteo per il giorno dell'allenamento
    async function aggiornaInfoMeteo(prossimoAllenamento) {
      const meteoDiv = document.getElementById('info-meteo');
      
      if (!prossimoAllenamento) {
        meteoDiv.innerHTML = '';
        return;
      }
      
      meteoDiv.innerHTML = 'Caricamento previsioni meteo...';
      
      const previsioni = await ottieniPrevisioniMeteo(prossimoAllenamento.data);
      
      if (previsioni && previsioni.daily) {
        const codiceMeteo = previsioni.daily.weathercode[0];
        const tempMax = Math.round(previsioni.daily.temperature_2m_max[0]);
        const tempMin = Math.round(previsioni.daily.temperature_2m_min[0]);
        
        const { descrizione, consiglio, classe } = decodificaCodiceMeteo(codiceMeteo);
        
        const dataFormattata = prossimoAllenamento.data.toLocaleDateString("it-IT", { 
          weekday: 'long', 
          day: 'numeric', 
          month: 'long' 
        });
        
        meteoDiv.className = `meteo-info ${classe}`;
        meteoDiv.innerHTML = `
          <span class="previsione-giorno">Previsioni per ${dataFormattata}:</span><br>
          ${descrizione}, ${tempMin}°C - ${tempMax}°C<br>
          <small>${consiglio}</small>
        `;
      } else {
        meteoDiv.innerHTML = 'Previsioni meteo non disponibili';
      }
    }

    // Decodifica i codici meteo di Open-Meteo
    function decodificaCodiceMeteo(codice) {
      const codiciMeteo = {
        0: { descrizione: 'Cielo sereno', consiglio: 'Ottima visibilità', classe: 'meteo-sole' },
        1: { descrizione: 'Prevalentemente sereno', consiglio: 'Buona visibilità', classe: 'meteo-sole' },
        2: { descrizione: 'Parzialmente nuvoloso', consiglio: 'Visibilità normale', classe: 'meteo-nuvoloso' },
        3: { descrizione: 'Nuvoloso', consiglio: 'Visibilità ridotta', classe: 'meteo-nuvoloso' },
        45: { descrizione: 'Nebbia', consiglio: 'Torcia consigliata', classe: 'meteo-nuvoloso' },
        48: { descrizione: 'Nebbia con brina', consiglio: 'Torcia obbligatoria', classe: 'meteo-nuvoloso' },
        51: { descrizione: 'Pioggerella leggera', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        53: { descrizione: 'Pioggerella moderata', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        55: { descrizione: 'Pioggerella intensa', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        61: { descrizione: 'Pioggia leggera', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        63: { descrizione: 'Pioggia moderata', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        65: { descrizione: 'Pioggia intensa', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        80: { descrizione: 'Rovesci leggeri', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        81: { descrizione: 'Rovesci moderati', consiglio: 'Torcia consigliata', classe: 'meteo-pioggia' },
        82: { descrizione: 'Rovesci violenti', consiglio: 'Allenamento sconsigliato', classe: 'meteo-pioggia' },
        95: { descrizione: 'Temporale', consiglio: 'Allenamento sconsigliato', classe: 'meteo-pioggia' },
        96: { descrizione: 'Temporale con grandine', consiglio: 'Allenamento pericoloso', classe: 'meteo-pioggia' }
      };
      
      return codiciMeteo[codice] || { descrizione: 'Condizioni variabili', consiglio: 'Visibilità normale', classe: 'meteo-nuvoloso' };
    }

    function getProssimoAllenamento() {
      const oggi = new Date();
      const giornoOggi = oggi.getDay();
      
      let prossimoAllenamento = null;
      let giorniMancanti = 0;

      // Cerca il prossimo giorno di allenamento
      for (let i = 1; i <= 7; i++) {
        const giornoCercato = (giornoOggi + i) % 7;
        if (impostazioniAllenamenti.giorni[giornoCercato]) {
          giorniMancanti = i;
          prossimoAllenamento = new Date(oggi);
          prossimoAllenamento.setDate(oggi.getDate() + giorniMancanti);
          break;
        }
      }

      // Se non trovato, cerca nella settimana successiva
      if (!prossimoAllenamento) {
        for (let i = 0; i < 7; i++) {
          if (impostazioniAllenamenti.giorni[i]) {
            giorniMancanti = (7 - giornoOggi + i) % 7 || 7;
            prossimoAllenamento = new Date(oggi);
            prossimoAllenamento.setDate(oggi.getDate() + giorniMancanti);
            break;
          }
        }
      }

      if (prossimoAllenamento) {
        const giornoAllenamento = prossimoAllenamento.getDay();
        const orarioInizio = impostazioniAllenamenti.orariInizio[giornoAllenamento];
        const orarioFine = impostazioniAllenamenti.orariFine[giornoAllenamento];
        const durata = calcolaDurata(orarioInizio, orarioFine);
        
        document.getElementById("prossimo").innerHTML = 
          `${prossimoAllenamento.toLocaleDateString("it-IT", { weekday: 'long', day: 'numeric', month: 'long' })}<br>
           Dalle ${orarioInizio} alle ${orarioFine} (${durata.toFixed(1)} ore)`;
        
        return { 
          data: prossimoAllenamento, 
          orarioInizio: orarioInizio,
          orarioFine: orarioFine,
          durata: durata
        };
      } else {
        document.getElementById("prossimo").innerText = "Nessun allenamento programmato";
        return null;
      }
    }

    function aggiornaCountdown(prossimoAllenamento) {
      if (!prossimoAllenamento) {
        document.getElementById("tempo").innerText = "Nessun allenamento programmato";
        return;
      }

      // Aggiorna immediatamente
      aggiornaTempoRimanente(prossimoAllenamento);

      // Poi aggiorna ogni secondo
      const intervallo = setInterval(() => {
        aggiornaTempoRimanente(prossimoAllenamento);
      }, 1000);

      function aggiornaTempoRimanente(prossimoAllenamento) {
        const [oreInizio, minutiInizio] = prossimoAllenamento.orarioInizio.split(':').map(Number);
        const oraAllenamento = new Date(prossimoAllenamento.data);
        oraAllenamento.setHours(oreInizio, minutiInizio, 0);
        
        const oraAttuale = new Date();
        const diff = oraAllenamento - oraAttuale;

        if (diff <= 0) {
          // Verifica se l'allenamento è ancora in corso
          const [oreFine, minutiFine] = prossimoAllenamento.orarioFine.split(':').map(Number);
          const oraFine = new Date(prossimoAllenamento.data);
          oraFine.setHours(oreFine, minutiFine, 0);
          
          if (oraAttuale < oraFine) {
            document.getElementById("tempo").innerText = "Allenamento in corso";
          } else {
            document.getElementById("tempo").innerText = "Allenamento terminato";
            clearInterval(intervallo);
          }
          return;
        }

        const oreMancanti = Math.floor(diff / 3600000);
        const minutiMancanti = Math.floor((diff % 3600000) / 60000);
        const secondiMancanti = Math.floor((diff % 60000) / 1000);
        document.getElementById("tempo").innerText = `${oreMancanti} ore ${minutiMancanti} minuti ${secondiMancanti} secondi`;
      }
    }

    async function controllaTorcia() {
      document.getElementById("risultato").innerHTML = '<span class="loading">Analisi condizioni luminose in corso...</span>';
      
      const prossimoAllenamento = getProssimoAllenamento();
      
      if (!prossimoAllenamento) {
        document.getElementById("risultato").innerText = "Configurare gli allenamenti nelle impostazioni";
        document.getElementById("tempo").innerText = "Nessun allenamento";
        document.getElementById("info-meteo").innerHTML = '';
        return;
      }

      aggiornaCountdown(prossimoAllenamento);
      await aggiornaInfoMeteo(prossimoAllenamento);

      const dataISO = prossimoAllenamento.data.toISOString().split("T")[0];
      const url = `https://api.sunrise-sunset.org/json?lat=${impostazioniAllenamenti.lat}&lng=${impostazioniAllenamenti.lng}&date=${dataISO}&formatted=0&tzid=Europe/Rome`;

      try {
        const response = await fetch(url);
        const data = await response.json();

        if (data.status !== "OK") {
          document.getElementById("risultato").innerText = "Errore nel recupero dati tramonto";
          return;
        }

        const sunset = new Date(data.results.sunset);
        const sunsetOra = sunset.getHours() + sunset.getMinutes() / 60;
        
        const [oreInizio, minutiInizio] = prossimoAllenamento.orarioInizio.split(':').map(Number);
        const [oreFine, minutiFine] = prossimoAllenamento.orarioFine.split(':').map(Number);
        const oraInizio = oreInizio + minutiInizio / 60;
        const oraFine = oreFine + minutiFine / 60;

        let messaggio = "";
        if (sunsetOra < oraInizio) {
          // Tramonto prima dell'inizio
          messaggio = "<span class='torcia'>🔦 Necessario utilizzo torcia per tutta la durata dell'allenamento</span>";
        } else if (sunsetOra < oraFine) {
          // Tramonto durante l'allenamento
          const oreDiLuce = (sunsetOra - oraInizio).toFixed(1);
          messaggio = `<span class='torcia'>🔦 Torcia necessaria nella fase finale (${oreDiLuce}h di luce naturale)</span>`;
        } else {
          // Tramonto dopo la fine
          messaggio = "<span class='sole'>☀️ Illuminazione naturale sufficiente per l'intero allenamento</span>";
        }

        document.getElementById("risultato").innerHTML = messaggio;
      } catch (error) {
        document.getElementById("risultato").innerHTML = "<span class='torcia'>Errore di connessione. Verifica la connessione internet.</span>";
      }
    }

    // Inizializzazione
    document.addEventListener('DOMContentLoaded', function() {
      caricaImpostazioni();
      generaInterfacciaGiorni();
      
      // Toggle impostazioni
      document.getElementById('toggleImpostazioni').addEventListener('click', function() {
        const impostazioniDiv = document.getElementById('impostazioni');
        if (impostazioniDiv.style.display === 'none') {
          impostazioniDiv.style.display = 'block';
          this.textContent = 'Nascondi Configurazione';
        } else {
          impostazioniDiv.style.display = 'none';
          this.textContent = 'Configura Allenamenti';
        }
      });
      
      // Salva impostazioni
      document.getElementById('salvaImpostazioni').addEventListener('click', function() {
        aggiornaImpostazioniDaUI();
        salvaImpostazioni();
      });
      
      // Aggiorna la posizione quando cambia la città
      document.getElementById('selezionaCitta').addEventListener('change', function() {
        const nomeCitta = this.options[this.selectedIndex].text;
        document.getElementById('info-posizione').textContent = `Posizione selezionata: ${nomeCitta}`;
      });
      
      // Avvia il controllo iniziale
      controllaTorcia();
    });
  </script>
</body>
</html>
