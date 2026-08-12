document.addEventListener('DOMContentLoaded', function () {

  /* ── 1. Navbar scroll ── */
  const navbar = document.getElementById('navbar');
  /* ── THEME TOGGLE ── */
  const themeToggle = document.getElementById('themeToggle');
  const body        = document.body;

  // Charger le thème sauvegardé (dark par défaut)
  if (localStorage.getItem('theme') === 'light') {
    body.classList.add('light');
  }

  if (themeToggle) {
    themeToggle.addEventListener('click', function () {
      body.classList.toggle('light');

      // Sauvegarder le choix de l'utilisateur
      if (body.classList.contains('light')) {
        localStorage.setItem('theme', 'light');
      } else {
        localStorage.setItem('theme', 'dark');
      }
    });
  }
  window.addEventListener('scroll', function () {
    navbar.classList.toggle('scrolled', window.scrollY > 40);
  });

  /* ── 2. Menu burger mobile ── */
  const burger   = document.getElementById('burger');
  const navLinks = document.getElementById('navLinks');
  if (burger && navLinks) {
    burger.addEventListener('click', function () {
      navLinks.classList.toggle('open');
    });
    navLinks.querySelectorAll('a').forEach(function (link) {
      link.addEventListener('click', function () {
        navLinks.classList.remove('open');
      });
    });
  }

  /* ── 3. Fade-in au scroll ── */
  const fadeObs = new IntersectionObserver(function (entries) {
    entries.forEach(function (entry, i) {
      if (entry.isIntersecting) {
        setTimeout(function () {
          entry.target.classList.add('visible');
        }, i * 80);
        fadeObs.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.fade-in').forEach(function (el) { fadeObs.observe(el); });

  /* ── 4. Barres de compétences ── */
  const skillsGrid = document.getElementById('skillsGrid');
  if (skillsGrid) {
    const skillObs = new IntersectionObserver(function (entries) {
      entries.forEach(function (entry) {
        if (entry.isIntersecting) {
          entry.target.querySelectorAll('.skill-fill').forEach(function (bar) {
            bar.style.width = bar.getAttribute('data-w') + '%';
          });
          skillObs.unobserve(entry.target);
        }
      });
    }, { threshold: 0.2 });
    skillObs.observe(skillsGrid);
  }

  /* ── 5. Compteurs animés (stats hero) ── */
  function animerCompteur(el, cible, duree) {
    var debut = 0;
    var increment = cible / (duree / 16);
    var timer = setInterval(function () {
      debut += increment;
      if (debut >= cible) {
        debut = cible;
        clearInterval(timer);
      }
      el.textContent = Math.floor(debut);
    }, 16);
  }

  var statsObserver = new IntersectionObserver(function (entries) {
    entries.forEach(function (entry) {
      if (entry.isIntersecting) {
        var el = entry.target;
        var cible = parseInt(el.getAttribute('data-target'));
        animerCompteur(el, cible, 1500);
        statsObserver.unobserve(el);
      }
    });
  }, { threshold: 0.5 });

  document.querySelectorAll('.stat-value').forEach(function (el) {
    statsObserver.observe(el);
  });

  /* ── 6. Smooth scroll ── */
  document.querySelectorAll('a[href^="#"]').forEach(function (anchor) {
    anchor.addEventListener('click', function (e) {
      var cible = document.querySelector(this.getAttribute('href'));
      if (cible) {
        e.preventDefault();
        var top = cible.getBoundingClientRect().top + window.scrollY - 80;
        window.scrollTo({ top: top, behavior: 'smooth' });
      }
    });
  });

  /* ── 7. Masquer alerte succès après 5s ── */
  var alerte = document.querySelector('.alert-success');
  if (alerte) {
    setTimeout(function () {
      alerte.style.transition = 'opacity .5s';
      alerte.style.opacity = '0';
      setTimeout(function () { alerte.remove(); }, 500);
    }, 5000);
  }

  function ouvrirModal(id) {
  var modal = document.getElementById(id);
  if (!modal) return;
  modal.classList.add('open');
  document.body.classList.add('modal-open');
}

function fermerModal(id) {
  var modal = document.getElementById(id);
  if (!modal) return;
  modal.classList.remove('open');
  document.body.classList.remove('modal-open');
}

// Fermer si on clique sur le fond sombre (pas sur la modal elle-même)
function fermerModalSiDehors(event, id) {
  if (event.target.id === id) {
    fermerModal(id);
  }
}

// Fermer avec la touche Échap
document.addEventListener('keydown', function (e) {
  if (e.key === 'Escape') {
    document.querySelectorAll('.modal-overlay.open').forEach(function (modal) {
      modal.classList.remove('open');
    });
    document.body.classList.remove('modal-open');
  }
});

/* ── Slider modal projets ── */
function slidePhoto(sliderId, direction) {
  var slider = document.getElementById(sliderId);
  if (!slider) return;

  var slides  = Array.from(slider.querySelectorAll('.screenshot-slide'));
  var actif   = slider.querySelector('.screenshot-slide.active');
  var index   = slides.indexOf(actif);
  var nouveau = ((index + direction) + slides.length) % slides.length;

  allerSlide(sliderId, sliderId.replace('slider-', 'dots-'), nouveau);
}

function allerSlide(sliderId, dotsId, index) {
  var slider = document.getElementById(sliderId);
  var dots   = document.getElementById(dotsId);
  if (!slider) return;

  var slides = Array.from(slider.querySelectorAll('.screenshot-slide'));

  // Désactiver tous
  slides.forEach(function(s) { s.classList.remove('active'); });

  // Activer le bon
  if (slides[index]) {
    slides[index].classList.add('active');
    // Scroll en haut du slider
    slider.scrollTop = 0;
  }

  // Mettre à jour les dots
  if (dots) {
    Array.from(dots.querySelectorAll('.dot')).forEach(function(d, i) {
      d.classList.toggle('active', i === index);
    });
  }
}

/* ── Onglets modal ── */
function switchTab(event, tabId, modalId) {
  var modal = document.getElementById(modalId);

  // Désactiver tous les onglets et contenus
  modal.querySelectorAll('.modal-tab').forEach(function (t) {
    t.classList.remove('active');
  });
  modal.querySelectorAll('.tab-content').forEach(function (c) {
    c.classList.remove('active');
  });

  // Activer l'onglet cliqué
  event.currentTarget.classList.add('active');

  var tabContent = document.getElementById(tabId);
  if (tabContent) tabContent.classList.add('active');
}

/* ── Copier identifiants de démo ── */
function copierTexte(el) {
  navigator.clipboard.writeText(el.textContent.trim()).then(function () {
    el.classList.add('copied');
    setTimeout(function () { el.classList.remove('copied'); }, 2000);
  });
}


/* ── Pré-remplir le sujet du formulaire de contact ── */
function remplirSujetContact(sujet) {
  setTimeout(function () {
    var champSujet = document.getElementById('sujet');
    if (champSujet) {
      champSujet.value = sujet;
      champSujet.focus();
      champSujet.scrollIntoView({ behavior: 'smooth', block: 'center' });
    }
  }, 400);
}

/* ── Switcher d'onglet sans événement click (depuis bouton action) ── */
function switchTabById(tabId, modalId) {
  var modal = document.getElementById(modalId);
  if (!modal) return;

  modal.querySelectorAll('.modal-tab').forEach(function (t) {
    t.classList.remove('active');
  });
  modal.querySelectorAll('.tab-content').forEach(function (c) {
    c.classList.remove('active');
  });

  var tabContent = document.getElementById(tabId);
  if (tabContent) {
    tabContent.classList.add('active');
    // Activer l'onglet correspondant
    var index = tabId.split('-').pop();
    var tabs = modal.querySelectorAll('.modal-tab');
    tabs.forEach(function (t) {
      if (t.getAttribute('onclick') && t.getAttribute('onclick').includes(tabId)) {
        t.classList.add('active');
      }
    });
  }
}
});