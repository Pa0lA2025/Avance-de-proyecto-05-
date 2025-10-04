class GestorDeNotas:
    def __init__(self):
        self.historial = []  # Pila para historial
        self.revision = []   # Cola para revisión
        self.notas = []      # Lista de notas

    # Agregar una nota
    def agregar_nota(self, nota):
        self.historial.append(("agregar", nota))
        self.notas.append(nota)
        self.revision.append(nota)
        print(f"Nota agregada: {nota}")

    # Deshacer la última acción
    def deshacer(self):
        if not self.historial:
            print("No hay acciones para deshacer.")
            return
        accion, nota = self.historial.pop()
        if accion == "agregar":
            self.notas.remove(nota)
            self.revision.remove(nota)
            print(f"Se deshizo la acción: {accion} - {nota}")

    # Revisar la nota más antigua
    def revisar(self):
        if not self.revision:
            print("No hay notas para revisar.")
            return
        nota = self.revision.pop(0)  # FIFO
        print(f"Nota revisada: {nota}")

    # Ordenar notas con burbuja
    def ordenar_burbuja(self):
        n = len(self.notas)
        for i in range(n):
            for j in range(0, n-i-1):
                if self.notas[j] > self.notas[j+1]:
                    self.notas[j], self.notas[j+1] = self.notas[j+1], self.notas[j]
        print("Notas ordenadas con burbuja:", self.notas)

    # Ordenar notas con inserción
    def ordenar_insercion(self):
        for i in range(1, len(self.notas)):
            clave = self.notas[i]
            j = i - 1
            while j >= 0 and clave < self.notas[j]:
                self.notas[j + 1] = self.notas[j]
                j -= 1
            self.notas[j + 1] = clave
        print("Notas ordenadas con inserción:", self.notas)


# Ejemplo de ejecución
gestor = GestorDeNotas()

# Agregar notas
gestor.agregar_nota(85)
gestor.agregar_nota(70)
gestor.agregar_nota(90)

# Revisar notas
gestor.revisar()

# Deshacer última acción
gestor.deshacer()

# Ordenar notas
gestor.ordenar_burbuja()
gestor.ordenar_insercion()


Evidencia  de ejecucicon personal (adicional) 

Nota agregada: 85
Nota agregada: 70
Nota agregada: 90
Nota revisada: 85
Se deshizo la acción: agregar - 90
Notas ordenadas con burbuja: [70, 85]
Notas ordenadas con inserción: [70, 85]
