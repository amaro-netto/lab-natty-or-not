# FaceGen Pro v3.9: Identity Lock & Branding Suite

![Badge Gemini](https://img.shields.io/badge/AI-Gemini%202.5%20Flash-blue?style=for-the-badge&logo=google)
![Badge Firebase](https://img.shields.io/badge/Backend-Firebase-orange?style=for-the-badge&logo=firebase)
![Badge Status](https://img.shields.io/badge/Project-Genetic%20Firewall-red?style=for-the-badge)

> **Projeto desenvolvido para o Desafio DIO: "Natural ou Fake Natty?"**

## Descrição

O **FaceGen Pro v3.9** é uma aplicação web (SPA) de engenharia de prompt assistida. Ela resolve o trilema da geração de imagens com IA: **Consistência Facial**, **Conflito de Prompt** e **Aplicação de Marca (Branding)**.

Utilizando um pipeline de múltiplos agentes (Sanitizador -> Gerador), a ferramenta garante que a identidade visual (seja um rosto humano ou uma logo corporativa) seja preservada, independentemente do que o usuário digite no texto.

## Funcionalidades Chave (v3.9)

### 🧬 1. Genetic Firewall (Novo!)
O maior problema da IA é quando o texto contradiz a imagem (ex: texto pede "olhos azuis", foto tem "olhos castanhos"). Isso deforma o rosto.
* **Solução:** Um agente de IA intercepta o prompt do usuário *antes* da geração e **remove cirurgicamente** qualquer descrição genética (olhos, cabelo, pele), garantindo que a única fonte de verdade para o rosto seja a foto de referência.

### 🛡️ 2. Identity Lock Protocol
Uma "Hierarquia da Verdade" injetada no sistema:
1.  **Imagem de Referência:** Autoridade absoluta sobre estrutura óssea e genética.
2.  **Texto Sanitizado:** Autoridade sobre iluminação, roupa e cenário.

### 🎨 3. Branding Mode (Suporte a Logos)
Lógica dedicada para marcas. Ao selecionar "Logo":
* A IA não busca traços faciais.
* A logo é usada como **inspiração arquitetônica e de iluminação** (ex: transformar a logo em um letreiro neon cyberpunk ou integrá-la ao tecido de uma roupa).

### 📸 4. Câmera 3D "Mobile First"
* **Full Sensor Readout:** Acesso direto ao hardware da câmera sem cortes de resolução, evitando o efeito de "zoom" em celulares.
* **Guia WYSIWYG:** Máscara visual com sombra que mostra exatamente a proporção 9:16 que será capturada.
* **Saída 9:8:** Fusão inteligente de duas capturas verticais para criar uma textura de alta fidelidade para a IA.

## Tecnologias Utilizadas
* **Frontend:** HTML5, TailwindCSS, Vanilla JS.
* **AI Orchestration:** Google Gemini API (`gemini-2.5-flash`).
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

Com a implementação do **Genetic Firewall** na versão 3.9, eliminamos a principal causa de "estranheza" (Uncanny Valley): a deformação causada por prompts conflitantes. 

Ao forçar a IA a ignorar descrições textuais sobre o rosto e focar exclusivamente na geometria da foto enviada, o resultado mantém a micro-expressão e a identidade da pessoa, enquanto a veste e ilumina de forma completamente sintética.

---
⌨️ Desenvolvido por Amaro Netto
