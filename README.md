#include <iostream>
using namespace std;

struct Vehiculo {
    string tipo;
    int movimientos;
    int tarifa;
};

const int MAX = 100;
Vehiculo pila[MAX];
int tope = -1;
int dineroGenerado = 0;

void ingresarVehiculo(string tipo) {
    if (tope < MAX - 1) {
        Vehiculo v;
        v.tipo = tipo;
        v.movimientos = 0;
        v.tarifa = (tipo == "carro") ? 2000 : 1000;
        pila[++tope] = v;
        cout << tipo << " ingresado al parqueadero.\n";
    } else {
        cout << "El parqueadero está lleno.\n";
    }
}

void moverVehiculo() {
    if (tope >= 0) {
        pila[tope].movimientos++;
        cout << "Movimiento realizado para el " << pila[tope].tipo << ".\n";
    } else {
        cout << "No hay vehículos en el parqueadero.\n";
    }
}

void retirarVehiculo() {
    if (tope >= 0) {
        Vehiculo v = pila[tope--];
        int total = v.tarifa + (v.movimientos * 100);
        dineroGenerado += total;
        cout << v.tipo << " retirado. Total a pagar: $" << total << ".\n";
    } else {
        cout << "No hay vehículos en el parqueadero.\n";
    }
}

void mostrarDineroGenerado() {
    cout << "Dinero generado hasta ahora: $" << dineroGenerado << ".\n";
}

int main() {
    int opcion;
    string tipo;

    do {
        cout << "\n--- Sistema de Parqueadero ---\n";
        cout << "1. Ingresar carro\n";
        cout << "2. Ingresar moto\n";
        cout << "3. Mover vehículo\n";
        cout << "4. Retirar vehículo\n";
        cout << "5. Mostrar dinero generado\n";
        cout << "6. Salir\n";
        cout << "Seleccione una opción: ";
        cin >> opcion;

        switch (opcion) {
            case 1:
                ingresarVehiculo("carro");
                break;
            case 2:
                ingresarVehiculo("moto");
                break;
            case 3:
                moverVehiculo();
                break;
            case 4:
                retirarVehiculo();
                break;
            case 5:
                mostrarDineroGenerado();
                break;
            case 6:
                cout << "Saliendo del sistema...\n";
                break;
            default:
                cout << "Opción inválida.\n";
        }
    } while (opcion != 6);

    return 0;
}
