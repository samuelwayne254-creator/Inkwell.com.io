<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Inkwell — Where Stories Find Their Readers</title>
<link href="https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Jost:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --ink:#0e0c0a;--parchment:#faf7f2;--cream:#f3ede3;--warm:#e8ddd0;
  --gold:#c9973a;--gold-light:#e8b84b;--rust:#8b3a2a;--sage:#4a6741;
  --text:#1a1714;--muted:#7a6e64;--border:#ddd5c8;
  --radius:4px;--radius-lg:8px;
}
html{scroll-behavior:smooth}
body{font-family:'Jost',sans-serif;background:var(--parchment);color:var(--text);overflow-x:hidden}
::-webkit-scrollbar{width:4px}::-webkit-scrollbar-track{background:var(--cream)}::-webkit-scrollbar-thumb{background:var(--gold);border-radius:2px}

/* ── NOISE TEXTURE ── */
body::before{content:'';position:fixed;inset:0;background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");pointer-events:none;z-index:1000;opacity:.4}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:100;padding:0 5%;display:flex;align-items:center;justify-content:space-between;height:70px;background:rgba(250,247,242,.92);backdrop-filter:blur(12px);border-bottom:1px solid var(--border)}
.nav-logo{font-family:'Libre Baskerville',serif;font-size:22px;letter-spacing:-.5px;color:var(--ink)}
.nav-logo span{color:var(--gold)}
.nav-links{display:flex;align-items:center;gap:32px}
.nav-links a{font-size:13px;font-weight:500;letter-spacing:1.5px;text-transform:uppercase;color:var(--muted);text-decoration:none;transition:color .2s}
.nav-links a:hover{color:var(--ink)}
.nav-cta{padding:9px 22px;background:var(--ink);color:var(--parchment);font-size:12px;font-weight:600;letter-spacing:1.5px;text-transform:uppercase;border:none;cursor:pointer;transition:background .2s;font-family:'Jost',sans-serif}
.nav-cta:hover{background:var(--gold)}
.hamburger{display:none;background:none;border:none;font-size:22px;cursor:pointer;color:var(--ink)}

/* ── HERO ── */
.hero{min-height:100vh;display:grid;grid-template-columns:1fr 1fr;position:relative;overflow:hidden}
.hero-left{padding:140px 5% 80px;display:flex;flex-direction:column;justify-content:center;position:relative}
.hero-overline{font-size:11px;letter-spacing:4px;text-transform:uppercase;color:var(--gold);margin-bottom:24px;display:flex;align-items:center;gap:12px}
.hero-overline::before{content:'';width:40px;height:1px;background:var(--gold)}
.hero-h1{font-family:'Libre Baskerville',serif;font-size:clamp(42px,5vw,72px);font-weight:700;line-height:1.05;letter-spacing:-1px;margin-bottom:28px;color:var(--ink)}
.hero-h1 em{font-style:italic;color:var(--gold)}
.hero-p{font-size:17px;line-height:1.75;color:var(--muted);max-width:480px;margin-bottom:44px;font-weight:300}
.hero-actions{display:flex;gap:16px;flex-wrap:wrap}
.btn-primary{padding:14px 32px;background:var(--ink);color:var(--parchment);font-family:'Jost';font-size:13px;font-weight:600;letter-spacing:1.5px;text-transform:uppercase;border:none;cursor:pointer;transition:all .25s;position:relative;overflow:hidden}
.btn-primary::after{content:'';position:absolute;inset:0;background:var(--gold);transform:translateX(-100%);transition:transform .3s}
.btn-primary:hover::after{transform:translateX(0)}
.btn-primary span{position:relative;z-index:1}
.btn-outline{padding:14px 32px;background:transparent;color:var(--ink);font-family:'Jost';font-size:13px;font-weight:600;letter-spacing:1.5px;text-transform:uppercase;border:1.5px solid var(--ink);cursor:pointer;transition:all .25s}
.btn-outline:hover{background:var(--ink);color:var(--parchment)}
.hero-stats{display:flex;gap:40px;margin-top:60px;padding-top:40px;border-top:1px solid var(--border)}
.hero-stat-num{font-family:'Libre Baskerville',serif;font-size:32px;font-weight:700;color:var(--ink)}
.hero-stat-lbl{font-size:12px;letter-spacing:1px;color:var(--muted);text-transform:uppercase;margin-top:4px}

.hero-right{background:var(--cream);position:relative;overflow:hidden}
.hero-book-stack{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;padding:40px}
.featured-book{width:220px;height:320px;position:relative;box-shadow:16px 16px 48px rgba(14,12,10,.25);transform:rotate(-3deg);transition:transform .4s;cursor:pointer}
.featured-book:hover{transform:rotate(0deg) scale(1.02)}
.featured-book img{width:100%;height:100%;object-fit:cover;display:block}
.book-spine{position:absolute;left:0;top:0;bottom:0;width:24px;background:linear-gradient(90deg,rgba(0,0,0,.4),rgba(0,0,0,.1));display:flex;align-items:center;justify-content:center}
.book-badge{position:absolute;top:-12px;right:-12px;width:56px;height:56px;border-radius:50%;background:var(--gold);display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;letter-spacing:.5px;text-transform:uppercase;color:var(--ink);text-align:center;line-height:1.2}
.floating-card{position:absolute;background:white;border-radius:var(--radius-lg);padding:14px 18px;box-shadow:0 8px 32px rgba(14,12,10,.12);font-size:13px;animation:float 4s ease-in-out infinite}
.fc-1{bottom:25%;left:8%;animation-delay:0s}
.fc-2{top:20%;right:8%;animation-delay:2s}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-8px)}}
.fc-author{font-weight:600;font-size:12px;color:var(--ink);margin-bottom:2px}
.fc-detail{color:var(--muted);font-size:11px}
.fc-stars{color:var(--gold);font-size:13px;margin-top:4px}

/* ── MARQUEE ── */
.marquee-wrap{background:var(--ink);padding:16px 0;overflow:hidden;position:relative}
.marquee-track{display:flex;gap:0;animation:marquee 30s linear infinite;white-space:nowrap}
.marquee-item{font-size:11px;letter-spacing:3px;text-transform:uppercase;color:var(--gold);padding:0 32px;opacity:.7}
.marquee-item.sep{color:rgba(201,151,58,.3);padding:0 8px}
@keyframes marquee{from{transform:translateX(0)}to{transform:translateX(-50%)}}

