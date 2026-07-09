# TFG: Desarrollo de Realidad Aumentada e interacción con Escenarios Virtuales para el Pilotaje de Drones en el Drone Engineering Ecosystem
El presente proyecto aborda el diseño y desarrollo de solución de realidad aumentada integrada en el DEE. Sobre esta base se han desarrollado distintos escenarios interactivos con sus propias mecánicas de juego. En estos escenarios, sobre el vídeo en primera persona que transmite la cámara del dron se superponen objetos virtuales con los que el piloto puede interactuar al volar como aros, arcos o túneles que el dron debe atravesar, gemas repartidas por el espacio que se destruyen al colisionar contra ellas o al dispararles, y paredes que forman un laberinto por el que el dron deberá explorar. Con todo esto, el piloto verá el entorno real, el DronLab, enriquecido con estos elementos. Cada escenario tendrá su propia mecánica de juego, que podrá ser recorrer un circuito, recoger gemas para acumular puntos o salir de un laberinto antes de que se acabe el tiempo. Además se ha desarrollado la posibilidad de que el propio usuario cree escenarios personalizados.
Por otro lado, también se han desarrollado dos aplicaciones web:
- WebApp de VideoStreaming: que permite visualizar el vídeo de recibido de la cámara del dron con los objetos virtuales superpuestos desde cualquier dispositivo con conexión a Internet.
- WebApp de Control: Qué además de ver vídeo permite controlar el dron de forma remota. 

En este repositorio se puede encontrar todo el material necesario para probar el funcionamiento del proyecto y continuar con su desarrollo.
- `Proyecto de Unity`: Aquí está todo el proyecto como tal (comprimido en un zip) que se puede abrir en Unity . El zip se llama TFG_AR-code.zip y el link para descargarlo se puede encontrar más abajo en la sección de Links. 
- `webapp-code`: Aquí está el código fuente de las WebApps desarrolladas.
- `csDronLink-code`: Aquí está el código fuente de la librería csDronLink.
- `Consideraciones Previas`: Algunas cosas a tener en cuenta antes de probar el proyecto. 
- `Links`: Aquí hay enlaces para acceder a el report donde hay información más detallada del desarrollo del proyecto y enlaces a vídeos con demostraciones de la aplicación final en uso.


# Proyecto de Unity
Al descargar y descomprimir el TFG_AR-code.zip, entre las carpetas más importamtes que nos encontraremos están:
- `ProjectSettings`: Configuración del proyecto: ajustes de físicas, calidad, capas, input, etc.
- `Packages`: Paquetes y dependencias que utiliza el proyecto.
- `Assets`: Contenido principal del proyecto: escenas, scripts, modelos, texturas, materiales y prefabs.

La carpeta Assets es la más importante porque es donde está todo el contenido que se ha creado y que define el proyecto. Dentro de esta habrá:
- `Scenes`: En este proyecto se han creado 4 escenas: OpenGameScene, MenuScene, GameScene y ResultsScene.
- `Scripts`: Código desarrolado en C# que determina el comportamiento y la lógica de todo el proyecto. Estos son todos los scripts que se crearon: *AlignWorldToAnchor.cs*, *ConnectionConfig.cs*, *CrossController.cs*, *DronControl.cs*, *DroneCollision.cs*, *DroneConnectionManager.cs*, *DroneTelemetry.cs*, *FenceGenerator.cs*, *GameResults.cs*, *GatePart.cs*, *GateTrigger.cs*, *GemaSpawner.cs*, *GemProximityDestroy.cs*, *MenuController.cs*, *OptimalAndRealPath.cs*, *RaceTimer.cs*, *ResultsDisplay.cs*, *ScenarioManager.cs*, *SceneManagement.cs*, *StatesHUD.cs*, *TooltipUI.cs*, *UIManager.cs*, *VirtualDroneTelemetry.cs*, *WebcamDisplay.cs*, *WebRTCStreamer.cs*, *WorldAnchor.cs*, *AssignSavedMeshes.cs* y *SaveMeshesEditor*.
- `Prefabs`: Plantillas de los objetos virtuales que se verán en escena.
- `Props&TexturesAssetStore`: Algunos elementos como Prefabs, Texturas y otros Assets creados por otros usuarios de Unity que se descargaron de la Unity Asset Store.
- `Shaders`: Dentro estará el shader *Undistort* creado para corregir el efecto ojo de pez de la cámara del dron.
- `StreamingAssets`: Un fichero *calibration_data.json* que tiene los parámetros de la cámara del dron.
- `UndistortMat`: Un material al que se le asigna el shader *Undistort*.
- `StreamRT`: Una textura que servirá para visualizar vídeo en las WebApps.
- `MoreMaterials`: Algunos materiales creados para algunos Prefabs.
- `SomeImages`: Algunas imágenes útiles para la apariencia de la interfaz de la aplicación final.
- `Plugins`: Aquí está el .dll de la librería csDronLink.

