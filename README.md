# Escenario-Procedural
Escenario Procedural

1- Limpieza de la escena

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

🔹Primero seleccionamos todos los objetos.
🔹 Luego los eliminamos.

 ¿Por qué?
 Para comenzar con una escena completamente vacía y evitar errores o acumulación de objetos anteriores.
 
2- Creación de materiales (Modelo de Color RGB)

def crear_material(nombre, color_rgb):

    mat = bpy.data.materials.new(name=nombre)
    mat.diffuse_color = (*color_rgb, 1.0)
    return mat
🔹 Creamos una función para no repetir código.
🔹 Usamos el modelo RGB (Rojo, Verde, Azul).
🔹 El valor 1.0 es la opacidad (canal Alpha).

Concepto aplicado:

 Modelo de color RGB y reutilización de código (programación estructurada).
 
3- Definición de parámetros

largo_pasillo = 10
ancho_pasillo = 4

🔹 largo_pasillo controla cuántos cubos se crean.
🔹 ancho_pasillo controla la separación entre paredes.

Esto permite modificar el escenario fácilmente sin cambiar todo el código.
 
4-Construcción de paredes (Transformación: Traslación)
for i in range(largo_pasillo):

🔹 Se usa un ciclo for para automatizar la creación.
🔹 Cada iteración crea un cubo nuevo.

Traslación en eje Y:

location=(-ancho_pasillo, i * 2, 1)

🔹 i * 2 mueve cada cubo hacia adelante.
🔹 Esto aplica la transformación de traslación.

5- Alternancia de materiales (Lógica condicional)
if i % 2 == 0:

🔹 Usamos el operador módulo %.
🔹 Alternamos colores entre oscuro y naranja.

Concepto aplicado:

Estructuras condicionales y lógica de programación.
 
6- Escalamiento

pared_izq.scale.z = 1.5

🔹 Modificamos el tamaño en el eje Z.
🔹 Hace que algunos cubos sean más altos.

Concepto aplicado:
 
Transformación de Escalamiento.

7- Simetría (pared derecha)

location=(ancho_pasillo, i * 2, 1)

🔹 Se replica la pared en el eje positivo X.
🔹 Se genera un pasillo simétrico.

8- Creación del suelo (Escalamiento y posicionamiento)

bpy.ops.mesh.primitive_plane_add(size=1, location=(0, largo_pasillo - 1, 0))

🔹 Se crea un plano.
🔹 Luego se escala en X y Y:

suelo.scale.x = ancho_pasillo + 1
suelo.scale.y = largo_pasillo + 1

Conceptos aplicados:

Escalamiento Posicionamiento


9- Iluminación

bpy.ops.object.light_add(type='POINT', location=(0, largo_pasillo, 6))

🔹 Se agrega una luz tipo Point.
🔹 Ilumina todo el recorrido.

Concepto aplicado:
 
Iluminación básica en entornos 3D.
 
10- Cámara

bpy.ops.object.camera_add(location=(0, -8, 6))

🔹 Se agrega una cámara.
🔹 Se ajusta la rotación para enfocar el pasillo.

Permite renderizar la escena correctamente.
<img width="941" height="529" alt="image" src="https://github.com/user-attachments/assets/bd4866bc-0db6-4110-a63e-b62160e8a5b4" />
<img width="941" height="529" alt="image" src="https://github.com/user-attachments/assets/87871293-1c83-4748-abc0-fa6e47be96cd" />
<img width="941" height="529" alt="image" src="https://github.com/user-attachments/assets/66275743-1d33-446a-9bdd-4e0ad41f0d22" />

1- Importación de librerías

import bpy
import math

🔹 bpy permite controlar Blender con código.
🔹 math se usa para funciones matemáticas como el seno.

Aquí aplicamos matemáticas para generar movimiento curvo.

2- Limpieza de la escena

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

🔹 Se seleccionan todos los objetos.
🔹 Se eliminan para empezar desde cero.

 Esto evita errores y acumulación de objetos.
 
3- Creación de materiales (Modelo RGB)

def crear_material(nombre, color_rgb):
    mat = bpy.data.materials.new(name=nombre)
    mat.diffuse_color = (*color_rgb, 1.0)
    return mat
    
🔹 Se crea una función para generar materiales.

🔹 Se usa el modelo de color RGB (Rojo, Verde, Azul).

🔹 El valor 1.0 es la opacidad (Alpha).

Se aplica el concepto de reutilización de código.

4- Definición de parámetros

largo_pasillo = 20
ancho_pasillo = 4
intensidad_curva = 3

🔹 largo_pasillo → número de repeticiones.
🔹 ancho_pasillo → separación entre paredes.
🔹 intensidad_curva → qué tan pronunciada es la curva.

Esto hace el código flexible y modificable.

5- Generación de la curva (Concepto clave)

curva = math.sin(i * 0.4) * intensidad_curva

🔹 math.sin() genera una onda suave.
🔹 i cambia en cada iteración del ciclo.
🔹 0.4 controla la frecuencia de la curva.
🔹 intensidad_curva controla la amplitud.

Matemáticamente:

x=A⋅sin⁡(k⋅i)x = A \cdot \sin(k \cdot i)x=A⋅sin(k⋅i)
Donde:

A = amplitud (intensidad)
k = frecuencia
i = posición en el ciclo
8- Aplicación de Traslación en curva
location=(-ancho_pasillo + curva, i * 2, 1)

🔹 El eje Y avanza normalmente (i * 2).
🔹 El eje X cambia con la función seno.

Esto genera un desplazamiento curvo en lugar de recto.

7- Alternancia de materiales

if i % 2 == 0:

🔹 Se usa el operador módulo %.
🔹 Permite alternar colores automáticamente.

Aplicación de estructuras condicionales.

8- Escalamiento

pared_izq.scale.z = 1.5

🔹 Se modifica el tamaño en el eje Z.
🔹 Se aplica transformación de escalamiento.

9- Creación del suelo

suelo.scale.x = ancho_pasillo + intensidad_curva + 2
suelo.scale.y = largo_pasillo + 2

🔹 Se ajusta el tamaño para cubrir toda la curva.
🔹 Se aplica escalamiento en X y Y.

10 - Iluminación

bpy.ops.object.light_add(type='POINT', location=(0, largo_pasillo, 8))

🔹 Se agrega una luz tipo Point.
🔹 Permite visualizar correctamente la escena.

11- Cámara
bpy.ops.object.camera_add(location=(0, -10, 8))
🔹 Se agrega una cámara.
🔹 Se orienta hacia el pasillo
<img width="941" height="529" alt="image" src="https://github.com/user-attachments/assets/a018f586-3110-40d5-b900-e082219315d4" />
<img width="941" height="529" alt="image" src="https://github.com/user-attachments/assets/014d92a5-1916-4201-b8fd-2c45f3f81fa5" />
<img width="941" height="528" alt="image" src="https://github.com/user-attachments/assets/a4e1aa04-1dd8-49a9-a8ac-b396f79e0abb" />