/* ── SECTIONS SHARED ── */
section{padding:100px 5%}
.section-label{font-size:11px;letter-spacing:4px;text-transform:uppercase;color:var(--gold);display:flex;align-items:center;gap:12px;margin-bottom:20px}
.section-label::before{content:'';width:30px;height:1px;background:var(--gold)}
.section-h2{font-family:'Libre Baskerville',serif;font-size:clamp(32px,4vw,52px);font-weight:700;line-height:1.1;letter-spacing:-1px;color:var(--ink);margin-bottom:16px}
.section-h2 em{font-style:italic;color:var(--gold)}
.section-sub{font-size:16px;line-height:1.7;color:var(--muted);max-width:560px;font-weight:300}

/* ── HOW IT WORKS ── */
.how{background:var(--cream)}
.steps-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin-top:64px;background:var(--border)}
.step{background:var(--cream);padding:48px 40px;position:relative;transition:background .25s}
.step:hover{background:white}
.step-num{font-family:'Libre Baskerville',serif;font-size:80px;font-weight:700;color:var(--warm);line-height:1;margin-bottom:20px;transition:color .25s}
.step:hover .step-num{color:var(--gold)}
.step-title{font-size:19px;font-weight:600;margin-bottom:12px;color:var(--ink)}
.step-body{font-size:14px;line-height:1.7;color:var(--muted)}

/* ── FEATURED WORKS ── */
.works-header{display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:48px;flex-wrap:wrap;gap:20px}
.view-all{font-size:13px;font-weight:600;letter-spacing:1px;color:var(--ink);text-decoration:none;text-transform:uppercase;border-bottom:1px solid var(--ink);padding-bottom:2px;transition:color .2s,border-color .2s}
.view-all:hover{color:var(--gold);border-color:var(--gold)}
.books-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:32px}
.book-card{cursor:pointer;group:true}
.book-cover{width:100%;aspect-ratio:2/3;overflow:hidden;margin-bottom:16px;position:relative;box-shadow:4px 4px 24px rgba(14,12,10,.12);transition:box-shadow .3s}
.book-card:hover .book-cover{box-shadow:8px 12px 36px rgba(14,12,10,.2)}
.book-cover img{width:100%;height:100%;object-fit:cover;transition:transform .5s}
.book-card:hover .book-cover img{transform:scale(1.04)}
.book-genre{font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--gold);margin-bottom:6px}
.book-title{font-family:'Libre Baskerville',serif;font-size:17px;font-weight:700;line-height:1.3;margin-bottom:6px;color:var(--ink)}
.book-author{font-size:13px;color:var(--muted);margin-bottom:8px}
.book-meta{display:flex;align-items:center;gap:12px;font-size:12px;color:var(--muted)}
.book-rating{color:var(--gold)}
.book-overlay{position:absolute;inset:0;background:linear-gradient(to top,rgba(14,12,10,.8) 0%,transparent 50%);opacity:0;transition:opacity .3s;display:flex;align-items:flex-end;padding:16px}
.book-card:hover .book-overlay{opacity:1}
.book-overlay-btn{width:100%;padding:10px;background:var(--gold);color:var(--ink);font-family:'Jost';font-size:11px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;border:none;cursor:pointer}

/* ── GENRES ── */
.genres{background:var(--ink)}
.genres .section-label{color:var(--gold)}
.genres .section-h2{color:var(--parchment)}
.genres .section-h2 em{color:var(--gold)}
.genres-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:2px;margin-top:56px}
.genre-tile{background:rgba(255,255,255,.04);padding:36px 24px;text-align:center;cursor:pointer;transition:background .2s;border:1px solid rgba(255,255,255,.06)}
.genre-tile:hover{background:var(--gold)}
.genre-icon{font-size:32px;margin-bottom:12px}
.genre-name{font-size:13px;font-weight:600;letter-spacing:.5px;color:rgba(250,247,242,.8);transition:color .2s}
.genre-count{font-size:11px;color:rgba(250,247,242,.4);margin-top:4px;transition:color .2s}
.genre-tile:hover .genre-name{color:var(--ink)}
.genre-tile:hover .genre-count{color:rgba(14,12,10,.6)}

/* ── AUTHOR SPOTLIGHT ── */
.spotlight{background:var(--cream)}
.spotlight-grid{display:grid;grid-template-columns:1fr 1fr;gap:64px;align-items:center;margin-top:56px}
.spotlight-img-wrap{position:relative}
.spotlight-img{width:100%;aspect-ratio:4/5;object-fit:cover;display:block}
.spotlight-quote-card{position:absolute;bottom:-24px;right:-24px;background:var(--ink);color:var(--parchment);padding:28px 32px;max-width:280px}
.spotlight-quote-text{font-family:'Libre Baskerville',serif;font-size:15px;font-style:italic;line-height:1.6;margin-bottom:12px}
.spotlight-quote-attr{font-size:11px;letter-spacing:1.5px;text-transform:uppercase;color:var(--gold)}
.spotlight-content{}
.spotlight-badge{display:inline-flex;align-items:center;gap:8px;background:rgba(201,151,58,.1);border:1px solid rgba(201,151,58,.2);padding:6px 14px;margin-bottom:24px;font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--gold)}
.spotlight-author-name{font-family:'Libre Baskerville',serif;font-size:36px;font-weight:700;line-height:1.1;margin-bottom:8px;color:var(--ink)}
.spotlight-genre{font-size:13px;color:var(--gold);letter-spacing:1px;margin-bottom:20px;text-transform:uppercase}
.spotlight-bio{font-size:15px;line-height:1.8;color:var(--muted);margin-bottom:32px;font-weight:300}
.spotlight-works{display:flex;gap:16px;margin-bottom:36px;flex-wrap:wrap}
.spotlight-work{padding:10px 16px;border:1px solid var(--border);font-size:13px;cursor:pointer;transition:all .2s;background:white}
.spotlight-work:hover{border-color:var(--gold);color:var(--gold)}
.spotlight-stats{display:flex;gap:32px}
.ss-num{font-family:'Libre Baskerville',serif;font-size:28px;font-weight:700;color:var(--ink)}
.ss-lbl{font-size:11px;letter-spacing:1px;color:var(--muted);text-transform:uppercase;margin-top:2px}

