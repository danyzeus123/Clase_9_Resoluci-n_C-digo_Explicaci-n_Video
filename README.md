# Clase_9_Resolucion_Codigo_Explicacion_Video
# Clase base para todas las tareas
class Tarea:
    def __init__(self, nombre, descripcion, prioridad):
        self.nombre = nombre
        self.descripcion = descripcion
        self.prioridad = prioridad

    def __str__(self):
        return f"Tarea: {self.nombre}\nDescripción: {self.descripcion}\nPrioridad: {self.prioridad}"

# Clase para tareas generales (hereda de Tarea)
class TareaGeneral(Tarea):
    pass

# Clase para tareas con fecha límite (hereda de Tarea)
class TareaConFecha(Tarea):
    def __init__(self, nombre, descripcion, prioridad, fecha_limite):
        super().__init__(nombre, descripcion, prioridad)
        self.fecha_limite = fecha_limite

    def __str__(self):
        return f"{super().__str__()}\nFecha límite: {self.fecha_limite}"

# Clase para administrar las tareas
class AdministradorTareas:
    def __init__(self):
        self.tareas = []

    def agregar_tarea(self, tarea):
        self.tareas.append(tarea)
        print(f"Tarea '{tarea.nombre}' agregada.")

    def eliminar_tarea(self, nombre_tarea):
        self.tareas = [tarea for tarea in self.tareas if tarea.nombre != nombre_tarea]
        print(f"Tarea '{nombre_tarea}' eliminada.")

    def listar_tareas(self):
        if not self.tareas:
            print("No hay tareas registradas.")
        else:
            print("Lista de Tareas:")
            for tarea in self.tareas:
                print(tarea)
                print("-" * 20)

# Función principal para interactuar con el usuario
def main():
    administrador = AdministradorTareas()

    while True:
        print("\n*** Menú de Tareas ***")
        print("1. Agregar Tarea General")
        print("2. Agregar Tarea con Fecha Límite")
        print("3. Eliminar Tarea")
        print("4. Listar Tareas")
        print("5. Salir")

        opcion = input("Seleccione una opción (1-5): ")

        if opcion == '1':
            tarea_general = TareaGeneral(
                input("Nombre de la tarea: "),
                input("Descripción: "),
                input("Prioridad (alta, media, baja): ")
            )
            administrador.agregar_tarea(tarea_general)

        elif opcion == '2':
            tarea_con_fecha = TareaConFecha(
                input("Nombre de la tarea: "),
                input("Descripción: "),
                input("Prioridad (alta, media, baja): "),
                input("Fecha límite (dd/mm/aaaa): ")
            )
            administrador.agregar_tarea(tarea_con_fecha)

        elif opcion == '3':
            tarea_a_eliminar = input("Nombre de la tarea a eliminar: ")
            administrador.eliminar_tarea(tarea_a_eliminar)

        elif opcion == '4':
            administrador.listar_tareas()

        elif opcion == '5':
            print("Saliendo del programa...")
            break

        else:
            print("Opción inválida. Intente nuevamente.")

# Llamada directa a main(), Ejecuta la función principal cada vez que se use este archivo
main()
