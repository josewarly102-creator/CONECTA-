# CONECTA-
O CONECTA+ é um aplicativo de comunicação inclusiva que conecta pessoas cegas, pessoas com deficiência na fala e todos que desejam se comunicar sem barreiras. Utilizando tecnologia e inteligência artificial, transforma voz em texto e texto em voz, promovendo autonomia, acessibilidade e inclusão. Porque se comunicar é um direito de todos!
conecta-plus/
├── src/
│   ├── App.jsx
│   ├── App.css
│   └── main.jsx
├── index.html
└── package.json

import { useState } from "react";
import "./App.css";

const frases = [
  { texto: "Olá, tudo bem?", emoji: "👋" },
  { texto: "Preciso de ajuda.", emoji: "🆘" },
  { texto: "Estou com dor.", emoji: "🤕" },
  { texto: "Quero beber água.", emoji: "💧" },
  { texto: "Quero ir ao banheiro.", emoji: "🚻" },
  { texto: "Obrigado!", emoji: "❤️" },
  { texto: "Sim", emoji: "✅" },
  { texto: "Não", emoji: "❌" },
];

function App() {
  const [mensagem, setMensagem] = useState("");
  const [categoria, setCategoria] = useState("Todas");
  const [falando, setFalando] = useState(false);

  function falar(texto) {
    if (!texto.trim()) return;

    window.speechSynthesis.cancel();

    const utterance = new SpeechSynthesisUtterance(texto);
    utterance.lang = "pt-BR";
    utterance.rate = 0.9;
    utterance.pitch = 1;

    utterance.onstart = () => setFalando(true);
    utterance.onend = () => setFalando(false);
    utterance.onerror = () => setFalando(false);

    window.speechSynthesis.speak(utterance);
  }

  function pararFala() {
    window.speechSynthesis.cancel();
    setFalando(false);
  }

  function limparMensagem() {
    setMensagem("");
  }

  return (
    <main className="app">
      <header className="header">
        <div className="logo">
          <span className="logo-icon">+</span>
          <div>
            <h1>CONECTA+</h1>
            <p>Comunicação para todos</p>
          </div>
        </div>

        <span className="accessibility-badge">
          ♿ Inclusivo
        </span>
      </header>

      <section className="welcome">
        <h2>Como podemos nos comunicar?</h2>
        <p>
          Escolha uma frase ou digite o que deseja dizer.
          Nós falaremos por você.
        </p>
      </section>

      <section className="message-box">
        <label htmlFor="mensagem">
          Digite sua mensagem
        </label>

        <textarea
          id="mensagem"
          value={mensagem}
          onChange={(e) => setMensagem(e.target.value)}
          placeholder="Escreva aqui o que você deseja comunicar..."
          rows={4}
        />

        <div className="actions">
          <button
            className="speak-button"
            onClick={() => falar(mensagem)}
            disabled={!mensagem.trim()}
          >
            🔊 FALAR
          </button>

          <button
            className="clear-button"
            onClick={limparMensagem}
          >
            Limpar
          </button>
        </div>

        {falando && (
          <button
            className="stop-button"
            onClick={pararFala}
          >
            ⏹ Parar áudio
          </button>
        )}
      </section>

      <section className="phrases">
        <h2>Frases rápidas</h2>
        <p className="section-description">
          Toque em uma frase para reproduzi-la.
        </p>

        <div className="phrase-grid">
          {frases.map((frase, index) => (
            <button
              key={index}
              className="phrase-button"
              onClick={() => {
                setMensagem(frase.texto);
                falar(frase.texto);
              }}
              aria-label={`Falar: ${frase.texto}`}
            >
              <span className="emoji">{frase.emoji}</span>
              <span>{frase.texto}</span>
            </button>
          ))}
        </div>
      </section>

      <footer>
        <p>
          CONECTA+ — Tecnologia que aproxima pessoas.
        </p>
      </footer>
    </main>
  );
}

export default App;

* {
  box-sizing: border-box;
}

