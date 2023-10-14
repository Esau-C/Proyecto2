# Proyecto 2
## Edgar Esau Contreras Garcia
## Ejercicio: 
Esta basado en el manejo de archivos, los lenguajes a utilizar son C++ (el incluir C afecta la
calificación) y Python, es decir dos aplicaciones que hacen lo mismo. Cada aplicación debe contener lo
siguiente.
* Creación del archivo
* Lectura del archivo
* Manipulación del archivo

Se debe crear al menos una estructura al que se llamará producto, donde contenga:
* nombre (alfanumérico)
* codigo (alfanumérico)
* precio (real)
* proveedor (alfanumérico)
* existencia (numérico)
* estado (Caracter) donde A = Aprobado y R = reprobado
* descuento (real)

# la opcion No.1 agregar producto
funciona para almacenar productos en un archivo txt, aqui te pedira que ingrese datos como:
* Nombre (del producto)
* Identificador (el codigo con el que se guardara)
* Precio
* Proveedor
* Existencia
* Estado (A: aprobado, R: Rechazado)
* Descuento

# La opcion No.2 Buscar producto
Ayudara a la facil obtencion de datos que se almacenaran en el archivo txt y se puede buscar por codigo y por nombre

# La opcion No.3 modificar producto
Esto ayudara a que si se presenta una alteracion en el precio o stock del producto se pueda cambiar para tener los datos actualizados

# Mas datos:
para ejecutar el programa se necesita tener python instalado y este programa fue elaborado despues de hacer investigaciones sobre como realizar algunas funciones

# Acontinuacion el ejercicio en python
```py
def guardar_inventario(inventario):
    with open("inventario.txt", "w") as archivo:
        for identificador, producto in inventario.items():
            archivo.write(f"{identificador},{producto['nombre']},{producto['precio']},{producto['proveedor']},{producto['existencia']},{producto['estado']},{producto['descuento']}\n")

# Función para cargar el inventario desde un archivo de texto
def cargar_inventario():
    inventario = {}
    try:
        with open("inventario.txt", "r") as archivo:
            for linea in archivo:
                datos = linea.strip().split(',')
                if len(datos) == 7:
                    identificador, nombre, precio, proveedor, existencia, estado, descuento = datos
                    inventario[identificador] = {
                        "nombre": nombre,
                        "precio": float(precio),
                        "proveedor": proveedor,
                        "existencia": int(existencia),
                        "estado": estado,
                        "descuento": float(descuento)
                    }
        return inventario
    except FileNotFoundError:
        return {}

# Función para agregar un producto al inventario
def agregar_producto(inventario):
    nombre = input("Nombre del producto: ")
    identificador = input("Identificador del producto: ")

    if identificador in inventario:
        print("El producto ya existe en el inventario.")
        return

    precio = float(input("Precio del producto: "))
    proveedor = input("Proveedor del producto: ")
    existencia = int(input("Existencia del producto: "))
    estado = input("Estado del producto (A/R): ")
    descuento = float(input("Descuento del producto: "))

    producto = {
        "nombre": nombre,
        "precio": precio,
        "proveedor": proveedor,
        "existencia": existencia,
        "estado": estado,
        "descuento": descuento
    }

    inventario[identificador] = producto
    guardar_inventario(inventario)
    print("Producto agregado con éxito.")

# Función para buscar un producto en el inventario
def buscar_producto(inventario):
    identificador = input("Ingrese el identificador o nombre del producto a buscar: ")

    encontrado = False
    for key, producto in inventario.items():
        if identificador == key or identificador == producto["nombre"]:
            print("Información del producto:")
            print(f"Nombre: {producto['nombre']}")
            print(f"Identificador: {key}")
            print(f"Precio: {producto['precio']}")
            print(f"Proveedor: {producto['proveedor']}")
            print(f"Existencia: {producto['existencia']}")
            print(f"Estado: {producto['estado']}")
            print(f"Descuento: {producto['descuento']}")
            encontrado = True

    if not encontrado:
        print("Producto no existente en el inventario.")

# Función para modificar la información de un producto en el inventario
def modificar_producto(inventario):
    identificador = input("Ingrese el identificador del producto a modificar: ")

    if identificador not in inventario:
        print("El producto no existe en el inventario.")
        return

    producto = inventario[identificador]
    print(f"Modificando el producto '{producto['nombre']}' (Identificador: {identificador})")

    producto["nombre"] = input("Nuevo nombre: ")
    producto["precio"] = float(input("Nuevo precio: "))
    producto["proveedor"] = input("Nuevo proveedor: ")
    producto["existencia"] = int(input("Nueva existencia: "))
    producto["estado"] = input("Nuevo estado (A/R): ")
    producto["descuento"] = float(input("Nuevo descuento: "))

    guardar_inventario(inventario)
    print("Producto modificado!!.")

if __name__ == "__main__":
    inventario = cargar_inventario()

    while True:
        print("Menú:\n1. Agregar producto\n2. Buscar producto\n3. Modificar producto\n4. Salir")
        opcion = input()
        
        if opcion == "1":
            agregar_producto(inventario)
        elif opcion == "2":
            buscar_producto(inventario)
        elif opcion == "3":
            modificar_producto(inventario)
        elif opcion == "4":
            break
        else:
            print("Error, eliga una opcion valida")

```
