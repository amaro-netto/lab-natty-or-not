# **FaceGen Pro: Diário de Engenharia e Arquitetura de Solução**

**Autor:**Amaro Amarante da Silva Netto **Stack:** JavaScript (Vanilla), Tailwind CSS, Firebase, Google Gemini 2.5 Flash. **Contexto:** Desafio "Natural ou Fake Natty?"

## **1\. Introdução: A Tese do Produto**

O mercado está saturado de geradores de imagem "text-to-image". No entanto, identificamos uma lacuna crítica para uso profissional: **Consistência de Identidade (Identity Consistency)**.

**A Hipótese:** É possível criar uma ferramenta web leve (SPA) que utilize a inteligência multimodal do Google Gemini não apenas para gerar imagens, mas para atuar como um "orquestrador" que blinda a identidade do usuário contra as alucinações comuns dos modelos de difusão.

## **2\. A Jornada de Desenvolvimento e Resolução de Problemas**

### **Fase 1: O Problema do "Pose Leakage" (Vazamento de Pose)**

**O Cenário:** Ao implementar a primeira versão do *Face Swap*, notamos um padrão frustrante. Se o usuário enviasse uma *selfie* como referência, o modelo gerava a imagem final também como uma selfie, ignorando o prompt que pedia "corpo inteiro" ou "caminhando na praia".

**Análise Técnica:** Descobrimos que modelos multimodais tendem a ter um viés visual forte. Eles interpretam a imagem de entrada não apenas como "quem é a pessoa", mas "como a foto deve ser".

**A Solução (Arquitetura de Prompt Desacoplado):** Implementamos uma lógica de `System Instruction` dividida:

1. **Instrução de Identidade:** "Extraia a biometria facial da imagem de referência."  
2. **Instrução de Bloqueio:** "IGNORE absolutamente a pose, iluminação e fundo da referência."  
3. **Hierarquia de Comando:** "O texto do usuário é a autoridade suprema para ângulo de câmera e corpo."

### **Fase 2: A Crise dos Filtros de Texto (Prompt Sanitizer)**

**O Cenário:** Usuários tentavam gerar imagens descrevendo a si mesmos: *"Homem loiro de olhos azuis na praia"*. Se a foto de referência fosse de um homem moreno, o modelo entrava em conflito (Hallucination Conflict), gerando artefatos bizarros ou ignorando a referência.

**Solução Criativa (Prompt Studio):** Criamos um agente intermediário, o **Prompt Sanitizer**. Antes da geração, uma chamada silenciosa à API do Gemini reescreve o prompt do usuário, **removendo cirurgicamente** qualquer adjetivo físico facial (cabelo, olhos, idade), deixando apenas o contexto (roupa, cenário). Isso garante que a única fonte de verdade para o rosto seja a imagem.

### **Fase 3: O Desafio Mobile (iOS Safari)**

**O Problema:** A aplicação funcionava perfeitamente em Desktop e Android, mas falhava no iPhone. O botão de download não respondia.

**Debugging e Causa Raiz:** Identificamos que o WebKit (motor do Safari) bloqueia downloads diretos de *Data URIs* (Base64) grandes dentro de contextos de script por segurança.

**Implementação da Correção:** Reescrevemos a camada de exportação para utilizar `Blob` e `ObjectUrl`.

1. Decodificamos a string Base64 para um array de bytes (`Uint8Array`).  
2. Criamos um objeto `Blob` (arquivo virtual na memória RAM).  
3. Geramos uma URL temporária (`blob:https://...`) que o Safari aceita como um arquivo legítimo para download.

### **Fase 4: Inovação com Captura 3D (Photogrammetry-Lite)**

**O Insight:** Fotos 2D achatam o rosto. Em ângulos de perfil, a IA frequentemente errava o formato do nariz, pois a referência frontal não tinha essa informação.

**A Solução Técnica:** Implementamos um módulo de câmera nativa usando a API `navigator.mediaDevices`.

* **Fluxo de UX:** Guiamos o usuário a tirar duas fotos sequenciais (Frente e Perfil).  
* **Processamento em Tempo Real:** Utilizamos um `Canvas` HTML5 oculto para "costurar" (stitch) as duas imagens em uma única textura horizontal.  
* **Resultado:** O Gemini recebe esse mapa visual composto e consegue inferir a volumetria 3D do rosto com precisão assustadora, elevando o nível de realismo ("Fake Natty").

## **3\. Arquitetura de Código e Estabilidade**

Para garantir a manutenibilidade de uma aplicação complexa em um único arquivo:

* **Estado Global Centralizado:** Uso de variáveis de estado (`currentUser`, `selectedFaces`, `promptInputMode`) para gerenciar a reatividade da UI.  
* **Guard Clauses:** Prevenção de erros de "null pointer" verificando a existência de elementos DOM antes da atracação de eventos.  
* **Isolamento de Contexto:** Cada ferramenta (Gerador, Editor, Prompt Studio) possui suas próprias definições de variáveis locais dentro das funções assíncronas, evitando vazamento de escopo.

## **4\. Conclusão**

O FaceGen Pro não é apenas um wrapper de API. É uma solução de engenharia que resolve problemas reais de consistência em IA Generativa através de um pipeline inteligente de pré-processamento (Sanitizer/Vision Analyst), processamento controlado (System Instructions) e pós-processamento (Inpainting/Editor), entregando uma ferramenta robusta para criadores de conteúdo.