/* ── TESTIMONIALS ── */
.testimonials{background:var(--parchment)}
.testi-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin-top:56px;background:var(--border)}
.testi-card{background:var(--parchment);padding:40px 36px;transition:background .25s}
.testi-card:hover{background:white}
.testi-quote{font-family:'Libre Baskerville',serif;font-size:15px;font-style:italic;line-height:1.8;color:var(--text);margin-bottom:24px;position:relative}
.testi-quote::before{content:'\201C';font-size:64px;color:var(--gold);opacity:.3;position:absolute;top:-20px;left:-8px;font-family:'Libre Baskerville',serif;line-height:1}
.testi-author-row{display:flex;align-items:center;gap:12px}
.testi-avatar{width:44px;height:44px;border-radius:50%;object-fit:cover;border:2px solid var(--border)}
.testi-name{font-size:14px;font-weight:600;color:var(--ink)}
.testi-role{font-size:12px;color:var(--muted)}
.testi-stars{color:var(--gold);font-size:13px;margin-bottom:4px}

/* ── PRICING ── */
.pricing{background:var(--cream)}
.pricing-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin-top:56px;background:var(--border)}
.price-card{background:var(--cream);padding:48px 40px;position:relative;transition:background .2s}
.price-card.featured{background:var(--ink)}
.price-card.featured *{color:var(--parchment) !important}
.price-card.featured .price-feature{color:rgba(250,247,242,.7) !important}
.price-badge{position:absolute;top:24px;right:24px;background:var(--gold);color:var(--ink);font-size:10px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;padding:4px 12px}
.price-tier{font-size:11px;letter-spacing:3px;text-transform:uppercase;color:var(--gold);margin-bottom:16px}
.price-card.featured .price-tier{color:var(--gold) !important}
.price-amount{font-family:'Libre Baskerville',serif;font-size:52px;font-weight:700;color:var(--ink);line-height:1}
.price-amount sup{font-size:22px;vertical-align:top;margin-top:10px;margin-right:2px}
.price-period{font-size:13px;color:var(--muted);margin-bottom:8px}
.price-desc{font-size:14px;line-height:1.6;color:var(--muted);margin-bottom:32px;padding-bottom:32px;border-bottom:1px solid var(--border)}
.price-card.featured .price-desc{border-color:rgba(255,255,255,.1) !important}
.price-features{list-style:none;display:flex;flex-direction:column;gap:12px;margin-bottom:36px}
.price-feature{font-size:13px;color:var(--muted);display:flex;align-items:center;gap:10px}
.price-feature::before{content:'✓';color:var(--gold);font-weight:700;flex-shrink:0}
.price-btn{width:100%;padding:14px;font-family:'Jost';font-size:12px;font-weight:700;letter-spacing:2px;text-transform:uppercase;cursor:pointer;border:none;transition:all .25s}
.price-btn.default{background:var(--ink);color:var(--parchment)}
.price-btn.default:hover{background:var(--gold)}
.price-btn.white{background:var(--parchment);color:var(--ink)}
.price-btn.white:hover{background:var(--gold)}

/* ── NEWSLETTER ── */
.newsletter{background:var(--ink);text-align:center;padding:100px 5%}
.newsletter .section-label{justify-content:center}
.newsletter .section-label::before{display:none}
.newsletter .section-h2{color:var(--parchment);text-align:center;margin:0 auto 16px}
.newsletter .section-sub{text-align:center;margin:0 auto 48px;color:rgba(250,247,242,.6)}
.newsletter-form{display:flex;gap:0;max-width:480px;margin:0 auto;flex-wrap:wrap}
.newsletter-input{flex:1;min-width:240px;padding:14px 20px;background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.15);border-right:none;color:var(--parchment);font-family:'Jost';font-size:14px;outline:none}
.newsletter-input::placeholder{color:rgba(250,247,242,.4)}
.newsletter-input:focus{background:rgba(255,255,255,.12)}
.newsletter-submit{padding:14px 28px;background:var(--gold);color:var(--ink);font-family:'Jost';font-size:12px;font-weight:700;letter-spacing:2px;text-transform:uppercase;border:none;cursor:pointer;transition:background .2s}
.newsletter-submit:hover{background:var(--gold-light)}

/* ── UPLOAD / PROFILE MODAL ── */
.modal-overlay{position:fixed;inset:0;background:rgba(14,12,10,.7);display:flex;align-items:center;justify-content:center;z-index:200;opacity:0;pointer-events:none;transition:opacity .3s;backdrop-filter:blur(4px)}
.modal-overlay.open{opacity:1;pointer-events:all}
.modal{background:var(--parchment);max-width:600px;width:90%;max-height:90vh;overflow-y:auto;position:relative;animation:slideUp .3s ease}
@keyframes slideUp{from{transform:translateY(20px);opacity:0}to{transform:none;opacity:1}}
.modal-header{padding:36px 40px 24px;border-bottom:1px solid var(--border)}
.modal-title{font-family:'Libre Baskerville',serif;font-size:26px;font-weight:700;color:var(--ink);margin-bottom:6px}
.modal-sub{font-size:14px;color:var(--muted)}
.modal-close{position:absolute;top:20px;right:20px;background:none;border:none;font-size:20px;cursor:pointer;color:var(--muted);line-height:1;width:32px;height:32px;display:flex;align-items:center;justify-content:center}
.modal-close:hover{color:var(--ink)}
.modal-body{padding:32px 40px}
.form-group{margin-bottom:22px}
.form-label{display:block;font-size:11px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--ink);margin-bottom:8px}
.form-input,.form-select,.form-textarea{width:100%;padding:12px 16px;background:white;border:1.5px solid var(--border);font-family:'Jost';font-size:14px;color:var(--ink);outline:none;transition:border .2s;border-radius:var(--radius)}
.form-input:focus,.form-select:focus,.form-textarea:focus{border-color:var(--gold)}
.form-textarea{min-height:100px;resize:vertical}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.upload-area{border:2px dashed var(--border);padding:40px;text-align:center;cursor:pointer;transition:all .2s;background:var(--cream)}
.upload-area:hover{border-color:var(--gold);background:rgba(201,151,58,.04)}
.upload-icon{font-size:36px;margin-bottom:12px}
.upload-text{font-size:14px;color:var(--muted);line-height:1.6}
.upload-text strong{color:var(--ink)}
.genre-pills{display:flex;flex-wrap:wrap;gap:8px;margin-top:8px}
.genre-pill{padding:6px 14px;border:1.5px solid var(--border);background:transparent;font-family:'Jost';font-size:12px;color:var(--muted);cursor:pointer;transition:all .2s;border-radius:30px}
.genre-pill:hover,.genre-pill.sel{border-color:var(--gold);color:var(--gold);background:rgba(201,151,58,.06)}
.modal-footer{padding:24px 40px 36px;display:flex;gap:12px}
.toast{position:fixed;bottom:30px;left:50%;transform:translateX(-50%) translateY(20px);background:var(--ink);color:var(--parchment);padding:14px 28px;font-size:14px;opacity:0;transition:all .3s;z-index:300;font-weight:500}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

