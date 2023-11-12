# ProyectoFinal
Archivos proyecto final
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

// Clientes
struct Cliente {
    string nombre;
    string apellido;
    string direccion;
    string telefono;
    string nit;
};

// Productos
struct Producto {
    string nombre;
    int cantidad;
    double precio;
};

// Ventas
struct Ventas {
	string vendedor;
    string cliente;
    string nit;
    string fecha;
    string n1;
    string n2;
    string n3;
    double c1;
    double c2;
    double c3;
    double p1;
    double p2;
    double p3;
    double t1;
    double t2;
    double t3;
    double total;

};

void registrarClientes();
void registrarProductos();
void consultarClientes();
void consultarProductos();
void facturador();
void consultarVentas();

int main() {
    int opcion;

    do {
        cout << "\n        MENU\n" << endl;
        cout << "1. Registrar clientes.\n";
        cout << "2. Registrar productos.\n";
        cout << "3. Consultar clientes.\n";
        cout << "4. Consultar productos.\n";
        cout << "5. Consultar Ventas.\n";
        cout << "6. Facturador.\n";
        cout << "7. Salir.\n";
        cout << "\nIngrese una opcion: ";
        cin >> opcion;

        switch (opcion) {
            case 1: registrarClientes(); break;
            case 2: registrarProductos(); break;
            case 3: consultarClientes(); break;
            case 4: consultarProductos(); break;
            case 5: consultarVentas(); break;
            case 6: facturador(); break;
            case 7: cout << "\nSaliendo...\n"; break;
            default: cout << "\n  ERROR: Opcion Invalida\n";
        }
    } while (opcion != 7);

    return 0;
}

void registrarClientes() {
    ofstream archivoClientes("clientes.txt", ios::app);
    Cliente cliente;
    
    cout << "--------------------------------\n";

    cout << "Ingrese el nombre del cliente: ";
    cin.ignore();
    getline(cin, cliente.nombre);

    cout << "Ingrese el apellido del cliente: ";
    getline(cin, cliente.apellido);

    cout << "Ingrese la direccion del cliente: ";
    getline(cin, cliente.direccion);

    cout << "Ingrese el telefono del cliente: ";
    getline(cin, cliente.telefono);

    cout << "Ingrese el NIT del cliente: ";
    getline(cin, cliente.nit);    

    archivoClientes << cliente.nombre << " " << cliente.apellido << " " << cliente.direccion << " " << cliente.telefono << " " << cliente.nit << "\n";
    archivoClientes.close();

    cout << "\nCliente registrado correctamente\n";
}

void registrarProductos() {
    ofstream archivoProductos("productos.txt", ios::app);
    Producto producto;

    cout << "Ingrese el nombre del producto: ";
    cin.ignore();
    getline(cin, producto.nombre);

    cout << "Ingrese la cantidad del producto: ";
    cin >> producto.cantidad;

    cout << "Ingrese el precio del producto: ";
    cin >> producto.precio;

    archivoProductos << producto.nombre << " " << producto.cantidad << " " << producto.precio << "\n";
    archivoProductos.close();

    cout << "\nProducto registrado correctamente\n";
}

void consultarClientes() {
    ifstream archivoClientes("clientes.txt");

    if (archivoClientes.is_open()) {
        string linea;
        cout << "\nCLIENTES:\n" << endl;
        cout << "Nombre|Apellido|Direccion|Tel|NIT \n";
        cout << "_________________________________________________\n";

        while (getline(archivoClientes, linea)) {
            cout << linea << "\n";
        }

        archivoClientes.close();
    } else {
        cout << "No se pudo abrir el archivo clientes.txt\n";
    }
}

void consultarProductos() {
    ifstream archivoProductos("productos.txt");

    if (archivoProductos.is_open()) {
        string linea;
        cout << "\nPRODUCTOS:\n" << endl;
        cout << "Nombre | Cantidad | Precio\n";
        cout << "______________________________\n";

        while (getline(archivoProductos, linea)) {
            cout << linea << "\n";
        }

        archivoProductos.close();
    } else {
        cout << "No se pudo abrir el archivo productos.txt\n";
    }
}
void consultarVentas() {
    ifstream archivoVentas("ventas.txt");

    if (archivoVentas.is_open()) {
        string linea;
        cout << "\nVENTAS:\n"<<endl;
        cout << "   Fecha |Vendedor|Cliente|Total\n";
        cout << "______________________________\n";

        while (getline(archivoVentas, linea)) {
            cout << linea << "\n";
        }

        archivoVentas.close();
    } else {
        cout << "No se pudo abrir el archivo productos.txt\n";
	}
}

void facturador() {
    ofstream archivoVentas("ventas.txt", ios::app);
    Ventas ventas;
    
    cout << "\n--------------------------------\n";
    cout << "Ingrese la Fecha DD/MM/YYYY: ";
    cin.ignore();
    getline(cin, ventas.fecha);

    cout << "Ingrese el nombre del vendedor: ";
    getline(cin, ventas.vendedor);

    cout << "Ingrese el nombre del cliente: ";
    getline(cin, ventas.cliente);
    
    cout << "Ingrese el nombre del producto 1: ";
    getline(cin, ventas.n1);
      
    cout << "Ingrese la cantidad de producto 1: ";
    cin >> ventas.c1;
    
    cout << "Ingrese el precio del producto 1: ";
    cin >> ventas.p1;

    cout << "Ingrese el nombre del producto 2: ";
    cin.ignore();
	getline(cin, ventas.n2);
      
    cout << "Ingrese la cantidad de producto 2: ";
    cin >> ventas.c2;
    
    cout << "Ingrese el precio del producto 2: ";
    cin >> ventas.p2;

    cout << "Ingrese el nombre del producto 3: ";
    cin.ignore();
	getline(cin, ventas.n3);
      
    cout << "Ingrese la cantidad de producto 3: ";
    cin >> ventas.c3;
    
    cout << "Ingrese el precio del producto 3: ";
    cin >> ventas.p3;
    
    ventas.t1 = ventas.c1 * ventas.p1;
    ventas.t2 = ventas.c2 * ventas.p2;
    ventas.t3 = ventas.c3 * ventas.p3;
    ventas.total = ventas.t1 + ventas.t2 + ventas.t3;

    cout << "\n--------------------------------------";
	
	cout << "\n-----------FACTURA--------\n" << endl;
	cout << "Fecha: " << ventas.fecha << endl;
	cout << "Vendedor: " << ventas.vendedor << endl;
	cout << "Cliente: " << ventas.cliente << endl;
	cout << "1. " << ventas.n1 << " Cant. " << ventas.c1 << " c/u " << ventas.p1 << " = " << ventas.t1 <<endl;
	cout << "2. " << ventas.n2 << " Cant. " << ventas.c2 << " c/u " << ventas.p2 << " = " << ventas.t2 <<endl;
	cout << "3. " << ventas.n3 << " Cant. " << ventas.c3 << " c/u " << ventas.p3 << " = " << ventas.t3 <<endl;
	cout << "\n     Total a Pagar: "<< ventas.total << endl;
	cout << "\n\n*******GRACIAS POR SU COMPRA*******" << endl;
	 
    archivoVentas << ventas.fecha << " " << ventas.vendedor << " " << ventas.cliente << " " << ventas.total <<"\n";
    archivoVentas.close();

    cout << "\nFactura registrada con exito\n";

}
