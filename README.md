# Buscaminas en Jack (Nand2Tetris)

## Integrantes

- Santiago Diaz
- Camila Rodriguez
- Sebastian Gudiño

Este trabajo fue hecho con apoyo de inteligencia artificial. VibeCoded

Juego de Buscaminas hecho en el lenguaje Jack para la plataforma Hack de Nand2Tetris, como proyecto de Organización de Computadores. Corre en el VM Emulator oficial, sobre una pantalla monocromática de 512 × 256 píxeles.

## Cómo se juega

- El tablero tiene 10 × 10 casillas y 10 minas ocultas.
- Con **Enter** se destapa la casilla donde está el cursor. El primer Enter nunca cae en una mina: esa casilla y sus 8 vecinas quedan libres de minas.
- Cada casilla destapada muestra cuántas minas hay a su alrededor (del 1 al 8). Si no tiene ninguna, se destapan en cadena las casillas vecinas.
- Con **B** se pone o se quita una bandera en una casilla cubierta. Una casilla con bandera no se puede destapar.
- Cada casilla destapada suma 1 punto, incluidas las que se abren en cadena.
- **Ganas** ("u win") cuando destapas las 90 casillas sin mina. **Pierdes** ("Perdiste pa") si destapas una mina: en ese caso se muestran todas las minas partidas en dos.

## Teclas

| Tecla | Acción |
|-------|--------|
| `W` `A` `S` `D` | Mover el cursor (arriba, izquierda, abajo, derecha). Funcionan en mayúscula y minúscula. |
| `Enter` | Destapar la casilla del cursor |
| `B` | Poner o quitar bandera |
| `R` | Reiniciar la partida |
| `Esc` | Salir del juego |

Cada pulsación hace una sola acción: si mantienes la tecla presionada no se repite.

## Cómo compilar y ejecutar

Estas instrucciones suponen que ya descargaste y descomprimiste la suite de Nand2Tetris. Dentro de esa carpeta hay una subcarpeta `tools` con los programas `JackCompiler` y `VMEmulator`. Los pasos son para Windows; en Mac o Linux se usan los archivos `.sh` en lugar de los `.bat`.

### 1. Preparar la carpeta

1. Descomprime el `.zip` de la entrega. Obtendrás una carpeta con los archivos `.jack`, los `.vm` y este `README.md`.
2. Copia esa carpeta (por ejemplo, con el nombre `Buscaminas`) dentro de la carpeta `tools` de Nand2Tetris.

### 2. Compilar (opcional)

La entrega ya incluye los archivos `.vm`, así que puedes saltar este paso. Si modificas algún `.jack` o quieres regenerarlos:

1. Abre el Explorador de archivos y entra a la carpeta `tools`.
2. Haz clic en la barra de direcciones, escribe `cmd` y presiona Enter. Se abre una terminal ubicada en `tools`.
3. Escribe `JackCompiler.bat Buscaminas` y presiona Enter. (En Mac o Linux: `./JackCompiler.sh Buscaminas`; si no tiene permiso de ejecución, usa antes `chmod +x JackCompiler.sh`.)
4. Si no aparece ningún mensaje de error, la compilación fue exitosa y la carpeta tendrá un `.vm` por cada clase.

### 3. Ejecutar en el VM Emulator

1. En la carpeta `tools`, haz doble clic en `VMEmulator.bat` (en Mac o Linux, `./VMEmulator.sh`).
2. Presiona el botón de la carpeta (*Load program*) y selecciona la carpeta `Buscaminas`.
3. Si aparece un aviso sobre funciones sin implementación, responde **Yes**: el emulador usa sus funciones integradas del sistema operativo (`Screen`, `Output`, `Keyboard`, etc.).
4. En el menú **Animate**, elige **No animation**. Sin esto el programa corre muy lento.
5. Haz clic en el ícono del teclado que está debajo de la pantalla, para que el emulador reciba las teclas.
6. Presiona el botón **Run** (la doble flecha `>>`) y juega con las teclas de la tabla anterior.

## Estructura del proyecto

| Archivo | Qué hace |
|---------|----------|
| `Main.jack` | Punto de entrada. Crea el juego, lo ejecuta y libera su memoria. |
| `Game.jack` | Ciclo principal del juego: lee el teclado, maneja el estado (jugando, ganó, perdió), el puntaje y el reinicio. |
| `Board.jack` | Tablero 10 × 10: guarda las casillas, coloca las minas tras el primer Enter, calcula las minas vecinas y destapa en cadena con una pila propia. |
| `Cell.jack` | Una casilla: su posición, su estado (mina, destapada, bandera, minas vecinas) y cómo se dibuja. |
| `Cursor.jack` | Marco resaltado que indica la casilla actual y se mueve con `W` `A` `S` `D`. |
| `Panel.jack` | Panel derecho con el título, los datos del tablero, el puntaje, el estado y la leyenda de teclas. |
| `Sprites.jack` | Dibujos de 16 × 16 píxeles (números del 1 al 8, mina, mina partida y bandera) compartidos por todas las casillas. |
| `Stack.jack` | Pila de enteros usada para destapar casillas en cadena sin recursión. |