/* ── FOOTER ── */
footer{background:var(--ink);color:var(--parchment);padding:80px 5% 40px}
.footer-grid{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:48px;margin-bottom:60px}
.footer-brand{font-family:'Libre Baskerville',serif;font-size:24px;margin-bottom:16px}
.footer-brand span{color:var(--gold)}
.footer-tagline{font-size:14px;line-height:1.7;color:rgba(250,247,242,.5);max-width:260px}
.footer-col-title{font-size:11px;letter-spacing:2.5px;text-transform:uppercase;color:var(--gold);margin-bottom:20px}
.footer-links{list-style:none;display:flex;flex-direction:column;gap:10px}
.footer-links a{font-size:14px;color:rgba(250,247,242,.6);text-decoration:none;transition:color .2s}
.footer-links a:hover{color:var(--gold)}
.footer-bottom{border-top:1px solid rgba(255,255,255,.08);padding-top:32px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:16px}
.footer-copy{font-size:12px;color:rgba(250,247,242,.4)}
.footer-socials{display:flex;gap:16px}
.social-link{width:36px;height:36px;border:1px solid rgba(255,255,255,.1);display:flex;align-items:center;justify-content:center;font-size:14px;text-decoration:none;transition:all .2s}
.social-link:hover{border-color:var(--gold);background:rgba(201,151,58,.1)}

/* ── SEARCH BAR ── */
.search-section{background:white;border-bottom:1px solid var(--border);padding:20px 5%}
.search-wrap{display:flex;gap:0;max-width:700px;margin:0 auto}
.search-input{flex:1;padding:13px 20px;border:1.5px solid var(--border);border-right:none;font-family:'Jost';font-size:14px;color:var(--ink);outline:none;background:var(--parchment)}
.search-input:focus{border-color:var(--gold)}
.search-select{padding:13px 16px;border:1.5px solid var(--border);border-right:none;font-family:'Jost';font-size:13px;color:var(--muted);outline:none;background:var(--cream);cursor:pointer}
.search-btn{padding:13px 28px;background:var(--ink);color:var(--parchment);font-family:'Jost';font-size:12px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;border:none;cursor:pointer;transition:background .2s}
.search-btn:hover{background:var(--gold)}

/* ── ANIMATIONS ── */
.fade-in{opacity:0;transform:translateY(24px);transition:opacity .7s,transform .7s}
.fade-in.visible{opacity:1;transform:none}

/* ── RESPONSIVE ── */
@media(max-width:1024px){
  .books-grid{grid-template-columns:repeat(2,1fr)}
  .genres-grid{grid-template-columns:repeat(3,1fr)}
  .footer-grid{grid-template-columns:1fr 1fr;gap:32px}
  .spotlight-quote-card{position:relative;right:auto;bottom:auto;margin-top:20px;max-width:100%}
}
@media(max-width:768px){
  .hero{grid-template-columns:1fr}
  .hero-right{height:400px}
  .hero-left{padding:120px 5% 60px}
  .steps-grid,.testi-grid,.pricing-grid{grid-template-columns:1fr}
  .steps-grid,.testi-grid,.pricing-grid{background:transparent;gap:2px}
  .genres-grid{grid-template-columns:repeat(2,1fr)}
  .spotlight-grid{grid-template-columns:1fr}
  .nav-links{display:none}
  .hamburger{display:block}
  .books-grid{grid-template-columns:repeat(2,1fr)}
  .newsletter-form{flex-direction:column}
  .newsletter-input{border-right:1px solid rgba(255,255,255,.15);border-bottom:none}
  .footer-grid{grid-template-columns:1fr}
}
@media(max-width:480px){
  .books-grid{grid-template-columns:1fr}
  .hero-stats{flex-wrap:wrap;gap:24px}
}
</style>
</head>
<body>

<!-- NAV -->
<nav id="nav">
  <div class="nav-logo">Ink<span>well</span></div>
  <div class="nav-links">
    <a href="#works">Browse</a>
    <a href="#how">How It Works</a>
    <a href="#authors">Authors</a>
    <a href="#pricing">Pricing</a>
  </div>
  <div style="display:flex;gap:12px;align-items:center">
    <button class="btn-outline" style="padding:9px 22px;font-size:12px" onclick="openModal('signin')">Sign In</button>
    <button class="nav-cta" onclick="openModal('publish')">Publish Now</button>
  </div>
  <button class="hamburger" id="hamburger">☰</button>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-left fade-in">
    <div class="hero-overline">The Author's Platform</div>
    <h1 class="hero-h1">Where Every Story<br>Finds Its <em>Perfect</em><br>Reader</h1>
    <p class="hero-p">Inkwell connects talented authors with passionate readers worldwide. Publish your work, build your audience, and earn from your craft — all in one elegant space.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="openModal('publish')"><span>Start Publishing →</span></button>
      <button class="btn-outline" onclick="document.getElementById('works').scrollIntoView({behavior:'smooth'})">Browse Books</button>
    </div>
    <div class="hero-stats">
      <div><div class="hero-stat-num" id="cnt-authors">0</div><div class="hero-stat-lbl">Authors</div></div>
      <div><div class="hero-stat-num" id="cnt-books">0</div><div class="hero-stat-lbl">Works Published</div></div>
      <div><div class="hero-stat-num" id="cnt-readers">0</div><div class="hero-stat-lbl">Active Readers</div></div>
    </div>
  </div>
  <div class="hero-right">
    <div class="hero-book-stack">
      <div class="featured-book" onclick="openModal('preview')">
        <img src="https://images.unsplash.com/photo-1544947950-fa07a98d237f?w=400&q=80" alt="Featured Book">
        <div class="book-spine"></div>
        <div class="book-badge">New<br>Release</div>
      </div>
    </div>
    <div class="floating-card fc-1">
      <div class="fc-author">📚 Amara Osei</div>
      <div class="fc-detail">The Quiet Storm · Literary Fiction</div>
      <div class="fc-stars">★★★★★ <span style="color:var(--muted);font-size:11px">4.9</span></div>
    </div>
    <div class="floating-card fc-2">
      <div class="fc-author">✍️ Just Published</div>
      <div class="fc-detail">12 new works this week</div>
      <div style="font-size:12px;color:var(--sage);margin-top:4px;font-weight:600">↑ Growing community</div>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item">Literary Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Poetry Collections</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Mystery & Thriller</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Science Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Historical Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Romance</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Non-Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Self-Help</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Fantasy & Magic</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Short Stories</span><span class="marquee-item sep">◆</span>
    <!-- duplicate for seamless loop -->
    <span class="marquee-item">Literary Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Poetry Collections</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Mystery & Thriller</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Science Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Historical Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Romance</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Non-Fiction</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Self-Help</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Fantasy & Magic</span><span class="marquee-item sep">◆</span>
    <span class="marquee-item">Short Stories</span><span class="marquee-item sep">◆</span>
  </div>