En la memoria del TFG, cuyo link está más abajo en la sección Links, está la información más detallada de para qué sirve cada Asset y cómo se han implemetado para hacer la aplicación final.


# WebApp
Aquí está el código de las WebApps en Python para que estas puedan funcionar correctamente:
- `servidorWebAppWebRTC.py`: servidor (Flask + flask_sock) que sirve las páginas web y hace de puente de señalización WebRTC y de reenvío de las órdenes de control entre el emisor (Unity) y los receptores.
- `indexWebAppWebRTC.html`: página web del visor que recibe y reproduce el vídeo desde Unity mediante WebRTC.
- `control.html`: página web de control que muestra el vídeo y permite pilotar el dron mediante joysticks y botones táctiles.
En la memoria del TFG, cuyo link está más abajo en la sección Links, está la información más detallada de cómo se han desarrollado estas WebApps y cómo acceder a ellas.

# csDronLink
Aquí está el código fuente de la librería csDronLink que se usó para general el archivo *csDronLink.dll*. Este código fue desarrollado por los profesores y otros alumnos que forman parte del DEE y seguramente se siga desarrollando y mejorando. La pongo en este repositorio porque esta es la versión más reciente que hay a la fecha en la que se está subiendo este proyecto y con la cual este proyecto es compatible.


# Consideraciones Previas
- Instalar Unity con el editor 6000.3.18f1.
- Descargar y descomprimir el proyecto de Unity TFG_AR-code.zip desde el link que está abajo en Links.
- Abrir Unity Hub, darle a 'Add Project' y seleccionar el TFG_AR-code descargado.
- Comprobar que estén todos los Assets descritos más arriba una vez se ha abierto el proyecto en Unity.
- Instalar en Unity el paquete WebRTC 3.0.0-pre.5 si no lo estuviese.
- Si al abrir el proyecto sale el error: CS0619: 'AndroidSdkVersions.AndroidApiLevel22' is obsolete: 'Minimum supported Android API level is 25', una forma rápida de solucionarlo sería ir a la ruta Library/PackageCache/com.unity.webrtc.../Editor/BuildProcessor.cs y sustituir AndroidApiLevel22 por AndroidApiLevel25.
- Darle Play a Unity solo si se está en la escena OpenGameScene.
- Si se quieren probar las WebApps en global, darle Run al archivo *servidorWebAppWebRTC.py* y abrir ngrok y ejecutar el comando *ngrok http 8106* (será necesario instalar ngrok y crear una cuenta) el cual dará la URL para acceder a la WebApp de Videostreaming desde otro dispositivo. Para acceder a la WebApp de Control habrá que usar la misma URL poniendo un */control* al final. Solo acceder a la URL, una vez la GameScene se haya abierto.
- Mirar el Capítulo 9: TESTS de la memoria del TFG para saber qué pruebas hacer para verificar el correcto funcionamiento de la aplicación.


# Links
- `TFG_AR-code.zip`: Se puede encontrar en el enlace https://drive.google.com/file/d/1888Kk9JKEib_J-WmRo8kp9n3tQr0XGUX/view?usp=drive_link
- `memoria del TFG`: Donde está la información más detallada de cada parte del proyecto - https://drive.google.com/file/d/1-2YDByxTGvYOLqZa_Xe1SZLV8xkoeA6X/view?usp=sharing
- `Vídeo 1`: Demostración de una partida en un escenario de inicio a fin con el dron real volando en el DronLab - https://www.youtube.com/watch?v=c9I47gwHjm0
- `Vídeo 2`: Demostración del resto de escenarios con el dron simulado, resaltando algunos detalles de las mecánicas de juego de estos y del funcionamiento de la aplicación que en el primer vídeo no se tocaron - https://www.youtube.com/watch?v=nIKDwmMLPFE
