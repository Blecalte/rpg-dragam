<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Dragam</title>
<link rel="icon" href="https://icons.iconarchive.com/icons/igh0zt/ios7-style-metro-ui/256/MetroUI-Browser-Comodo-Dragon-icon.png" type="image/png" />
<style>
  :root {
    --bg-start: #050005;
    --bg-end: #000000;
    --accent: #ff0050;
    --muted: #cfcfcf;
    --font: 'Segoe UI', Roboto, Arial, sans-serif;
    --shadow: rgba(255, 0, 80, 0.25);
    --scrollbar-bg: rgba(255, 0, 80, 0.15);
  }
  html, body {
    margin: 0; padding: 0; height: 100%;
    background: linear-gradient(180deg, var(--bg-start), var(--bg-end));
    color: white;
    font-family: var(--font);
    overflow: hidden;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  ::-webkit-scrollbar {
    width: 8px;
  }
  ::-webkit-scrollbar-track {
    background: transparent;
  }
  ::-webkit-scrollbar-thumb {
    background: var(--scrollbar-bg);
    border-radius: 4px;
  }
  header {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 60px;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 24px;
    z-index: 1000;
    border-bottom: 1px solid rgba(255, 255, 255, 0.12);
    backdrop-filter: blur(8px);
    box-shadow: 0 2px 8px var(--shadow);
  }
  header h1 {
    font-size: 26px;
    color: var(--accent);
    margin: 0;
    letter-spacing: 1.2px;
    font-weight: 900;
    user-select: none;
    text-shadow: 0 0 6px var(--accent);
  }
  .header-right {
    display: flex;
    align-items: center;
    gap: 12px;
  }
  #userIcon {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid var(--accent);
    cursor: pointer;
  }
  header button, #loginBtn {
    background: var(--accent);
    border: none;
    border-radius: 50%;
    width: 48px;
    height: 48px;
    color: white;
    font-size: 28px;
    cursor: pointer;
    transition: transform 0.25s, box-shadow 0.25s;
    box-shadow: 0 0 8px var(--accent);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  header button:hover, header button:focus,
  #loginBtn:hover, #loginBtn:focus {
    transform: scale(1.15);
    box-shadow: 0 0 14px var(--accent);
    outline: none;
  }
  #searchInput {
    background: #222;
    border: none;
    border-radius: 12px;
    padding: 8px 16px;
    font-size: 16px;
    color: white;
    width: 180px;
    transition: box-shadow 0.3s;
  }
  #searchInput:focus {
    outline: none;
    box-shadow: 0 0 8px var(--accent);
  }
  #userArea {
    color: var(--accent);
    font-weight: 700;
    user-select: none;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .app {
    padding-top: 60px;
    height: 100vh;
    position: relative;
    overflow: hidden;
    background: transparent;
    display: flex;
    justify-content: center;
  }
  .feed {
    height: 100%;
    width: 100%;
    max-width: 600px;
    position: relative;
    touch-action: none;
    outline: none;
    -webkit-overflow-scrolling: touch;
  }
  .reel {
    height: 100vh;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    padding: 24px 24px 48px;
    box-sizing: border-box;
    flex-direction: row;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    will-change: transform;
    border-radius: 20px;
    box-shadow: 0 8px 32px var(--shadow);
    background: rgba(10, 0, 10, 0.8);
    backdrop-filter: blur(12px);
    user-select: none;
  }
  video {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 20px;
    filter: brightness(0.9);
    background: #000;
  }
  .meta {
    z-index: 2;
    background: linear-gradient(180deg, transparent, rgba(0, 0, 0, 0.85));
    padding: 18px 22px;
    border-radius: 14px;
    max-width: 65%;
    user-select: text;
    box-shadow: 0 0 12px rgba(0,0,0,0.6);
  }
  .meta .user {
    font-weight: 900;
    font-size: 17px;
    color: var(--accent);
    margin-bottom: 6px;
    text-shadow: 0 0 4px var(--accent);
  }
  .meta .caption {
    font-size: 15px;
    color: var(--muted);
    line-height: 1.4;
    white-space: pre-wrap;
  }
  .actions {
    z-index: 2;
    display: flex;
    flex-direction: column;
    gap: 18px;
    align-items: center;
    user-select: none;
  }
  .action {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: rgba(0, 0, 0, 0.65);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.25s, background 0.25s, box-shadow 0.25s;
    font-size: 26px;
    line-height: 1;
    box-shadow: 0 0 8px rgba(0,0,0,0.3);
    position: relative;
  }
  .action:hover, .action:focus {
    transform: scale(1.2);
    background: rgba(255, 255, 255, 0.15);
    box-shadow: 0 0 16px var(--accent);
    outline: none;
  }
  .action .count {
    position: absolute;
    bottom: 6px;
    right: 6px;
    background: var(--accent);
    color: #111;
    font-weight: 900;
    font-size: 12px;
    border-radius: 8px;
    padding: 2px 6px;
    box-shadow: 0 0 6px var(--accent);
    user-select: none;
  }
  .progress-wrap {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: rgba(255, 255, 255, 0.15);
    border-radius: 2px;
    z-index: 3;
  }
  .progress {
    height: 100%;
    width: 0;
    background: var(--accent);
    transition: width 0.1s linear;
    border-radius: 2px;
  }
  .modal {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
    z-index: 2000;
  }
  .modal.open {
    opacity: 1;
    pointer-events: auto;
  }
  .modal-content {
    background: #111;
    padding: 28px 30px;
    border-radius: 16px;
    width: 90%;
    max-width: 480px;
    box-shadow: 0 0 25px var(--accent);
    font-size: 16px;
    color: white;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  .modal-content h2 {
    margin: 0 0 20px 0;
    font-weight: 900;
    color: var(--accent);
    text-align: center;
    letter-spacing: 1.3px;
    user-select: none;
    text-shadow: 0 0 8px var(--accent);
  }
  .modal-content input,
  .modal-content textarea {
    width: 100%;
    padding: 14px 16px;
    border: none;
    border-radius: 10px;
    background: #222;
    color: white;
    font-size: 15px;
    font-family: var(--font);
    resize: none;
    box-sizing: border-box;
    transition: background 0.3s;
  }
  .modal-content input:focus,
  .modal-content textarea:focus {
    outline: none;
    background: #333;
    box-shadow: 0 0 8px var(--accent);
  }
  .modal-content button {
    padding: 14px;
    background: var(--accent);
    border: none;
    color: white;
    border-radius: 10px;
    cursor: pointer;
    font-weight: 900;
    letter-spacing: 0.7px;
    font-size: 18px;
    transition: background 0.3s, box-shadow 0.3s;
    user-select: none;
    box-shadow: 0 0 12px var(--accent);
  }
  .modal-content button:hover,
  .modal-content button:focus {
    background: #e60045;
    box-shadow: 0 0 20px #e60045;
    outline: none;
  }
  /* Chat modal styles */
  #chatModal .modal-content {
    max-height: 500px;
    display: flex;
    flex-direction: column;
  }
  #chatMessages {
    flex-grow: 1;
    background: #222;
    border-radius: 12px;
    padding: 12px;
    overflow-y: auto;
    margin-bottom: 12px;
    font-size: 14px;
    line-height: 1.3;
  }
  #chatMessages .message {
    display: flex;
    align-items: flex-start;
    margin: 8px 0;
    gap: 10px;
  }
  #chatMessages .message img {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    object-fit: cover;
    border: 1.5px solid var(--accent);
    flex-shrink: 0;
  }
  #chatMessages .message .text {
    background: rgba(255,255,255,0.1);
    padding: 8px 12px;
    border-radius: 12px;
    max-width: 80%;
    word-wrap: break-word;
    color: white;
    font-size: 14px;
    user-select: text;
  }
  #chatInput {
    width: 100%;
    padding: 12px 14px;
    border-radius: 12px;
    border: none;
    font-size: 15px;
    font-family: var(--font);
    background: #222;
    color: white;
    box-sizing: border-box;
  }
  #chatInput:focus {
    outline: none;
    box-shadow: 0 0 8px var(--accent);
  }
  #chatSendBtn {
    margin-top: 10px;
    padding: 12px;
    background: var(--accent);
    border: none;
    color: white;
    font-weight: 900;
    font-size: 16px;
    border-radius: 12px;
    cursor: pointer;
    transition: background 0.3s, box-shadow 0.3s;
  }
  #chatSendBtn:hover, #chatSendBtn:focus {
    background: #e60045;
    box-shadow: 0 0 14px #e60045;
    outline: none;
  }
  /* Responsive */
  @media (max-width: 900px) {
    .reel {
      border-radius: 0;
      box-shadow: none;
      padding: 20px;
      background: transparent;
      backdrop-filter: none;
    }
    video {
      border-radius: 0;
      filter: none;
    }
    .meta {
      max-width: 80%;
      padding: 12px 14px;
      background: linear-gradient(180deg, transparent, rgba(0,0,0,0.7));
      box-shadow: none;
    }
    .actions {
      gap: 12px;
    }
    .action {
      width: 46px;
      height: 46px;
      font-size: 20px;
    }
    header {
      padding: 0 16px;
    }
    header h1 {
      font-size: 20px;
    }
    header button {
      width: 40px;
      height: 40px;
      font-size: 24px;
    }
    #searchInput {
      width: 130px;
    }
  }