</div>

<!-- SEARCH -->
<div class="search-section">
  <div class="search-wrap">
    <select class="search-select" id="searchGenre">
      <option>All Genres</option>
      <option>Fiction</option>
      <option>Non-Fiction</option>
      <option>Poetry</option>
      <option>Mystery</option>
      <option>Romance</option>
      <option>Sci-Fi</option>
      <option>Fantasy</option>
    </select>
    <input class="search-input" id="searchInput" placeholder="Search books, authors, or topics…" type="text">
    <button class="search-btn" onclick="handleSearch()">Search</button>
  </div>
</div>

<!-- HOW IT WORKS -->
<section class="how" id="how">
  <div class="section-label">Getting Started</div>
  <h2 class="section-h2">Simple steps to share<br>your <em>voice</em> with the world</h2>
  <div class="steps-grid fade-in">
    <div class="step">
      <div class="step-num">01</div>
      <div class="step-title">Create Your Profile</div>
      <div class="step-body">Build a beautiful author page that showcases your biography, writing style, and published works. Your profile is your literary identity — make it unforgettable.</div>
    </div>
    <div class="step">
      <div class="step-num">02</div>
      <div class="step-title">Upload Your Work</div>
      <div class="step-body">Upload manuscripts, poetry, short stories, or full novels in any format. Our intelligent system formats your work beautifully for every device and screen.</div>
    </div>
    <div class="step">
      <div class="step-num">03</div>
      <div class="step-title">Reach Your Readers</div>
      <div class="step-body">Our algorithm connects your work with readers who love your genre. Get discovered through curated lists, featured spots, and our growing reader community.</div>
    </div>
  </div>
</section>

<!-- FEATURED WORKS -->
<section id="works" style="background:var(--parchment)">
  <div class="works-header">
    <div>
      <div class="section-label">Curated Selection</div>
      <h2 class="section-h2">Featured <em>Works</em></h2>
    </div>
    <a class="view-all" href="#">View All 2,400+ Books</a>
  </div>
  <div class="books-grid fade-in" id="booksGrid"></div>
</section>

<!-- GENRES -->
<section class="genres" id="genres">
  <div class="section-label" style="color:var(--gold)">Explore by Genre</div>
  <h2 class="section-h2" style="color:var(--parchment)">Find stories that <em>move</em> you</h2>
  <div class="genres-grid fade-in" id="genresGrid"></div>
</section>

<!-- AUTHOR SPOTLIGHT -->
<section class="spotlight" id="authors">
  <div class="section-label">Author Spotlight</div>
  <h2 class="section-h2">Meet the voices<br>shaping <em>tomorrow's</em> literature</h2>
  <div class="spotlight-grid fade-in">
    <div class="spotlight-img-wrap">
      <img class="spotlight-img" src="https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?w=600&q=80" alt="Featured Author">
      <div class="spotlight-quote-card">
        <div class="spotlight-quote-text">"Writing is not just my passion — it is how I make sense of the world and share that understanding with others."</div>
        <div class="spotlight-quote-attr">— Amara Osei, Author</div>
      </div>
    </div>
    <div class="spotlight-content">
      <div class="spotlight-badge">✦ Author of the Month</div>
      <div class="spotlight-author-name">Amara Osei</div>
      <div class="spotlight-genre">Literary Fiction · African Contemporary</div>
      <div class="spotlight-bio">Amara Osei is a celebrated Ghanaian-British author whose lyrical prose has captivated readers across three continents. Her debut novel won the Commonwealth Writers Prize, and her work has been translated into fourteen languages. She writes stories that illuminate the human experience with unflinching tenderness.</div>
      <div class="spotlight-works">
        <div class="spotlight-work">The Quiet Storm</div>
        <div class="spotlight-work">Between Two Skies</div>
        <div class="spotlight-work">Letters to Accra</div>
      </div>
      <div class="spotlight-stats">
        <div><div class="ss-num">24K</div><div class="ss-lbl">Readers</div></div>
        <div><div class="ss-num">3</div><div class="ss-lbl">Published Works</div></div>
        <div><div class="ss-num">4.9</div><div class="ss-lbl">Avg Rating</div></div>
      </div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials">
  <div style="text-align:center;margin-bottom:16px">
    <div class="section-label" style="justify-content:center"><span style="width:30px;height:1px;background:var(--gold);display:block"></span>What Authors Say</div>
    <h2 class="section-h2" style="text-align:center">Voices from our <em>community</em></h2>
  </div>
  <div class="testi-grid fade-in">
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <div class="testi-quote">Inkwell gave my self-published novel the audience it deserved. Within three months I had more readers than I'd dreamed possible, and the royalty system is genuinely fair and transparent.</div>
      <div class="testi-author-row">
        <img class="testi-avatar" src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100&q=80" alt="James">
        <div><div class="testi-name">James Mwangi</div><div class="testi-role">Thriller Author · Nairobi</div></div>
      </div>
    </div>
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <div class="testi-quote">As a poet, I always struggled to find my audience. Inkwell's genre community feature connected me with poetry lovers who truly appreciate my work. I've never felt more seen as a writer.</div>
      <div class="testi-author-row">
        <img class="testi-avatar" src="https://images.unsplash.com/photo-1494790108755-2616b612b786?w=100&q=80" alt="Priya">
        <div><div class="testi-name">Priya Sharma</div><div class="testi-role">Poet · Mumbai</div></div>
      </div>
    </div>
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <div class="testi-quote">The analytics dashboard showed me exactly which chapters readers loved and where they stopped — invaluable feedback that made my second book significantly better than my first.</div>
      <div class="testi-author-row">
        <img class="testi-avatar" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=100&q=80" alt="Carlos">
        <div><div class="testi-name">Carlos Mendoza</div><div class="testi-role">Sci-Fi Author · Buenos Aires</div></div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section class="pricing" id="pricing">
  <div style="text-align:center">
    <div class="section-label" style="justify-content:center"><span style="width:30px;height:1px;background:var(--gold);display:inline-block;margin-right:12px"></span>Simple, Fair Pricing</div>
    <h2 class="section-h2" style="text-align:center">Invest in your <em>writing</em></h2>
    <div class="section-sub" style="text-align:center;margin:0 auto">Every plan includes a 30-day free trial. No credit card required.</div>
  </div>
  <div class="pricing-grid">
    <div class="price-card">
      <div class="price-tier">Starter</div>
      <div class="price-amount"><sup>$</sup>0</div>
      <div class="price-period">Forever free</div>
      <div class="price-desc">Perfect for writers just beginning their publishing journey.</div>
      <ul class="price-features">
        <li class="price-feature">Up to 3 published works</li>
        <li class="price-feature">Basic author profile</li>
        <li class="price-feature">Community access</li>
        <li class="price-feature">70% royalty rate</li>
        <li class="price-feature">Reader reviews & ratings</li>
      </ul>
      <button class="price-btn default" onclick="openModal('publish')">Get Started Free</button>
    </div>
    <div class="price-card featured">
      <div class="price-badge">Most Popular</div>
      <div class="price-tier">Author Pro</div>
      <div class="price-amount"><sup>$</sup>12</div>
      <div class="price-period">per month, billed annually</div>
      <div class="price-desc">For serious authors ready to build a sustainable writing career.</div>
      <ul class="price-features">
        <li class="price-feature">Unlimited published works</li>
        <li class="price-feature">Premium author profile</li>
        <li class="price-feature">Advanced analytics dashboard</li>
        <li class="price-feature">85% royalty rate</li>
        <li class="price-feature">Featured placement algorithm</li>
        <li class="price-feature">Newsletter to your followers</li>
      </ul>
      <button class="price-btn white" onclick="openModal('publish')">Start Free Trial</button>
    </div>
    <div class="price-card">
      <div class="price-tier">Publisher</div>
      <div class="price-amount"><sup>$</sup>49</div>
      <div class="price-period">per month, billed annually</div>
      <div class="price-desc">For publishing houses and prolific authors managing multiple titles.</div>
      <ul class="price-features">
        <li class="price-feature">Everything in Author Pro</li>
        <li class="price-feature">Up to 10 author profiles</li>
        <li class="price-feature">Dedicated account manager</li>
        <li class="price-feature">90% royalty rate</li>
        <li class="price-feature">Priority customer support</li>
        <li class="price-feature">Custom branding options</li>
      </ul>
      <button class="price-btn default" onclick="openModal('publish')">Contact Sales</button>
    </div>
  </div>
