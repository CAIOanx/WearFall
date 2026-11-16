# 🧪 Testes físicos — WearFall

Registro resumido das verificações realizadas e informadas no desenvolvimento do protótipo:

| Etapa | Objetivo | Resultado informado |
| --- | --- | --- |
| 2.0A | Monitoramento normal sem alerta indevido | PASSOU |
| 2.0B | Sequência completa de queda, alerta, botão, página e histórico | PASSOU |
| 2.0C | Evento sem todos os critérios, descartado sem alerta | PASSOU |
| 2.0D | Recuperar histórico e sequência após reinicialização do ESP32 | PASSOU |

Outros testes anteriores cobriram leitura I²C, acelerômetro, giroscópio, queda livre, impacto, postura, imobilidade, atuadores, página local e `Preferences/NVS`.

## Escopo e limitações

- Testes executados com manipulação manual do sensor em **bancada**.
- Ainda não representam validação clínica, testes com pessoas caindo nem estimativas estatísticas de sensibilidade/especificidade.
- Os parâmetros de 0,6 g, 2,5 g, 150 °/s e os intervalos temporais ainda requerem calibração no formato vestível final.
- A confirmação por magnitude próxima de 1 g é uma aproximação de imobilidade e poderá ser aprimorada.
- A versão `2.3` encontrada no repositório de firmware foi incorporada como arquivo de referência. **Não se afirma aqui que todas as mudanças dessa versão passaram pelos testes 2.0A–2.0D.**
