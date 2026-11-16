# 🛡️ WearFall

<div align="center">

**Sistema inteligente de detecção de quedas com ESP32 e sensor inercial.**

[![ESP32](https://img.shields.io/badge/Hardware-ESP32-1F6FEB)](https://www.espressif.com/en/products/socs/esp32)
[![Arduino IDE](https://img.shields.io/badge/IDE-Arduino-00979D)](https://www.arduino.cc/en/software)
[![C++](https://img.shields.io/badge/Linguagem-C%2B%2B-00599C)](https://isocpp.org/)
![Status](https://img.shields.io/badge/Status-Prot%C3%B3tipo%20acad%C3%AAmico-yellow)
[![Stars](https://img.shields.io/github/stars/CAIOanx/WearFall?style=social)](https://github.com/CAIOanx/WearFall/stargazers)
[![Forks](https://img.shields.io/github/forks/CAIOanx/WearFall?style=social)](https://github.com/CAIOanx/WearFall/forks)

[**Código**](firmware/Wearfall/Wearfall.ino) · [**Montagem**](docs/README.md) · [**Testes**](testes/README.md) · [**Reportar problema**](https://github.com/CAIOanx/WearFall/issues)

</div>

---

## 📋 Sobre o Projeto

O **WearFall** é um protótipo acadêmico voltado a apoiar o cuidado e a segurança de **pessoas idosas**. Usa um ESP32 e um sensor inercial para identificar eventos compatíveis com quedas. Em vez de considerar somente o impacto, o algoritmo analisa **queda livre, impacto, rotação, postura após o impacto e imobilidade**. A proposta é contribuir para soluções de monitoramento, ainda em fase de validação.

### ✨ Principais Funcionalidades

- 🎯 **Detecção em etapas:** análise temporal de sinais do acelerômetro e do giroscópio.
- ⚡ **Alerta local:** LED e buzzer quando um evento é confirmado.
- 🛑 **Cancelamento:** botão físico para interromper o alerta.
- 💾 **Histórico persistente:** até dez eventos salvos usando Preferences/NVS.
- 📶 **Rede própria:** ESP32 configurado como Access Point (`WearFall_AP`), sem depender de roteador.
- 🖥️ **Painel web local:** consulta a status e eventos pelo navegador.

---

## 🎬 Demonstração

### 🧰 Montagem física do protótipo

<div align="center">
  <img src="docs/screenshots/montagem-prototipo.jpg" alt="Montagem do protótipo WearFall em protoboard com ESP32, sensor inercial, LED e buzzer" width="720">
</div>

### 🎞️ Vídeo do teste de bancada

<div align="center">
  <img src="docs/media/wearfall-demonstracao.gif" alt="GIF do teste físico de bancada do protótipo WearFall" width="720">
</div>

> Esta é uma demonstração do protótipo em bancada. O registro não comprova a detecção confiável de quedas reais nem validação clínica.

### 🖥️ Telas do projeto

**Página inicial — proposta de cuidado e acompanhamento de pessoas idosas**

![Página inicial do site WearFall](docs/screenshots/pagina-inicial.png)

**Tela de entrada — visualização do acesso ao painel**

<div align="center">
  <img src="docs/screenshots/tela-login.png" alt="Tela de login da versão web de apresentação do WearFall" width="440">
</div>

**Dashboard — monitoramento, alertas e histórico**

![Dashboard de monitoramento do WearFall](docs/screenshots/dashboard-monitoramento.png)

> As imagens de página inicial, login e dashboard acima representam a versão web demonstrativa, que usa dados de exemplo. O painel **local** do ESP32, acessível em **http://192.168.4.1** quando conectado à rede `WearFall_AP`, exibe os dados do dispositivo.

Para conhecer a interface de apresentação, consulte [WearFall-Dashboard-Online](https://github.com/CAIOanx/WearFall-Dashboard-Online).

---

## 🛠️ Tecnologias Utilizadas

### Firmware e hardware

- **ESP32** e **Arduino IDE** (C++).
- Sensor inercial com leitura direta dos registradores por **I²C / Wire**.
- **FreeRTOS** para tarefas de amostragem, processamento e controle.
- **Preferences/NVS** para persistência dos eventos.
- **WiFi** e **WebServer** para o painel local.
- LED, buzzer e botão físico.

### Interface

- **HTML, CSS e JavaScript**, incorporados ao firmware pelo arquivo `dashboard_assets.h`.
- Um painel web experimental separado também está disponível em [WearFall-Dashboard-Online](https://github.com/CAIOanx/WearFall-Dashboard-Online).

---

## 🚀 Começando

### 📦 Pré-requisitos

- Uma placa **ESP32 Dev Module** e um cabo USB de dados.
- [Arduino IDE](https://www.arduino.cc/en/software).
- Pacote de placas **esp32 by Espressif Systems**.
- Componentes e ligações descritos na [documentação de montagem](docs/README.md).

### 💻 Instalação

1. Instale e abra o **Arduino IDE**.
2. Em **Arquivo → Preferências**, adicione a URL:
   ```text
   https://espressif.github.io/arduino-esp32/package_esp32_index.json
   ```
3. No **Gerenciador de Placas**, instale **esp32 by Espressif Systems**.
4. Conecte a placa via USB e selecione **ESP32 Dev Module** e a porta correspondente.
5. Abra [`firmware/Wearfall/Wearfall.ino`](firmware/Wearfall/Wearfall.ino) no Arduino IDE. Mantenha o arquivo **`dashboard_assets.h` na mesma pasta**.
6. Clique em **Upload** e, depois, abra o **Monitor Serial em 115200 baud**.

### 🌐 Acesso ao painel

1. Com o ESP32 ligado e o firmware carregado, conecte o celular/notebook à rede **`WearFall_AP`**.
2. Consulte a senha definida em `AP_SENHA` no código.
3. Acesse **http://192.168.4.1** no navegador.

O sensor é lido diretamente por I²C; **não é necessário instalar a biblioteca Adafruit_MPU6050** para este firmware. O módulo físico usado nos testes apresentou `WHO_AM_I = 0x72`, portanto a identificação exata do componente ainda merece verificação.

---

## 📖 Como Usar

O ESP32 começa no estado `MONITORANDO`. Uma sequência compatível com queda inicia a análise; se os critérios são confirmados, o dispositivo entra em `ALERTA`, acende o LED e toca o buzzer. O botão físico cancela o alerta.

Para consultar o histórico pelo **Monitor Serial**, use `H`. Para limpar os eventos salvos, use `L`. A interface web também permite acompanhar o sistema.

### Critérios experimentais da versão de bancada

| Verificação | Parâmetro utilizado |
| --- | --- |
| Queda livre | magnitude abaixo de 0,6 g |
| Impacto | acima de 2,5 g, em até 3 s |
| Rotação | acima de 150 °/s |
| Postura alterada | \|Az\| abaixo de 0,5 g por 800 ms |
| Imobilidade aproximada | magnitude entre 0,85 e 1,15 g por 800 ms |
| Janela pós-impacto | 6 s |

**Atenção:** esses parâmetros são experimentais. Os testes de bancada não comprovam precisão ou confiabilidade em quedas reais.

---

## 🗂️ Estrutura de Pastas

```text
WearFall/
├── firmware/
│   └── Wearfall/
│       ├── Wearfall.ino           # Código do ESP32
│       └── dashboard_assets.h     # HTML, CSS e JS do painel local
├── docs/
│   ├── README.md                  # Montagem e instruções
│   ├── screenshots/
│   │   ├── montagem-prototipo.jpg
│   │   ├── pagina-inicial.png
│   │   ├── tela-login.png
│   │   ├── dashboard-monitoramento.png
│   │   └── README.md
│   └── media/
│       ├── wearfall-demonstracao.gif
│       ├── wearfall-capa.jpg
│       └── README.md
├── testes/
│   └── README.md                  # Registros de bancada
├── imagens/
│   └── README.md                  # Espaço reservado para logo e imagens extras
└── README.md
```

---

## 🧪 Testes

Os testes abaixo **foram relatados como aprovados na validação física de bancada**, até a etapa 2.0D:

| Teste | Verificação | Resultado |
| --- | --- | --- |
| 2.0A | Repouso normal | ✅ Passou |
| 2.0B | Queda confirmada, alerta e cancelamento | ✅ Passou |
| 2.0C | Evento descartado | ✅ Passou |
| 2.0D | Histórico preservado após reinício | ✅ Passou |

Veja [registros e limitações dos testes](testes/README.md). **Não há suíte automatizada nem cobertura de testes publicada**.

---

## 🔮 Próximas Etapas

- 🔋 Adicionar **bateria recarregável** com alimentação e proteção adequadas.
- 🎽 Criar **estrutura compacta vestível na cintura**.
- 🌐 Implementar **comunicação pela internet** para notificar um responsável.
- 📊 Calibrar os limiares e avaliar a detecção na posição final de uso.

Essas funções **ainda não são recursos validados do protótipo atual**.

---

## 🤝 Contribuindo

Sugestões, relatos de problemas e propostas de melhoria podem ser enviados em [Issues](https://github.com/CAIOanx/WearFall/issues). Quem quiser colaborar pode criar um *fork*, propor mudanças em uma *branch* e abrir um *pull request*.

---

## 📄 Licença

**Licença ainda não escolhida.** O repositório está público para consulta, mas a publicação do código não concede automaticamente permissão de cópia, modificação ou redistribuição. Uma licença será adicionada após definição pelos responsáveis pelo projeto.

---

## 👨‍💻 Autor e Projeto

**WearFall — Trabalho de Conclusão de Curso (TCC).**

- GitHub: [@CAIOanx](https://github.com/CAIOanx)
- Código e documentação: [este repositório](https://github.com/CAIOanx/WearFall)

---

## 🙏 Agradecimentos

Agradecimentos aos colaboradores e à orientação acadêmica do TCC.

---

<div align="center">

**WearFall — protótipo acadêmico em desenvolvimento.**

⚠️ Não substitui sistemas profissionais ou certificados de atendimento e monitoramento de emergências.

</div>
