# TRABAJOS C++

 ESTE CODIGO ESTA ECHO EN UN LENGUAJE DE C++ LA CUAL TIENE COMO FUNCION DAR MANEJO A UNA SALA DE CINE ES SEMCILLA PERO ES UN POCO DE LO QUE HEMOS APRENDIDO EN EL CURSO
 <br>
    <h1>TRABAJOS C++</h1>
    <br>
    <pre>
#include &lt;iostream&gt;
#include &lt;stdlib.h&gt;
#include &lt;cctype&gt;
using namespace std;

void mayusc(string pal) {
    for (int c = 0; c < pal.length(); c++) {
        pal[c] = toupper(pal[c]);
    }
}

int main() {
    string sala[30] = {
        "A1", "A2", "A3", "A4", "A5",
        "B1", "B2", "B3", "B4", "B5",
        "C1", "C2", "C3", "C4", "C5",
        "D1", "D2", "D3", "D4", "D5",
        "E1", "E2", "E3", "E4", "E5",
        "F1", "F2", "F3", "F4", "F5"
    };
    string asiento;
    int costo = 0, boletos = 0, boletosvendidos = 0, venta = 0, menu = 0, final = 0;
    char confirmacion;
    bool continuar = true;
    float porcentocupacion = 0;
    cout << "EVER SANCHEZ ANTONIO\tOSCAR URIEL MELLADO MINERO\tLUIS ANTONIO CASTANEDA ORTUNO" << endl;
    cout << "\n\n\nINGRESA EL COSTO DE LOS BOLETOS  $: ";
    cin >> costo;

    do {
        porcentocupacion = 0;
        for (int i = 0; i < 30; i++) {
            if (sala[i] == "##") {
                porcentocupacion += 3.33;
            }
        }

        if (porcentocupacion < 25) {
            system("color 3");
        } else if (porcentocupacion < 50) {
            system("color 6");
        } else if (porcentocupacion < 75) {
            system("color e");
        } else {
            system("color b");
        }

        cout << "\t\t _______________________________" << endl;
        cout << "\t\t|     ******PANTALLA******      |" << endl;
        cout << "\t\t|_______________________________|" << endl;
        cout << "\t";
        for (int i = 0; i < 30; i++) {
            cout << "\t" << sala[i];
            if (i == 4 || i == 9 || i == 14 || i == 19 || i == 24 || i == 29) {
                cout << "\t" << endl << "\t\t \t \t \t \t \t" << endl << "\t";
            }
        }
        cout << " \t \t \t \t \t \t";

        do {
            cout << "\n-----------------------------------------------------------------------------------------------------------------------" << endl;
            cout << "1.-COMPRAR BOLETOS" << endl;
            cout << "2.-REALIZAR CORTE DE CAJA" << endl;
            cout << "3.-FIN DEL PROGRAMA" << endl;
            cout << "\n\nELIJE EL NUMERO DE OPCION: ";
            cin >> menu;
        } while (menu > 3 || menu < 1);

        switch (menu) {
        case 1: {
            do {
                cout << "\nINGRESA LA CANTIDAD DE BOLETOS A COMPRAR: ";
                cin >> boletos;
                if (boletos > 30 || boletos < 1) {
                    cout << "\tOPCION NO VALIDA: " << endl;
                }
            } while (boletos > 30 || boletos < 1);

            string asientosSeleccionados[30];
            bool asientoValido;

            if (boletos == 30) {
                for (int j = 0; j < boletos; j++) {
                    asiento = sala[j];
                    asientosSeleccionados[j] = asiento;
                    sala[j] = "XX";
                }
                asientoValido = true;
            } else {
                for (int i = 0; i < boletos; i++) {
                    asientoValido = false;
                    do {
                        cout << "\nINGRESA LA UBICACION DEL ASIENTO " << i + 1 << ": ";
                        cin >> asiento;
                        mayusc(asiento);
                        if (asiento == "30") {
                            cout << "El asiento 30 no esta disponible" << endl;
                            break;
                        }
                        for (int z = 0; z < 30; z++) {
                            if (asiento == asientosSeleccionados[z]) {
                                cout << "\nEL ASIENTO YA SE ENCUENTRA OCUPADO" << endl;
                                break;
                            } else if (asiento == sala[z]) {
                                asientosSeleccionados[i] = asiento;
                                sala[z] = "XX";
                                asientoValido = true;
                                break;
                            }
                        }
                    } while (!asientoValido);
                }
            }

            if (asientoValido) {
                cout << "\nEL TOTAL A PAGAR ES: " << costo * boletos << endl;
                do {
                    cout << "DESEA CONFIRMAR LA COMPRA DE LOS BOLETOS (S/N): ";
                    cin >> confirmacion;
                    confirmacion = toupper(confirmacion);
                    if (confirmacion != 'S' && confirmacion != 'N') {
                        cout << "\nOPCION NO VALIDA" << endl;
                    }
                } while (confirmacion != 'S' && confirmacion != 'N');

                if (confirmacion == 'S') {
                    boletosvendidos += boletos;
                    venta += (costo * boletos);
                    cout << "\t\t ______________________________" << endl;
                    cout << "\t\t|     ******PANTALLA******     |" << endl;
                    cout << "\t\t|______________________________|" << endl;
                    cout << "\t";
                    for (int i = 0; i < 30; i++) {
                        cout << "\t" << sala[i];
                        if (i == 4 || i == 9 || i == 14 || i == 19 || i == 24 || i == 29) {
                            cout << "\t" << endl << "\t \t \t \t \t \t \t" << endl << "\t";
                        }
                    }
                    cout << "\n**********" << endl << "\t";
                    system("pause");
                    system("cls");
                }
            }
            break;
        }
        case 2: {
            if (venta == 0) {
                cout << "SE REQUIERE COMPRAR BOLETOS " << endl;
                system("pause");
                system("cls");
                break;
            }
            cout << "\n\t\tCORTE DE CAJA " << endl;
            cout << "TOTAL DE BOLETOS VENDIDOS: " << boletosvendidos << endl;
            cout << "PORCENTAJE DE OCUPACION: " << porcentocupacion << "%" << endl;
            cout << "COSTO TOTAL: " << venta << "\n\t";
            system("pause");
            system("cls");
            break;
        }
        }

        for (int i = 0; i < 30; i++) {
            if (sala[i] == "XX") {
                final++;
            }
        }

        if (final == 30) {
            break;
        } else {
            final = 0;
        }
    } while (menu > 0 && menu <= 2);
    return 0;
}
    </pre>
