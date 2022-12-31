# Bluetooth-LE-BBQ-ProbeE
Reading and parsing a BBQ ProbeE Bluetooth Low Energy Temperature sensor.
Compatible with FMG SH253B Bluetooth BBQ Thermometer: https://www.fmg-tech.com/pid18124267/Bluetooth-Oven-Grill-Kitchen-BBQ-Smoker2022-New-IP67-Waterproof-Wireless-BBQ-Thermometer-Steak-Cooking-Checker.htm

![alt text](https://raw.githubusercontent.com/cvasquez-github/Bluetooth-LE-BBQ-ProbeE/main/bbq-app.png)

- Description Service: 00001800-0000-1000-8000-00805f9b34fb
  - Device Name Characteristic:  00002a00-0000-1000-8000-00805f9b34fb
    - Read Property: BBQ ProbeE 26012
  

- Data Service: 0000fb00-0000-1000-8000-00805f9b34fb
  - Temperature Value Characteristic: 0000fb02-0000-1000-8000-00805f9b34fb
    - Notify Property: FF-FF-80-02-94-02-0C
      - FF-FF-80-02-A8-02-0C
      - FF-FF-80-02-94-02-0C
      - FF-FF-80-02-94-02-0C (24, 27)
      
- Reading Temperature Values (7 bytes data)
  - Temperature 1 (Meat), byte 2 and 4:
    ```
    short temp1 = (short)(bytes[2] | (bytes[3] << 8));
    float temp1Celsius = temp1 / 10.0f - 40.0f;
    ```
      
  - Temperature 2 (Grill), byte 4 and 5:
    ```
    short temp2 = (short)(bytes[4] | (bytes[5] << 8));
    float temp2Celsius = temp2 / 10.0f - 40.0f;
    ```