</style>
</head>
<body>
<header>
  <h1>Dragam</h1>
  <div class="header-right">
    <input type="text" id="searchInput" placeholder="Buscar usuário..." aria-label="Buscar usuário" />
    <div id="userArea" tabindex="0" aria-live="polite" aria-atomic="true" role="region">
      <img id="userIcon" src="" alt="Ícone do usuário" title="Clique para alterar seu ícone" tabindex="0" />
      <span id="userNameText">Não logado</span>
    </div>
    <button id="loginBtn" title="Logar usuário" aria-label="Logar usuário">👤</button>
    <button id="addBtn" aria-label="Postar novo Reels">+</button>
  </div>
</header>
<div class="app">
  <div class="feed" id="feed" tabindex="0" aria-live="polite" aria-atomic="true"></div>
</div>

<!-- Upload Modal -->
<div class="modal" id="uploadModal" role="dialog" aria-modal="true" aria-labelledby="modalTitle" aria-hidden="true">
  <div class="modal-content">
    <h2 id="modalTitle">Postar Reels</h2>
    <input type="file" id="videoFile" accept="video/mp4,video/webm" aria-label="Selecionar arquivo de vídeo" />
    <input type="text" id="username" placeholder="Seu usuário" aria-label="Nome do usuário" />
    <textarea id="caption" placeholder="Legenda" rows="3" aria-label="Legenda do vídeo"></textarea>
    <button id="postBtn">Postar</button>
  </div>
