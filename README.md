# Projeto Unidade 1 - Controle de LED via MQTT5 no ESP32

Repositório do projeto: [https://github.com/VicRyan007/MQTT-example](https://github.com/VicRyan007/MQTT-example)

## Descrição
Este projeto implementa um cliente MQTT5 no ESP32 utilizando o ESP-IDF. O dispositivo se inscreve no tópico `/ifpe/ads/embarcados/esp32/led` e controla o LED onboard (GPIO2) conforme os comandos recebidos:
- Envie `1` para acender o LED
- Envie `0` para apagar o LED

O broker utilizado e validado é: `mqtt://test.mosquitto.org`

## Passos para rodar e testar o projeto

### 1. Pré-requisitos
- ESP-IDF instalado e configurado ([guia oficial](https://docs.espressif.com/projects/esp-idf/pt/latest/esp32/get-started/))
- Placa ESP32 conectada ao computador
- Acesso à internet via Wi-Fi 2.4GHz

### 2. Clonando o projeto
```sh
git clone https://github.com/VicRyan007/MQTT-example.git
cd mqtt5
```

### 3. Configurando o Wi-Fi e o broker (menuconfig)
Execute:
```sh
idf.py menuconfig
```
- Em **Example Connection Configuration**:
  - Configure o **WiFi SSID** (nome da sua rede Wi-Fi)
  - Configure o **WiFi Password** (senha da sua rede)
- Em **Example Configuration**:
  - Em **Broker URL**, coloque:
    ```
    mqtt://test.mosquitto.org
    ```
- Salve e saia

> É fundamental que o ESP32 e o cliente MQTT (MQTT Explorer) estejam usando o mesmo broker (`test.mosquitto.org`) e a mesma porta (`1883`).

### 4. Compilando e gravando no ESP32
```sh
idf.py build
idf.py -p COMx flash
idf.py -p COMx monitor
```
(Substitua `COMx` pela porta correta do seu ESP32, ex: COM3, COM8, etc.)

### 5. Testando o projeto

#### Usando o MQTT Explorer
1. Baixe e instale: https://mqtt-explorer.com/
2. Configure:
   - **Host:** `test.mosquitto.org`
   - **Port:** `1883`
   - **Tópico:** `/ifpe/ads/embarcados/esp32/led`
   - **Payload:** `1` (para acender) ou `0` (para apagar)
   - **Modo:** `raw`
3. Clique em **PUBLISH**

### 6. Observando o resultado
- O LED azul (GPIO2) do ESP32 deve acender/apagar conforme o comando.
- No monitor serial, aparecerão mensagens como:
  ```
  TOPIC=/ifpe/ads/embarcados/esp32/led
  DATA=1
  LED ACESO
  ```

## Estrutura do projeto
- `main/app_main.c`: Código principal do controle do LED via MQTT
- `sdkconfig`: Configurações do projeto
- `README.md`: Este guia

## Observações
- Não envie a pasta `build/` para o repositório.
- Inclua o link do vídeo de demonstração no README, se solicitado.

---

Projeto referente à Unidade 1 de Sistemas Embarcados.

## Funcionamento
- O ESP32 conecta ao Wi-Fi, se inscreve no tópico MQTT e aguarda comandos.
- Ao receber `1`, acende o LED (GPIO2). Ao receber `0`, apaga o LED.

## Código-fonte
- O arquivo principal é `main/app_main.c`.
- O código está comentado para facilitar o entendimento.

## Vídeo de demonstração
Inclua aqui o link do vídeo mostrando o funcionamento do projeto.