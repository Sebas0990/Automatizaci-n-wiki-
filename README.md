<h1 style="font-size:60px">ACP TanqueAgua</h1>

<h2 style="font-size:40px">PRESENTACIÓN DEL PROBLEMA</h2>

<p style="font-size:20px">
Se pide realizar un sistema de alarmas para un tanque de agua. El tanque tiene tres 
sensores que miden el nivel del agua y cinco alarmas; cuatro alarmas para determinar el 
nivel del agua y una para determinar errores. Los errores se dan cuando los sensores no 
son activados en el orden secuencial; por ejemplo si el sensor B3 se activa pero los 
sensores B1 y B2 no. Solo puede haber una alarma activa a la vez. 
</p>

<img width="1400" height="456" alt="image" src="https://github.com/user-attachments/assets/4fe7f30f-9c86-4e07-8bc9-e755cc91051b" />

<p style="font-size:20px">
Para este ejercicio utilizamos una tabla de verdad en la que consideramos B1, B2 y B3 
como las entradas del sistema y H1, H2, H3, H4, H5 como las salidas. Según las 
indicaciones solo puede haber una única salida encendida, es decir en valor 1. 
</p>

<table style="font-size:18px">
<tr><th>B1</th><th>B2</th><th>B3</th><th>H1</th><th>H2</th><th>H3</th><th>H4</th><th>H5</th></tr>
<tr><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
<tr><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
<tr><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td></tr>
<tr><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
<tr><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
<tr><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
<tr><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
<tr><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
</table>

<h2 style="font-size:40px">IMPLEMENTACIÓN EN CODESYS</h2>

<p style="font-size:20px">
Para representar los sensores (entradas) utilizamos tres interruptores de palanca; mientras 
que para las alarmas (salidas) utilizamos luces.  
</p>

<img width="718" height="673" alt="image" src="https://github.com/user-attachments/assets/e6389027-441f-44f8-b395-0dd0114ffe5a" />

<p style="font-size:20px">
En la lógica Ladder colocamos en serie los contactos que representan los interruptores B1, 
B2 y B3 representando una lógica AND; para las luces colocamos en paralelo las bobinas. 
Para las salidas colocamos bobinas tipo SET y RESET para asegurar que solo una salida 
esté activa a la vez.  
</p>

<img width="928" height="677" alt="image" src="https://github.com/user-attachments/assets/42323fb7-7465-46a9-9909-bac3a7564587" />

<p style="font-size:20px">
Para los casos de errores conectamos los tres contactos en serie pero con diferentes 
configuraciones en paralelo con la finalidad de obtener un OR con entradas AND.  
</p>

<img width="1214" height="248" alt="image" src="https://github.com/user-attachments/assets/4263092d-12df-4b37-a508-e59dc0d53469" />

<p style="font-size:20px">
Para probar si la configuración fue correcta se ejecutó la simulación y se realizaron todas 
las configuraciones presentadas en la tabla de verdad; procurando que se prenda la luz 
correspondiente.  
</p>

<img width="778" height="737" alt="image" src="https://github.com/user-attachments/assets/d21ba923-042b-466b-9083-4acf2ff13ea8" />
<img width="795" height="745" alt="image" src="https://github.com/user-attachments/assets/ae47a92d-eb89-42f5-bac5-6ee642f4cb09" />
<img width="787" height="748" alt="image" src="https://github.com/user-attachments/assets/cd075244-d5dc-4546-8a31-6258369edef0" />
<img width="867" height="758" alt="image" src="https://github.com/user-attachments/assets/7df5b50d-9ee3-4fdd-9929-e74260114431" />
<img width="808" height="719" alt="image" src="https://github.com/user-attachments/assets/9e71c4b7-696f-441d-b881-ac2ebe7fe66a" />

<h2 style="font-size:40px">IMPLEMENTACIÓN EN OPENPLC</h2>

<p style="font-size:20px">
Primero declaramos nuestras variables de entradas y salidas; a todas les otorgamos un 
valor de tipo BOOL y basándonos en la documentación de OpenPLC le asignamos las 
entradas y salidas digitales para un microcontrolador Arduino Uno.  
</p>

<img width="1038" height="430" alt="image" src="https://github.com/user-attachments/assets/7f5cc3e8-0148-4a1e-a512-7e598f376b74" />

<p style="font-size:20px">
Dada la limitación de la cantidad de salidas digitales que tenemos en el microcontrolador; 
para representar el error activaremos todas las salidas simultáneamente.  
</p>

<p style="font-size:20px">
Ahora conectamos las entradas en serie y las salidas en paralelo; y para el error creamos 
una configuración en serie de las entradas y conectamos estas configuraciones en paralelo.  
</p>

<img width="819" height="507" alt="image" src="https://github.com/user-attachments/assets/ad68b070-9265-412a-b7de-12a075c1ede7" />
<img width="775" height="423" alt="image" src="https://github.com/user-attachments/assets/436c9348-fea1-48f9-b602-5563f701adc3" />
<img width="775" height="478" alt="image" src="https://github.com/user-attachments/assets/7124e9c3-5ec9-4037-a1bf-d1e5a0a7a300" />
<img width="744" height="421" alt="image" src="https://github.com/user-attachments/assets/b8e3f0d9-cd9e-4176-8a38-7dae65eeb934" />
<img width="1072" height="345" alt="image" src="https://github.com/user-attachments/assets/0242ddf7-a736-48b4-bfdc-9e689b7be4b0" />

<h2 style="font-size:40px">IMPLEMENTACIÓN FÍSICA</h2>

<p style="font-size:20px">
Para simular los sensores utilizamos conexiones en vcc con cables asignados a las 
entradas; y para las alarmas utilizamos 4 bombillos led con los colores correspondientes 
según la imagen de representación del problema.  
</p>

<img width="583" height="534" alt="image" src="https://github.com/user-attachments/assets/6e938e13-7cb1-480b-a210-b67542c24a33" />

