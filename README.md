
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#160d1c">
  <meta name="description" content="Noite Liberal — conexões, respeito e encontros entre adultos.">
  <title>Noite Liberal | Conexões sem preconceito</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #100b14;
      --panel: #201426;
      --pink: #ff3d91;
      --purple: #b65cff;
      --text: #fff5fb;
      --muted: #c6b5c9;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      font-family: system-ui, Arial, sans-serif;
      color: var(--text);
      background:
        radial-gradient(ellipse at top, #492044 0, transparent 55%),
        var(--bg);
    }
    header {
      padding: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #ffffff18;
    }
    .logo { font-weight: 900; font-size: 22px; }
    .logo span { color: var(--pink); }
    .adult {
      border: 1px solid #ff3d9170;
      border-radius: 20px;
      padding: 6px 10px;
      color: #ff9cc6;
      font-size: 12px;
    }
    main {
      width: min(100% - 28px, 960px);
      margin: 35px auto;
    }
    .hero { text-align: center; padding: 15px 0 30px; }
    .hero h1 {
      font-size: clamp(34px, 8vw, 58px);
      line-height: 1.08;
      margin: 10px 0 16px;
    }
    .hero h1 span {
      color: var(--pink);
    }
    .hero p {
      color: var(--muted);
      max-width: 620px;
      margin: 0 auto;
      line-height: 1.7;
    }
    .layout {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      align-items: start;
    }
    .panel {
      background: #201426eF;
      border: 1px solid #ffffff17;
      border-radius: 20px;
      padding: 22px;
      box-shadow: 0 15px 45px #0004;
    }
    h2 { margin-top: 0; }
    .muted { color: var(--muted); font-size: 14px; line-height: 1.6; }
    label {
      display: block;
      margin: 15px 0 7px;
      font-size: 14px;
    }
    input, select {
      width: 100%;
      padding: 13px;
      border-radius: 10px;
      border: 1px solid #604563;
      background: #130d18;
      color: white;
      font: inherit;
    }
    input:focus, select:focus {
      outline: 2px solid var(--purple);
      border-color: transparent;
    }
    .check {
      display: flex;
      gap: 10px;
      align-items: flex-start;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }
    .check input { width: auto; margin-top: 4px; }
    button {
      width: 100%;
      padding: 13px;
      margin-top: 15px;
      border: 0;
      border-radius: 11px;
      background: linear-gradient(100deg, var(--pink), var(--purple));
      color: white;
      font-weight: 800;
      font-size: 15px;
      cursor: pointer;
    }
    button:disabled { opacity: .55; cursor: wait; }
    .secondary {
      background: #392641;
      border: 1px solid #68486f;
    }
    .message {
      display: none;
      margin-top: 15px;
      padding: 12px;
      border-radius: 10px;
      background: #38233e;
      overflow-wrap: anywhere;
      font-size: 14px;
      line-height: 1.5;
    }
    .features {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
      margin-top: 22px;
    }
    .feature {
      background: #ffffff08;
      border: 1px solid #ffffff12;
      padding: 15px;
      border-radius: 14px;
      text-align: center;
    }
    .feature strong { display: block; margin-bottom: 7px; }
    .feature span { font-size: 13px; color: var(--muted); }
    #account { display: none; }
    footer {
      padding: 30px 15px;
      text-align: center;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.7;
    }
    @media (max-width: 650px) {
      .layout { grid-template-columns: 1fr; }
      .features { grid-template-columns: 1fr; }
      header { padding: 16px; }
      main { margin-top: 22px; }
    }
  </style>
