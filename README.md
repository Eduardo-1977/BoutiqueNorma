struct Producto {
    var nombre: String
    var precio: Double
    var stock: Int
}

// Función para mostrar los productos disponibles
func mostrarProductos(_ productos: [Producto]) {
    print("\nPRODUCTOS DISPONIBLES:")
    for (index, producto) in productos.enumerated() {
        print("\(index + 1). \(producto.nombre) - $\(producto.precio) - Stock: \(producto.stock)")
    }
}

// Función para realizar la compra de un producto
func comprarProducto(_ productos: inout [Producto]) {
    mostrarProductos(productos)
    print("\nIngrese el número del producto que desea comprar (0 para salir):")
    
    if let opcion = Int(readLine() ?? "0"), opcion > 0 && opcion <= productos.count {
        let indiceProducto = opcion - 1
        var cantidad = 0
        
        print("Ingrese la cantidad que desea comprar:")
        if let cantidadIngresada = Int(readLine() ?? "0") {
            cantidad = cantidadIngresada
        }
        
        if cantidad > 0 {
            let productoSeleccionado = productos[indiceProducto]
            
            if cantidad <= productoSeleccionado.stock {
                let totalPagar = productoSeleccionado.precio * Double(cantidad)
                print("\n¡Compra realizada!")
                print("Ha comprado \(cantidad) unidades de \(productoSeleccionado.nombre).")
                print("Total a pagar: $\(totalPagar)")
                
                productos[indiceProducto].stock -= cantidad
            } else {
                print("\nLo sentimos, no hay suficiente stock disponible.")
            }
        } else {
            print("\nCantidad inválida. La compra no se realizó.")
        }
    } else {
        print("\nOpción inválida. La compra no se realizó.")
    }
}

func main() {
    var productos: [Producto] = [
        Producto(nombre: "Camiseta", precio: 25.0, stock: 10),
        Producto(nombre: "Pantalón", precio: 40.0, stock: 5),
        Producto(nombre: "Zapatos", precio: 60.0, stock: 3),
        Producto(nombre: "Bufanda", precio: 15.0, stock: 8)
    ]
    
    var continuar = true
    
    while continuar {
        print("***** Bienvenido a la Pagina de Boutique Norma *****")
        print("\n¿Qué desea hacer?")
        print("1. Mostrar productos disponibles.")
        print("2. Comprar un producto.")
        print("3. Salir.")
        
        if let opcion = Int(readLine() ?? "0") {
            switch opcion {
            case 1:
                mostrarProductos(productos)
            case 2:
                comprarProducto(&productos)
            case 3:
                continuar = false
            default:
                print("\nOpción inválida.")
            }
        } else {
            print("\nOpción inválida.")
        }
    }
}

// Ejecutar el programa
main()