</div>

<!-- Chat Modal -->
<div class="modal" id="chatModal" role="dialog" aria-modal="true" aria-labelledby="chatTitle" aria-hidden="true">
  <div class="modal-content">
    <h2 id="chatTitle">Comentários</h2>
    <div id="chatMessages" aria-live="polite" aria-atomic="false" tabindex="0"></div>
    <input type="text" id="chatInput" placeholder="Escreva um comentário..." aria-label="Campo para escrever comentário" />
    <button id="chatSendBtn">Enviar</button>
  </div>
</div>

<!-- User Icon Upload Modal -->
<div class="modal" id="iconUploadModal" role="dialog" aria-modal="true" aria-labelledby="iconModalTitle" aria-hidden="true">
  <div class="modal-content">
    <h2 id="iconModalTitle">Alterar Ícone do Usuário</h2>
    <input type="file" id="iconFile" accept="image/png, image/jpeg, image/jpg, image/gif" aria-label="Selecionar imagem para ícone" />
    <button id="iconSaveBtn">Salvar</button>
  </div>
</div>

<script>
  const feed = document.getElementById('feed');
  const modal = document.getElementById('uploadModal');
  const chatModal = document.getElementById('chatModal');
  const addBtn = document.getElementById('addBtn');
  const postBtn = document.getElementById('postBtn');
  const loginBtn = document.getElementById('loginBtn');
  const userArea = document.getElementById('userArea');
  const searchInput = document.getElementById('searchInput');
  const chatMessages = document.getElementById('chatMessages');
  const chatInput = document.getElementById('chatInput');
  const chatSendBtn = document.getElementById('chatSendBtn');
  const userIconImg = document.getElementById('userIcon');
  const userNameText = document.getElementById('userNameText');

  const iconUploadModal = document.getElementById('iconUploadModal');
  const iconFileInput = document.getElementById('iconFile');
  const iconSaveBtn = document.getElementById('iconSaveBtn');

  let reels = [];
  let likes = {};
  let comments = {};
  let loggedUser = null;
  let userIcons = {}; // { username: base64string }
  let current = 0;
  let isTransitioning = false;
  let filteredReels = [];
  let videos = [];
  let chatCurrentId = null;

  // Função para salvar estado no localStorage
  function saveState() {
    localStorage.setItem('dragam_reels', JSON.stringify(reels));
    localStorage.setItem('dragam_likes', JSON.stringify(likes));
    localStorage.setItem('dragam_comments', JSON.stringify(comments));
    localStorage.setItem('dragam_user', loggedUser || '');
    localStorage.setItem('dragam_userIcons', JSON.stringify(userIcons));
  }

  // Função para carregar estado do localStorage
  function loadState() {
    const reelsData = localStorage.getItem('dragam_reels');
    if (reelsData) reels = JSON.parse(reelsData);

    const likesData = localStorage.getItem('dragam_likes');
    if (likesData) likes = JSON.parse(likesData);

    const commentsData = localStorage.getItem('dragam_comments');
    if (commentsData) comments = JSON.parse(commentsData);

    const userData = localStorage.getItem('dragam_user');
    loggedUser = userData && userData.length > 0 ? userData : null;

    const iconsData = localStorage.getItem('dragam_userIcons');
    if (iconsData) userIcons = JSON.parse(iconsData);
  }

  loadState();

  // Ícone padrão genérico
  const defaultUserIcon = 'https://cdn-icons-png.flaticon.com/512/149/149071.png';

  function getUserIcon(user) {
    return userIcons[user] || defaultUserIcon;
  }

  function updateUserArea() {
    if (loggedUser) {
      userNameText.textContent = `@${loggedUser}`;
      userIconImg.src = getUserIcon(loggedUser);
      userIconImg.alt = `Ícone do usuário ${loggedUser}`;
      userIconImg.style.cursor = 'pointer';
      loginBtn.textContent = '🔓'; // logout icon
      loginBtn.title = 'Deslogar usuário';
    } else {
      userNameText.textContent = 'Não logado';
      userIconImg.src = defaultUserIcon;
      userIconImg.alt = 'Ícone padrão usuário';
      userIconImg.style.cursor = 'default';
      loginBtn.textContent = '👤'; // login icon
      loginBtn.title = 'Logar usuário';
    }
  }

  updateUserArea();

  // Renderiza os reels filtrados
  function renderReels() {
    filteredReels = reels.filter(r => {
      if (!searchInput.value) return true;
      return r.user.toLowerCase().includes(searchInput.value.toLowerCase());
    });
    if (filteredReels.length === 0) {
      feed.innerHTML = '<p style="text-align:center; margin-top: 40vh; color: var(--muted);">Nenhum reel encontrado.</p>';
      return;
    }
    if (current >= filteredReels.length) current = filteredReels.length - 1;
    feed.innerHTML = '';
    filteredReels.forEach((reel, i) => {
      const reelDiv = document.createElement('div');
      reelDiv.className = 'reel';
      reelDiv.style.transform = `translateY(${(i - current) * 100}vh)`;
      reelDiv.setAttribute('aria-hidden', i !== current);
      const liked = likes[reel.id] && likes[reel.id].includes(loggedUser);
      const likeCount = likes[reel.id]?.length || 0;
      const commentCount = comments[reel.id]?.length || 0;

      reelDiv.innerHTML = `
        <div class="progress-wrap"><div class="progress"></div></div>
        <video src="${reel.video}" playsinline loop muted></video>
        <div class="meta">
          <div class="user">@${reel.user}</div>
          <div class="caption">${reel.caption}</div>
        </div>
        <div class="actions">
          <div class="action like" role="button" tabindex="0" aria-label="Curtir vídeo" data-id="${reel.id}">
            ❤
            <span class="count">${likeCount}</span>
          </div>
          <div class="action comment" role="button" tabindex="0" aria-label="Comentários" data-id="${reel.id}">
            💬
            <span class="count">${commentCount}</span>
          </div>
        </div>
      `;
      feed.appendChild(reelDiv);
    });
    videos = [...document.querySelectorAll('video')];
    updatePlayState();
  }

  function updatePlayState() {
    videos.forEach((v, i) => {
      const progress = feed.children[i].querySelector('.progress');
      if (i === current) {
        v.play().catch(() => {});
        v.ontimeupdate = () => {
          if (v.duration) progress.style.width = (v.currentTime / v.duration) * 100 + '%';
        };
      } else {
        v.pause();
        v.currentTime = 0;
        progress.style.width = '0%';
      }
      feed.children[i].setAttribute('aria-hidden', i !== current);
    });
    feed.childNodes.forEach((el, i) => {
      el.style.transform = `translateY(${(i - current) * 100}vh)`;
    });
    feed.setAttribute('aria-label', `Reels ${current + 1} de ${filteredReels.length}`);
  }

  function changeReel(newIndex) {
    if (isTransitioning || newIndex < 0 || newIndex >= filteredReels.length) return;
    isTransitioning = true;
    current = newIndex;
    updatePlayState();
    setTimeout(() => {
      isTransitioning = false;
    }, 500);
  }

  // Eventos teclado
  window.addEventListener('keydown', e => {
    if (e.key === 'ArrowDown') changeReel(current + 1);
    if (e.key === 'ArrowUp') changeReel(current - 1);
  });

  // Swipe mobile
  let startY = null;
  let startTime = 0;
  feed.addEventListener('touchstart', e => {
    if (e.touches.length === 1) {
      startY = e.touches[0].clientY;
      startTime = Date.now();
    }
  });
  feed.addEventListener('touchend', e => {
    if (startY === null) return;
    const endY = e.changedTouches[0].clientY;
    const dy = endY - startY;
    const dt = Date.now() - startTime;
    if (Math.abs(dy) > 50 && dt < 600) {
      if (dy < 0) changeReel(current + 1);
      else changeReel(current - 1);
    }
    startY = null;
  });

  // Scroll roda mouse
  feed.addEventListener('wheel', e => {
    if (isTransitioning) return;
    if (e.deltaY > 30) changeReel(current + 1);
    else if (e.deltaY < -30) changeReel(current - 1);
  }, { passive: true });

  // Botões header
  addBtn.onclick = () => {
    if (!loggedUser) {
      alert('Você precisa estar logado para postar.');
      return;
    }
    modal.classList.add('open');
    modal.setAttribute('aria-hidden', 'false');
    document.getElementById('videoFile').value = '';
    document.getElementById('username').value = loggedUser;
    document.getElementById('caption').value = '';
  };

  modal.onclick = e => {
    if (e.target === modal) {
      modal.classList.remove('open');
      modal.setAttribute('aria-hidden', 'true');
    }
  };

  postBtn.onclick = () => {
    const fileInput = document.getElementById('videoFile');
    const username = document.getElementById('username').value.trim();
    const caption = document.getElementById('caption').value.trim();
    if (fileInput.files.length === 0) {
      alert('Por favor, selecione um arquivo de vídeo.');
      return;
    }
    if (!username) {
      alert('Por favor, informe seu nome de usuário.');
      return;
    }
    const file = fileInput.files[0];
    const url = URL.createObjectURL(file);
    const id = Date.now().toString();
    reels.unshift({ id, video: url, user: username, caption });
    likes[id] = [];
    comments[id] = [];
    saveState();
    modal.classList.remove('open');
    modal.setAttribute('aria-hidden', 'true');
    current = 0;
    renderReels();
  };

  // Login simples
  loginBtn.onclick = () => {
    if (loggedUser) {
      if (confirm(`Deseja deslogar ${loggedUser}?`)) {
        loggedUser = null;
        saveState();
        updateUserArea();
        renderReels();
      }
      return;
    }
    const user = prompt('Digite seu nome de usuário para logar:');
    if (user && user.trim().length > 0) {
      loggedUser = user.trim();
      saveState();
      updateUserArea();
      renderReels();
    }
  };

  // Alterar ícone do usuário ao clicar na imagem
  userIconImg.onclick = () => {
    if (!loggedUser) {
      alert('Você precisa estar logado para alterar o ícone.');
      return;
    }
    iconUploadModal.classList.add('open');
    iconUploadModal.setAttribute('aria-hidden', 'false');
    iconFileInput.value = '';
  };

  // Fechar modais clicando fora do conteúdo
  iconUploadModal.onclick = e => {
    if (e.target === iconUploadModal) {
      iconUploadModal.classList.remove('open');
      iconUploadModal.setAttribute('aria-hidden', 'true');
    }
  };

  // Salvar novo ícone do usuário
  iconSaveBtn.onclick = () => {
    if (iconFileInput.files.length === 0) {
      alert('Por favor, selecione uma imagem.');
      return;
    }
    const file = iconFileInput.files[0];
    const reader = new FileReader();
    reader.onload = function(e) {
      userIcons[loggedUser] = e.target.result; // base64
      saveState();
      updateUserArea();
      iconUploadModal.classList.remove('open');
      iconUploadModal.setAttribute('aria-hidden', 'true');
      // Re-render chat messages para atualizar ícones se chat estiver aberto
      if (chatCurrentId !== null) renderChatMessages();
    };
    reader.readAsDataURL(file);
  };

  // Like toggle e abrir chat
  feed.addEventListener('click', e => {
    const likeBtn = e.target.closest('.action.like');
    const commentBtn = e.target.closest('.action.comment');
    if (likeBtn) {
      if (!loggedUser) {
        alert('Você precisa estar logado para curtir.');
        return;
      }
      const id = likeBtn.dataset.id;
      if (!likes[id]) likes[id] = [];
      const index = likes[id].indexOf(loggedUser);
      if (index === -1) {
        likes[id].push(loggedUser);
        animateLike(likeBtn);
      } else {
        likes[id].splice(index, 1);
      }
      saveState();
      renderReels();
    }
    if (commentBtn) {
      if (!loggedUser) {
        alert('Você precisa estar logado para comentar.');
        return;
      }
      const id = commentBtn.dataset.id;
      openChat(id);
    }
  });

  // Animação like
  function animateLike(button) {
    button.style.transition = 'none';
    button.style.transform = 'scale(1.6)';
    setTimeout(() => {
      button.style.transition = 'transform 0.3s ease';
      button.style.transform = 'scale(1)';
    }, 150);
  }

  // Chat funcionalidade
  function openChat(id) {
    chatCurrentId = id;
    chatModal.classList.add('open');
    chatModal.setAttribute('aria-hidden', 'false');
    renderChatMessages();
    chatInput.focus();
  }

  function closeChat() {
    chatModal.classList.remove('open');
    chatModal.setAttribute('aria-hidden', 'true');
    chatInput.value = '';
    chatCurrentId = null;
  }

  chatModal.addEventListener('click', e => {
    if (e.target === chatModal) {
      closeChat();
    }
  });

  chatSendBtn.onclick = () => {
    if (!loggedUser) return alert('Você precisa estar logado para comentar.');
    const msg = chatInput.value.trim();
    if (!msg) return;
    if (!comments[chatCurrentId]) comments[chatCurrentId] = [];
    comments[chatCurrentId].push({ user: loggedUser, text: msg, time: Date.now() });
    saveState();
    chatInput.value = '';
    renderChatMessages();
  };

  chatInput.addEventListener('keydown', e => {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      chatSendBtn.click();
    }
  });

  // Renderiza as mensagens do chat com ícones
  function renderChatMessages() {
    if (!comments[chatCurrentId]) comments[chatCurrentId] = [];
    chatMessages.innerHTML = '';
    comments[chatCurrentId].forEach(c => {
      const msgDiv = document.createElement('div');
      msgDiv.className = 'message';

      const icon = document.createElement('img');
      icon.src = getUserIcon(c.user);
      icon.alt = `Ícone de ${c.user}`;

      const textSpan = document.createElement('div');
      textSpan.className = 'text';
      textSpan.textContent = `@${c.user}: ${c.text}`;

      msgDiv.appendChild(icon);
      msgDiv.appendChild(textSpan);
      chatMessages.appendChild(msgDiv);
    });
    chatMessages.scrollTop = chatMessages.scrollHeight;
  }

  // Busca usuário
  searchInput.addEventListener('input', () => {
    current = 0;
    renderReels();
  });

  // Carregar alguns reels iniciais sobre RPG para já ter conteúdo
  if (reels.length === 0) {
    const defaultRPGReels = [
      {
        id: 'rpg1',
        video: 'https://cdn.coverr.co/videos/coverr-a-man-playing-dungeons-and-dragons-3420/1080p.mp4',
        user: 'mestreRPG',
        caption: 'Partida épica de D&D! #RPG #DnD'
      },
      {
        id: 'rpg2',
        video: 'https://cdn.coverr.co/videos/coverr-rolling-dice-in-board-game-3492/1080p.mp4',
        user: 'jogadorLendario',
        caption: 'A sorte está lançada! 🎲 #RPG'
      },
      {
        id: 'rpg3',
        video: 'https://cdn.coverr.co/videos/coverr-group-of-people-rolling-dice-3347/1080p.mp4',
        user: 'grupoAventureiro',
        caption: 'Juntos em mais uma aventura! #RPGFriends'
      }
    ];
    reels = defaultRPGReels;
    defaultRPGReels.forEach(r => {
      likes[r.id] = [];
      comments[r.id] = [];
    });
    saveState();
  }

  renderReels();
  updateUserArea();
</script>
</body>
</html>
