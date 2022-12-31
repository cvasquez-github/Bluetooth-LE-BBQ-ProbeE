# Bluetooth-LE-BBQ-ProbeE
Reading and parsing a BBQ ProbeE Bluetooth Low Energy Temperature sensor.

- Compatible with FMG SH253B Bluetooth BBQ Thermometer: https://www.fmg-tech.com/pid18124267/Bluetooth-Oven-Grill-Kitchen-BBQ-Smoker2022-New-IP67-Waterproof-Wireless-BBQ-Thermometer-Steak-Cooking-Checker.htm. 

  - Available at Mercado Libre: https://articulo.mercadolibre.cl/MLC-559743013-termometro-bluetooth-con-app-para-asado-carne-horno-parrilla-_JM#position=41&search_layout=stack&type=item&tracking_id=632057ea-efe6-4621-b7d1-b8afca1f168e

- Important: Pair the Bluetooth temperature sensor with your computer before running the app.

- Make sure your Bluetooth adapter is Bluetooth v5+ compatible (LMP 9 or higher, LMP 11 recommended): https://support.microsoft.com/en-us/windows/what-bluetooth-version-is-on-my-pc-f5d4cff7-c00d-337b-a642-d2d23b082793

  - If you don't have one, something like this cheap one may work: https://articulo.mercadolibre.cl/MLC-575881930-adaptador-transmisor-receptor-bluetooth-50-usb-notebook-pc-_JM

![alt text](https://raw.githubusercontent.com/cvasquez-github/Bluetooth-LE-BBQ-ProbeE/main/bbq-app-ui.png)

- Description Service: 00001800-0000-1000-8000-00805f9b34fb
  - Device Name Characteristic:  00002a00-0000-1000-8000-00805f9b34fb
    - Read Property: BBQ ProbeE 26012
  

- Data Service: 0000fb00-0000-1000-8000-00805f9b34fb
  - Temperature Value Characteristic: 0000fb02-0000-1000-8000-00805f9b34fb
    - Has Notify Property
      
- Reading Temperature Values from the Notify message (7 bytes data, example : FF-FF-80-02-94-02-0C)
  - Temperature 1 (Meat), byte 2 and 3:
    ```
    short temp1 = (short)(bytes[2] | (bytes[3] << 8));
    float temp1Celsius = temp1 / 10.0f - 40.0f;
    ```
      
  - Temperature 2 (Grill), byte 4 and 5:
    ```
    short temp2 = (short)(bytes[4] | (bytes[5] << 8));
    float temp2Celsius = temp2 / 10.0f - 40.0f;
    ```