</section>

<!-- NEWSLETTER -->
<section class="newsletter">
  <div class="section-label">Stay in the Story</div>
  <h2 class="section-h2">Never miss a great <em>read</em></h2>
  <div class="section-sub">Weekly curated recommendations, author interviews, and writing tips delivered to your inbox.</div>
  <div class="newsletter-form">
    <input class="newsletter-input" id="nlEmail" placeholder="Your email address" type="email">
    <button class="newsletter-submit" onclick="handleNewsletter()">Subscribe</button>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div>
      <div class="footer-brand">Ink<span>well</span></div>
      <div class="footer-tagline">Where stories find their readers. A platform built by writers, for writers — with love for literature.</div>
    </div>
    <div>
      <div class="footer-col-title">Platform</div>
      <ul class="footer-links">
        <li><a href="#">Browse Books</a></li>
        <li><a href="#">Featured Authors</a></li>
        <li><a href="#">New Releases</a></li>
        <li><a href="#">Genre Guides</a></li>
        <li><a href="#">Reading Lists</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Authors</div>
      <ul class="footer-links">
        <li><a href="#" onclick="openModal('publish');return false">Publish Your Work</a></li>
        <li><a href="#">Author Dashboard</a></li>
        <li><a href="#">Royalties & Payments</a></li>
        <li><a href="#">Writing Resources</a></li>
        <li><a href="#">Community Forum</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Company</div>
      <ul class="footer-links">
        <li><a href="#">About Inkwell</a></li>
        <li><a href="#">Press & Media</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Privacy Policy</a></li>
        <li><a href="#">Terms of Service</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2025 Inkwell Literary Platform. All rights reserved.</div>
    <div class="footer-socials">
      <a class="social-link" href="#" title="Twitter">𝕏</a>
      <a class="social-link" href="#" title="Instagram">◎</a>
      <a class="social-link" href="#" title="Facebook">f</a>
      <a class="social-link" href="#" title="LinkedIn">in</a>
    </div>
  </div>
</footer>

<!-- PUBLISH MODAL -->
<div class="modal-overlay" id="modal-publish">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Publish Your Work</div>
      <div class="modal-sub">Share your story with thousands of passionate readers worldwide</div>
      <button class="modal-close" onclick="closeModal('publish')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Your Name</label>
          <input class="form-input" placeholder="Full name" type="text">
        </div>
        <div class="form-group">
          <label class="form-label">Email Address</label>
          <input class="form-input" placeholder="you@example.com" type="email">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Book / Work Title</label>
        <input class="form-input" placeholder="Enter the title of your work" type="text">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Type of Work</label>
          <select class="form-select">
            <option>Novel</option>
            <option>Short Story Collection</option>
            <option>Poetry Collection</option>
            <option>Novella</option>
            <option>Non-Fiction</option>
            <option>Memoir</option>
            <option>Essay Collection</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Language</label>
          <select class="form-select">
            <option>English</option>
            <option>Spanish</option>
            <option>French</option>
            <option>Portuguese</option>
            <option>Swahili</option>
            <option>Arabic</option>
            <option>Other</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Genre</label>
        <div class="genre-pills" id="genrePills">
          <button class="genre-pill" onclick="togglePill(this)">Literary Fiction</button>
          <button class="genre-pill" onclick="togglePill(this)">Mystery</button>
          <button class="genre-pill" onclick="togglePill(this)">Romance</button>
          <button class="genre-pill" onclick="togglePill(this)">Sci-Fi</button>
          <button class="genre-pill" onclick="togglePill(this)">Fantasy</button>
          <button class="genre-pill" onclick="togglePill(this)">Thriller</button>
          <button class="genre-pill" onclick="togglePill(this)">Historical</button>
          <button class="genre-pill" onclick="togglePill(this)">Poetry</button>
          <button class="genre-pill" onclick="togglePill(this)">Self-Help</button>
          <button class="genre-pill" onclick="togglePill(this)">Biography</button>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Synopsis / Description</label>
        <textarea class="form-textarea" placeholder="Write a compelling description that will draw readers in…"></textarea>
      </div>
      <div class="form-group">
        <label class="form-label">Upload Manuscript</label>
        <div class="upload-area" onclick="showToast('File upload ready — connect your backend to enable!')">
          <div class="upload-icon">📄</div>
          <div class="upload-text"><strong>Click to upload</strong> or drag and drop<br>PDF, EPUB, DOCX, TXT up to 50MB</div>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Cover Image</label>
        <div class="upload-area" onclick="showToast('Cover upload ready — connect your backend to enable!')">
          <div class="upload-icon">🖼️</div>
          <div class="upload-text"><strong>Upload cover art</strong><br>JPG or PNG, minimum 1200×1800px</div>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Pricing</label>
        <select class="form-select">
          <option>Free to read</option>
          <option>$0.99</option>
          <option>$1.99</option>
          <option>$2.99</option>
          <option>$4.99</option>
          <option>$7.99</option>
          <option>$9.99</option>
          <option>Custom price</option>
        </select>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn-primary" style="flex:1" onclick="handlePublish()"><span>Submit for Review →</span></button>
      <button class="btn-outline" onclick="closeModal('publish')">Cancel</button>
    </div>
  </div>