</head>
<body>
  <header>
    <div class="logo">🌙 Noite<span>Liberal</span></div>
    <div class="adult">18+ · Somente adultos</div>
  </header>

  <main>
    <section class="hero">
      <h1>Conexões reais.<br><span>Respeito sempre.</span></h1>
      <p>
        Um espaço para adultos que desejam conhecer pessoas,
        trocar experiências e descobrir novas conexões com
        diálogo, privacidade e consentimento.
      </p>
    </section>

    <section id="account" class="panel">
      <h2>Você está conectado! 💜</h2>
      <p id="welcome" class="muted"></p>
      <p class="muted">
        Sua conta está criada. A área de descoberta de perfis e
        as conversas privadas ainda serão implementadas.
      </p>
      <button id="logout" class="secondary" type="button">Sair da conta</button>
      <div id="accountMessage" class="message" role="status"></div>
    </section>

    <section id="auth" class="layout">
      <div class="panel">
        <h2>✨ Criar conta</h2>
        <p class="muted">Entre para fazer parte da comunidade.</p>
        <form id="signup">
          <label for="nickname">Apelido</label>
          <input id="nickname" maxlength="40" required
            autocomplete="nickname" placeholder="Como deseja ser chamado?">

          <label for="type">Tipo de perfil</label>
          <select id="type" required>
            <option value="casal">Casal</option>
            <option value="individual">Pessoa individual</option>
          </select>

          <label for="email">E-mail</label>
          <input id="email" type="email" required
            autocomplete="email" placeholder="voce@exemplo.com">

          <label for="password">Senha (mínimo 8 caracteres)</label>
          <input id="password" type="password" required minlength="8"
            autocomplete="new-password" placeholder="Crie uma senha">

          <label class="check">
            <input id="age" type="checkbox" required>
            <span>Confirmo que tenho 18 anos ou mais.</span>
          </label>
          <label class="check">
            <input id="consent" type="checkbox" required>
            <span>
              Aceito as regras de respeito, privacidade e consentimento.
              Entendo que encontros devem ser voluntários e entre adultos.
            </span>
          </label>
          <button id="signupButton" type="submit">Criar minha conta</button>
          <div id="signupMessage" class="message" role="status"></div>
        </form>
      </div>

      <div class="panel">
        <h2>💌 Já tem uma conta?</h2>
        <p class="muted">Entre para continuar.</p>
        <form id="login">
          <label for="loginEmail">E-mail</label>
          <input id="loginEmail" type="email" required
            autocomplete="email" placeholder="Seu e-mail">

          <label for="loginPassword">Senha</label>
          <input id="loginPassword" type="password" required
            autocomplete="current-password" placeholder="Sua senha">

          <button id="loginButton" type="submit">Entrar</button>
          <div id="loginMessage" class="message" role="status"></div>
        </form>
        <p class="muted">
          Nunca compartilhe sua senha. Use um apelido e evite publicar
          dados pessoais ou informações que revelem seu endereço.
        </p>
      </div>
    </section>

    <section class="features">
      <div class="feature">
        <strong>🔒 Privacidade</strong>
        <span>Cuide dos seus dados e respeite os dos outros.</span>
      </div>
      <div class="feature">
        <strong>🤝 Consentimento</strong>
        <span>Limites claros e respeito em todas as interações.</span>
      </div>
      <div class="feature">
        <strong>💬 Novas conexões</strong>
        <span>Conheça pessoas sem pressão e com responsabilidade.</span>
      </div>
    </section>
  </main>

  <footer>
    Noite Liberal · Comunidade exclusiva para maiores de 18 anos.<br>
    Respeito, privacidade e consentimento são indispensáveis.<br>
    Não publique fotos ou informações de outras pessoas sem autorização.
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
  <script>
    const SUPABASE_URL = "https://utdxjlfobsxjxxqjpvta.supabase.co";
    const SUPABASE_KEY = "sb_publishable_ChVy9FSLXuJLRhkBx3o9gg_OhmNEuzE";

    const authSection = document.getElementById("auth");
    const accountSection = document.getElementById("account");

    function showMessage(id, text) {
      const el = document.getElementById(id);
      el.textContent = text;
      el.style.display = "block";
    }

    function setBusy(id, busy, text) {
      const button = document.getElementById(id);
      button.disabled = busy;
      if (!button.dataset.original) button.dataset.original = button.textContent;
      button.textContent = busy ? "Aguarde..." : button.dataset.original;
      if (text) button.textContent = text;
    }

    async function start() {
      if (!window.supabase) {
        showMessage("loginMessage",
          "Não foi possível carregar o serviço de autenticação. Confira sua conexão e recarregue a página.");
        return;
      }

      const client = window.supabase.createClient(
        SUPABASE_URL,
        SUPABASE_KEY
      );

      async function refreshAccount(session) {
        if (!session) {
          authSection.style.display = "grid";
          accountSection.style.display = "none";
          return;
        }

        authSection.style.display = "none";
        accountSection.style.display = "block";

        const user = session.user;
        const nickname = user.user_metadata?.nickname || "membro";
        document.getElementById("welcome").textContent =
          "Olá, " + nickname + "! Você entrou com " + user.email + ".";

        // Tenta manter o perfil básico sincronizado após o login.
        const userType = user.user_metadata?.user_type;
        if (nickname && userType) {
          const { error } = await client.from("profiles").upsert({
            id: user.id,
            nickname: nickname,
            user_type: userType
          }, { onConflict: "id" });

          if (error) {
            showMessage("accountMessage",
              "Login realizado. O perfil não pôde ser sincronizado agora. Verifique as colunas e as políticas RLS da tabela profiles no Supabase.");
          }
        }
      }

      document.getElementById("signup").addEventListener("submit", async (event) => {
        event.preventDefault();
        setBusy("signupButton", true);

        const nickname = document.getElementById("nickname").value.trim();
        const email = document.getElementById("email").value.trim();
        const password = document.getElementById("password").value;
        const userType = document.getElementById("type").value;

        if (!document.getElementById("age").checked ||
            !document.getElementById("consent").checked) {
          showMessage("signupMessage",
            "Confirme a idade mínima e aceite as regras para continuar.");
          setBusy("signupButton", false);
          return;
        }

        const { data, error } = await client.auth.signUp({
          email,
          password,
          options: {
            data: {
              nickname,
              user_type: userType
            }
          }
        });

        setBusy("signupButton", false);

        if (error) {
          showMessage("signupMessage", "Não foi possível criar a conta: " + error.message);
          return;
        }

        if (data.session) {
          await refreshAccount(data.session);
          showMessage("accountMessage", "Conta criada com sucesso!");
        } else {
          showMessage("signupMessage",
            "Cadastro iniciado! Confira seu e-mail e confirme o endereço antes de entrar. Se não receber a mensagem, confira a pasta de spam.");
        }
      });

      document.getElementById("login").addEventListener("submit", async (event) => {
        event.preventDefault();
        setBusy("loginButton", true);

        const email = document.getElementById("loginEmail").value.trim();
        const password = document.getElementById("loginPassword").value;

        const { data, error } = await client.auth.signInWithPassword({
          email,
          password
        });

        setBusy("loginButton", false);

        if (error) {
          showMessage("loginMessage", "Não foi possível entrar: " + error.message);
          return;
        }

        await refreshAccount(data.session);
      });

      document.getElementById("logout").addEventListener("click", async () => {
        const { error } = await client.auth.signOut();
        if (error) {
          showMessage("accountMessage", "Não foi possível sair: " + error.message);
          return;
        }
        await refreshAccount(null);
      });

      const { data, error } = await client.auth.getSession();
      if (error) {
        showMessage("loginMessage", "Erro ao verificar a sessão. Tente recarregar a página.");
        return;
      }
      await refreshAccount(data.session);

      client.auth.onAuthStateChange((_event, session) => {
        refreshAccount(session);
      });
    }

    start().catch(() => {
      showMessage("loginMessage",
        "Ocorreu um erro ao iniciar o site. Atualize a página e tente novamente.");
    });
  </script>
</body>
</html>
