# Proyecto-Pyton

import json

try:
    with open("base_de_datos.json", "r") as archivo_db:
        print("Leyendo base de datos...")
        lista_estudiantes = json.load(archivo_db)
        print("Base de datos cargada exitosamente")
except:
    print("Creando nueva base de datos...")
    lista_estudiantes = []

def calcular_promedio(lista_notas_estudiante):
    total_suma = 0
    for nota in lista_notas_estudiante:
        total_suma = total_suma + nota
    cantidad_notas = len(lista_notas_estudiante)
    promedio = total_suma / cantidad_notas
    return promedio

def ingresar_nuevo_estudiante():
    nombre = input("Ingrese nombre: ")
    carnet = input("Ingrese carnet: ")
    lista_notas = []
    opcion_notas = input("Desea ingresar una nota? (y / n): ")
    while opcion_notas == 'y' or opcion_notas == 'Y':
        
        nueva_nota = input("Ingrese la nota: ")
        nueva_nota = int(nueva_nota)
        lista_notas.append(nueva_nota)
        opcion_notas = input("Desea ingresar otra nota? (y / n): ")
    promedio_estudiante = calcular_promedio(lista_notas)
    
    estudiante = {
      'Nombre': nombre, 
        'Carnet': carnet,
        'Notas': lista_notas,
        'Promedio': promedio_estudiante,
      
    }
   
    lista_estudiantes.append(estudiante)
       
    return

def mostrar_lista_estudiantes():
    
    print(lista_estudiantes)
    return

def mostrar_cantidad_estudiantes():
    cantidad = len(lista_estudiantes)
    print(f'Hay {cantidad} cantidad de estudiantes')
    return
    

def mostrar_menu():
    print("================================================")
    mensaje_menu = """
    Ingrese la opcion deseada\n
    1. Ingresar un nuevo estudiante
    2. Ver lista de estudiantes
    3. Mostrar cantidad de estudiantes
    0. Salir\n
================================================
    > 
    """
    opcion = input(mensaje_menu)
    opcion = int(opcion)
    if opcion == 1:
        ingresar_nuevo_estudiante()
        print("================================================")
    if opcion == 2:
        mostrar_lista_estudiantes()
        print("================================================")
    if opcion == 3:
        mostrar_cantidad_estudiantes()
        print("================================================")
    if opcion == 0:
        with open("base_de_datos.json", "w") as archivo_db:
            print("Guardando base de datos...")
            json.dump(lista_estudiantes, archivo_db)
        return
    mostrar_menu()
    return


mostrar_menu()
