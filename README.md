import random
import os

# Definir las preguntas y respuestas por categoría
preguntas = {
    "sumas": {
        "¿Cuánto es 2 + 2?": ["a) 3", "b) 4", "c) 5", "d) 6"],
        "¿Cuánto es 7 + 5?": ["a) 10", "b) 11", "c) 12", "d) 13"],
    },
    "restas": {
        "¿Cuánto es 8 - 5?": ["a) 1", "b) 2", "c) 3", "d) 4"],
        "¿Cuánto es 15 - 7?": ["a) 6", "b) 7", "c) 8", "d) 9"],
    },
    "multiplicaciones": {
        "¿Cuánto es 5 * 3?": ["a) 10", "b) 15", "c) 25", "d) 30"],
        "¿Cuánto es 6 * 4?": ["a) 20", "b) 22", "c) 24", "d) 26"],
    },
    "divisiones": {
        "¿Cuánto es 12 / 3?": ["a) 2", "b) 3", "c) 4", "d) 6"],
        "¿Cuánto es 16 / 4?": ["a) 3", "b) 4", "c) 5", "d) 6"],
    },
    "potencias": {
        "¿Cuánto es 10 ** 2?": ["a) 100", "b) 200", "c) 50", "d) 25"],
        "¿Cuánto es 3 ** 2?": ["a) 6", "b) 8", "c) 9", "d) 12"],
    }
}

# Definir las respuestas correctas por categoría
respuestas_correctas = {
    "sumas": {
        "¿Cuánto es 2 + 2?": "b",
        "¿Cuánto es 7 + 5?": "c",
    },
    "restas": {
        "¿Cuánto es 8 - 5?": "c",
        "¿Cuánto es 15 - 7?": "c",
    },
    "multiplicaciones": {
        "¿Cuánto es 5 * 3?": "b",
        "¿Cuánto es 6 * 4?": "c",
    },
    "divisiones": {
        "¿Cuánto es 12 / 3?": "c",
        "¿Cuánto es 16 / 4?": "b",
    },
    "potencias": {
        "¿Cuánto es 10 ** 2?": "a",
        "¿Cuánto es 3 ** 2?": "c",
    }
}

# Función para mostrar preguntas al azar de una categoría específica
def mostrar_pregunta(categoria):
    preguntas_categoria = preguntas[categoria]
    respuestas_categoria = respuestas_correctas[categoria]
   
    num_preguntas = min(3, len(preguntas_categoria))
    preguntas_seleccionadas = random.sample(list(preguntas_categoria.keys()), num_preguntas)
   
    puntaje = 0

    for pregunta in preguntas_seleccionadas:
        print(pregunta)
        for opcion in preguntas_categoria[pregunta]:
            print(opcion)
       
        respuesta_usuario = ""
        opciones_validas = ['a', 'b', 'c', 'd']

        while respuesta_usuario not in opciones_validas:
            respuesta_usuario = input("Respuesta: ").lower()
            if respuesta_usuario not in opciones_validas:
                print("Por favor, ingresa una opción válida (a, b, c, d).")

        if respuesta_usuario == respuestas_categoria[pregunta]:
            print("¡Respuesta correcta!")
            puntaje += 1
        else:
            print("Respuesta incorrecta.")

        print()  # Salto de línea entre preguntas

    return puntaje, num_preguntas

# Ejecutar el juego
print("¡Bienvenido al juego de preguntas matemáticas!")

nombre = input("Por favor, ingresa tu nombre: ")

while True:
    edad = input("Por favor, ingresa tu edad: ")
    if edad.isdigit():
        edad = int(edad)
        break
    else:
        print("Por favor, ingresa un número válido para la edad.")

categoria = ""
categorias_disponibles = ["sumas", "restas", "multiplicaciones", "divisiones", "potencias"]
while categoria not in categorias_disponibles:
    categoria = input(f"Selecciona la categoría ({'/'.join(categorias_disponibles)}): ").lower()

print(f"¡Hola, {nombre}! Vamos a comenzar con las preguntas de {categoria}.")

puntaje_total, num_preguntas = mostrar_pregunta(categoria)

print(f"{nombre}, tu puntaje total es: {puntaje_total} puntos.")

if puntaje_total == num_preguntas:
    print("¡Felicitaciones! ¡Obtuviste todas las respuestas correctas!")
elif puntaje_total == 0:
    print("¡Sigue practicando, lo harás mejor la próxima vez!")
else:
    print("¡Buen trabajo! Sigue practicando para mejorar aún más.")

# Guardar los resultados en un archivo de texto en la carpeta "resultados" en el escritorio
ruta_escritorio = os.path.join(os.path.expanduser("~"), "Desktop")
ruta_carpeta_resultados = os.path.join(ruta_escritorio, "resultados")

if not os.path.exists(ruta_carpeta_resultados):
    os.makedirs(ruta_carpeta_resultados)

ruta_resultados = os.path.join(ruta_carpeta_resultados, "resultados.txt")

with open(ruta_resultados, "w") as archivo:
    archivo.write(f"Nombre: {nombre}\n")
    archivo.write(f"Edad: {edad}\n")
    archivo.write(f"Categoría: {categoria.capitalize()}\n")
    archivo.write(f"Puntaje Total: {puntaje_total} puntos\n")

print(f"Los resultados han sido guardados en '{ruta_resultados}'.")
