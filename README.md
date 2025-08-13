
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>[Tu Marca] – Jardinería en [Tu Ciudad] | Mantenimiento, podas, riego</title>
  <meta name="description" content="Servicios de jardinería en [Tu Ciudad]: creación y mantenimiento de jardines, poda y tala de árboles, desbroces y riego automático. Presupuesto gratuito." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --green:#245b2a; /* principal (inspirado en vigojardin) */
      --green-2:#2f7b36; /* acento */
      --beige:#f4f6f3;   /* fondo suave */
      --ink:#1f2937;     /* texto */
    }
    *{box-sizing:border-box}
    html,body{margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial,sans-serif;color:var(--ink);}
    a{color:inherit;text-decoration:none}
    img{max-width:100%;display:block}
    .container{max-width:1160px;margin-inline:auto;padding:0 1.25rem}
    /* Header */
    header{position:sticky;top:0;z-index:50;background:#fff;border-bottom:1px solid #e5e7eb}
    .nav{display:flex;align-items:center;justify-content:space-between;height:64px}
    .brand{display:flex;align-items:center;gap:.6rem;font-weight:700;color:var(--green)}
    .brand .leaf{width:28px;height:28px;border-radius:8px;background:conic-gradient(from 180deg,var(--green),var(--green-2));display:inline-block}
    .menu{display:flex;gap:1.2rem;align-items:center}
    .menu a{font-weight:600}
    .cta{background:var(--green);color:#fff;padding:.6rem 1rem;border-radius:.7rem;display:inline-flex;gap:.5rem;align-items:center}
    .burger{display:none;background:none;border:none;font-size:1.6rem}
    /* Hero */
    .hero{background:linear-gradient(180deg,rgba(36,91,42,.08),rgba(36,91,42,.02)), url('https://images.unsplash.com/photo-1518860308377-870b866b159c?q=80&w=1600&auto=format&fit=crop') center/cover no-repeat;}
    .hero .wrap{backdrop-filter:saturate(110%) brightness(1);padding:96px 0}
    .badge{display:inline-block;background:#e8f2ea;color:var(--green);font-weight:700;padding:.35rem .7rem;border-radius:999px;font-size:.85rem}
    .hero h1{font-size: clamp(2rem, 4vw + 1rem, 3.2rem);line-height:1.1;margin:.6rem 0 1rem;color:#0f172a}
    .hero p{max-width:750px;font-size:1.1rem}
    .actions{margin-top:1.2rem;display:flex;gap:.8rem;flex-wrap:wrap}
    .btn{border-radius:.75rem;padding:.9rem 1.1rem;font-weight:700;border:2px solid transparent}
    .btn-primary{background:var(--green);color:#fff}
    .btn-outline{border-color:var(--green);color:var(--green)}
    /* Services */
    section{padding:72px 0}
    .section-head{display:flex;align-items:flex-end;justify-content:space-between;gap:1rem;margin-bottom:28px}
    h2{font-size: clamp(1.6rem, 2.2vw + .8rem, 2.2rem);margin:0}
    .grid{display:grid;grid-template-columns:repeat(12,1fr);gap:1rem}
    .card{grid-column:span 12;background:#fff;border:1px solid #e5e7eb;border-radius:1rem;padding:1rem;display:flex;gap:1rem;align-items:center}
    .icon{width:48px;height:48px;border-radius:12px;background:radial-gradient(circle at 30% 30%,#fff, #dbeee0);display:grid;place-items:center;color:var(--green);font-weight:900}
    .card h3{margin:.2rem 0 .3rem}
    @media (min-width:768px){
      .card{grid-column:span 6}
    }
    @media (min-width:1024px){
      .card{grid-column:span 4}
    }
    .muted{color:#475569}
    /* Feature blocks */
    .feature{display:grid;gap:2rem;align-items:center}
    .feature img{border-radius:1rem}
    @media (min-width:900px){
      .feature{grid-template-columns:1.1fr 1fr}
      .feature.reverse{grid-template-columns:1fr 1.1fr}
    }
    .list{margin:0;padding-left:1.1rem}
    .list li{margin:.3rem 0}
    /* Gallery */
    .gallery{display:grid;gap:1rem;grid-template-columns:repeat(2,1fr)}
    @media (min-width:900px){.gallery{grid-template-columns:repeat(4,1fr)}}
    .gallery img{aspect-ratio:4/3;object-fit:cover;border-radius:.8rem}
    /* Contact */
    #contacto{background:var(--beige)}
    form{display:grid;gap:.8rem;max-width:680px}
    input,textarea{width:100%;padding:.9rem;border:1px solid #cbd5e1;border-radius:.7rem;font:inherit}
    .legal{font-size:.85rem;color:#64748b}
    /* Footer */
    footer{background:#0b1f0e;color:#cfe6d2}
    .foot{display:grid;gap:1rem;padding:36px 0}
    @media (min-width:900px){.foot{grid-template-columns:1.2fr 1fr 1fr}}
    .foot a{color:#e5f6e8}
  </style>
  <script>
    // WhatsApp helper: replace with your number (international format, no +)
    const WHATSAPP = '34999999999';
    document.addEventListener('DOMContentLoaded',()=>{
      document.querySelectorAll('[data-wa]').forEach(el=>{
        el.href = `https://wa.me/${WHATSAPP}?text=${encodeURIComponent('Hola, me gustaría pedir un presupuesto de jardinería.')}`;
      });
      const burger=document.getElementById('burger');
      const nav=document.getElementById('navlinks');
      burger?.addEventListener('click',()=>{
        nav.style.display = nav.style.display==='flex'?'none':'flex';
      });
    });
  </script>
  <script type="application/ld+json">
  {
    "@context":"https://schema.org",
    "@type":"GardenService",
    "name":"[Tu Marca]",
    "areaServed":"[Tu Ciudad]",
    "url":"https://tu-dominio.com",
    "telephone":"+34 999 999 999",
    "sameAs":["https://www.instagram.com/tu_marca","https://www.facebook.com/tu_marca"],
    "address":{"@type":"PostalAddress","addressLocality":"[Tu Ciudad]","addressRegion":"[Provincia]","addressCountry":"ES"}
  }
  </script>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="container nav">
      <a class="brand" href="#inicio"><span class="leaf"></span> <span>[Tu Marca]</span></a>
      <nav>
        <button class="burger" id="burger">☰</button>
        <div class="menu" id="navlinks">
          <a href="#servicios">Servicios</a>
          <a href="#trabajos">Trabajos</a>
          <a href="#sobre">Sobre nosotros</a>
          <a href="#contacto" class="cta">Contactar</a>
        </div>
      </nav>
    </div>
  </header>

  <!-- Hero -->
  <section id="inicio" class="hero">
    <div class="container wrap">
      <span class="badge">Jardinería en [Tu Ciudad]</span>
      <h1>Creamos y cuidamos jardines bonitos, funcionales y de bajo mantenimiento</h1>
      <p>Especialistas en <strong>creación y mantenimiento de jardines</strong>, <strong>poda y tala</strong>, <strong>desbroces</strong> y <strong>riego automático</strong>. Presupuesto gratuito y trato cercano.</p>
      <div class="actions">
        <a class="btn btn-primary" data-wa target="_blank" rel="noopener">Pedir presupuesto por WhatsApp</a>
        <a class="btn btn-outline" href="#servicios">Ver servicios</a>
      </div>
    </div>
  </section>

  <!-- Servicios -->
  <section id="servicios">
    <div class="container">
      <div class="section-head">
        <h2>Nuestros servicios de jardinería</h2>
        <a class="cta" href="#contacto">Solicitar info</a>
      </div>
      <div class="grid">
        <article class="card">
          <div class="icon">🌱</div>
          <div>
            <h3>Creación de jardines</h3>
            <p class="muted">Diseño y obra: césped natural o tepe, jardineras, rocallas, parterres, selección de plantas y setos.</p>
          </div>
        </article>
        <article class="card">
          <div class="icon">✂️</div>
          <div>
            <h3>Poda y tala de árboles</h3>
            <p class="muted">Poda en altura con medios técnicos y retiradas seguras. Gestión de restos en planta de reciclaje.</p>
          </div>
        </article>
        <article class="card">
          <div class="icon">🧹</div>
          <div>
            <h3>Desbroce y limpieza</h3>
            <p class="muted">Desbroces de fincas, control de malas hierbas y puesta a punto de jardines y comunidades.</p>
          </div>
        </article>
        <article class="card">
          <div class="icon">🫛</div>
          <div>
            <h3>Mantenimiento integral</h3>
            <p class="muted">Corte de césped, abonados, escarificado, riegos, control fitosanitario y calendario estacional.</p>
          </div>
        </article>
        <article class="card">
          <div class="icon">💧</div>
          <div>
            <h3>Riego automático</h3>
            <p class="muted">Instalación y revisión de sistemas de riego con primeras marcas. Programación eficiente.</p>
          </div>
        </article>
      </div>
    </div>
  </section>

  <!-- Bloques destacados (inspirados en secciones internas) -->
  <section class="beige">
    <div class="container feature">
      <div>
        <h2>Jardines funcionales y de bajo mantenimiento</h2>
        <p>Nos adaptamos a tu espacio y a tu presupuesto para crear zonas verdes bonitas y prácticas durante todo el año.</p>
        <ul class="list">
          <li>Selección de especies resistentes a tu clima</li>
          <li>Césped natural o alternativas de bajo consumo</li>
          <li>Soluciones de drenaje y riego optimizado</li>
        </ul>
      </div>
      <img src="https://images.unsplash.com/photo-1523419409543-8a7f71b3a9a0?q=80&w=1200&auto=format&fit=crop" alt="Jardín de bajo mantenimiento" />
    </div>
  </section>

  <section>
    <div class="container feature reverse">
      <img src="https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1200&auto=format&fit=crop" alt="Poda en altura" />
      <div>
        <h2>Poda y tala con seguridad</h2>
        <p>Equipo cualificado y medios mecánicos para trabajos de altura. Retiramos y gestionamos los restos.</p>
        <ul class="list">
          <li>Poda de formación y saneamiento</li>
          <li>Tala de ejemplares peligrosos</li>
          <li>Informes y asesoramiento</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- Galería -->
  <section id="trabajos">
    <div class="container">
      <div class="section-head">
        <h2>Trabajos recientes</h2>
        <span class="muted">Antes / después</span>
      </div>
      <div class="gallery">
        <img src="https://images.unsplash.com/photo-1592841200221-9c9d7560d9b1?q=80&w=1200&auto=format&fit=crop" alt="Césped recién cortado" />
        <img src="https://images.unsplash.com/photo-1505575972945-2804b56ba39f?q=80&w=1200&auto=format&fit=crop" alt="Seto recortado" />
        <img src="https://images.unsplash.com/photo-1496661415325-ef852f9e8e7c?q=80&w=1200&auto=format&fit=crop" alt="Rocalla con flores" />
        <img src="https://images.unsplash.com/photo-1499951360447-b19be8fe80f5?q=80&w=1200&auto=format&fit=crop" alt="Detalle de jardín" />
      </div>
    </div>
  </section>

  <!-- Sobre nosotros -->
  <section id="sobre" style="background:var(--beige)">
    <div class="container feature">
      <div>
        <h2>Sobre nosotros</h2>
        <p>Somos <strong>[Tu Marca]</strong>, jardineros en <strong>[Tu Ciudad]</strong> con <strong>[X] años</strong> de experiencia. Nos gusta trabajar bien, a tiempo y dejarlo todo limpio. Nuestro objetivo es que disfrutes tu jardín sin complicaciones.</p>
        <p class="muted">Damos servicio a viviendas, comunidades y empresas en [Zonas de servicio].</p>
      </div>
      <img src="https://images.unsplash.com/photo-1607546944281-39e96bdb1fad?q=80&w=1200&auto=format&fit=crop" alt="Equipo de jardinería" />
    </div>
  </section>

  <!-- Contacto -->
  <section id="contacto">
    <div class="container">
      <div class="section-head">
        <h2>Contacto y presupuesto</h2>
        <a class="cta" data-wa target="_blank" rel="noopener">Escribir por WhatsApp</a>
      </div>
      <form onsubmit="alert('Este formulario es de ejemplo. Conéctalo a tu email o Google Forms.'); return false;">
        <div class="grid" style="grid-template-columns:repeat(12,1fr);gap:1rem">
          <div style="grid-column:span 12;"> <input required placeholder="Tu nombre" /> </div>
          <div style="grid-column:span 6;"> <input type="tel" placeholder="Teléfono" /> </div>
          <div style="grid-column:span 6;"> <input type="email" placeholder="Email" /> </div>
          <div style="grid-column:span 12;"> <textarea rows="5" placeholder="Cuéntanos qué necesitas"></textarea> </div>
        </div>
        <label class="legal"><input type="checkbox" required> Acepto el aviso legal y la política de privacidad.</label>
        <div class="actions"><button class="btn btn-primary" type="submit">Enviar</button></div>
      </form>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <div class="container foot">
      <div>
        <div class="brand"><span class="leaf"></span><span>[Tu Marca]</span></div>
        <p style="margin:.6rem 0">Jardinería en [Tu Ciudad] – Mantenimiento, podas, desbroces y riego automático.</p>
        <p>Tel.: <a href="tel:+34999999999">+34 999 999 999</a> · Email: <a href="mailto:info@tu-marca.com">info@tu-marca.com</a></p>
      </div>
      <div>
        <h4>Secciones</h4>
        <p><a href="#servicios">Servicios</a><br><a href="#trabajos">Trabajos</a><br><a href="#sobre">Sobre nosotros</a><br><a href="#contacto">Contacto</a></p>
      </div>
      <div>
        <h4>Legal</h4>
        <p><a href="#">Aviso legal</a><br><a href="#">Política de privacidad</a><br><a href="#">Cookies</a></p>
      </div>
    </div>
    <div style="text-align:center;padding:12px 0;border-top:1px solid #174a1c">© <span id="year"></span> [Tu Marca]. Todos los derechos reservados.</div>
  </footer>
  <script>document.getElementById('year').textContent = new Date().getFullYear()</script>
</body>
</html>