</div>

<!-- SIGN IN MODAL -->
<div class="modal-overlay" id="modal-signin">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Welcome Back</div>
      <div class="modal-sub">Sign in to your Inkwell author account</div>
      <button class="modal-close" onclick="closeModal('signin')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">Email Address</label>
        <input class="form-input" placeholder="you@example.com" type="email">
      </div>
      <div class="form-group">
        <label class="form-label">Password</label>
        <input class="form-input" placeholder="Your password" type="password">
      </div>
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:24px">
        <label style="display:flex;align-items:center;gap:8px;font-size:13px;color:var(--muted);cursor:pointer">
          <input type="checkbox"> Remember me
        </label>
        <a href="#" style="font-size:13px;color:var(--gold);text-decoration:none">Forgot password?</a>
      </div>
      <div style="text-align:center;margin-bottom:20px;font-size:13px;color:var(--muted)">— or continue with —</div>
      <div style="display:flex;gap:12px;margin-bottom:8px">
        <button class="btn-outline" style="flex:1;padding:12px" onclick="showToast('OAuth coming soon!')">G  Google</button>
        <button class="btn-outline" style="flex:1;padding:12px" onclick="showToast('OAuth coming soon!')">f  Facebook</button>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn-primary" style="flex:1" onclick="handleSignin()"><span>Sign In →</span></button>
      <button class="btn-outline" onclick="closeModal('signin');openModal('publish')">Create Account</button>
    </div>
  </div>
</div>

<!-- PREVIEW MODAL -->
<div class="modal-overlay" id="modal-preview">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">The Quiet Storm</div>
      <div class="modal-sub">Amara Osei · Literary Fiction · 2024</div>
      <button class="modal-close" onclick="closeModal('preview')">✕</button>
    </div>
    <div class="modal-body">
      <div style="display:grid;grid-template-columns:140px 1fr;gap:24px;margin-bottom:28px">
        <img src="https://images.unsplash.com/photo-1544947950-fa07a98d237f?w=300&q=80" style="width:100%;aspect-ratio:2/3;object-fit:cover" alt="Book">
        <div>
          <div style="font-size:12px;letter-spacing:2px;text-transform:uppercase;color:var(--gold);margin-bottom:8px">Literary Fiction</div>
          <div style="font-family:'Libre Baskerville';font-size:22px;font-weight:700;margin-bottom:8px">The Quiet Storm</div>
          <div style="font-size:14px;color:var(--muted);margin-bottom:16px">by Amara Osei</div>
          <div style="color:var(--gold);font-size:16px;margin-bottom:8px">★★★★★ <span style="color:var(--muted);font-size:13px">4.9 (1,240 reviews)</span></div>
          <div style="font-size:22px;font-weight:700;color:var(--ink);margin-bottom:4px">$4.99</div>
          <div style="font-size:12px;color:var(--sage)">✓ Includes free sample chapter</div>
        </div>
      </div>
      <div style="font-size:15px;line-height:1.8;color:var(--muted);margin-bottom:24px;font-style:italic;padding:20px;background:var(--cream);border-left:3px solid var(--gold)">
        "In the sweltering heat of Accra, Ama discovers a box of letters that will unravel three generations of her family's secrets — and force her to confront everything she thought she knew about love, sacrifice, and what it means to belong."
      </div>
      <div style="display:flex;gap:24px;margin-bottom:20px;flex-wrap:wrap">
        <div><strong style="font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--ink)">Pages</strong><div style="color:var(--muted);font-size:14px;margin-top:4px">342</div></div>
        <div><strong style="font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--ink)">Language</strong><div style="color:var(--muted);font-size:14px;margin-top:4px">English</div></div>
        <div><strong style="font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--ink)">Published</strong><div style="color:var(--muted);font-size:14px;margin-top:4px">March 2024</div></div>
        <div><strong style="font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--ink)">Readers</strong><div style="color:var(--muted);font-size:14px;margin-top:4px">8,430</div></div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn-primary" style="flex:1" onclick="showToast('Added to your library! 📚');closeModal('preview')"><span>Purchase · $4.99</span></button>
      <button class="btn-outline" onclick="showToast('Sample chapter downloaded!');closeModal('preview')">Read Sample</button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ── BOOKS DATA ──
