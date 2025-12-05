# **FaceGen Pro: Diário de Engenharia e Arquitetura de Solução**

**Autor:** Amaro Amarante da Silva Netto  
**Stack:** JavaScript (Vanilla), Tailwind CSS, Firebase, Google Gemini 2.5 Flash.  
**Versão Atual:** v3.9 Identity Lock

## **1\. Introdução: A Tese do Produto**

O mercado está saturado de geradores de imagem "text-to-image". No entanto, identificamos uma lacuna crítica para uso profissional: **Consistência de Identidade (Identity Consistency)** e **Aplicação de Branding**.

**A Hipótese:** É possível criar uma ferramenta web leve (SPA) que utilize a inteligência multimodal do Google Gemini não apenas para gerar imagens, mas para atuar como um "orquestrador" que blinda a identidade do usuário contra as alucinações comuns dos modelos de difusão.

## **2\. A Jornada de Desenvolvimento e Resolução de Problemas**

### **Fase 1: O Problema do "Pose Leakage" (Vazamento de Pose)**

**O Cenário:** Ao implementar a primeira versão do *Face Swap*, notamos um padrão frustrante. Se o usuário enviasse uma *selfie* como referência, o modelo gerava a imagem final também como uma selfie, ignorando o prompt que pedia "corpo inteiro" ou "caminhando na praia".

**A Solução (Arquitetura de Prompt Desacoplado):** Implementamos uma lógica de `System Instruction` dividida:
1. **Instrução de Identidade:** "Extraia a biometria facial da imagem de referência."  
2. **Instrução de Bloqueio:** "IGNORE absolutamente a pose, iluminação e fundo da referência."

### **Fase 2: A Crise dos Filtros de Texto (Prompt Sanitizer v1)**

**O Cenário:** Usuários tentavam gerar imagens descrevendo a si mesmos: *"Homem loiro de olhos azuis"*. Se a foto de referência fosse de um homem moreno, o modelo entrava em conflito (Hallucination Conflict), gerando artefatos bizarros.

**Solução:** Criamos um agente intermediário simples para remover adjetivos conflitantes.

### **Fase 3: O Desafio Mobile (iOS Safari)**

**O Problema:** O WebKit bloqueava downloads diretos de *Data URIs* grandes.
**Correção:** Implementação de `Blob` e `ObjectUrl` para criar URLs temporárias seguras para download.

### **Fase 4: Inovação com Captura 3D (Photogrammetry-Lite) & Mobile Native**

**O Insight:** Fotos 2D achatam o rosto. Além disso, câmeras de celular aplicavam um "zoom" digital indesejado ao solicitar resoluções fixas (ex: 1280x720).

**A Solução Técnica:** * **Full Sensor Readout:** Removemos restrições de resolução (`width/height`) no `getUserMedia`, solicitando apenas `facingMode: "user"`. Isso força o navegador a entregar o campo de visão máximo do sensor do celular.
* **Stitching 9:8:** O algoritmo captura duas fatias verticais (9:16) e as une, criando uma textura final na proporção 9:8, ideal para a IA entender a volumetria sem distorção.

### **Fase 5: O Pivô para Branding (Modo Logo)**

**O Problema:** Ao tentar usar a ferramenta para criar artes de marketing, a IA tentava encontrar "olhos e boca" em logotipos, gerando aberrações visuais.

**A Solução (Branching Logic):** Implementamos uma ramificação no código. Se o item selecionado for marcado como "Logo":
1. A *System Instruction* muda de "Transferência Facial" para "Integração Artística".
2. A IA é instruída a usar as cores e formas da logo como **matéria-prima** para o cenário (ex: luzes neon, arquitetura), em vez de tentar "colar" a imagem.

### **Fase 6: O "Genetic Firewall" e a Hierarquia da Verdade (v3.9)**

**O Desafio Crítico:** Mesmo com instruções, se o usuário digitasse "Olhos verdes" e a foto tivesse olhos castanhos, a IA deformava a estrutura óssea do rosto tentando resolver o conflito impossível.

**A Solução Definitiva (Pipeline de 3 Estágios):**
1.  **Genetic Firewall (Agente Sanitizador):** Antes de gerar a imagem, um agente de IA lê o prompt do usuário e **deleta** qualquer menção a genética (cor de olhos, cabelo, pele, etnia), mantendo apenas roupas e cenário.
2.  **Negative Prompt Dinâmico:** O sistema injeta automaticamente termos como `wrong eye color` e `face morphing` nos parâmetros negativos.
3.  **Hierarquia de Verdade:** A instrução final para o gerador impõe que a **Imagem de Referência é a autoridade absoluta** sobre a estrutura facial, enquanto o **Texto (Sanitizado)** governa apenas o estilo.

## **3\. Conclusão**

O FaceGen Pro v3.9 evoluiu de um simples gerador para uma suíte de engenharia de prompt. A introdução do **Genetic Firewall** prova que, para obter consistência profissional em IA, é necessário controlar a entrada de dados (Input) com tanto rigor quanto o modelo de processamento.
