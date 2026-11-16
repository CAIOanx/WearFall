# 📘 Montagem e documentação

## Ligações do protótipo

| Componente | Pino | ESP32 |
| --- | --- | --- |
| Sensor inercial | VCC | 3V3 |
| Sensor inercial | GND | GND |
| Sensor inercial | SDA | GPIO 21 |
| Sensor inercial | SCL | GPIO 22 |
| LED | positivo | GPIO 4 via resistor de 220 Ω |
| LED | negativo | GND |
| Buzzer do protótipo | positivo | GPIO 18 |
| Buzzer do protótipo | negativo | GND |
| Botão | um terminal | GPIO 19 |
| Botão | contato que fecha ao pressionar | GND |

A conexão direta do buzzer considera **o mesmo buzzer de baixo consumo validado na bancada**. Outros modelos podem exigir um estágio de acionamento. Desligue a alimentação USB antes de refazer conexões.

## Execução

O programa principal está em [`firmware/Wearfall/Wearfall.ino`](../firmware/Wearfall/Wearfall.ino). Abra no Arduino IDE, mantendo `dashboard_assets.h` na mesma pasta, selecione **ESP32 Dev Module** e monitore em **115200 baud**.

Conecte-se a `WearFall_AP` e abra `http://192.168.4.1` para usar a interface local.

## Estado do projeto

A montagem foi validada em bancada. **Bateria, encapsulamento de cintura e envio remoto de alertas ainda são etapas futuras.**
