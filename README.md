<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Compendio de Mapas de Contenido</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap');

  :root {
    --ink: #0f0e17;
    --paper: #faf9f6;
    --accent: #c84b31;
    --accent2: #2d6a4f;
    --accent3: #1a4e8c;
    --accent4: #7b2d8b;
    --accent5: #b5600a;
    --muted: #6b6b6b;
    --line: #ddd8d0;
    --node-bg: #fff;
    --shadow: 0 2px 8px rgba(0,0,0,0.07);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--paper);
    color: var(--ink);
    font-size: 11px;
    line-height: 1.5;
  }

  /* ── COVER PAGE ── */
  .cover {
    width: 210mm;
    min-height: 297mm;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 40mm 20mm;
    text-align: center;
    background: var(--ink);
    color: var(--paper);
    page-break-after: always;
  }

  .cover-label {
    font-size: 9px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    font-weight: 500;
  }

  .cover h1 {
    font-family: 'DM Serif Display', serif;
    font-size: 42px;
    line-height: 1.1;
    margin-bottom: 16px;
    color: #fff;
  }

  .cover-sub {
    font-size: 13px;
    color: #aaa;
    max-width: 300px;
    margin-bottom: 40px;
    font-weight: 300;
  }

  .cover-sites {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    width: 100%;
    max-width: 320px;
    margin-bottom: 50px;
  }

  .cover-site {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    padding: 10px 14px;
    text-align: left;
    font-size: 10px;
  }

  .cover-site .num {
    font-size: 8px;
    color: var(--accent);
    letter-spacing: 2px;
    display: block;
    margin-bottom: 2px;
    font-weight: 600;
  }

  .cover-site .name {
    font-weight: 500;
    color: #eee;
  }

  .cover-site-5 {
    grid-column: 1 / -1;
  }

  .cover-meta {
    font-size: 9px;
    color: #555;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  /* ── CONTENT PAGES ── */
  .page {
    width: 210mm;
    min-height: 297mm;
    margin: 0 auto;
    padding: 14mm 14mm 12mm;
    background: var(--paper);
    page-break-after: always;
    position: relative;
  }

  .page-landscape {
    width: 297mm;
    min-height: 210mm;
    padding: 12mm 14mm 10mm;
  }

  /* ── PAGE HEADER ── */
  .page-header {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    border-bottom: 2px solid var(--ink);
    padding-bottom: 8px;
    margin-bottom: 14px;
  }

  .site-number {
    font-size: 9px;
    letter-spacing: 3px;
    color: var(--muted);
    font-weight: 500;
    text-transform: uppercase;
  }

  .site-name {
    font-family: 'DM Serif Display', serif;
    font-size: 22px;
    line-height: 1;
    color: var(--ink);
  }

  .site-score-badge {
    font-size: 22px;
    font-family: 'DM Serif Display', serif;
    font-weight: 600;
  }

  .score-label {
    font-size: 8px;
    color: var(--muted);
    display: block;
    text-align: right;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  /* ── MAP SECTION ── */
  .map-section {
    margin-bottom: 12px;
  }

  .section-title {
    font-size: 8px;
    font-weight: 600;
    letter-spacing: 3px;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  /* ── TREE MAP ── */
  .tree-container {
    overflow-x: auto;
    overflow-y: hidden;
  }

  .tree {
    display: flex;
    align-items: flex-start;
    gap: 0;
    min-width: max-content;
  }

  /* ROOT NODE */
  .root-node {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
    margin-right: 0;
  }

  .root-box {
    background: var(--site-color, var(--ink));
    color: #fff;
    padding: 8px 14px;
    font-weight: 600;
    font-size: 10px;
    white-space: nowrap;
    writing-mode: vertical-rl;
    text-orientation: mixed;
    transform: rotate(180deg);
    min-height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    letter-spacing: 1px;
  }

  /* CONNECTOR */
  .connector-h {
    width: 24px;
    display: flex;
    align-items: center;
    flex-shrink: 0;
  }

  .connector-h::after {
    content: '';
    display: block;
    width: 100%;
    height: 1.5px;
    background: var(--line);
  }

  /* MAIN BRANCHES */
  .branches {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  .branch-group {
    display: flex;
    align-items: flex-start;
    gap: 0;
  }

  .branch-connector {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 20px;
    flex-shrink: 0;
    position: relative;
  }

  /* LEVEL 1 NODE */
  .l1-node {
    background: var(--node-bg);
    border: 1.5px solid var(--site-color, var(--ink));
    padding: 4px 9px;
    font-size: 9px;
    font-weight: 500;
    white-space: nowrap;
    color: var(--ink);
    position: relative;
  }

  /* LEVEL 2 NODES */
  .l2-nodes {
    display: flex;
    flex-direction: column;
    gap: 3px;
    margin-left: 14px;
    padding-left: 10px;
    border-left: 1.5px solid var(--line);
    margin-top: 6px;
  }

  .l2-node {
    background: rgba(0,0,0,0.03);
    border: 1px solid var(--line);
    padding: 3px 8px;
    font-size: 8px;
    white-space: nowrap;
    color: var(--muted);
    position: relative;
  }

  .l2-node::before {
    content: '';
    position: absolute;
    left: -10px;
    top: 50%;
    width: 10px;
    height: 1px;
    background: var(--line);
  }

  /* BRANCH WITH CHILDREN */
  .branch-with-children {
    display: flex;
    flex-direction: column;
  }

  .branch-header {
    display: flex;
    align-items: center;
    gap: 0;
  }

  .branch-children {
    display: flex;
    gap: 0;
    margin-left: 32px;
    padding-left: 12px;
    border-left: 1.5px solid var(--line);
    margin-top: 3px;
    flex-direction: column;
    gap: 2px;
  }

  /* HORIZONTAL FULL MAP */
  .full-map {
    display: flex;
    align-items: flex-start;
    gap: 6px;
    flex-wrap: nowrap;
    overflow: visible;
  }

  .map-column {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
  }

  .map-col-header {
    background: var(--site-color, #333);
    color: #fff;
    font-size: 8px;
    font-weight: 600;
    padding: 4px 8px;
    letter-spacing: 1px;
    text-transform: uppercase;
    white-space: nowrap;
    width: 100%;
    text-align: center;
  }

  .map-col-item {
    background: var(--node-bg);
    border: 1px solid var(--line);
    padding: 3px 7px;
    font-size: 8px;
    white-space: nowrap;
    color: var(--ink);
    width: 100%;
  }

  .map-col-sub {
    background: rgba(0,0,0,0.025);
    border: 1px solid var(--line);
    padding: 2px 7px;
    font-size: 7.5px;
    white-space: nowrap;
    color: var(--muted);
    margin-left: 8px;
    width: calc(100% - 8px);
    position: relative;
  }

  .map-col-sub::before {
    content: '';
    position: absolute;
    left: -8px;
    top: 50%;
    width: 8px;
    height: 1px;
    background: var(--line);
  }

  /* ── ANALYSIS TABLE ── */
  .analysis-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 6px;
  }

  .analysis-table th {
    font-size: 7.5px;
    font-weight: 600;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--muted);
    text-align: left;
    padding: 5px 8px;
    border-bottom: 1.5px solid var(--ink);
    background: transparent;
  }

  .analysis-table td {
    padding: 5px 8px;
    font-size: 8.5px;
    border-bottom: 1px solid var(--line);
    vertical-align: top;
    line-height: 1.4;
  }

  .analysis-table tr:last-child td {
    border-bottom: none;
  }

  .analysis-table .score-cell {
    font-family: 'DM Serif Display', serif;
    font-size: 14px;
    font-weight: 700;
    white-space: nowrap;
    text-align: center;
  }

  .analysis-table .system-name {
    font-weight: 600;
    font-size: 9px;
    color: var(--ink);
    white-space: nowrap;
  }

  .score-bar {
    width: 100%;
    height: 4px;
    background: var(--line);
    margin-top: 3px;
    position: relative;
  }

  .score-bar-fill {
    position: absolute;
    left: 0; top: 0; bottom: 0;
    background: var(--site-color, var(--ink));
    opacity: 0.7;
  }

  .tag {
    display: inline-block;
    font-size: 7px;
    font-weight: 600;
    padding: 2px 6px;
    letter-spacing: 1px;
    text-transform: uppercase;
    border: 1px solid currentColor;
  }

  .tag-optimal { color: var(--accent2); }
  .tag-good { color: var(--accent3); }
  .tag-improve { color: var(--accent); }

  /* ── RECOMMENDATIONS ── */
  .recs {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4px;
    margin-top: 8px;
  }

  .rec-item {
    font-size: 8px;
    color: var(--muted);
    padding: 4px 8px;
    border-left: 2px solid var(--site-color, var(--ink));
    background: rgba(0,0,0,0.02);
    line-height: 1.4;
  }

  .rec-item strong {
    display: block;
    font-weight: 600;
    color: var(--ink);
    font-size: 8px;
    margin-bottom: 1px;
  }

  /* ── COMPARATIVE PAGE ── */
  .compare-table {
    width: 100%;
    border-collapse: collapse;
    margin: 10px 0;
  }

  .compare-table th {
    background: var(--ink);
    color: #fff;
    font-size: 8px;
    font-weight: 500;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    padding: 7px 10px;
    text-align: center;
  }

  .compare-table th:first-child { text-align: left; }

  .compare-table td {
    padding: 7px 10px;
    font-size: 9px;
    border-bottom: 1px solid var(--line);
    text-align: center;
    vertical-align: middle;
  }

  .compare-table td:first-child {
    text-align: left;
    font-weight: 600;
    font-size: 10px;
  }

  .compare-table tr:nth-child(even) td { background: rgba(0,0,0,0.02); }

  .compare-table .total-cell {
    font-family: 'DM Serif Display', serif;
    font-size: 15px;
    font-weight: 700;
  }

  .bar-cell {
    position: relative;
    min-width: 60px;
  }

  .bar-inner {
    height: 5px;
    background: var(--site-color, #999);
    margin-top: 2px;
    opacity: 0.6;
    display: inline-block;
  }

  .score-num {
    font-weight: 600;
    display: block;
    font-size: 9px;
  }

  /* CONCLUSION BOXES */
  .conclusion-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 14px;
  }

  .conclusion-box {
    border: 1.5px solid var(--line);
    padding: 12px;
  }

  .conclusion-box h4 {
    font-size: 8px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
    padding-bottom: 5px;
    border-bottom: 1px solid var(--line);
  }

  .conclusion-box ul {
    list-style: none;
    padding: 0;
  }

  .conclusion-box ul li {
    font-size: 8.5px;
    padding: 3px 0;
    border-bottom: 1px solid rgba(0,0,0,0.04);
    color: var(--ink);
    line-height: 1.4;
  }

  .conclusion-box ul li::before {
    content: 'o  ';
    color: var(--accent);
    font-weight: 700;
  }

  .conclusion-box ul li.minus::before {
    content: 'x  ';
    color: var(--muted);
  }

  /* PAGE FOOTER */
  .page-footer {
    position: absolute;
    bottom: 10mm;
    left: 14mm;
    right: 14mm;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top: 1px solid var(--line);
    padding-top: 5px;
  }

  .footer-text {
    font-size: 7px;
    color: var(--muted);
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  /* PRINT */
  @media print {
    @page { margin: 0; size: A4 portrait; }
    @page :landscape { size: A4 landscape; }
    body { background: white; }
    .page { margin: 0; box-shadow: none; }
    .page-landscape { margin: 0; }
  }

  /* DIVIDER */
  .divider {
    height: 1px;
    background: var(--line);
    margin: 10px 0;
  }

  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    align-items: start;
  }

  .three-col {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
    align-items: start;
  }

  .map-wrap {
    overflow: auto;
    max-width: 100%;
  }
</style>
</head>
<body>

<!-- ══════════════════════════════════════════════════════
     COVER
══════════════════════════════════════════════════════ -->
<div class="cover">
  <div class="cover-label">Arquitectura de Información</div>
  <h1>Compendio de<br>Mapas de<br>Contenido</h1>
  <div class="cover-sub">Análisis comparativo de arquitectura de información para sitios web de salud</div>

  <div class="cover-sites">
    <div class="cover-site">
      <span class="num">01</span>
      <span class="name">WebMD</span>
    </div>
    <div class="cover-site">
      <span class="num">02</span>
      <span class="name">Healthline</span>
    </div>
    <div class="cover-site">
      <span class="num">03</span>
      <span class="name">Patient.info</span>
    </div>
    <div class="cover-site">
      <span class="num">04</span>
      <span class="name">MedlinePlus ES</span>
    </div>
    <div class="cover-site cover-site-5">
      <span class="num">05</span>
      <span class="name">BeyondType1.org</span>
    </div>
  </div>

  <div class="cover-meta">Benchmark de UX y Usabilidad</div>
</div>


<!-- ══════════════════════════════════════════════════════
     SITE 1 — WEBMD  (page 1: map)
══════════════════════════════════════════════════════ -->
<div class="page" style="--site-color: #c84b31;">
  <div class="page-header">
    <div>
      <div class="site-number">01 / 05</div>
      <div class="site-name">WebMD</div>
    </div>
    <div>
      <span class="score-label">Puntuacion General</span>
      <span class="site-score-badge" style="color:#c84b31;">7.8 / 10</span>
    </div>
  </div>

  <div class="section-title">Mapa de Contenido — Estructura de Navegacion</div>

  <!-- FULL HORIZONTAL MAP -->
  <div class="map-wrap">
    <div class="full-map">

      <!-- ROOT -->
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;margin-right:6px;">
        <div style="background:#c84b31;color:#fff;padding:8px 12px;font-weight:700;font-size:11px;writing-mode:vertical-rl;transform:rotate(180deg);min-height:90px;display:flex;align-items:center;justify-content:center;letter-spacing:1px;">WebMD</div>
      </div>
      <div style="width:20px;display:flex;align-items:center;margin-right:0;align-self:center;"><div style="width:100%;height:1.5px;background:#ddd;"></div></div>

      <!-- COLUMN: Condiciones -->
      <div class="map-column">
        <div class="map-col-header" style="background:#c84b31;">Condiciones</div>
        <div class="map-col-item">Enfermedades por Sistema</div>
        <div class="map-col-item">A-Z Condiciones</div>
        <div class="map-col-item">Condiciones Cronicas</div>
        <div class="map-col-item">Infecciones</div>
        <div class="map-col-item">Salud Mental</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Sintomas -->
      <div class="map-column">
        <div class="map-col-header" style="background:#b54029;">Sintomas</div>
        <div class="map-col-item">Por Organo</div>
        <div class="map-col-item">A-Z Sintomas</div>
        <div class="map-col-item">Comparador</div>
        <div class="map-col-item">Guias de Sintomas</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Medicamentos -->
      <div class="map-column">
        <div class="map-col-header" style="background:#a33825;">Medicamentos</div>
        <div class="map-col-item">Busqueda</div>
        <div class="map-col-item">Efectos Secundarios</div>
        <div class="map-col-item">Interacciones</div>
        <div class="map-col-item">Genericos</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Bienestar -->
      <div class="map-column">
        <div class="map-col-header" style="background:#962f1f;">Bienestar</div>
        <div class="map-col-item">Nutricion</div>
        <div class="map-col-item">Ejercicio</div>
        <div class="map-col-item">Salud Mental</div>
        <div class="map-col-item">Sueno</div>
        <div class="map-col-item">Sexualidad</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Medicos -->
      <div class="map-column">
        <div class="map-col-header" style="background:#8a2819;">Medicos</div>
        <div class="map-col-item">Encontrar Medicos</div>
        <div class="map-col-item">Hospitales</div>
        <div class="map-col-item">Urgencias</div>
        <div class="map-col-item">Especialidades</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Herramientas -->
      <div class="map-column">
        <div class="map-col-header" style="background:#7e2214;">Herramientas</div>
        <div class="map-col-item">Calculadoras</div>
        <div class="map-col-item">Pruebas de Evaluacion</div>
        <div class="map-col-item">Interactivas</div>
      </div>

      <div style="width:8px;"></div>

      <!-- COLUMN: Noticias -->
      <div class="map-column">
        <div class="map-col-header" style="background:#721c0e;">Noticias</div>
        <div class="map-col-item">Ultimas Noticias</div>
        <div class="map-col-item">Temas Populares</div>
        <div class="map-col-item">Boletin</div>
        <div class="map-col-item">Blog / Video</div>
        <div class="map-col-item">Podcasts</div>
        <div class="map-col-item">Comunidad</div>
      </div>

    </div>
  </div>

  <div class="divider" style="margin-top:14px;"></div>

  <!-- ANALYSIS -->
  <div class="section-title" style="margin-top:10px;">Analisis por Sistema de Arquitectura de Informacion</div>
  <table class="analysis-table">
    <thead>
      <tr>
        <th style="width:18%;">Sistema</th>
        <th style="width:8%; text-align:center;">Puntaje</th>
        <th style="width:12%;">Estado</th>
        <th>Analisis Detallado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="system-name">Organizacion</span><div class="score-bar"><div class="score-bar-fill" style="width:75%;"></div></div></td>
        <td class="score-cell" style="color:#c84b31;">7.5</td>
        <td><span class="tag tag-good">Buena</span></td>
        <td>Estructura clara con categorias bien definidas. Algunos elementos dispersos en la seccion "Mas". Jerarquia profunda puede causar confusion.</td>
      </tr>
      <tr>
        <td><span class="system-name">Navegacion</span><div class="score-bar"><div class="score-bar-fill" style="width:70%;"></div></div></td>
        <td class="score-cell" style="color:#c84b31;">7.0</td>
        <td><span class="tag tag-good">Buena</span></td>
        <td>Barra principal clara, pero menus extensos. Ausencia de breadcrumbs en secciones profundas. Navegacion secundaria poco intuitiva.</td>
      </tr>
      <tr>
        <td><span class="system-name">Etiquetado</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;"></div></div></td>
        <td class="score-cell" style="color:#c84b31;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Titulos descriptivos y concisos. Terminologia medica consistente y accesible. Categorias bien identificadas.</td>
      </tr>
      <tr>
        <td><span class="system-name">Busqueda</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;"></div></div></td>
        <td class="score-cell" style="color:#c84b31;">8.5</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Barra de busqueda prominente con sugerencias inteligentes. Permite busqueda diferenciada por medicamentos, sintomas y condiciones.</td>
      </tr>
      <tr>
        <td><span class="system-name">Contenido / UX</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;"></div></div></td>
        <td class="score-cell" style="color:#c84b31;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Contenido medico verificado. Multiples formatos (articulos, videos, herramientas). Diseno limpio pero algo denso en algunas secciones.</td>
      </tr>
    </tbody>
  </table>

  <div class="section-title" style="margin-top:10px;">Recomendaciones de Mejora</div>
  <div class="recs">
    <div class="rec-item"><strong>Breadcrumbs</strong>Implementar en todas las paginas internas para orientar al usuario.</div>
    <div class="rec-item"><strong>Menus Simplificados</strong>Reducir la extension de los menus desplegables.</div>
    <div class="rec-item"><strong>Jerarquia Visual</strong>Mejorar la estructura visual para reducir el ruido.</div>
    <div class="rec-item"><strong>Busqueda Avanzada</strong>Agregar filtros por tipo de contenido, fecha y relevancia.</div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">WebMD — Pagina 1</span>
  </div>
</div>


<!-- ══════════════════════════════════════════════════════
     SITE 2 — HEALTHLINE
══════════════════════════════════════════════════════ -->
<div class="page" style="--site-color: #1a4e8c;">
  <div class="page-header">
    <div>
      <div class="site-number">02 / 05</div>
      <div class="site-name">Healthline</div>
    </div>
    <div>
      <span class="score-label">Puntuacion General</span>
      <span class="site-score-badge" style="color:#1a4e8c;">8.2 / 10</span>
    </div>
  </div>

  <div class="section-title">Mapa de Contenido — Estructura de Navegacion</div>

  <div class="map-wrap">
    <div class="full-map">
      <!-- ROOT -->
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;margin-right:6px;">
        <div style="background:#1a4e8c;color:#fff;padding:8px 12px;font-weight:700;font-size:11px;writing-mode:vertical-rl;transform:rotate(180deg);min-height:90px;display:flex;align-items:center;justify-content:center;letter-spacing:1px;">Healthline</div>
      </div>
      <div style="width:20px;display:flex;align-items:center;margin-right:0;align-self:center;"><div style="width:100%;height:1.5px;background:#ddd;"></div></div>

      <div class="map-column">
        <div class="map-col-header" style="background:#1a4e8c;">Condiciones</div>
        <div class="map-col-item">Por Categoria</div>
        <div class="map-col-item">A-Z Condiciones</div>
        <div class="map-col-item">Sintomas</div>
        <div class="map-col-item">Primeros Auxilios</div>
        <div class="map-col-item">Salud Mental</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#174480;">Medicamentos</div>
        <div class="map-col-item">Busqueda</div>
        <div class="map-col-item">Suplementos</div>
        <div class="map-col-item">Venta Libre</div>
        <div class="map-col-item">Medicina Alternativa</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#143a74;">Nutricion</div>
        <div class="map-col-item">Dietas</div>
        <div class="map-col-item">Nutrientes</div>
        <div class="map-col-item">Recetas Saludables</div>
        <div class="map-col-item">Restricciones</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#113068;">Bienestar</div>
        <div class="map-col-item">Ejercicio</div>
        <div class="map-col-item">Sueno</div>
        <div class="map-col-item">Estres y Ansiedad</div>
        <div class="map-col-item">Bienestar General</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#0e265c;">Sexo y Relaciones</div>
        <div class="map-col-item">Anticoncepcion</div>
        <div class="map-col-item">ETS</div>
        <div class="map-col-item">Disfuncion Sexual</div>
        <div class="map-col-item">Salud Reproductiva</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#0b1c50;">Padres e Hijos</div>
        <div class="map-col-item">Embarazo</div>
        <div class="map-col-item">Padres</div>
        <div class="map-col-item">Ninos</div>
        <div class="map-col-item">Adolescentes</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#081244;">Cannabis / Mas</div>
        <div class="map-col-item">Usos Medicos</div>
        <div class="map-col-item">Efectos Secundarios</div>
        <div class="map-col-item">Legales y Seguridad</div>
        <div class="map-col-item">Blog / Video</div>
        <div class="map-col-item">Comunidad</div>
        <div class="map-col-item">Recursos</div>
      </div>
    </div>
  </div>

  <div class="divider" style="margin-top:14px;"></div>

  <div class="section-title" style="margin-top:10px;">Analisis por Sistema de Arquitectura de Informacion</div>
  <table class="analysis-table">
    <thead>
      <tr>
        <th style="width:18%;">Sistema</th>
        <th style="width:8%;text-align:center;">Puntaje</th>
        <th style="width:12%;">Estado</th>
        <th>Analisis Detallado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="system-name">Organizacion</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;background:#1a4e8c;"></div></div></td>
        <td class="score-cell" style="color:#1a4e8c;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Categorias diferenciadas y seccion especializada en Cannabis. Jerarquia clara y balanceada.</td>
      </tr>
      <tr>
        <td><span class="system-name">Navegacion</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;background:#1a4e8c;"></div></div></td>
        <td class="score-cell" style="color:#1a4e8c;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Intuitiva con menus bien organizados. Subcategorias logicas. Falta breadcrumbs en algunas paginas.</td>
      </tr>
      <tr>
        <td><span class="system-name">Etiquetado</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#1a4e8c;"></div></div></td>
        <td class="score-cell" style="color:#1a4e8c;">8.5</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Etiquetas descriptivas con palabras clave orientadas al usuario. Jerarquia visual clara y consistente.</td>
      </tr>
      <tr>
        <td><span class="system-name">Busqueda</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;background:#1a4e8c;"></div></div></td>
        <td class="score-cell" style="color:#1a4e8c;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Barra prominente con sugerencias inteligentes. Falta filtrado avanzado por tipo de contenido.</td>
      </tr>
      <tr>
        <td><span class="system-name">Contenido / UX</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#1a4e8c;"></div></div></td>
        <td class="score-cell" style="color:#1a4e8c;">8.5</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Contenido revisado y confiable. Variedad de formatos. Diseno limpio y moderno con excelente legibilidad.</td>
      </tr>
    </tbody>
  </table>

  <div class="section-title" style="margin-top:10px;">Recomendaciones de Mejora</div>
  <div class="recs">
    <div class="rec-item" style="border-color:#1a4e8c;"><strong>Breadcrumbs</strong>Agregar en todas las paginas para orientar al usuario.</div>
    <div class="rec-item" style="border-color:#1a4e8c;"><strong>Filtros Avanzados</strong>Incluir filtros por tipo, fecha y relevancia en busqueda.</div>
    <div class="rec-item" style="border-color:#1a4e8c;"><strong>Accesibilidad</strong>Mejorar contraste y compatibilidad con lectores de pantalla.</div>
    <div class="rec-item" style="border-color:#1a4e8c;"><strong>Contenido Verificado</strong>Destacar articulos certificados vs. contenido general.</div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">Healthline — Pagina 2</span>
  </div>
</div>


<!-- ══════════════════════════════════════════════════════
     SITE 3 — PATIENT.INFO
══════════════════════════════════════════════════════ -->
<div class="page" style="--site-color: #2d6a4f;">
  <div class="page-header">
    <div>
      <div class="site-number">03 / 05</div>
      <div class="site-name">Patient.info</div>
    </div>
    <div>
      <span class="score-label">Puntuacion General</span>
      <span class="site-score-badge" style="color:#2d6a4f;">8.5 / 10</span>
    </div>
  </div>

  <div class="section-title">Mapa de Contenido — Estructura de Navegacion</div>

  <div class="map-wrap">
    <div class="full-map">
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;margin-right:6px;">
        <div style="background:#2d6a4f;color:#fff;padding:8px 12px;font-weight:700;font-size:11px;writing-mode:vertical-rl;transform:rotate(180deg);min-height:90px;display:flex;align-items:center;justify-content:center;letter-spacing:1px;">Patient.info</div>
      </div>
      <div style="width:20px;display:flex;align-items:center;margin-right:0;align-self:center;"><div style="width:100%;height:1.5px;background:#ddd;"></div></div>

      <div class="map-column">
        <div class="map-col-header" style="background:#2d6a4f;">Condiciones</div>
        <div class="map-col-item">Por Sistema</div>
        <div class="map-col-item">A-Z Condiciones</div>
        <div class="map-col-item">Cronicas</div>
        <div class="map-col-item">Infecciones</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#275e45;">Sintomas</div>
        <div class="map-col-item">A-Z Sintomas</div>
        <div class="map-col-item">Por Localizacion</div>
        <div class="map-col-item">Comparador</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#21523b;">Medicamentos</div>
        <div class="map-col-item">Busqueda</div>
        <div class="map-col-item">Efectos Secundarios</div>
        <div class="map-col-item">Interacciones</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#1b4631;">Pruebas Medicas</div>
        <div class="map-col-item">Analisis de Sangre</div>
        <div class="map-col-item">Pruebas de Imagen</div>
        <div class="map-col-item">Especializadas</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#153a27;">Procedimientos</div>
        <div class="map-col-item">Quirurgicos</div>
        <div class="map-col-item">Menores</div>
        <div class="map-col-item">Diagnosticos</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#0f2e1d;">Embarazo</div>
        <div class="map-col-item">Embarazo</div>
        <div class="map-col-item">Parto</div>
        <div class="map-col-item">Posparto</div>
        <div class="map-col-item">Cuidado del Bebe</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#092213;">Bienestar / Mas</div>
        <div class="map-col-item">Dieta y Nutricion</div>
        <div class="map-col-item">Ejercicio</div>
        <div class="map-col-item">Salud Mental</div>
        <div class="map-col-item">Relaciones</div>
        <div class="map-col-item">Blog / Podcast</div>
        <div class="map-col-item">Comunidad</div>
      </div>
    </div>
  </div>

  <div class="divider" style="margin-top:14px;"></div>

  <div class="section-title" style="margin-top:10px;">Analisis por Sistema de Arquitectura de Informacion</div>
  <table class="analysis-table">
    <thead>
      <tr>
        <th style="width:18%;">Sistema</th>
        <th style="width:8%;text-align:center;">Puntaje</th>
        <th style="width:12%;">Estado</th>
        <th>Analisis Detallado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="system-name">Organizacion</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#2d6a4f;"></div></div></td>
        <td class="score-cell" style="color:#2d6a4f;">8.5</td>
        <td><span class="tag tag-optimal">Muy Buena</span></td>
        <td>Estructura sistematica. Inclusion de "Pruebas Medicas" y "Procedimientos" como secciones independientes es una ventaja diferencial clave.</td>
      </tr>
      <tr>
        <td><span class="system-name">Navegacion</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#2d6a4f;"></div></div></td>
        <td class="score-cell" style="color:#2d6a4f;">8.5</td>
        <td><span class="tag tag-optimal">Muy Buena</span></td>
        <td>Navegacion intuitiva y fluida. Menus bien organizados con accesibilidad evidente. Falta breadcrumbs en algunas secciones.</td>
      </tr>
      <tr>
        <td><span class="system-name">Etiquetado</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#2d6a4f;"></div></div></td>
        <td class="score-cell" style="color:#2d6a4f;">8.5</td>
        <td><span class="tag tag-optimal">Muy Buena</span></td>
        <td>Etiquetas claras, descriptivas y consistentes. Uso de iconografia para identificacion rapida de categorias.</td>
      </tr>
      <tr>
        <td><span class="system-name">Busqueda</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#2d6a4f;"></div></div></td>
        <td class="score-cell" style="color:#2d6a4f;">8.5</td>
        <td><span class="tag tag-optimal">Muy Buena</span></td>
        <td>Barra bien posicionada con autocompletado. Permite filtrar por tipo de contenido, ventaja sobre competidores.</td>
      </tr>
      <tr>
        <td><span class="system-name">Contenido / UX</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#2d6a4f;"></div></div></td>
        <td class="score-cell" style="color:#2d6a4f;">8.5</td>
        <td><span class="tag tag-optimal">Muy Buena</span></td>
        <td>Contenido basado en evidencia. Diseno limpio, moderno y accesible con excelente manejo del color y tipografia.</td>
      </tr>
    </tbody>
  </table>

  <div class="section-title" style="margin-top:10px;">Recomendaciones de Mejora</div>
  <div class="recs">
    <div class="rec-item" style="border-color:#2d6a4f;"><strong>Breadcrumbs</strong>Implementar en todas las paginas internas.</div>
    <div class="rec-item" style="border-color:#2d6a4f;"><strong>Filtros Avanzados</strong>Ampliar opciones de filtrado en busqueda.</div>
    <div class="rec-item" style="border-color:#2d6a4f;"><strong>Preguntas Frecuentes</strong>Hacer la seccion FAQ mas visible y accesible.</div>
    <div class="rec-item" style="border-color:#2d6a4f;"><strong>Comunidad</strong>Integrar mejor la comunidad en la navegacion principal.</div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">Patient.info — Pagina 3</span>
  </div>
</div>


<!-- ══════════════════════════════════════════════════════
     SITE 4 — MEDLINEPLUS ES
══════════════════════════════════════════════════════ -->
<div class="page" style="--site-color: #7b2d8b;">
  <div class="page-header">
    <div>
      <div class="site-number">04 / 05</div>
      <div class="site-name">MedlinePlus en Espanol</div>
    </div>
    <div>
      <span class="score-label">Puntuacion General</span>
      <span class="site-score-badge" style="color:#7b2d8b;">8.6 / 10</span>
    </div>
  </div>

  <div class="section-title">Mapa de Contenido — Estructura de Navegacion</div>

  <div class="map-wrap">
    <div class="full-map">
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;margin-right:6px;">
        <div style="background:#7b2d8b;color:#fff;padding:8px 12px;font-weight:700;font-size:10px;writing-mode:vertical-rl;transform:rotate(180deg);min-height:90px;display:flex;align-items:center;justify-content:center;letter-spacing:1px;text-align:center;">MedlinePlus ES</div>
      </div>
      <div style="width:20px;display:flex;align-items:center;margin-right:0;align-self:center;"><div style="width:100%;height:1.5px;background:#ddd;"></div></div>

      <div class="map-column">
        <div class="map-col-header" style="background:#7b2d8b;">Enciclopedia</div>
        <div class="map-col-item">Terminos A-Z</div>
        <div class="map-col-item">Organos y Sistemas</div>
        <div class="map-col-item">Enfermedades</div>
        <div class="map-col-item">Procedimientos</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#6e287e;">Medicamentos</div>
        <div class="map-col-item">Medicamentos</div>
        <div class="map-col-item">Suplementos</div>
        <div class="map-col-item">Interacciones</div>
        <div class="map-col-item">Efectos Secundarios</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#612371;">Pruebas Medicas</div>
        <div class="map-col-item">Laboratorio</div>
        <div class="map-col-item">Imagen</div>
        <div class="map-col-item">Geneticas</div>
        <div class="map-col-item">Otros Examenes</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#541e64;">Guias</div>
        <div class="map-col-item">Condiciones Cronicas</div>
        <div class="map-col-item">Enf. Infecciosas</div>
        <div class="map-col-item">Salud Reproductiva</div>
        <div class="map-col-item">Bienestar</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#471957;">Videos</div>
        <div class="map-col-item">Videos Educativos</div>
        <div class="map-col-item">Procedimientos</div>
        <div class="map-col-item">Testimonios</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#3a144a;">Noticias</div>
        <div class="map-col-item">Ultimas Noticias</div>
        <div class="map-col-item">Temas de Interes</div>
        <div class="map-col-item">Archivo</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#2d0f3d;">Recursos / Herr.</div>
        <div class="map-col-item">Para Cuidadores</div>
        <div class="map-col-item">Salud del Nino</div>
        <div class="map-col-item">Adulto Mayor</div>
        <div class="map-col-item">Otros Idiomas</div>
        <div class="map-col-item">Calculadoras</div>
        <div class="map-col-item">Herramientas</div>
      </div>
    </div>
  </div>

  <div class="divider" style="margin-top:14px;"></div>

  <div class="section-title" style="margin-top:10px;">Analisis por Sistema de Arquitectura de Informacion</div>
  <table class="analysis-table">
    <thead>
      <tr>
        <th style="width:18%;">Sistema</th>
        <th style="width:8%;text-align:center;">Puntaje</th>
        <th style="width:12%;">Estado</th>
        <th>Analisis Detallado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="system-name">Organizacion</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#7b2d8b;"></div></div></td>
        <td class="score-cell" style="color:#7b2d8b;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Estructura altamente sistematica y jerarquica. Modelo ejemplar de organizacion informativa para sitios gubernamentales de salud.</td>
      </tr>
      <tr>
        <td><span class="system-name">Navegacion</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;background:#7b2d8b;"></div></div></td>
        <td class="score-cell" style="color:#7b2d8b;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Navegacion clara y accesible. Menus bien estructurados. Ausencia de breadcrumbs es una debilidad notable para un sitio de esta envergadura.</td>
      </tr>
      <tr>
        <td><span class="system-name">Etiquetado</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#7b2d8b;"></div></div></td>
        <td class="score-cell" style="color:#7b2d8b;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Terminologia medica estandarizada. Etiquetas extremadamente claras y consistentes. Facilitan la busqueda del usuario.</td>
      </tr>
      <tr>
        <td><span class="system-name">Busqueda</span><div class="score-bar"><div class="score-bar-fill" style="width:80%;background:#7b2d8b;"></div></div></td>
        <td class="score-cell" style="color:#7b2d8b;">8.0</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Barra prominente y funcional con sugerencias. Falta de filtros avanzados y refinamiento en la busqueda.</td>
      </tr>
      <tr>
        <td><span class="system-name">Contenido / UX</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#7b2d8b;"></div></div></td>
        <td class="score-cell" style="color:#7b2d8b;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Confiabilidad maxima como recurso gubernamental. Excelente legibilidad y accesibilidad. Informacion bien estructurada.</td>
      </tr>
    </tbody>
  </table>

  <div class="section-title" style="margin-top:10px;">Recomendaciones de Mejora</div>
  <div class="recs">
    <div class="rec-item" style="border-color:#7b2d8b;"><strong>Breadcrumbs</strong>Implementar en todas las paginas internas.</div>
    <div class="rec-item" style="border-color:#7b2d8b;"><strong>Filtros Avanzados</strong>Opciones de refinamiento en la busqueda.</div>
    <div class="rec-item" style="border-color:#7b2d8b;"><strong>Modernizacion UI</strong>Actualizar interfaz manteniendo funcionalidad.</div>
    <div class="rec-item" style="border-color:#7b2d8b;"><strong>Personalizacion</strong>Dashboards y alertas para usuarios frecuentes.</div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">MedlinePlus ES — Pagina 4</span>
  </div>
</div>


<!-- ══════════════════════════════════════════════════════
     SITE 5 — BEYONDTYPE1.ORG
══════════════════════════════════════════════════════ -->
<div class="page" style="--site-color: #b5600a;">
  <div class="page-header">
    <div>
      <div class="site-number">05 / 05</div>
      <div class="site-name">BeyondType1.org</div>
    </div>
    <div>
      <span class="score-label">Puntuacion General</span>
      <span class="site-score-badge" style="color:#b5600a;">8.6 / 10</span>
    </div>
  </div>

  <div class="section-title">Mapa de Contenido — Estructura de Navegacion</div>

  <div class="map-wrap">
    <div class="full-map">
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;margin-right:6px;">
        <div style="background:#b5600a;color:#fff;padding:8px 12px;font-weight:700;font-size:10px;writing-mode:vertical-rl;transform:rotate(180deg);min-height:90px;display:flex;align-items:center;justify-content:center;letter-spacing:1px;text-align:center;">BeyondType1</div>
      </div>
      <div style="width:20px;display:flex;align-items:center;margin-right:0;align-self:center;"><div style="width:100%;height:1.5px;background:#ddd;"></div></div>

      <div class="map-column">
        <div class="map-col-header" style="background:#b5600a;">Beyond Type 1</div>
        <div class="map-col-item">Concienciacion</div>
        <div class="map-col-item">Diagnostico Reciente T1</div>
        <div class="map-col-item">Vivir con T1</div>
        <div class="map-col-item">Cuidadores T1</div>
        <div class="map-col-item">Abogacia</div>
        <div class="map-col-item">Proveedores Salud</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#a05509;">Beyond Type 2</div>
        <div class="map-col-item">Concienciacion T2</div>
        <div class="map-col-item">Prediabetes</div>
        <div class="map-col-item">Diagnostico Reciente T2</div>
        <div class="map-col-item">Vivir con T2</div>
        <div class="map-col-item">Cuidadores T2</div>
        <div class="map-col-item">Abogacia</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#8b4a08;">Recursos</div>
        <div class="map-col-item">Cuidado de la Salud</div>
        <div class="map-col-item">Tecnologia</div>
        <div class="map-col-item">Insulina y Medicamentos</div>
        <div class="map-col-item">Embarazo</div>
        <div class="map-col-item">Viajar</div>
        <div class="map-col-item">Bienestar Fisico</div>
        <div class="map-col-item">Defensa</div>
        <div class="map-col-item">Ver Todos</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#763f07;">Programas</div>
        <div class="map-col-item">Equipo de Maraton</div>
        <div class="map-col-item">Mas Alla del Diagnostico</div>
        <div class="map-col-item">Get Insulin</div>
        <div class="map-col-item">Comunidad T1</div>
        <div class="map-col-item">Comunidad T2</div>
        <div class="map-col-item">Beyond Scholars</div>
        <div class="map-col-item">Beyond Barriers</div>
        <div class="map-col-item">Ve las Senales</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#613406;">Quienes Somos</div>
        <div class="map-col-item">Nuestra Historia</div>
        <div class="map-col-item">Conoce al Equipo</div>
        <div class="map-col-item">Portafolio</div>
        <div class="map-col-item">Carreras</div>
        <div class="map-col-item">Contactanos</div>
      </div>
      <div style="width:8px;"></div>
      <div class="map-column">
        <div class="map-col-header" style="background:#4c2905;">Involucrate</div>
        <div class="map-col-item">Dona</div>
        <div class="map-col-item">Embajador</div>
        <div class="map-col-item">Patrocinador</div>
        <div class="map-col-item">Recaudar Fondos</div>
        <div class="map-col-item">Comparte Historia</div>
        <div class="map-col-item">Organiza Encuentro</div>
      </div>
    </div>
  </div>

  <div class="divider" style="margin-top:14px;"></div>

  <div class="section-title" style="margin-top:10px;">Analisis por Sistema de Arquitectura de Informacion</div>
  <table class="analysis-table">
    <thead>
      <tr>
        <th style="width:18%;">Sistema</th>
        <th style="width:8%;text-align:center;">Puntaje</th>
        <th style="width:12%;">Estado</th>
        <th>Analisis Detallado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="system-name">Organizacion</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#b5600a;"></div></div></td>
        <td class="score-cell" style="color:#b5600a;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Diferenciacion excepcional entre T1 y T2. Categorias por etapa de vida (Diagnostico, Vivir con, Cuidadores) muy centradas en el usuario.</td>
      </tr>
      <tr>
        <td><span class="system-name">Navegacion</span><div class="score-bar"><div class="score-bar-fill" style="width:85%;background:#b5600a;"></div></div></td>
        <td class="score-cell" style="color:#b5600a;">8.5</td>
        <td><span class="tag tag-good">Muy Buena</span></td>
        <td>Intuitiva con menus bien estructurados. Llamadas a la accion claras y bien ubicadas. Falta breadcrumbs en secciones profundas.</td>
      </tr>
      <tr>
        <td><span class="system-name">Etiquetado</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#b5600a;"></div></div></td>
        <td class="score-cell" style="color:#b5600a;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Lenguaje accesible y orientado a la audiencia. Etiquetas concisos, descriptivos y no tecnicos. Consistencia terminologica excelente.</td>
      </tr>
      <tr>
        <td><span class="system-name">Busqueda</span><div class="score-bar"><div class="score-bar-fill" style="width:75%;background:#b5600a;"></div></div></td>
        <td class="score-cell" style="color:#b5600a;">7.5</td>
        <td><span class="tag tag-improve">Mejorable</span></td>
        <td>Barra de busqueda no prominente. La buena organizacion reduce la necesidad, pero un buscador robusto con filtros mejoraria la experiencia.</td>
      </tr>
      <tr>
        <td><span class="system-name">Contenido / UX</span><div class="score-bar"><div class="score-bar-fill" style="width:90%;background:#b5600a;"></div></div></td>
        <td class="score-cell" style="color:#b5600a;">9.0</td>
        <td><span class="tag tag-optimal">Optimo</span></td>
        <td>Contenido empatico y de alta calidad. Mezcla educacion con apoyo comunitario. Diseno limpio, moderno y centrado en el usuario con excelente tono.</td>
      </tr>
    </tbody>
  </table>

  <div class="section-title" style="margin-top:10px;">Recomendaciones de Mejora</div>
  <div class="recs">
    <div class="rec-item" style="border-color:#b5600a;"><strong>Busqueda Prominente</strong>Agregar barra de busqueda visible con filtros.</div>
    <div class="rec-item" style="border-color:#b5600a;"><strong>Breadcrumbs</strong>Implementar en todas las paginas internas.</div>
    <div class="rec-item" style="border-color:#b5600a;"><strong>Testimonios</strong>Integrar mejor historias de la comunidad.</div>
    <div class="rec-item" style="border-color:#b5600a;"><strong>Alertas</strong>Crear alertas personalizadas para usuarios registrados.</div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">BeyondType1.org — Pagina 5</span>
  </div>
</div>


<!-- ══════════════════════════════════════════════════════
     COMPARATIVE PAGE
══════════════════════════════════════════════════════ -->
<div class="page">
  <div class="page-header">
    <div>
      <div class="site-number">Resumen Comparativo</div>
      <div class="site-name">Analisis Global de los 5 Sitios</div>
    </div>
    <div>
      <span class="score-label">Benchmark de UX</span>
    </div>
  </div>

  <div class="section-title">Tabla Comparativa de Puntajes</div>

  <table class="compare-table">
    <thead>
      <tr>
        <th>Sitio Web</th>
        <th>Organizacion</th>
        <th>Navegacion</th>
        <th>Etiquetado</th>
        <th>Busqueda</th>
        <th>Contenido/UX</th>
        <th>TOTAL</th>
      </tr>
    </thead>
    <tbody>
      <tr style="--site-color:#c84b31;">
        <td style="border-left:3px solid #c84b31;padding-left:12px;">WebMD</td>
        <td class="bar-cell"><span class="score-num">7.5</span><div class="bar-inner" style="width:75%;background:#c84b31;"></div></td>
        <td class="bar-cell"><span class="score-num">7.0</span><div class="bar-inner" style="width:70%;background:#c84b31;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#c84b31;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#c84b31;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#c84b31;"></div></td>
        <td class="total-cell" style="color:#c84b31;">7.8</td>
      </tr>
      <tr style="--site-color:#1a4e8c;">
        <td style="border-left:3px solid #1a4e8c;padding-left:12px;">Healthline</td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#1a4e8c;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#1a4e8c;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#1a4e8c;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#1a4e8c;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#1a4e8c;"></div></td>
        <td class="total-cell" style="color:#1a4e8c;">8.2</td>
      </tr>
      <tr style="--site-color:#2d6a4f;">
        <td style="border-left:3px solid #2d6a4f;padding-left:12px;">Patient.info</td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#2d6a4f;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#2d6a4f;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#2d6a4f;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#2d6a4f;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#2d6a4f;"></div></td>
        <td class="total-cell" style="color:#2d6a4f;">8.5</td>
      </tr>
      <tr style="--site-color:#7b2d8b;">
        <td style="border-left:3px solid #7b2d8b;padding-left:12px;">MedlinePlus ES</td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#7b2d8b;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#7b2d8b;"></div></td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#7b2d8b;"></div></td>
        <td class="bar-cell"><span class="score-num">8.0</span><div class="bar-inner" style="width:80%;background:#7b2d8b;"></div></td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#7b2d8b;"></div></td>
        <td class="total-cell" style="color:#7b2d8b;">8.6</td>
      </tr>
      <tr style="--site-color:#b5600a;">
        <td style="border-left:3px solid #b5600a;padding-left:12px;">BeyondType1.org</td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#b5600a;"></div></td>
        <td class="bar-cell"><span class="score-num">8.5</span><div class="bar-inner" style="width:85%;background:#b5600a;"></div></td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#b5600a;"></div></td>
        <td class="bar-cell"><span class="score-num">7.5</span><div class="bar-inner" style="width:75%;background:#b5600a;"></div></td>
        <td class="bar-cell"><span class="score-num">9.0</span><div class="bar-inner" style="width:90%;background:#b5600a;"></div></td>
        <td class="total-cell" style="color:#b5600a;">8.6</td>
      </tr>
    </tbody>
  </table>

  <div class="divider" style="margin-top:14px;"></div>

  <div class="section-title" style="margin-top:10px;">Conclusiones y Recomendaciones Globales</div>

  <div class="conclusion-grid">
    <div class="conclusion-box">
      <h4>Fortalezas Comunes</h4>
      <ul>
        <li>Contenido medico confiable y bien estructurado</li>
        <li>Navegacion intuitiva en la mayoria de casos</li>
        <li>Disenos modernos y accesibles</li>
        <li>Multiples formatos de contenido</li>
        <li>Terminologia medica clara y consistente</li>
        <li>Jerarquia informativa logica</li>
      </ul>
    </div>
    <div class="conclusion-box">
      <h4>Debilidades Comunes</h4>
      <ul>
        <li class="minus">Ausencia de breadcrumbs consistentes</li>
        <li class="minus">Busqueda poco avanzada sin filtros</li>
        <li class="minus">Jerarquia visual mejorable</li>
        <li class="minus">Falta de personalizacion de usuario</li>
        <li class="minus">Mobile-first no siempre prioritario</li>
        <li class="minus">Comunidad poco integrada</li>
      </ul>
    </div>
    <div class="conclusion-box">
      <h4>Recomendaciones Prioritarias</h4>
      <ul>
        <li>Breadcrumbs en TODAS las paginas internas</li>
        <li>Busqueda avanzada con filtros multiples</li>
        <li>Personalizacion para usuarios frecuentes</li>
        <li>Mejora de accesibilidad (WCAG 2.1)</li>
        <li>Optimizacion Mobile-First</li>
        <li>Mayor integracion de comunidad</li>
      </ul>
    </div>
    <div class="conclusion-box">
      <h4>Lider por Categoria</h4>
      <ul>
        <li>Organizacion: MedlinePlus / BeyondType1</li>
        <li>Navegacion: BeyondType1 (8.5)</li>
        <li>Etiquetado: MedlinePlus / BeyondType1</li>
        <li>Busqueda: WebMD (8.5)</li>
        <li>Contenido/UX: MedlinePlus / BeyondType1</li>
        <li>General: MedlinePlus = BeyondType1 (8.6)</li>
      </ul>
    </div>
  </div>

  <div class="page-footer">
    <span class="footer-text">Compendio de Mapas de Contenido</span>
    <span class="footer-text">Resumen Comparativo — Pagina 6</span>
  </div>
</div>

</body>
</html>
