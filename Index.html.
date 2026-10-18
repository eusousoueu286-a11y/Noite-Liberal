<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#100d17">
  <meta name="description" content="Noite Liberal: encontros e conexões com respeito e consentimento.">
  <title>Noite Liberal | Encontros e conexões</title>

  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      background: #100d17;
      color: #fff;
      font-family: Arial, sans-serif;
      padding: 24px 16px;
    }

    main { max-width: 440px; margin: 30px auto; }

    header { text-align: center; margin-bottom: 28px; }

    .logo { font-size: 38px; }

    h1 { margin: 10px 0; color: #f0abfc; }

    p { color: #c7bfd1; line-height: 1.5; }

    .card {
      background: #1c1726;
      border: 1px solid #40334e;
      padding: 22px;
      border-radius: 18px;
    }

    label {
      display: block;
      margin: 14px 0 7px;
    }

    input, select {
      display: block;
      width: 100%;
      padding: 13px;
      border-radius: 9px;
      border: 1px solid #51445f;
      background: #110e18;
      color: white;
      font-size: 16px;
    }

    input[type="checkbox"] {
      display: inline;
      width: auto;
      margin-right: 6px;
    }

    button {
      width: 100%;
      border: 0;
      border-radius: 9px;
      padding: 14px;
      margin-top: 13px;
      background: #d946ef;
      color: #190d20;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    button.secondary {
      background: #352841;
      color: white;
    }

    button:disabled { opacity: .55; }

    #status { overflow-wrap: anywhere; }

    .small { font-size: 12px; text-align: center; }

    [hidden] { display: none !important; }
  </style>
</head>

<body>
<main>
  <header>
    <div class="logo">🌙</div>
    <h1>Noite Liberal</h1>
    <p>Encontros, conexões e liberdade com respeito e consentimento.</p>
  </header>

  <section class="card" id="authPanel">
    <h2>Entre ou crie sua conta</h2>
    <p>Plataforma destinada exclusivamente a maiores de 18 anos.</p>

    <form id="signupForm">
      <h3>Criar conta</h3>

      <label for="nickname">Apelido</label>
      <input id="nickname" maxlength="40" minlength="2"
        autocomplete="nickname" required>

      <label for="type">Tipo de perfil</label>
      <select id="type" required>
        <option value="casal">Casal</option>
        <option value="solteiro">Solteiro(a)</option>
        <option value="grupo">Grupo</option>
      </select>

      <label for="signupEmail">E-mail</label>
      <input id="signupEmail" type="email"
        autocomplete="email" required>

      <label for="signupPassword">Senha (mínimo 8 caracteres)</label>
      <input id="signupPassword" type="password"
        minlength="8" autocomplete="new-password" required>

      <label>
        <input id="age" type="checkbox" required>
        Confirmo que tenho 18 anos ou mais.
      </label>

      <label>
        <input id="consent" type="checkbox" required>
        Concordo com as regras de respeito, consentimento e privacidade.
      </label>

      <button type="submit">Criar minha conta</button>
    </form>

    <hr style="border-color:#40334e;margin:25px 0">

    <form id="loginForm">
      <h3>Já tenho uma conta</h3>

      <label for="loginEmail">E-mail</label>
      <input id="loginEmail" type="email"
        autocomplete="email" required>

      <label for="loginPassword">Senha</label>
      <input id="loginPassword" type="password"
        autocomplete="current-password" required>

      <button type="submit" class="secondary">Entrar</button>
    </form>
  </section>

  <section class="card" id="accountPanel" hidden>
    <h2>Bem-vindo(a)!</h2>
    <p id="welcome"></p>
    <p>Sua conta está conectada ao Noite Liberal.</p>
    <p>Esta é a área inicial do seu perfil.</p>
    <button id="logout" class="secondary">Sair da conta</button>
  </section>

  <p id="status" role="status" aria-live="polite"></p>

  <p class="small">
    Respeite os limites e o consentimento de todas as pessoas.
    Nunca compartilhe imagens íntimas sem autorização.
  </p>
</main>

<script>
(() => {
  const SUPABASE_URL = "https://utdxjlfobsxjxxqjpvta.supabase.co";
  const SUPABASE_KEY = "sb_publishable_ChVy9FSLXuJLRhkBx3o9gg_OhmNEuzE";

  const status = document.getElementById("status");
  const authPanel = document.getElementById("authPanel");
  const accountPanel = document.getElementById("accountPanel");
  const signupForm = document.getElementById("signupForm");
  const loginForm = document.getElementById("loginForm");

  function message(text) {
    status.textContent = text;
  }

  if (!window.supabase) {
    message("Não foi possível carregar o Supabase. Verifique sua conexão.");
    return;
  }

  const db = window.supabase.createClient(
    SUPABASE_URL,
    SUPABASE_KEY
  );

  function showAccount(user) {
    authPanel.hidden = true;
    accountPanel.hidden = false;
    document.getElementById("welcome").textContent =
      "Conta conectada: " + user.email;
  }

  async function ensureProfile(user) {
    const meta = user.user_metadata || {};
    const nickname = meta.nickname;
    const userType = meta.user_type;

    if (!nickname || !["casal", "solteiro", "grupo"].includes(userType)) {
      return;
    }

    const { error } = await db.from("profiles").upsert({
      id: user.id,
      nickname: nickname,
      user_type: userType
    }, {
      onConflict: "id"
    });

    if (error) {
      console.error("Erro ao salvar perfil:", error.message);
      message("Conta conectada, mas houve um erro ao salvar o perfil.");
    }
  }

  signupForm.addEventListener("submit", async (event) => {
    event.preventDefault();

    const button = signupForm.querySelector('button[type="submit"]');
    button.disabled = true;
    message("Criando sua conta...");

    try {
      const nickname = document.getElementById("nickname").value.trim();
      const type = document.getElementById("type").value;
      const email = document.getElementById("signupEmail").value.trim();
      const password = document.getElementById("signupPassword").value;

      const { data, error } = await db.auth.signUp({
        email,
        password,
        options: {
          data: {
            nickname: nickname,
            user_type: type
          }
        }
      });

      if (error) throw error;

      if (data.session && data.user) {
        await ensureProfile(data.user);
        showAccount(data.user);
        message("Conta criada com sucesso!");
      } else {
        message(
          "Cadastro realizado! Confira seu e-mail para confirmar a conta. Depois, faça login."
        );
      }
    } catch (error) {
      message("Erro no cadastro: " + error.message);
    } finally {
      button.disabled = false;
    }
  });

  loginForm.addEventListener("submit", async (event) => {
    event.preventDefault();

    const button = loginForm.querySelector('button[type="submit"]');
    button.disabled = true;
    message("Entrando...");

    try {
      const email = document.getElementById("loginEmail").value.trim();
      const password = document.getElementById("loginPassword").value;

      const { data, error } = await db.auth.signInWithPassword({
        email,
        password
      });

      if (error) throw error;

      await ensureProfile(data.user);
      showAccount(data.user);
      message("Login realizado com sucesso!");
    } catch (error) {
      message("Erro ao entrar: " + error.message);
    } finally {
      button.disabled = false;
    }
  });

  document.getElementById("logout").addEventListener("click", async () => {
    const { error } = await db.auth.signOut();

    if (error) {
      message("Erro ao sair: " + error.message);
      return;
    }

    accountPanel.hidden = true;
    authPanel.hidden = false;
    message("Você saiu da conta.");
  });

  db.auth.onAuthStateChange((event, session) => {
    if (session && session.user) {
      showAccount(session.user);
    } else {
      accountPanel.hidden = true;
      authPanel.hidden = false;
    }
  });

  db.auth.getSession().then(({ data, error }) => {
    if (error) {
      message("Não foi possível verificar sua sessão.");
      return;
    }

    if (data.session && data.session.user) {
      showAccount(data.session.user);
    }
  });
})();
</script>
</body>
</html>
