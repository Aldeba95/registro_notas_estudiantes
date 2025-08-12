# registro_notas_estudiantes
📚 Gestión de Notas de Estudiantes  Este programa en Python permite registrar estudiantes con sus notas, calcular el promedio de cada uno y clasificar si han aprobado o reprobado según su rendimiento académico.

#--------------------- FUNCION ENCARGADA DE CAPTURAR DATOS--------------------------------
def ingresar_datos_estudiantes():
    registro_estudiante = {}

    while True:
        nombre_estudiante = input("Ingresar nombre del estudiante: ").upper()
        notas_estudiante = [] #Lista que almacenara las notas de los estudiantes

        # Captura de notas
        for i in range(3):
            while True:
                try:
                    nota_estudiante = float(input(f"Ingresar nota {i+1} del estudiante: "))
                    if 0 <= nota_estudiante <= 5: #if nota_estudiante > 0 and nota_estudiante < 5:
                        notas_estudiante.append(nota_estudiante)
                        break
                    else:
                        print("Nota invalida, por favor ingrese una nota entre 0.0 y 5.0")
                except ValueError:
                    print("Entrada invalida, por favor ingrese un numero")

        registro_estudiante[nombre_estudiante] = notas_estudiante # Diccionario que almacena los nombres de los estudiantes como keys y las notas como values.

        # Validar si se sigue ejecutando el programa
        while True:
            continuar = input("Desea ingresar a otro estudiante? (SI/NO): ").upper()
            print("-"*100)
            if continuar in ("SI", "NO"):
                break
            else:
                print("Respuesta invalida, por favor ingrese SI o NO")
        if continuar == "NO":
            print("Saliendo del programa")
            break
    return registro_estudiante
#--------------------- FUNCION ENCARGADA DE REALIZAR CALCULOS--------------------------------
def promedio_notas(registro_estudiante):
    promedios = {}
    for nombre, notas in registro_estudiante.items():
        promedio = sum(notas) / len(notas)
        promedios[nombre] = promedio
    return promedios
#--------------------- FUNCION ENCARGADA EVALUAR A LOS ESTUDIANTES--------------------------------
def clasificacion(promedios):
    resultados = {}
    for nombre, promedio in promedios.items():
        if promedio >= 3:
            resultados[nombre] = "APROBADO"
        else:
            resultados[nombre]= "REPROBADO"
    return resultados
#--------------------- FUNCION ENCARGADA DE CONTROLAR EL FLUJO--------------------------------
def main():
    registro = ingresar_datos_estudiantes()
    promedios = promedio_notas(registro)
    resultados = clasificacion(promedios)

    print("*"*8 + "INFORME FINAL" + "*"*8)
    for nombre in registro:
        print(f"{nombre} - PROMEDIO: {promedios[nombre]:.2f} - {resultados[nombre]}")
if __name__ == "__main__":
    main()