:root {
  font-family: Arial, Helvetica, sans-serif;
  color: #172033;
  background: #f3f6fb;
}

body {
  margin: 0;
  min-width: 320px;
}

button,
textarea {
  font: inherit;
}

button {
  cursor: pointer;
}

button:focus-visible,
textarea:focus-visible {
  outline: 4px solid #ffbf47;
  outline-offset: 4px;
}

.app {
  max-width: 850px;
  margin: auto;
  padding: 24px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  background: #ffffff;
  padding: 20px;
  border-radius: 20px;
  box-shadow: 0 4px 20px #00000008;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-icon {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #155eef;
  color: white;
  width: 55px;
  height: 55px;
  border-radius: 15px;
  font-size: 36px;
  font-weight: bold;
}

.logo h1 {
  margin: 0;
  font-size: 24px;
  color: #155eef;
}

.logo p {
  margin: 5px 0 0;
  color: #536078;
}

.accessibility-badge {
  background: #e5f1ff;
  color: #124db3;
  padding: 10px 14px;
  border-radius: 30px;
  font-weight: bold;
}

.welcome {
  padding: 30px 8px 20px;
}

.welcome h2 {
  font-size: 30px;
  margin-bottom: 10px;
}

.welcome p {
  font-size: 18px;
  line-height: 1.6;
  color: #526078;
}

.message-box {
  background: white;
  padding: 24px;
  border-radius: 20px;
  box-shadow: 0 4px 20px #00000008;
}

.message-box label {
  display: block;
  font-weight: bold;
  font-size: 18px;
  margin-bottom: 12px;
}

textarea {
  width: 100%;
  padding: 16px;
  border: 2px solid #cbd5e1;
  border-radius: 14px;
  resize: vertical;
  font-size: 18px;
  color: #172033;
  background: white;
}

textarea::placeholder {
  color: #64748b;
}

.actions {
  display: flex;
  gap: 12px;
  margin-top: 15px;
}

.speak-button {
  flex: 1;
  min-height: 65px;
  border: none;
  border-radius: 14px;
  background: #155eef;
  color: white;
  font-size: 21px;
  font-weight: bold;
}

.speak-button:hover {
  background: #1049bd;
}

.speak-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.clear-button {
  padding: 15px 25px;
  border-radius: 14px;
  border: 2px solid #cbd5e1;
  background: white;
  color: #172033;
  font-weight: bold;
}

.stop-button {
  width: 100%;
  margin-top: 12px;
  min-height: 55px;
  background: #b42318;
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 18px;
  font-weight: bold;
}

.phrases {
  margin-top: 32px;
}

.phrases h2 {
  font-size: 26px;
}

.section-description {
  color: #526078;
  font-size: 17px;
}

.phrase-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 14px;
  margin-top: 20px;
}

.phrase-button {
  display: flex;
  align-items: center;
  gap: 15px;
  min-height: 100px;
  padding: 20px;
  background: white;
  border: 2px solid #d9e2f0;
  border-radius: 18px;
  text-align: left;
  font-size: 19px;
  font-weight: bold;
  color: #172033;
  transition: 0.2s;
}

.phrase-button:hover {
  border-color: #155eef;
  background: #edf4ff;
  transform: translateY(-2px);
}

.emoji {
  font-size: 32px;
}

footer {
  text-align: center;
  padding: 30px 10px;
  color: #526078;
  font-size: 14px;
}

@media (max-width: 550px) {
  .app {
    padding: 14px;
  }

  .header {
    padding: 15px;
  }

  .logo h1 {
    font-size: 21px;
  }

  .accessibility-badge {
    font-size: 12px;
    padding: 8px;
  }

  .welcome h2 {
    font-size: 25px;
  }

  .phrase-grid {
    grid-template-columns: 1fr;
  }

  .phrase-button {
    min-height: 85px;
    font-size: 20px;
  }

  .actions {
    flex-direction: column;
  }

  .clear-button {
    min-height: 55px;
  }
}