const BOOKS=[
  {title:"The Cartographer's Daughter",author:"Elena Vasquez",genre:"Historical Fiction",price:"$5.99",rating:"4.8",reviews:"892",cover:"https://images.unsplash.com/photo-1512820790803-83ca734da794?w=400&q=80"},
  {title:"Neon Requiem",author:"Kai Tanaka",genre:"Cyberpunk",price:"$3.99",rating:"4.7",reviews:"1,203",cover:"https://images.unsplash.com/photo-1543002588-bfa74002ed7e?w=400&q=80"},
  {title:"Salt & Ash",author:"Zara Okonkwo",genre:"Literary Fiction",price:"Free",rating:"4.9",reviews:"2,140",cover:"https://images.unsplash.com/photo-1532012197267-da84d127e765?w=400&q=80"},
  {title:"The Memory Weavers",author:"Ravi Patel",genre:"Fantasy",price:"$6.99",rating:"4.6",reviews:"741",cover:"https://images.unsplash.com/photo-1497633762265-9d179a990aa6?w=400&q=80"},
  {title:"Drift",author:"Mila Johansson",genre:"Poetry",price:"$2.99",rating:"4.8",reviews:"520",cover:"https://images.unsplash.com/photo-1481627834876-b7833e8f5570?w=400&q=80"},
  {title:"The Last Consul",author:"Diego Reyes",genre:"Thriller",price:"$4.99",rating:"4.5",reviews:"1,890",cover:"https://images.unsplash.com/photo-1589998059171-988d887df646?w=400&q=80"},
  {title:"Between Two Moons",author:"Amara Osei",genre:"Literary Fiction",price:"$3.99",rating:"4.9",reviews:"3,420",cover:"https://images.unsplash.com/photo-1516979187457-637abb4f9353?w=400&q=80"},
  {title:"Quantum Hearts",author:"Sam Lee",genre:"Sci-Fi Romance",price:"$2.99",rating:"4.4",reviews:"617",cover:"https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&q=80"},
];

const GENRES=[
  {icon:"📖",name:"Literary Fiction",count:"4,820 works"},
  {icon:"🔮",name:"Fantasy",count:"3,210 works"},
  {icon:"🚀",name:"Sci-Fi",count:"2,890 works"},
  {icon:"🕵️",name:"Mystery",count:"3,640 works"},
  {icon:"💝",name:"Romance",count:"5,120 works"},
  {icon:"📜",name:"Historical",count:"2,340 works"},
  {icon:"✍️",name:"Poetry",count:"1,980 works"},
  {icon:"💡",name:"Non-Fiction",count:"4,100 works"},
  {icon:"😱",name:"Thriller",count:"2,780 works"},
  {icon:"🌍",name:"Biography",count:"1,540 works"},
  {icon:"🧘",name:"Self-Help",count:"2,210 works"},
  {icon:"🎭",name:"Drama",count:"1,870 works"},
];

// ── RENDER BOOKS ──
function renderBooks(){
  const grid=document.getElementById('booksGrid');
  grid.innerHTML=BOOKS.map(b=>`
    <div class="book-card" onclick="openBookPreview('${b.title}')">
      <div class="book-cover">
        <img src="${b.cover}" alt="${b.title}">
        <div class="book-overlay">
          <button class="book-overlay-btn">Quick Preview</button>
        </div>
      </div>
      <div class="book-genre">${b.genre}</div>
      <div class="book-title">${b.title}</div>
      <div class="book-author">${b.author}</div>
      <div class="book-meta">
        <span class="book-rating">★ ${b.rating}</span>
        <span>(${b.reviews})</span>
        <span style="margin-left:auto;font-weight:600;color:var(--ink)">${b.price}</span>
      </div>
    </div>
  `).join('');
}

// ── RENDER GENRES ──
function renderGenres(){
  const grid=document.getElementById('genresGrid');
  grid.innerHTML=GENRES.map(g=>`
    <div class="genre-tile" onclick="filterByGenre('${g.name}')">
      <div class="genre-icon">${g.icon}</div>
      <div class="genre-name">${g.name}</div>
      <div class="genre-count">${g.count}</div>
    </div>
  `).join('');
}

// ── COUNTER ANIMATION ──
function animateCounter(el,target,suffix=''){
  let start=0;
  const step=target/60;
  const interval=setInterval(()=>{
    start+=step;
    if(start>=target){start=target;clearInterval(interval);}
    el.textContent=Math.floor(start).toLocaleString()+suffix;
  },25);
}

// ── MODAL ──
function openModal(name){
  document.getElementById('modal-'+name).classList.add('open');
  document.body.style.overflow='hidden';
}
function closeModal(name){
  document.getElementById('modal-'+name).classList.remove('open');
  document.body.style.overflow='';
}
document.querySelectorAll('.modal-overlay').forEach(o=>{
  o.addEventListener('click',e=>{if(e.target===o){const id=o.id.replace('modal-','');closeModal(id);}});
});
document.addEventListener('keydown',e=>{if(e.key==='Escape')document.querySelectorAll('.modal-overlay.open').forEach(m=>{m.classList.remove('open');document.body.style.overflow='';});});

// ── TOAST ──
function showToast(msg,dur=3000){
  const t=document.getElementById('toast');
  t.textContent=msg;t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),dur);
}

// ── ACTIONS ──
function openBookPreview(title){openModal('preview');}
function filterByGenre(g){showToast(`Browsing: ${g} →`);document.getElementById('works').scrollIntoView({behavior:'smooth'});}
function handleSearch(){const q=document.getElementById('searchInput').value.trim();if(q)showToast(`Searching for "${q}"…`);else showToast('Please enter a search term');}
function handleNewsletter(){const e=document.getElementById('nlEmail').value.trim();if(e&&e.includes('@')){showToast('Subscribed! Welcome to the Inkwell community 📚');document.getElementById('nlEmail').value='';}else showToast('Please enter a valid email address');}
function handlePublish(){showToast('Submitted! We\'ll review your work within 48 hours. ✨');closeModal('publish');}
function handleSignin(){showToast('Welcome back! Redirecting to your dashboard…');closeModal('signin');}
function togglePill(el){el.classList.toggle('sel');}

// ── HAMBURGER ──
document.getElementById('hamburger').addEventListener('click',()=>showToast('Mobile menu — add your navigation here'));

// ── INTERSECTION OBSERVER (fade-in) ──
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');observer.unobserve(e.target);}});
},{threshold:.1});
document.querySelectorAll('.fade-in').forEach(el=>observer.observe(el));

// ── INIT ──
renderBooks();
renderGenres();

// Trigger counters when hero is visible
const heroObserver=new IntersectionObserver(entries=>{
  if(entries[0].isIntersecting){
    animateCounter(document.getElementById('cnt-authors'),12400,'+');
    animateCounter(document.getElementById('cnt-books'),48200,'+');
    animateCounter(document.getElementById('cnt-readers'),320000,'+');
    heroObserver.disconnect();
  }
},{threshold:.3});
heroObserver.observe(document.querySelector('.hero-stats'));

// Scroll: shrink nav
window.addEventListener('scroll',()=>{
  const nav=document.getElementById('nav');
  nav.style.boxShadow=window.scrollY>50?'0 2px 20px rgba(14,12,10,.08)':'none';
});
</script>
</body>
</html>
