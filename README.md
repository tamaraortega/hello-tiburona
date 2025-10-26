# Soroban Project

## Project Structure

This repository uses the recommended structure for a Soroban project:
```text
.
├── contracts
│   └── hello_world
│       ├── src
│       │   ├── lib.rs
│       │   └── test.rs
│       └── Cargo.toml
├── Cargo.toml
└── README.md
```
# 🦈 hello-tiburona-rust
💬 Un saludo de Tamara

Antes de iniciar, quiero compartir mis reflexiones personales del proceso (La tarea de encuentra al 70%, no he podido implementar pruebas):

## 🏄‍♀️ ¿Qué fue lo más retador?
Que mi version de SDK no es compatible con el codigo de la tarea entonces tuve que hacer algunas modificaciones. 

## 🐇 ¿Qué aprendiste que no esperabas?
Paciencia con los errores y seguir adelante! Hice bastantes anotaciones de recordatorios. 
Aprendi a hacer un readme y subir el repo sola a GitHub!! Espero haberlo subido bien sjs.

## 🏖️ ¿Qué aplicarías en tus propios proyectos?


# 🚀 FASE 1: Verificación de instalaciones y creación del proyecto
🔧 Verificar instalaciones

SOROBAN instalado:
Tuve que instalar Soroban CLI con:


cargo install --locked soroban-cli
soroban --version

RUST instalado:
Ya lo tenía previamente:

rustc --version

😊 Crear el proyecto

Paso 1.1

mkdir proyectos-soroban
cd proyectos-soroban
soroban contract init hello-tiburona
cd hello-tiburona


Paso 1.2: Verificar estructura
En PowerShell ls no funcionó, así que usé Git Bash.

📸 Capturas:
<img width="877" height="448" alt="image" src="https://github.com/user-attachments/assets/5dd3c78f-94f8-4cbd-9035-1cbe5b81b9aa" />
<img width="846" height="318" alt="image" src="https://github.com/user-attachments/assets/563d122d-f3c1-4e08-8c75-632cd995b070" />

Checkpoint 1 ✅

Proyecto creado

VS Code abierto

Carpeta contracts/ visible

# 🧱 FASE 2: Implementar las definiciones base
Paso 2.1: Abrir lib.rs
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/94c772a1-83ce-4be8-8a2c-e97865136a4a" />
Paso 2.2: Imports y setup inicial

Se agregan las importaciones, definición de errores y la DataKey.

Paso 2.3: Definir errores

💡 ¿Por qué cada error tiene un número?
Para usarlos como índice (por ejemplo, “error 3”).

💡 ¿Qué error usarías si alguien intenta resetear el contador sin ser admin?
NoAutorizado.

Paso 2.4: Definir DataKey

pub → el enum es público y puede usarse fuera del módulo.

enum DataKey → define un tipo con varias variantes.

💡 ¿Por qué Admin no tiene parámetros, pero UltimoSaludo sí?
Admin es un dato global único, mientras que UltimoSaludo puede cambiar.

Checkpoint 2 ✅

Imports correctos (incluyendo String)

4 errores definidos

3 keys en DataKey

Estructura creada

Compila con cargo check

💬 Al principio no compilaba, pero corregí typos y comas faltantes:

<img width="1059" height="147" alt="image" src="https://github.com/user-attachments/assets/3266ec2d-7d3d-404a-91c4-cf9b75a40e4d" />
# ⚙️ FASE 3: Implementar initialize()
Paso 3.1: Firma de la función

💡 ¿Por qué retorna Result<(), Error> y no solo ()?
Porque incluir el error facilita entender qué salió mal.

💡 ¿Qué podría fallar en una inicialización?
Que alguien intente inicializar el contrato con otra cuenta.

Paso 3.2 - 3.6

💡 ¿Por qué usar instance storage para Admin?
Para guardar el valor asociado al contrato.

💡 ¿Qué significan los dos 100?
Son unidades de tiempo para el TTL (Time To Live).

📸 Captura:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9427c839-e5f6-4e76-8c84-38d170b7fde5" />

Checkpoint 3 ✅

initialize() implementada

Verifica si ya está inicializado

Guarda admin y contador

Extiende TTL

Compila sin errores

# 💬 FASE 4: Implementar hello()

💡 ¿Por qué retorna Result<Symbol, Error> y no solo Symbol?
Para manejar errores de forma controlada y segura.

💡 ¿Por qué validar la longitud antes de tocar storage?
Porque los errores en blockchain cuestan dinero, así que se evita trabajo innecesario.

📸 Compiló a la primera 🎉
<img width="1020" height="90" alt="image" src="https://github.com/user-attachments/assets/192f8cae-fdac-4bc4-8c6e-7678de42baec" />

Checkpoint 4 ✅

hello() implementada

2 validaciones de input

Contador incrementado

Saludo guardado

TTL extendido

Compila sin errores

# 🔍 FASE 5: Funciones de consulta
Recordatorios importantes

⭐ La flecha (->) indica el tipo de valor que se retorna.
⭐ unwrap() extrae el valor de un Option.
⭐ Option vs Result:

Option → algo puede o no existir (no es error).

Result → algo puede fallar y queremos saber por qué.

Ejemplo:

pub fn get_contador(env: Env) -> u32 {
    env.storage()
        .instance()
        .get(&DataKey::ContadorSaludos)
        .unwrap_or(0) // No hay error
}


📸 Captura:
<img width="941" height="88" alt="image" src="https://github.com/user-attachments/assets/b505fa07-110e-4e1b-85b3-554bc4e48fcd" />

Checkpoint 5 ✅

get_contador() implementado

get_ultimo_saludo() implementado

Entiendes Option vs Result

Compila sin errores

# 🧑‍💼 FASE 6: Función administrativa

💡 Recordatorio:
El operador ? indica “si todo está bien, continúa; si no, detente”.

Checkpoint 6 ✅

reset_contador() implementado

Verifica admin

Control de acceso funcional

Compila sin errores

# 🧪 FASE 7: Pruebas

Aqui vienen los errores, estuve intentando corregir pero al final solo logre que 3 de 7 tests corrieran (agrege uno extra). 
ERROR 1: 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ced26186-68c3-4195-97aa-7406a7604db2" />

ERROR 2: 
<img width="828" height="95" alt="image" src="https://github.com/user-attachments/assets/97c6bea7-ce74-4168-a565-c945e300d9b3" />


Checkpoint 7 

✅6 tests implementados

❌Todos los tests pasan

✅ Entiendes cada test

✅ Casos exitosos y de error verificados


⭐ FASE 8: A penas logre solucionar los tests completo esta fase


![TypingCatTypingGIF](https://github.com/user-attachments/assets/0086e0f2-1edf-4caa-a59b-5aea290cd728)


