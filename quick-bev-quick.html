<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Quick Bev Quick — Map + Radius + Pop‑Art</title>
  <style>
    :root { --blk:#000; --ylw:#FFEB3B; --bg:#fff; --shadow: 8px 8px 0 0 #000; }
    * { box-sizing: border-box; }
    body {
      margin: 0; background: var(--bg);
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      color: #000;
      /* subtle grid */
      background-image:
        repeating-linear-gradient(0deg, rgba(0,0,0,0.06) 0px, rgba(0,0,0,0.06) 1px, transparent 1px, transparent 24px),
        repeating-linear-gradient(90deg, rgba(0,0,0,0.06) 0px, rgba(0,0,0,0.06) 1px, transparent 1px, transparent 24px);
    }
    .wrap { max-width: 1024px; margin: 0 auto; padding: 24px 24px 48px; }
    .card { background:#fff; border:4px solid var(--blk); box-shadow: var(--shadow); }
    .pad { padding: 16px; }
    .pad-lg { padding: 24px; }
    .row { display:flex; gap:12px; align-items:center; }
    .row-space { display:flex; gap:12px; align-items:center; justify-content:space-between; }
    .title { font-weight: 900; text-transform: uppercase; letter-spacing: -0.02em; }
    .h1 { font-size: clamp(24px, 4.2vw, 48px); line-height: 1; }
    .h2 { font-size: clamp(18px, 3vw, 32px); }
    .small { font-size: 12px; }
    .badge { border:2px solid #000; background:#fff; padding:2px 6px; font-size:11px; }
    .badge-ylw { background: var(--ylw); }
    .btn {
      border:4px solid var(--blk); background:#fff; font-weight: 900; text-transform: uppercase;
      box-shadow: 6px 6px 0 0 #000; padding: 10px 14px; cursor: pointer;
    }
    .btn:active { transform: translate(2px,2px); box-shadow: 4px 4px 0 0 #000; }
    .btn-primary { background:#000; color:#fff; }
    .btn-ylw { background: var(--ylw); }
    .controls { display:grid; grid-template-columns: 1fr 1fr 1fr; gap:12px; }
    @media (max-width: 640px){ .controls { grid-template-columns: 1fr; } }
    #map { width: 100%; height: 360px; }
    .list { display: grid; gap: 12px; }
    .rating { display:inline-flex; gap:8px; align-items:center; font-size: 13px;}
    .rating .box { border:2px solid #000; padding:2px 6px; background:#fff; font-variant-numeric: tabular-nums; }
    .kbd { border:2px solid #000; padding: 2px 6px; background:#fff; font-size:11px; }
    .slider { width:100%; height:36px; }
    .muted { color: #333; }
  </style>
</head>
<body>
  <div class="wrap">
    <header class="card pad-lg" style="margin-bottom:16px;">
      <div class="row-space">
        <div class="title h1">Quick Bev Quick</div>
        <div class="row small">
          <span class="badge badge-ylw">v1.7</span>
          <span class="badge" id="locState">LOC: unknown</span>
        </div>
      </div>
      <p class="small" style="margin-top:8px;">Closest <b id="modeLabel">café</b> rated <b>4.6★+</b> within your radius. Pop‑art pins. Brutalist chrome.</p>
      <div class="row small" style="margin-top:8px;">
        <span class="kbd">C</span><span>= café</span>
        <span class="kbd">B</span><span>= bar</span>
        <span class="kbd">Enter</span><span>= search</span>
      </div>
    </header>

    <section class="controls" style="margin-bottom:12px;">
      <button id="btnCafe" class="btn">☕ CAFE</button>
      <button id="btnBar" class="btn">🍺 BAR</button>
      <button id="btnFind" class="btn btn-primary">FIND IN RADIUS</button>
    </section>

    <section class="card pad" style="margin-bottom:16px;">
      <div class="row-space">
        <div class="title">Radius Dial</div>
        <div><b id="radiusLabel">5</b> km</div>
      </div>
      <input id="radius" class="slider" type="range" min="1" max="20" step="1" value="5" />
      <div class="small muted">Starts at 5 km. Slide to expand up to 20 km.</div>
    </section>

    <section id="geoPanel" class="card pad" style="margin-bottom:16px; display:none;">
      <div id="geoMsg" class="small">Requesting location… (allow the browser prompt)</div>
      <button id="btnEnableLoc" class="btn btn-ylw" style="margin-top:8px;">Enable Location</button>
      <div id="geoErr" class="small" style="color:#b00020; margin-top:6px;"></div>
    </section>

    <section class="card" style="margin-bottom:16px;">
      <div id="map"></div>
    </section>

    <section id="status" class="card pad small" style="margin-bottom:16px; display:none;"></section>

    <section id="best" class="card pad-lg" style="margin-bottom:16px; display:none;"></section>

    <section id="list" class="list"></section>

    <footer class="card pad small" style="margin-top:24px;">
      Nothing 4.6★+? Expand the dial or switch type. Geolocation needs HTTPS or <code>localhost</code>.
    </footer>
  </div>

  <script>
    // --- Config / API key via URL (?key=YOUR_KEY) or fallback placeholder ---
    const urlKey = new URLSearchParams(location.search).get('key');
    const GOOGLE_MAPS_API_KEY = urlKey || 'YOUR_API_KEY_HERE'; // replace or pass ?key=YOUR_KEY
    const state = {
      mode: 'cafe',            // 'cafe' | 'bar'
      radiusKm: 5,
      coords: null,
      permission: 'unknown',
      searching: false,
      results: [],
    };

    // --- DOM helpers ---
    const $ = (sel) => document.querySelector(sel);
    const locStateEl = $('#locState');
    const modeLabelEl = $('#modeLabel');
    const statusEl = $('#status');
    const bestEl = $('#best');
    const listEl = $('#list');
    const geoPanel = $('#geoPanel');
    const geoMsg = $('#geoMsg');
    const geoErr = $('#geoErr');
    const btnEnableLoc = $('#btnEnableLoc');
    const radiusInput = $('#radius');
    const radiusLabel = $('#radiusLabel');
    const btnFind = $('#btnFind');
    const btnCafe = $('#btnCafe');
    const btnBar = $('#btnBar');
    const mapEl = $('#map');

    // --- Load Google Maps (Places) ---
    function loadGoogleMaps(apiKey) {
      return new Promise((resolve, reject) => {
        if (window.google?.maps?.places) return resolve(window.google);
        const s = document.createElement('script');
        s.src = `https://maps.googleapis.com/maps/api/js?key=${apiKey}&libraries=places`;
        s.async = true;
        s.onload = () => window.google?.maps?.places ? resolve(window.google) : reject(new Error('Maps loaded without places'));
        s.onerror = () => reject(new Error('Failed to load Google Maps'));
        document.head.appendChild(s);
      });
    }

    // --- Haversine ---
    function metersBetween(a,b){
      const R=6371e3;
      const toRad = (d)=> d*Math.PI/180;
      const φ1=toRad(a.lat), φ2=toRad(b.lat);
      const Δφ=toRad(b.lat-a.lat), Δλ=toRad(b.lng-a.lng);
      const s=Math.sin(Δφ/2)**2 + Math.cos(φ1)*Math.cos(φ2)*Math.sin(Δλ/2)**2;
      return R*2*Math.atan2(Math.sqrt(s),Math.sqrt(1-s));
    }
    function prettyDistance(m){ return m<1000? Math.round(m)+' m' : (m/1000).toFixed(2)+' km'; }

    // --- Rating stars HTML ---
    function ratingHtml(r){
      const v = Math.max(0, Math.min(5, Number(r||0)));
      const full = Math.floor(v);
      const half  = (v - full) >= 0.5;
      let icons='';
      for(let i=0;i<5;i++){ icons += (i<full? '★' : (i===full && half? '☆':'✩')); }
      return `<span class="rating"><span class="box">${v.toFixed(1)}</span><span>${icons}</span></span>`;
    }

    // --- Pop-art icons ---
    function svgUrl(svg){ return 'data:image/svg+xml;utf8,'+encodeURIComponent(svg); }
    function coffeeIcon(highlight=false){
      const fill = highlight ? '#FFEB3B' : '#FFFFFF';
      return svgUrl(`
        <svg xmlns='http://www.w3.org/2000/svg' width='48' height='48' viewBox='0 0 48 48'>
          <rect x='2' y='10' width='28' height='20' fill='${fill}' stroke='#000' stroke-width='3' />
          <rect x='30' y='14' width='10' height='12' rx='2' fill='${fill}' stroke='#000' stroke-width='3' />
          <rect x='6' y='30' width='24' height='4' fill='#000' />
          <path d='M12 8 c0 -4 6 -4 6 0 M20 8 c0 -4 6 -4 6 0' stroke='#000' stroke-width='3' fill='none' />
        </svg>
      `);
    }
    function beerIcon(highlight=false){
      const fill = highlight ? '#FFEB3B' : '#FFFFFF';
      return svgUrl(`
        <svg xmlns='http://www.w3.org/2000/svg' width='48' height='48' viewBox='0 0 48 48'>
          <rect x='8' y='12' width='24' height='24' rx='2' fill='${fill}' stroke='#000' stroke-width='3' />
          <rect x='32' y='16' width='8' height='14' rx='2' fill='${fill}' stroke='#000' stroke-width='3' />
          <rect x='12' y='36' width='16' height='4' fill='#000' />
          <circle cx='20' cy='10' r='6' fill='#FFF' stroke='#000' stroke-width='3' />
        </svg>
      `);
    }

    // --- Maps state ---
    let gmaps = null, map = null, service = null, infoWindow = null, userMarker = null, circle = null, markers = [];

    function clearMarkers(){ markers.forEach(m=>m.setMap(null)); markers = []; }
    function drawMarkers(list){
      clearMarkers();
      if(!map || !gmaps) return;
      list.forEach((p,idx)=>{
        const pos = p.geometry.location;
        const iconUrl = state.mode === 'cafe' ? coffeeIcon(idx===0) : beerIcon(idx===0);
        const m = new gmaps.maps.Marker({
          position: pos,
          map,
          icon: { url: iconUrl, scaledSize: new gmaps.maps.Size(36,36), anchor: new gmaps.maps.Point(18,24) },
          title: p.name,
          zIndex: idx===0? 999 : 1
        });
        m.addListener('click', ()=>{
          infoWindow.setContent(`
            <div style="font-family: ui-sans-serif, system-ui;">
              <div style="font-weight:800; text-transform:uppercase; margin-bottom:4px;">${p.name}</div>
              <div style="font-size:12px;">${(p.rating||0).toFixed(1)}★ • ${(p.user_ratings_total||0)} reviews • ${prettyDistance(p._distance)}</div>
            </div>
          `);
          infoWindow.open({ anchor:m, map, shouldFocus:false });
        });
        markers.push(m);
      });
      if(markers.length){
        const b = new gmaps.maps.LatLngBounds();
        markers.forEach(m=>b.extend(m.getPosition()));
        if(userMarker) b.extend(userMarker.getPosition());
        map.fitBounds(b);
      }
    }

    function updateHeader(){
      modeLabelEl.textContent = state.mode === 'cafe' ? 'café' : 'bar';
      locStateEl.textContent = 'LOC: ' + state.permission;
      radiusLabel.textContent = String(state.radiusKm);
    }

    function showStatus(msg){
      if(!msg){ statusEl.style.display='none'; statusEl.textContent=''; return; }
      statusEl.style.display='block'; statusEl.textContent = msg;
    }

    function openInMaps(place){
      const q = encodeURIComponent(place.name);
      const url = `https://www.google.com/maps/search/?api=1&query=${q}&query_place_id=${place.place_id}`;
      window.open(url, '_blank');
    }

    function renderBest(best){
      if(!best){ bestEl.style.display='none'; bestEl.innerHTML=''; return; }
      bestEl.style.display='block';
      bestEl.innerHTML = `
        <div class="row-space">
          <div>
            <div class="title h2">${best.name}</div>
            <div class="small" style="margin-top:6px;">
              ${ratingHtml(best.rating || 0)}
              ${typeof best.user_ratings_total==='number' ? `<span class="badge">${best.user_ratings_total} reviews</span>` : ''}
              ${typeof best._distance==='number' ? `<span class="badge">${prettyDistance(best._distance)} away</span>` : ''}
            </div>
            ${best.vicinity ? `<div class="small muted" style="margin-top:6px;">${best.vicinity}</div>` : ''}
          </div>
          <button class="btn btn-ylw" id="btnNavBest">Navigate →</button>
        </div>`;
      $('#btnNavBest').onclick = ()=> openInMaps(best);
    }

    function renderList(list){
      listEl.innerHTML = '';
      if(list.length <= 1) return;
      list.slice(1, 12).forEach((p, i)=>{
        const item = document.createElement('div');
        item.className = 'card pad';
        item.innerHTML = `
          <div class="row-space">
            <div>
              <div class="title">${i+2}. ${p.name}</div>
              <div class="small" style="margin-top:6px;">${ratingHtml(p.rating || 0)} <span class="badge">${prettyDistance(p._distance)}</span></div>
              ${p.vicinity ? `<div class="small muted" style="margin-top:6px;">${p.vicinity}</div>` : ''}
            </div>
            <div class="row">
              <button class="btn btn-primary btn-pin">Pin</button>
              <button class="btn btn-ylw btn-nav">Go</button>
            </div>
          </div>`;
        item.querySelector('.btn-pin').onclick = ()=>{
          if(!map) return;
          const pos = p.geometry.location;
          map.panTo(pos); map.setZoom(15);
        };
        item.querySelector('.btn-nav').onclick = ()=> openInMaps(p);
        listEl.appendChild(item);
      });
    }

    function updateCircle(){
      if(!map || !gmaps || !state.coords) return;
      const radiusMeters = state.radiusKm * 1000;
      if(!circle){
        circle = new gmaps.maps.Circle({
          map, center: state.coords, radius: radiusMeters,
          strokeColor:'#000', strokeOpacity:1, strokeWeight:3,
          fillColor:'#FFEB3B', fillOpacity:0.15, clickable:false
        });
      } else {
        circle.setCenter(state.coords);
        circle.setRadius(radiusMeters);
      }
      const bounds = circle.getBounds();
      if(bounds) map.fitBounds(bounds);
    }

    function ensureMap(){
      if(!gmaps || !state.coords || map) return;
      map = new gmaps.maps.Map(mapEl, {
        center: state.coords, zoom: 14,
        mapTypeControl:false, fullscreenControl:false, streetViewControl:false, gestureHandling:'greedy',
      });
      infoWindow = new gmaps.maps.InfoWindow();
      userMarker = new gmaps.maps.Marker({
        position: state.coords, map,
        icon: { path: gmaps.maps.SymbolPath.CIRCLE, fillColor:'#000', fillOpacity:1, strokeColor:'#000', strokeWeight:2, scale:5 },
        zIndex: 1000
      });
      updateCircle();
    }

    function runSearch(){
      showStatus('');
      if(!state.coords){ showStatus('Location not available yet — allow location or try again.'); return; }
      if(!service){ showStatus('Places service not ready — one sec then retry.'); return; }
      state.searching = true; btnFind.disabled = true;
      const location = new gmaps.maps.LatLng(state.coords.lat, state.coords.lng);
      service.nearbySearch(
        { location, radius: state.radiusKm * 1000, type: state.mode },
        (places, status) => {
          state.searching = false; btnFind.disabled = false;
          if(status !== gmaps.maps.places.PlacesServiceStatus.OK || !Array.isArray(places)){
            showStatus('No places found in radius.'); state.results = []; clearMarkers(); renderBest(null); renderList([]); return;
          }
          const enriched = places
            .filter(p => (p.rating || 0) >= 4.6 && p.geometry?.location)
            .map(p => ({
              ...p,
              _distance: metersBetween(state.coords, { lat: p.geometry.location.lat(), lng: p.geometry.location.lng() }),
            }))
            .filter(p => p._distance <= state.radiusKm * 1000)
            .sort((a,b)=> a._distance - b._distance);
          state.results = enriched;
          drawMarkers(enriched);
          if(!enriched.length){ showStatus('0 spots ≥ 4.6★ in this radius. Expand the dial.'); }
          renderBest(enriched[0]); renderList(enriched);
        }
      );
    }

    function setMode(m){ state.mode = m; updateHeader(); runSearch(); }
    function setRadius(km){ state.radiusKm = km; updateHeader(); updateCircle(); runSearch(); }

    // --- Geolocation + permissions ---
    function requestLocation(){
      geoErr.textContent = '';
      if(!navigator.geolocation){ geoMsg.textContent = 'Geolocation not supported in this browser.'; geoPanel.style.display='block'; return; }
      geoMsg.textContent = 'Requesting location… (allow the browser prompt)'; geoPanel.style.display='block';
      navigator.geolocation.getCurrentPosition(
        (pos)=>{
          state.coords = { lat: pos.coords.latitude, lng: pos.coords.longitude };
          geoPanel.style.display='none';
          ensureMap(); updateCircle(); runSearch();
        },
        (err)=>{
          geoErr.textContent = err && err.message ? err.message : 'Location permission denied.';
          geoPanel.style.display='block';
        },
        { enableHighAccuracy:true, timeout:12000, maximumAge:10000 }
      );
    }

    async function trackPermission(){
      try{
        if(navigator.permissions?.query){
          const st = await navigator.permissions.query({ name: 'geolocation' });
          state.permission = st.state || 'unknown'; updateHeader();
          st.onchange = ()=>{ state.permission = st.state || 'unknown'; updateHeader(); };
        }
      }catch(e){ /* ignore */ }
    }

    // --- Init ---
    (async function init(){
      updateHeader();
      trackPermission();
      btnCafe.onclick = ()=> setMode('cafe');
      btnBar.onclick = ()=> setMode('bar');
      btnFind.onclick = ()=> runSearch();
      btnEnableLoc.onclick = ()=> requestLocation();
      radiusInput.oninput = (e)=> setRadius(parseInt(e.target.value,10));
      document.addEventListener('keydown', (e)=>{
        const k = (e.key||'').toLowerCase();
        if(k==='c') setMode('cafe');
        if(k==='b') setMode('bar');
        if(e.key==='Enter') runSearch();
      });

      try {
        gmaps = await loadGoogleMaps(GOOGLE_MAPS_API_KEY);
        service = new gmaps.maps.places.PlacesService(document.createElement('div'));
      } catch (e) {
        showStatus("Couldn't load Google Maps — check API key & billing.");
      }

      // Auto-request location immediately
      requestLocation();
    })();
  </script>
</body>
</html>
