# Mini Tetris con joystick Arduino

Juego web de Tetris en un solo archivo (`index.html`), con HTML, CSS y JavaScript incluidos. Permite jugar con teclado, botones táctiles o un joystick conectado a Arduino mediante USB.

## Requisitos
- Arduino UNO con el joystick conectado: VRX → A0, VRY → A1, SW → D2, VCC → 5V y GND → GND.
- Google Chrome o Microsoft Edge.
- Página abierta desde HTTPS (GitHub Pages) o `localhost`.
- Cable USB de datos.

## Preparar Arduino
Sube este programa al Arduino:

```cpp
const int pinX = A0;
const int pinY = A1;
const int pinSW = 2;

void setup() {
  pinMode(pinSW, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  int valorX = analogRead(pinX);
  int valorY = analogRead(pinY);
  int estadoSW = digitalRead(pinSW);

  Serial.print("X: ");
  Serial.print(valorX);
  Serial.print(" | Y: ");
  Serial.print(valorY);
  Serial.print(" | Botón: ");
  Serial.println(estadoSW);
  delay(100);
}
```

## Cómo jugar con Arduino
1. Sube el programa al Arduino.
2. Cierra el Monitor Serie de Arduino IDE (solo una aplicación puede usar el puerto serie a la vez).
3. Abre el juego en Chrome o Edge.
4. Pulsa **Conectar joystick Arduino** y elige el puerto del Arduino.
5. Pulsa **Empezar**.
6. Inclina el joystick a izquierda/derecha para mover, hacia abajo para bajar la pieza y presiona el botón para girarla.

El juego interpreta el centro del joystick cerca de 512. Si el joystick se mueve solo, se puede ajustar la zona muerta en `handleJoystick()` dentro de `index.html`.

## Publicar en GitHub Pages
Sube `index.html` y `README.md` al repositorio. Luego entra en **Settings → Pages**, selecciona **Deploy from a branch**, rama `main` y carpeta `/ (root)`. GitHub Pages publicará la web en HTTPS.

**Nota:** Web Serial requiere Chrome o Edge y una página segura (HTTPS/localhost). No funciona desde el archivo abierto como `file://` ni desde todos los navegadores.
