<div align="center">

# HOPE

### Assistente de IA com personalidade de VTuber

Uma assistente virtual desenvolvida em Python capaz de conversar naturalmente em português, responder por voz, pesquisar na internet e interagir em tempo real com um avatar no VTube Studio.

<br>

<img src="./assets/foto-hope.png" alt="HOPE - VTuber AI Assistant" width="850">

<br><br>

[▶️ Assistir à demonstração da HOPE]


https://github.com/user-attachments/assets/07b05c2f-b707-42f2-8ec9-12e7914d2223



</div>

---

# Sobre o projeto

A **HOPE** foi criada para aproximar inteligência artificial de uma experiência mais humana.

Mais do que um chatbot, ela possui voz, memória de conversa, pesquisa na internet, integração com modelos locais e em nuvem, além de controlar um avatar no **VTube Studio**, tornando as interações muito mais naturais.

Toda a arquitetura foi pensada para funcionar de forma resiliente, utilizando sistemas de fallback quando algum serviço externo fica indisponível.

---

# Como a HOPE funciona

A interação pode acontecer por texto ou voz.

Após receber uma mensagem, a HOPE interpreta o contexto, consulta sua memória recente, realiza pesquisas na internet quando necessário e gera uma resposta utilizando modelos de linguagem locais ou em nuvem.

O texto é convertido em voz, enviado para o VTube Studio e sincronizado automaticamente com o avatar.

```text
Usuário fala ou digita
          ↓
Reconhecimento de fala (Speech Recognition)
          ↓
Memória da conversa
          ↓
Pesquisa Web / Clima (quando necessário)
          ↓
Modelo de IA
(OpenRouter → fallback Ollama)
          ↓
Resposta
          ↓
Síntese de Voz
(ElevenLabs → fallback Edge TTS)
          ↓
VB-CABLE
          ↓
VTube Studio
(Lip Sync + Expressões)
```

---

# Principais recursos

### Inteligência Artificial

- Conversação em português.
- Suporte a múltiplos provedores de LLM.
- Pesquisa automática na internet.
- Consulta de clima em tempo real.
- Memória curta de conversação.
- Prompt personalizado para personalidade.
- Fallback automático entre provedores.

### Voz

- Respostas por voz.
- Múltiplos provedores de TTS.
- Voz natural utilizando ElevenLabs.
- Ajuste de expressividade da voz.
- Fallback automático para Edge TTS.

### Reconhecimento de fala

- Entrada por microfone.
- Palavra de ativação.
- Ajuste de sensibilidade.
- Configuração de dispositivo de áudio.

### Avatar

- Integração completa com VTube Studio.
- Controle de expressões.
- Lip Sync automático.
- Movimentação durante a fala.

### Monitoramento

- Medição do tempo de resposta.
- Scripts de teste para microfone e TTS.

---

# Inteligência Artificial

A HOPE suporta diferentes provedores de modelos de linguagem.

## Provedores

- OpenRouter
- Groq
- Ollama

Atualmente o projeto utiliza **OpenRouter** como provedor principal para obter respostas mais rápidas.

Caso o serviço fique indisponível, a HOPE alterna automaticamente para um modelo executado localmente pelo **Ollama**.

---

# Pesquisa Web e Clima

A assistente pode pesquisar informações recentes automaticamente quando necessário.

Também possui integração com a API pública do **Open-Meteo**, permitindo responder perguntas como:

- Temperatura atual
- Condições climáticas
- Previsão resumida

Além disso, entende perguntas em sequência.

Exemplo:

```text
Usuário:
Clima

HOPE:
De qual cidade?

Usuário:
Brasília

HOPE:
Hoje em Brasília...
```

---

# Voz (TTS)

A HOPE suporta diversos motores de síntese de voz.

## Provedores

- ElevenLabs
- Edge TTS
- Microsoft SAPI
- Murf AI
- Voicebox (experimental)

### Configuração atual

**Provedor principal**

- ElevenLabs

**Modelo**

- eleven_flash_v2_5

**Voz**

- Jessica — Playful, Bright, Warm

**Expressividade**

```
ELEVENLABS_STYLE = 0.35
```

Caso a ElevenLabs fique indisponível, o sistema utiliza automaticamente o **Edge TTS**.

---

# Reconhecimento de fala (STT)

O reconhecimento de voz foi ajustado para reduzir falsos positivos e melhorar a experiência durante conversas.

### Configuração atual

```
Microfone:
USB AUDIO

Timeout:
10 segundos

Phrase Time Limit:
5 segundos

Energy Threshold:
450
```

Também foram criados scripts específicos para calibração do microfone.

- test_stt_capture.py
- test_mic_levels.py

---

# Palavra de ativação

A HOPE possui sistema de Wake Word.

Após diversos testes foi observado que "Hope" apresentava baixa taxa de reconhecimento.

Hoje a chamada principal é:

- Assistente

Também reconhece:

- Assiste

Exemplos:

```
Assistente
```

↓

```
Sim, estou aqui!
```

ou

```
Assistente, tudo bem?
```

↓

A HOPE entende apenas "tudo bem?" como comando.

---

# Integração com o VTube Studio

A comunicação acontece através da API pública do VTube Studio utilizando WebSocket.

Durante as respostas, a HOPE pode:

- alterar expressões;
- acionar hotkeys;
- movimentar o rosto;
- sincronizar a boca automaticamente.

Parâmetros utilizados:

- FaceAngleX
- FaceAngleY
- FaceAngleZ
- FacePositionX
- FacePositionY

O lip sync acontece através do áudio enviado para o **VB-CABLE**, permitindo que o VTube Studio utilize a própria voz da assistente para movimentar a boca.

---

# Tecnologias utilizadas

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/OpenRouter-6C47FF?style=for-the-badge">
  <img src="https://img.shields.io/badge/Groq-F55036?style=for-the-badge">
  <img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white">
  <img src="https://img.shields.io/badge/ElevenLabs-000000?style=for-the-badge">
  <img src="https://img.shields.io/badge/VTube_Studio-FF6B9D?style=for-the-badge">
  <img src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socketdotio&logoColor=white">
</p>

### Principais tecnologias

- Python
- OpenRouter
- Groq
- Ollama
- ElevenLabs
- Edge TTS
- Microsoft SAPI
- Murf AI
- Speech Recognition
- Open-Meteo
- WebSocket
- VTube Studio API
- VB-CABLE

---

# Scripts auxiliares

O projeto também possui diversos scripts para testes individuais dos componentes.

| Script | Função |
|---------|--------|
| test_stt_capture.py | Testa reconhecimento de voz |
| test_mic_levels.py | Mede intensidade do microfone |
| test_voicebox_tts.py | Testes de síntese de voz |
| web_search.py | Pesquisa web e consulta clima |

---

# Roadmap

- Memória de longo prazo
- Reconhecimento emocional avançado
- Expressões mais naturais
- Sistema de emoções persistentes
- Visão computacional
- Integração com plataformas de streaming
- Leitura de chat em tempo real
- Sistema de plugins
- Personalidade dinâmica baseada em contexto

---

# Status

🚧 Projeto em desenvolvimento ativo.

A HOPE continua evoluindo com foco em criar uma assistente virtual cada vez mais natural, rápida e expressiva, explorando integração entre inteligência artificial, síntese de voz e avatares virtuais.

---

<div align="center">

Desenvolvido por **Emanuel Penna**

</div>
