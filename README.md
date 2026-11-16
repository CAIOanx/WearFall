# 🛡️ WearFall

**Sistema inteligente de detecção de quedas utilizando ESP32 e sensor inercial.**

---

## 📋 Sobre o Projeto

O **WearFall** é um protótipo de dispositivo vestível desenvolvido para identificar possíveis quedas por meio da análise de aceleração, rotação, postura e imobilidade.

O objetivo é contribuir para a segurança de pessoas que necessitam de monitoramento, oferecendo alertas locais e registro dos eventos detectados.

## ✨ Principais Funcionalidades

- **Detecção de quedas:** análise de queda livre, impacto, rotação, postura e imobilidade.
- **Alerta imediato:** acionamento de LED e buzzer após a confirmação de uma queda.
- **Cancelamento manual:** botão físico para interromper o alerta.
- **Histórico de eventos:** armazenamento das últimas 10 ocorrências.
- **Memória persistente:** preservação do histórico após reinicialização do ESP32.
- **Interface web:** consulta ao estado e histórico por uma rede Wi-Fi criada pelo próprio ESP32.

## 🛠️ Tecnologias Utilizadas

**Hardware:** ESP32, módulo inercial compatível com o mapa de registradores MPU6050, LED, buzzer e botão.

**Software:** Arduino IDE, C++, I2C, FreeRTOS, WiFi, WebServer e Preferences/NVS.

## 🚀 Como Executar

1. Instale o Arduino IDE.
2. Adicione o suporte às placas ESP32 da Espressif.
3. Selecione a placa `ESP32 Dev Module`.
4. Conecte o ESP32 e selecione a porta USB correspondente.
5. Abra o código do projeto na pasta `firmware`.
6. Envie o programa para a placa.
7. Abra o Monitor Serial em `115200 baud`.

Para visualizar a interface, conecte-se à rede `WearFall_AP` e acesse `http://192.168.4.1`.

## 🔌 Conexões do Circuito

| Componente | Conexão no ESP32 |
|---|---|
| Sensor VCC | 3V3 |
| Sensor GND | GND |
| Sensor SDA | GPIO 21 |
| Sensor SCL | GPIO 22 |
| LED | GPIO 4, com resistor de 220 Ω |
| Buzzer | GPIO 18 |
| Botão | GPIO 19 e GND |

## 🧪 Testes Realizados

O protótipo foi testado fisicamente, com os seguintes resultados:

| Teste | Resultado |
|---|---|
| 2.0A — Monitoramento normal | Aprovado |
| 2.0B — Detecção completa de queda | Aprovado |
| 2.0C — Descarte de evento | Aprovado |
| 2.0D — Persistência após reinício | Aprovado |

Os testes foram realizados em condições controladas de bancada. O sistema ainda precisa de validação e calibração para o uso real.

## 🔮 Próximas Etapas

Implementar uma bateria recarregável, desenvolver uma estrutura vestível compacta para uso na cintura e adicionar comunicação via internet para notificar um responsável em caso de queda confirmada.

## ⚠️ Limitações

Atualmente, o dispositivo depende de alimentação externa, não envia notificações remotas e ainda utiliza parâmetros experimentais de detecção.

**O WearFall é um protótipo acadêmico em desenvolvimento e não substitui sistemas certificados de monitoramento ou atendimento de emergências.**

## 👨‍💻 Desenvolvimento

Projeto acadêmico desenvolvido como Trabalho de Conclusão de Curso (TCC).
