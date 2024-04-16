# Quicksort
#include <iostream>
#include <chrono>
using namespace std;
using namespace std::chrono;

void printArray(int arreglo[], int size) {
    for (int i = 0; i < size; i++)
        cout << arreglo[i] << " ";
    cout << endl;
}

int partition(int arreglo[], int inicio, int final, int size) {
    int pivote = arreglo[final];
    int i = inicio - 1;

    for (int j = inicio; j <= final - 1; j++) {
        if (arreglo[j] < pivote) {
            i++;
            swap(arreglo[i], arreglo[j]);
            cout << "Intercambio: " << arreglo[i] << " con " << arreglo[j] << endl;
            printArray(arreglo, size);
        }
    }
    swap(arreglo[i + 1], arreglo[final]);
    cout << "Intercambio: " << arreglo[i + 1] << " con " << arreglo[final] << endl;
    printArray(arreglo, size);
    return (i + 1);
}

void quicksort(int arreglo[], int inicio, int final, int size) {
    if (inicio < final) {
        int pivoteIndex = partition(arreglo, inicio, final, size);
        quicksort(arreglo, inicio, pivoteIndex - 1, size);
        quicksort(arreglo, pivoteIndex + 1, final, size);
    }
}

int main() {
    int arreglo[] = {8, 6, 5, 4, 3, 2, 9};
    int n = sizeof(arreglo) / sizeof(arreglo[0]);

    auto start = high_resolution_clock::now();
    quicksort(arreglo, 0, n - 1, n);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);

    cout << "Arreglo ordenado:" << endl;
    printArray(arreglo, n);
    cout << "\nTiempo de ejecución: " << duration.count() << " microsegundos" << endl;
    return 0;
}
