
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --ta-blue: #185FA5;
    --ta-blue-light: #E6F1FB;
    --ta-blue-mid: #378ADD;
    --ta-dark: #0C447C;
    --ta-text: #11233E;
    --ta-muted: #5F6C86;
    --ta-bg: #F8FAFC;
    --ta-surface: #FFFFFF;
    --ta-border: #D7E0EF;
    --border-radius-md: 14px;
    --border-radius-lg: 20px;
  }
  body { font-family: Inter, system-ui, -apple-system, BlinkMacSystemFont, sans-serif; background: #E7EFF8; }

  .app-frame {
    max-width: 390px;
    margin: 0 auto;
    border: 0.5px solid var(--ta-border);
    border-radius: 28px;
    overflow: hidden;
    background: var(--ta-bg);
    min-height: 700px;
  }
  .screen { display: none; flex-direction: column; min-height: 700px; }
  .screen.active { display: flex; }

  /* Status bar */
  .status-bar {
    background: var(--ta-blue);
    padding: 10px 20px 6px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    font-size: 11px;
    font-weight: 500;
  }
  .status-icons { display: flex; gap: 4px; align-items: center; font-size: 13px; }

  /* Header */
  .app-header {
    background: var(--ta-blue);
    padding: 10px 20px 16px;
    color: white;
  }
  .app-header.small {
    padding: 8px 20px 12px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .brand { display: flex; align-items: center; gap: 10px; }
  .brand-logo {
    width: 42px; height: 42px;
    border-radius: 12px;
    background: white;
    overflow: hidden;
    display: flex; align-items: center; justify-content: center;
    box-shadow: 0 4px 18px rgba(0,0,0,.08);
  }
  .brand-logo img {
    width: 100%; height: 100%; object-fit: cover;
  }
  .brand-name { font-size: 18px; font-weight: 600; line-height: 1.1; }
  .brand-tagline { font-size: 11px; opacity: 0.85; margin-top: 2px; }
  .header-back {
    background: rgba(255,255,255,0.15);
    border: none; border-radius: 8px;
    color: white; font-size: 18px;
    width: 32px; height: 32px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; flex-shrink: 0;
  }
  .header-title { font-size: 16px; font-weight: 500; color: white; flex: 1; }

  /* Content */
  .content { flex: 1; overflow-y: auto; padding: 16px; background: var(--ta-surface); }
  .content.white { background: var(--ta-bg); }

  /* Hero banner */
  .hero {
    background: linear-gradient(135deg, #0C447C 0%, #185FA5 45%, #378ADD 100%);
    border-radius: var(--border-radius-lg);
    padding: 18px;
    color: white;
    margin-bottom: 14px;
  }
  .hero-title { font-size: 15px; font-weight: 600; margin-bottom: 4px; line-height: 1.3; }
  .hero-image {
    margin-top: 16px;
    border-radius: 18px;
    overflow: hidden;
    border: 1px solid rgba(255,255,255,0.18);
  }
  .hero-image img {
    width: 100%; display: block;
    filter: brightness(1.05);
  }
  .image-row {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 10px;
    margin-bottom: 14px;
  }
  .image-row img {
    width: 100%;
    height: 120px;
    object-fit: cover;
    border-radius: 18px;
    border: 1px solid rgba(0,0,0,.08);
  }
  .contact-qr {
    display: flex;
    gap: 12px;
    align-items: center;
    padding: 14px;
    background: #FFFFFF;
    border: 0.5px solid var(--ta-border);
    border-radius: var(--border-radius-lg);
    margin-bottom: 14px;
  }
  .contact-qr img {
    width: 84px;
    height: 84px;
    border-radius: 18px;
    object-fit: cover;
  }
  .contact-qr-text {
    flex: 1;
    font-size: 13px;
    color: var(--ta-text);
    line-height: 1.4;
  }
  .contact-qr-text strong { display: block; margin-bottom: 4px; }
  .hero-sub { font-size: 12px; opacity: 0.85; line-height: 1.5; }
  .hero-badge {
    display: inline-block;
    background: rgba(255,255,255,0.2);
    font-size: 11px; padding: 3px 8px;
    border-radius: 20px; margin-top: 10px;
  }

  /* Section label */
  .section-label {
    font-size: 12px; font-weight: 500;
    color: var(--ta-muted);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin: 14px 0 8px;
  }

  /* Quick action grid */
  .quick-grid {
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 8px; margin-bottom: 14px;
  }
  .quick-btn {
    background: var(--ta-bg);
    border: 0.5px solid var(--ta-border);
    border-radius: var(--border-radius-md);
    padding: 10px 4px;
    display: flex; flex-direction: column;
    align-items: center; gap: 5px;
    cursor: pointer; transition: background 0.15s;
  }
  .quick-btn:hover { background: var(--ta-blue-light); }
  .quick-btn-icon {
    width: 32px; height: 32px;
    background: var(--ta-blue-light);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px; color: var(--ta-blue);
  }
  .quick-btn-label { font-size: 10px; color: var(--ta-muted); text-align: center; line-height: 1.2; }

  /* Cards */
  .card {
    background: var(--ta-bg);
    border: 0.5px solid var(--ta-border);
    border-radius: var(--border-radius-lg);
    padding: 14px;
    margin-bottom: 10px;
    cursor: pointer;
    transition: border-color 0.15s, transform 0.15s;
  }
  .card:hover { transform: translateY(-1px); }
  .card-image {
    width: 100%;
    border-radius: 16px;
    margin-bottom: 10px;
    overflow: hidden;
  }
  .card-image img {
    width: 100%; display: block;
    object-fit: cover;
    height: 150px;
  }
  .card:hover { border-color: var(--ta-blue-mid); }
  .card-header { display: flex; align-items: center; gap: 10px; margin-bottom: 6px; }
  .card-icon {
    width: 36px; height: 36px;
    background: var(--ta-blue-light);
    border-radius: 9px;
    display: flex; align-items: center; justify-content: center;
    font-size: 17px; color: var(--ta-blue);
    flex-shrink: 0;
  }
  .card-title { font-size: 14px; font-weight: 500; color: var(--ta-text); }
  .card-sub { font-size: 12px; color: var(--ta-muted); }
  .card-desc { font-size: 12px; color: var(--ta-muted); line-height: 1.5; }
  .card-price {
    display: inline-block;
    background: var(--ta-blue-light);
    color: var(--ta-dark);
    font-size: 13px; font-weight: 500;
    padding: 3px 10px; border-radius: 20px;
    margin-top: 8px;
  }
  .card-arrow { margin-left: auto; color: var(--ta-muted); font-size: 16px; }
  .chip {
    display: inline-block;
    font-size: 11px; padding: 2px 8px;
    border-radius: 20px; margin-right: 4px;
    background: #E6F1FB; color: #0C447C;
  }
  .chip.green { background: #EAF3DE; color: #27500A; }

  /* Contact items */
  .contact-item {
    display: flex; align-items: center; gap: 12px;
    padding: 12px;
    background: var(--ta-bg);
    border: 0.5px solid var(--ta-border);
    border-radius: var(--border-radius-md);
    margin-bottom: 8px;
  }
  .contact-icon {
    width: 38px; height: 38px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px; flex-shrink: 0;
  }
  .contact-icon.blue { background: var(--ta-blue-light); color: var(--ta-blue); }
  .contact-icon.green { background: #EAF3DE; color: #3B6D11; }
  .contact-text { flex: 1; }
  .contact-label { font-size: 11px; color: var(--ta-muted); }
  .contact-val { font-size: 14px; font-weight: 500; color: var(--ta-text); }
  .contact-action {
    background: var(--ta-blue);
    color: white; border: none;
    border-radius: 8px; padding: 6px 12px;
    font-size: 12px; cursor: pointer;
  }

  /* Bottom nav */
  .bottom-nav {
    display: flex;
    border-top: 0.5px solid var(--ta-border);
    background: var(--ta-bg);
    padding: 8px 0 10px;
  }
  .nav-item {
    flex: 1; display: flex; flex-direction: column;
    align-items: center; gap: 3px;
    cursor: pointer; padding: 4px;
    border: none; background: none;
  }
  .nav-item i { font-size: 20px; color: var(--ta-muted); transition: color 0.15s; }
  .nav-item span { font-size: 10px; color: var(--ta-muted); transition: color 0.15s; }
  .nav-item.active i, .nav-item.active span { color: var(--ta-blue); }
  .nav-dot {
    width: 4px; height: 4px;
    background: var(--ta-blue);
    border-radius: 50%; margin-top: -2px;
  }

  /* Divider */
  .divider { height: 0.5px; background: var(--ta-border); margin: 12px 0; }

  /* Info row */
  .info-row { display: flex; gap: 8px; margin-bottom: 10px; }
  .info-pill {
    background: var(--ta-bg);
    border: 0.5px solid var(--ta-border);
    border-radius: 20px;
    padding: 5px 12px;
    font-size: 12px; color: var(--ta-muted);
    display: flex; align-items: center; gap: 5px;
  }
  .info-pill i { font-size: 14px; color: var(--ta-blue); }

  /* About section */
  .about-box {
    background: var(--ta-blue);
    border-radius: var(--border-radius-lg);
    padding: 16px; color: white; margin-bottom: 12px;
  }
  .about-box .name { font-size: 15px; font-weight: 500; }
  .about-box .role { font-size: 12px; opacity: 0.8; margin-top: 2px; }
  .about-box .phones { display: flex; gap: 6px; margin-top: 10px; flex-wrap: wrap; }
  .phone-chip {
    background: rgba(255,255,255,0.18);
    border-radius: 20px; padding: 4px 10px;
    font-size: 12px;
  }
</style>

<div class="app-frame">

  <!-- HOME SCREEN -->
  <div class="screen active" id="screen-home">
    <div class="status-bar">
      <span>TecnicoAngeles</span>
      <div class="status-icons">
        <i class="ti ti-wifi" aria-hidden="true"></i>
        <i class="ti ti-battery-2" aria-hidden="true"></i>
      </div>
    </div>
    <div class="app-header">
      <div class="brand">
        <div class="brand-logo">
          <img src="imgA/Logo.png" alt="Logo TecnicoAngeles">
        </div>
        <div>
          <div class="brand-name">TecnicoAngeles</div>
          <div class="brand-tagline">Punto Tecnológico · Soporte Técnico</div>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="hero">
        <div class="hero-title">Bienvenido al Punto Tecnológico</div>
        <div class="hero-sub">Soluciones profesionales en sistemas y teleinformática para hogares y negocios.</div>
        <div class="hero-badge">✓ Servicio rápido y confiable</div>
        <div class="hero-image"><img src="imgA/programando.png" alt="Soporte técnico en acción"></div>
      </div>

      <div class="image-grid" style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:14px;">
        <div style="overflow:hidden;border-radius:16px;"><img src="imgA/red.png" alt="Redes WiFi" style="width:100%;height:100%;object-fit:cover;" /></div>
        <div style="overflow:hidden;border-radius:16px;"><img src="imgA/3PC.png" alt="Mantenimiento de PC" style="width:100%;height:100%;object-fit:cover;" /></div>
        <div style="overflow:hidden;border-radius:16px;"><img src="imgA/Hardware-Discos-Duros-Mecanicos.jpg" alt="Reparación de hardware" style="width:100%;height:100%;object-fit:cover;" /></div>
      </div>

      <div class="section-label">Acceso rápido</div>
      <div class="quick-grid">
        <div class="quick-btn" onclick="goTo('servicios')">
          <div class="quick-btn-icon"><i class="ti ti-tool" aria-hidden="true"></i></div>
          <div class="quick-btn-label">Servicios</div>
        </div>
        <div class="quick-btn" onclick="goTo('productos')">
          <div class="quick-btn-icon"><i class="ti ti-package" aria-hidden="true"></i></div>
          <div class="quick-btn-label">Productos</div>
        </div>
        <div class="quick-btn" onclick="goTo('contacto')">
          <div class="quick-btn-icon"><i class="ti ti-phone" aria-hidden="true"></i></div>
          <div class="quick-btn-label">Contacto</div>
        </div>
        <div class="quick-btn" onclick="goTo('nosotros')">
          <div class="quick-btn-icon"><i class="ti ti-info-circle" aria-hidden="true"></i></div>
          <div class="quick-btn-label">Nosotros</div>
        </div>
      </div>

      <div class="section-label">Servicios destacados</div>
      <div class="card" onclick="goTo('servicios')">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-cpu" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Mantenimiento de equipos</div>
            <div class="card-sub">Hardware · Software · Limpieza</div>
          </div>
          <i class="ti ti-chevron-right card-arrow" aria-hidden="true"></i>
        </div>
        <div class="card-desc">Mantenimiento preventivo, limpieza interna, optimización y formateo de PC.</div>
      </div>
      <div class="card" onclick="goTo('servicios')">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-network" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Redes e internet</div>
            <div class="card-sub">LAN · WiFi · Cableado</div>
          </div>
          <i class="ti ti-chevron-right card-arrow" aria-hidden="true"></i>
        </div>
        <div class="card-desc">Instalación de cableado UTP, canaletas, configuración de redes LAN y WiFi.</div>
      </div>

      <div class="info-row">
        <div class="info-pill"><i class="ti ti-phone" aria-hidden="true"></i>317 570 2147</div>
        <div class="info-pill"><i class="ti ti-phone" aria-hidden="true"></i>321 763 3207</div>
      </div>
    </div>
    <nav class="bottom-nav">
      <button class="nav-item active" onclick="goTo('home')">
        <i class="ti ti-home"></i><span>Inicio</span><div class="nav-dot"></div>
      </button>
      <button class="nav-item" onclick="goTo('servicios')"><i class="ti ti-tool"></i><span>Servicios</span></button>
      <button class="nav-item" onclick="goTo('productos')"><i class="ti ti-package"></i><span>Productos</span></button>
      <button class="nav-item" onclick="goTo('contacto')"><i class="ti ti-phone"></i><span>Contacto</span></button>
    </nav>
  </div>

  <!-- SERVICIOS SCREEN -->
  <div class="screen" id="screen-servicios">
    <div class="status-bar">
      <span>TecnicoAngeles</span>
      <div class="status-icons"><i class="ti ti-wifi" aria-hidden="true"></i><i class="ti ti-battery-2" aria-hidden="true"></i></div>
    </div>
    <div class="app-header small">
      <button class="header-back" onclick="goTo('home')"><i class="ti ti-arrow-left" aria-hidden="true"></i></button>
      <span class="header-title">Servicios técnicos</span>
    </div>
    <div class="content">
      <div class="image-row">
        <img src="imgA/red y red.png" alt="Redes e internet">
        <img src="imgA/yo configurando red.png" alt="Soporte técnico remoto">
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-refresh" aria-hidden="true"></i></div>
          <div><div class="card-title">Formateo e instalación de SO</div></div>
        </div>
        <div class="card-desc">Formateo completo e instalación de Windows 7 al 10 con drivers y actualizaciones.</div>
        <span class="chip">Windows</span><span class="chip">SO</span>
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-cpu" aria-hidden="true"></i></div>
          <div><div class="card-title">Mantenimiento de hardware y software</div></div>
        </div>
        <div class="card-desc">Limpieza física, cambio de pasta térmica, optimización del sistema operativo y diagnóstico de fallas.</div>
        <span class="chip">PC escritorio</span>
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-apps" aria-hidden="true"></i></div>
          <div><div class="card-title">Instalación de programas</div></div>
        </div>
        <div class="card-desc">Office, antivirus, utilidades, navegadores y paquetes completos de software.</div>
        <span class="chip">Office</span><span class="chip">Antivirus</span>
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-network" aria-hidden="true"></i></div>
          <div><div class="card-title">Instalación de redes LAN y WiFi</div></div>
        </div>
        <div class="card-desc">Cableado UTP, canaletas, switches y configuración completa de red e internet.</div>
        <span class="chip">LAN</span><span class="chip">WiFi</span>
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-headset" aria-hidden="true"></i></div>
          <div><div class="card-title">Soporte técnico remoto y presencial</div></div>
        </div>
        <div class="card-desc">Asistencia en sitio o a distancia, diagnóstico y resolución de problemas técnicos.</div>
        <span class="chip green">Disponible</span>
      </div>
      <div class="card">
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-speakerphone" aria-hidden="true"></i></div>
          <div><div class="card-title">Publicidad y marketing digital</div></div>
        </div>
        <div class="card-desc">Planes de marketing digital y publicidad para pequeños negocios.</div>
      </div>
    </div>
    <nav class="bottom-nav">
      <button class="nav-item" onclick="goTo('home')"><i class="ti ti-home"></i><span>Inicio</span></button>
      <button class="nav-item active" onclick="goTo('servicios')"><i class="ti ti-tool"></i><span>Servicios</span><div class="nav-dot"></div></button>
      <button class="nav-item" onclick="goTo('productos')"><i class="ti ti-package"></i><span>Productos</span></button>
      <button class="nav-item" onclick="goTo('contacto')"><i class="ti ti-phone"></i><span>Contacto</span></button>
    </nav>
  </div>

  <!-- PRODUCTOS SCREEN -->
  <div class="screen" id="screen-productos">
    <div class="status-bar">
      <span>TecnicoAngeles</span>
      <div class="status-icons"><i class="ti ti-wifi" aria-hidden="true"></i><i class="ti ti-battery-2" aria-hidden="true"></i></div>
    </div>
    <div class="app-header small">
      <button class="header-back" onclick="goTo('home')"><i class="ti ti-arrow-left" aria-hidden="true"></i></button>
      <span class="header-title">Catálogo de productos</span>
    </div>
    <div class="content">
      <div class="card">
        <div class="card-image"><img src="imgA/Activiruz .png" alt="Antivirus de alta gama"></div>
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-shield-check" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Antivirus de alta gama</div>
            <div class="card-sub">Protección en tiempo real</div>
          </div>
        </div>
        <div class="card-desc">Protección avanzada contra malware, amenazas digitales y actualizaciones automáticas.</div>
        <div class="card-price">$10.000 COP</div>
      </div>
      <div class="card">
        <div class="card-image"><img src="imgA/Producto de Windows y office.png" alt="Licencia de Windows"></div>
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-brand-windows" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Licencia de Windows</div>
            <div class="card-sub">Activación original</div>
          </div>
        </div>
        <div class="card-desc">Activación original de Windows garantizando funcionamiento óptimo, seguro y sin restricciones.</div>
        <div class="card-price">$50.000 COP</div>
      </div>
      <div class="card">
        <div class="card-image"><img src="imgA/Producto de Windows y office.png" alt="Microsoft Office"></div>
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-file-text" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Microsoft Office</div>
            <div class="card-sub">Licencia completa</div>
          </div>
        </div>
        <div class="card-desc">Licenciamiento de Office para uso correcto de todas sus funciones sin restricciones.</div>
        <div class="card-price">$50.000 COP</div>
      </div>
      <div class="card">
        <div class="card-image"><img src="imgA/yo.png" alt="Limpieza de CPU con técnico"></div>
        <div class="card-header">
          <div class="card-icon"><i class="ti ti-tool" aria-hidden="true"></i></div>
          <div>
            <div class="card-title">Limpieza y mantenimiento de CPU</div>
            <div class="card-sub">Torre / PC escritorio</div>
          </div>
        </div>
        <div class="card-desc">Limpieza interna de la torre, mantenimiento preventivo para optimizar rendimiento y prolongar la vida útil del equipo.</div>
        <div class="card-price">$75.000 COP</div>
      </div>
      <div style="padding: 4px 0 8px;">
        <div style="font-size: 12px; color: var(--ta-muted); text-align: center; line-height: 1.6;">
          Para solicitar cualquier servicio,<br>comunícate por WhatsApp o llama directamente.
        </div>
      </div>
    </div>
    <nav class="bottom-nav">
      <button class="nav-item" onclick="goTo('home')"><i class="ti ti-home"></i><span>Inicio</span></button>
      <button class="nav-item" onclick="goTo('servicios')"><i class="ti ti-tool"></i><span>Servicios</span></button>
      <button class="nav-item active" onclick="goTo('productos')"><i class="ti ti-package"></i><span>Productos</span><div class="nav-dot"></div></button>
      <button class="nav-item" onclick="goTo('contacto')"><i class="ti ti-phone"></i><span>Contacto</span></button>
    </nav>
  </div>

  <!-- CONTACTO SCREEN -->
  <div class="screen" id="screen-contacto">
    <div class="status-bar">
      <span>TecnicoAngeles</span>
      <div class="status-icons"><i class="ti ti-wifi" aria-hidden="true"></i><i class="ti ti-battery-2" aria-hidden="true"></i></div>
    </div>
    <div class="app-header small">
      <button class="header-back" onclick="goTo('home')"><i class="ti ti-arrow-left" aria-hidden="true"></i></button>
      <span class="header-title">Contacto</span>
    </div>
    <div class="content white">
      <div class="contact-qr">
        <img src="imgA/numeroQR.png" alt="Código QR WhatsApp">
        <div class="contact-qr-text">
          <strong>WhatsApp rápido</strong>
          Escanea el código o pulsa el botón para escribirnos al instante. Atendemos dudas, presupuestos y soporte técnico.
        </div>
      </div>
      <div class="about-box">
        <div style="display:flex;align-items:center;gap:12px">
          <div style="width:46px;height:46px;border-radius:50%;overflow:hidden;background:white;display:flex;align-items:center;justify-content:center;font-size:20px;box-shadow:0 12px 24px rgba(0,0,0,.08);">
            <img src="imgA/yo.png" alt="Ángel A.R.M" style="width:100%;height:100%;object-fit:cover;">
          </div>
          <div>
            <div class="name">Ángel A.R.M</div>
            <div class="role">Técnico en Sistemas y Teleinformática</div>
          </div>
        </div>
        <div class="phones">
          <div class="phone-chip">317 570 2147</div>
          <div class="phone-chip">321 763 3207</div>
        </div>
      </div>

      <div class="section-label">Canales de atención</div>

      <div class="contact-item">
        <div class="contact-icon green"><i class="ti ti-brand-whatsapp" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">WhatsApp</div>
          <div class="contact-val">317 570 2147</div>
        </div>
        <button class="contact-action" onclick="openLink('https://wa.me/573175702147')">Abrir</button>
      </div>
      <div class="contact-item">
        <div class="contact-icon blue"><i class="ti ti-phone" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">Teléfono 1</div>
          <div class="contact-val">317 570 2147</div>
        </div>
        <button class="contact-action" onclick="openLink('tel:3175702147')">Llamar</button>
      </div>
      <div class="contact-item">
        <div class="contact-icon blue"><i class="ti ti-phone" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">Teléfono 2</div>
          <div class="contact-val">321 763 3207</div>
        </div>
        <button class="contact-action" onclick="openLink('tel:3217633207')">Llamar</button>
      </div>
      <div class="contact-item">
        <div class="contact-icon blue"><i class="ti ti-brand-facebook" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">Facebook</div>
          <div class="contact-val">Angel Antonio Rodriguez Moreno</div>
        </div>
        <button class="contact-action" onclick="openLink('https://www.facebook.com/share/p/1ETVKac9DR/')">Ver</button>
      </div>
      <div class="contact-item">
        <div class="contact-icon blue"><i class="ti ti-brand-tiktok" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">TikTok</div>
          <div class="contact-val">tecnicoen_sistemas_telei</div>
        </div>
        <button class="contact-action" onclick="openLink('https://www.tiktok.com/@tecnicoen_sistemas_telei')">Ver</button>
      </div>
      <div class="contact-item">
        <div class="contact-icon blue"><i class="ti ti-world" aria-hidden="true"></i></div>
        <div class="contact-text">
          <div class="contact-label">Sitio web</div>
          <div class="contact-val" style="font-size:12px">tecnicoangeles</div>
        </div>
        <button class="contact-action" onclick="openLink('https://arodriguezmoreno69-prog.github.io/tecnicoangeles/index.html')">Ver</button>
      </div>

      <div class="divider"></div>
      <div style="background:var(--ta-blue-light);border-radius:var(--border-radius-md);padding:12px;border:0.5px solid var(--color-border-tertiary);">
        <div style="font-size:12px;color:#0c217c;font-weight:500;margin-bottom:4px;">
          <i class="ti ti-quote" aria-hidden="true"></i> Lema
        </div>
        <div style="font-size:12px;color:#185FA5;line-height:1.5;font-style:italic">
          "Tu equipo queda funcionando correctamente para el mejor rendimiento."
        </div>
      </div>
    </div>
    <nav class="bottom-nav">
      <button class="nav-item" onclick="goTo('home')"><i class="ti ti-home"></i><span>Inicio</span></button>
      <button class="nav-item" onclick="goTo('servicios')"><i class="ti ti-tool"></i><span>Servicios</span></button>
      <button class="nav-item" onclick="goTo('productos')"><i class="ti ti-package"></i><span>Productos</span></button>
      <button class="nav-item active" onclick="goTo('contacto')"><i class="ti ti-phone"></i><span>Contacto</span><div class="nav-dot"></div></button>
    </nav>
  </div>

  <!-- NOSOTROS SCREEN -->
  <div class="screen" id="screen-nosotros">
    <div class="status-bar">
      <span>TecnicoAngeles</span>
      <div class="status-icons"><i class="ti ti-wifi" aria-hidden="true"></i><i class="ti ti-battery-2" aria-hidden="true"></i></div>
    </div>
    <div class="app-header small">
      <button class="header-back" onclick="goTo('home')"><i class="ti ti-arrow-left" aria-hidden="true"></i></button>
      <span class="header-title">Quiénes somos</span>
    </div>
    <div class="content white">
      <div style="text-align:center;padding:20px 10px 12px;">
        <div style="width:72px;height:72px;border-radius:18px;margin:0 auto 12px;overflow:hidden;box-shadow:0 10px 24px rgba(0,0,0,.12);">
          <img src="imgA/Logo.png" alt="Logo TecnicoAngeles" style="width:100%;height:100%;object-fit:cover;">
        </div>
        <div style="font-size:18px;font-weight:500;color:var(--ta-text)">TécnicoAngeles</div>
        <div style="font-size:12px;color:var(--ta-muted);margin-top:4px">Punto Tecnológico · Sistemas y Teleinformática</div>
      </div>

      <div class="card" style="cursor:default">
        <div style="font-size:13px;color:var(--ta-muted);line-height:1.7">
          Emprendimiento dedicado al soporte técnico en sistemas y teleinformática. Nuestro objetivo es ofrecer un servicio responsable, eficiente y de calidad, enfocado en la satisfacción del cliente y el buen uso de la tecnología.
        </div>
      </div>

      <div class="section-label">Misión</div>
      <div class="card" style="cursor:default">
        <div style="font-size:13px;color:var(--ta-muted);line-height:1.7">
          Brindar soluciones tecnológicas confiables, rápidas y seguras para hogares y pequeños negocios, impulsando el mundo digital con compromiso, calidad y confianza.
        </div>
      </div>

      <div class="section-label">Especialidades</div>
      <div style="display:flex;flex-wrap:wrap;gap:6px;margin-bottom:14px">
        <span class="chip">Soporte técnico</span>
        <span class="chip">Redes LAN / WiFi</span>
        <span class="chip">Cableado UTP</span>
        <span class="chip green">Mantenimiento de PC Escritorio</span>
        <span class="chip green">Instalación SO</span>
        <span class="chip">Licencias Windows</span>
        <span class="chip">Desarrollo de Base de Datos</span>
        <span class="chip">Marketing digital</span>
      </div>

      <button onclick="goTo('contacto')" style="width:100%;background:var(--ta-blue);color:white;border:none;border-radius:var(--border-radius-md);padding:12px;font-size:14px;font-weight:500;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;">
        <i class="ti ti-phone" aria-hidden="true"></i> Contáctanos ahora
      </button>
    </div>
    <nav class="bottom-nav">
      <button class="nav-item" onclick="goTo('home')"><i class="ti ti-home"></i><span>Inicio</span></button>
      <button class="nav-item" onclick="goTo('servicios')"><i class="ti ti-tool"></i><span>Servicios</span></button>
      <button class="nav-item" onclick="goTo('productos')"><i class="ti ti-package"></i><span>Productos</span></button>
      <button class="nav-item" onclick="goTo('contacto')"><i class="ti ti-phone"></i><span>Contacto</span></button>
    </nav>
  </div>

</div>

<script>
function goTo(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  const target = document.getElementById('screen-' + id);
  if (target) target.classList.add('active');
}
function openLink(url) {
  window.open(url, '_blank');
}
</script>
