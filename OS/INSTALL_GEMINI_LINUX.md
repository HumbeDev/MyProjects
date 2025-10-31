# Cómo Instalar Gemini CLI en Ubuntu usando WSL en Windows 11

Esta guía te mostrará cómo instalar y configurar Gemini CLI en un entorno de Ubuntu a través del Subsistema de Windows para Linux (WSL) en Windows 11.

## Prerrequisitos

Antes de comenzar, asegúrate de tener lo siguiente:

*   **Windows 11:** Tu sistema operativo debe ser Windows 11.
*   **Conexión a Internet:** Necesitarás una conexión a internet para descargar los componentes necesarios.
*   **Permisos de Administrador:** Deberás tener permisos de administrador en tu máquina con Windows 11.

## Paso 1: Instalar el Subsistema de Windows para Linux (WSL)

1.  **Abrir PowerShell como Administrador:**
    *   Haz clic derecho en el botón de Inicio de Windows y selecciona "Windows Terminal (Administrador)" o "PowerShell (Administrador)".
    *   Si se te solicita, permite que la aplicación realice cambios en tu dispositivo.

2.  **Instalar WSL:**
    *   En la ventana de PowerShell, ejecuta el siguiente comando para instalar WSL y los componentes necesarios:
        ```bash
        wsl --install
        ```
    *   Este comando habilitará las características necesarias de Windows, descargará la última versión del kernel de Linux y establecerá WSL 2 como tu versión predeterminada.

3.  **Reiniciar tu Computadora:**
    *   Una vez que el proceso de instalación se complete, reinicia tu computadora para finalizar la instalación.

## Paso 2: Instalar Ubuntu desde la Microsoft Store

1.  **Abrir la Microsoft Store:**
    *   Busca "Microsoft Store" en el menú de Inicio y ábrela.

2.  **Buscar Ubuntu:**
    *   En la barra de búsqueda de la Microsoft Store, escribe "Ubuntu" y presiona Enter.

3.  **Instalar Ubuntu:**
    *   Selecciona la versión de Ubuntu que prefieras (generalmente la última versión LTS es una buena opción) y haz clic en "Obtener" o "Instalar".
    *   Espera a que la descarga e instalación se completen.

## Paso 3: Configurar Ubuntu

1.  **Iniciar Ubuntu por Primera Vez:**
    *   Una vez instalado, puedes iniciar Ubuntu desde el menú de Inicio.
    *   La primera vez que inicies Ubuntu, se te pedirá que crees un nombre de usuario y una contraseña. Estos serán tus credenciales de superusuario (sudo) para el entorno de Ubuntu.

2.  **Actualizar tu Sistema:**
    *   Es una buena práctica actualizar los paquetes de tu sistema. Abre tu terminal de Ubuntu y ejecuta los siguientes comandos:
        ```bash
        sudo apt update
        sudo apt upgrade
        ```

## Paso 4: Instalar Gemini CLI

Actualmente, no existe un "Gemini CLI" oficial de Google para instalar de la manera tradicional. Sin embargo, si te refieres a una herramienta de línea de comandos para interactuar con los modelos de Gemini, generalmente se hace a través de las bibliotecas de cliente de la API de Google en lenguajes de programación como Python.

Aquí te mostramos cómo configurar un entorno de Python para usar la API de Gemini:

1.  **Instalar Python y pip:**
    *   Ubuntu generalmente viene con Python preinstalado. Puedes verificarlo con `python3 --version`.
    *   Asegúrate de tener `pip`, el instalador de paquetes de Python:
        ```bash
        sudo apt install python3-pip
        ```

2.  **Instalar la Biblioteca de Cliente de Google AI para Python:**
    *   Usa `pip` para instalar la biblioteca:
        ```bash
        pip3 install google-generativeai
        ```

3.  **Obtener una Clave de API de Gemini:**
    *   Ve a [Google AI Studio](https://aistudio.google.com/).
    *   Inicia sesión con tu cuenta de Google.
    *   Crea un nuevo proyecto o selecciona uno existente.
    *   Ve a la sección "API Keys" y crea una nueva clave de API.
    *   **¡IMPORTANTE!** Copia y guarda tu clave de API en un lugar seguro. No la compartas públicamente.

4.  **Configurar tu Clave de API:**
    *   Puedes configurar tu clave de API como una variable de entorno en tu terminal de Ubuntu. Esto es más seguro que escribirla directamente en tu código.
        ```bash
        export GOOGLE_API_KEY='TU_CLAVE_DE_API'
        ```
    *   **Nota:** Deberás hacer esto cada vez que abras una nueva terminal, o puedes añadirlo a tu archivo de perfil de shell (como `~/.bashrc` o `~/.zshrc`) para que se cargue automáticamente.

## Paso 5: Verificar la Instalación

Ahora puedes verificar que puedes interactuar con la API de Gemini usando Python.

1.  **Crear un Script de Python:**
    *   Crea un archivo de Python llamado `test_gemini.py`:
        ```bash
        nano test_gemini.py
        ```

2.  **Añadir el Siguiente Código:**
    *   Pega el siguiente código en el editor. Este código utiliza la biblioteca que instalaste para generar texto a partir de un prompt.

    ```python
    import google.generativeai as genai
    import os

    # Configura la clave de API desde la variable de entorno
    genai.configure(api_key=os.environ["GOOGLE_API_KEY"])

    # Crea el modelo
    model = genai.GenerativeModel('gemini-pro')

    # Genera contenido
    response = model.generate_content("Hola, mundo!")

    # Imprime la respuesta
    print(response.text)
    ```

3.  **Ejecutar el Script:**
    *   Guarda el archivo (`Ctrl+O`, `Enter`, `Ctrl+X` en nano) y ejecuta el script desde tu terminal:
        ```bash
        python3 test_gemini.py
        ```

Si todo está configurado correctamente, deberías ver una respuesta generada por el modelo de Gemini en tu terminal.

¡Felicidades! Ahora tienes un entorno de trabajo para interactuar con la API de Gemini desde la línea de comandos en Ubuntu a través de WSL en Windows 11.
