# Simulador Balístico 3D
> ⚠️ **Propósito:** O projeto foi desenvolvido originalmente como parte prática para a disciplina de Computação Gráfica.

O objetivo principal era aplicar fundamentos avançados de renderização 3D na Web e aprender boas práticas de integração entre bibliotecas gráficas e motores de física. O simulador recria um estande de tiro com uma proposta técnica rigorosa: ir além da movimentação tradicional de um FPS arcade e exigir que o jogador lide com cálculos reais de balística, gravidade e física de corpos rígidos operando nativamente no navegador.

---

Um ambiente de simulação em primeira pessoa focado no estudo de balística computacional e geração procedural de cenários, explorando a integração entre a pipeline de renderização do **Three.js** e a simulação física do **Cannon.js**.

<div align="center">
  <img src="https://github.com/user-attachments/assets/6fa663ab-84bd-4789-a2fc-679b62bfa43a" width="45%" />
  <img src="https://github.com/user-attachments/assets/f4086f6a-9fcc-4937-b899-ea5a3f05fabf" width="45%" />
  
</div>

## Arquitetura

Diferente de shooters arcades que utilizam *raycasting* linear para detecção de acertos, este simulador implementa física realística para cada projétil disparado, operando sobre um mundo gerado dinamicamente.

* **Geração Procedural:** O cenário é instanciado e destruído dinamicamente em blocos (*chunks*) com base nas coordenadas do jogador. Esta técnica de culling otimiza o uso de memória e processamento, permitindo a exploração contínua sem degradação do *framerate*.
* **Física Aplicada e Balística:** Os projéteis possuem massa e são afetados pela gravidade em tempo real. O comportamento balístico exige que o operador calcule e compense ativamente a queda do projétil (*bullet drop*) para engajar alvos a longas distâncias (100m, 200m, 400m+).
* **Colisões (Hitboxes):** O carregamento de modelos 3D (`.obj` e mapas de materiais `.mtl`) ocorre de forma assíncrona. O motor físico calcula algoritmicamente as malhas de colisão para envelopar os modelos visuais de forma exata, garantindo detecção precisa mesmo em superfícies diagonais ou irregulares.
* **Ferramental de Debug/Raio-X:** Sistema nativo integrado para visualização e calibração da física. Ativa a renderização dos *wireframes* de colisão sobrepostos aos modelos renderizados, facilitando o isolamento de bugs de contato.
* **Câmera:** Gerenciamento fluido entre diferentes contextos de visualização, permitindo a transição livre entre a inspeção de ambiente (`OrbitControls`) e a operação travada em primeira pessoa (`PointerLockControls`).

## Gráfico Balístico Interativo

O simulador conta com um sistema gráficos em tempo real, projetado para fornecer feedback analítico imediato sobre o comportamento dos disparos e a performance da simulação. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/2382f569-47ee-4f99-94bc-5af257c5788a" width="70%" alt="Gráfico Interativo e Telemetria do Simulador" />
</div>


## Stack Tecnológico

A aplicação foi construída utilizando tecnologias web padrão, sem dependência de engines compiladas, rodando inteiramente via JavaScript no lado do cliente.

* **JavaScript (ES6+)**
* **Three.js:** Renderização WebGL, manipulação de malhas, luzes e shaders.
* **Cannon.js:** Detecção de colisão, física de corpos rígidos e aplicação de vetores de força.
