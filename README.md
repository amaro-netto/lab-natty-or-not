# FaceGen Pro v4.7: Identity Lock, Branding & Studio Suite

![Badge Gemini](https://img.shields.io/badge/AI-Gemini%202.5%20Flash-blue?style=for-the-badge&logo=google)
![Badge Firebase](https://img.shields.io/badge/Backend-Firebase-orange?style=for-the-badge&logo=firebase)
![Badge Status](https://img.shields.io/badge/Project-Genetic%20Firewall-red?style=for-the-badge)

> **Projeto desenvolvido para o Desafio DIO: "Natural ou Fake Natty?"**

## Descrição

O **FaceGen Pro v4.7** é uma aplicação web (SPA) de engenharia de prompt assistida e geração multimodal. Ela resolve o trilema da geração de imagens com IA: **Consistência Facial**, **Conflito de Prompt** e **Alucinação de Layout**.

Utilizando um pipeline de múltiplos agentes (Sanitizador -> Gerador -> Editor), a ferramenta garante que a identidade visual (seja um rosto humano, um casal ou uma logo corporativa) seja preservada, independentemente do que o usuário digite no texto.

## Funcionalidades Chave (v4.7)

### 🧬 1. Genetic Firewall
O maior problema da IA é quando o texto contradiz a imagem.
* **Solução:** Um agente de IA intercepta o prompt do usuário *antes* da geração e **remove cirurgicamente** qualquer descrição genética (olhos, cabelo, pele), garantindo que a única fonte de verdade para o rosto seja a foto de referência.

### 🛡️ 2. Identity Lock Protocol
Uma "Hierarquia da Verdade" injetada no sistema:
1.  **Imagem de Referência:** Autoridade absoluta sobre estrutura óssea e genética.
2.  **Texto Sanitizado:** Autoridade sobre iluminação, roupa e cenário.

### 🖼️ 3. Composition Enforcement (Anti-Split) (Novo!)
Resolve o problema de imagens saindo divididas ou duplicadas quando a referência é uma montagem (frente/perfil).
* **Solução:** Uma regra de sistema força a IA a ignorar o layout da imagem de referência e gerar uma cena única e contínua, cinematográfica, sem bordas ou divisões.

### 👥 4. Dual Subject Intelligence (Casais) (Novo!)
Lógica específica para quando o usuário seleciona dois rostos.
* **Solução:** O sistema ativa o "Dual Subject Mode", instruindo o gerador a criar duas figuras corporais distintas ("Figura A" e "Figura B") e impedir a fusão de identidades, permitindo *face swap* preciso em fotos de casais.

### 🎨 5. Branding Mode & Prompt Studio
* **Branding:** Transforma logos em elementos arquitetônicos ou de iluminação na cena.
* **Prompt Studio:** Ferramenta integrada que permite fazer upload de uma imagem de estilo e obter a engenharia reversa do prompt (Vision Analysis) ou construir prompts complexos via interface visual.

### 📸 6. Câmera 3D "Mobile First"
* **Full Sensor Readout:** Acesso direto ao hardware da câmera sem cortes de resolução.
* **Stitching 9:8:** Fusão inteligente de duas capturas verticais para criar uma textura de alta fidelidade para a IA.

## Tecnologias Utilizadas
* **Frontend:** HTML5, TailwindCSS, Vanilla JS.
* **AI Orchestration:** Google Gemini API (`gemini-2.5-flash` text & vision).
* **Backend:** Firebase Firestore & Auth.
* **Hardware:** API `MediaDevices` com seleção de `facingMode`.

### Screenshots

| Gerador (Identity Lock) | Modo Branding (Logo) | Câmera 3D (Mobile) |
|:-----------------------:|:--------------------:|:------------------:|
| <img src="assets/gerador.png" style="max-height: 500px;"> | <img src="assets/logo_mode.png" style="max-height: 500px;"> | <img src="assets/camera_mobile.jpg" style="max-height: 500px;"> |

> [!NOTE]
> A interface foi otimizada para remover proporções que causam alucinação (como 16:9 para retratos), focando em 1:1, 4:5 e 9:16.

## Resultados: Natural ou Fake Natty?

**Veredito: Fake Natty Indetectável.**

Com a implementação do **Composition Enforcement** na versão 4.7, eliminamos não apenas a deformação facial, mas também as falhas estruturais (imagens divididas). O **FaceGen Pro** agora consegue gerar cenas complexas de casais ou retratos artísticos mantendo a identidade intacta e uma composição de imagem perfeitamente orgânica.

---
⌨️ Desenvolvido por Amaro Netto