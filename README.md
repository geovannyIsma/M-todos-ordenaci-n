# Métodos de Ordenación

Geovanny Romero
Computacion 3ro "A"

## Quick Sort

**Descripción:**
Quick Sort es un algoritmo de ordenación basado en el paradigma "divide y vencerás". La estrategia principal implica seleccionar un elemento pivote y dividir la lista en dos partes, organizando recursivamente cada sublista.

**Uso:**
```Java

    public DynamicList<Venta> quickSort(DynamicList<Venta> lista, int inicio, int fin, String field, Integer tipo) throws Exception {
        tiempoInicio = 0;
        tiempoFinal = 0;
        Field attribute = Utiles.getField(Venta.class, field);
        Integer n = lista.getLenght() - 1;
        Venta[] ventasArr = lista.toArray();
        tiempoInicio = System.nanoTime();
        if (attribute != null) {
            quickSortRecursivo(ventasArr, 0, n, field, tipo);
        } else {
            throw new Exception("no existe el crieterio de busqueda");
        }
        tiempoFinal = System.nanoTime();
        System.out.println("Tiempo quick sort: " + (tiempoFinal-tiempoInicio) + " nanosegundos");
        return lista.toList(ventasArr);
    }

   private void quickSortRecursivo(Venta[] arr, int inicio, int fin, String field, Integer tipo){
        if (inicio < fin) {
            // Particionar el arreglo, arr[p] estará ahora en el lugar correcto
            int p = particion(arr, inicio, fin, field, tipo);

            // Ordenar recursivamente los elementos antes y después de la partición
            quickSortRecursivo(arr, inicio, p - 1, field, tipo);
            quickSortRecursivo(arr, p + 1, fin, field, tipo);
        }
    }

   private int particion(Venta[] arr, int inicio, int fin, String field, Integer tipo) {
        Venta pivote = arr[fin];
        int i = inicio - 1;

        for (int j = inicio; j < fin; j++) {
            if (arr[j].compare(pivote, field, tipo)) {
                i++;
                Venta temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        Venta temp = arr[i + 1];
        arr[i + 1] = arr[fin];
        arr[fin] = temp;

        return i + 1;
    }
```
## Shell Sort

**Descripción:**
Shell Sort es un algoritmo de ordenación que divide la lista en sublistas más pequeñas, ordenándolas de forma independiente. Utiliza brechas (gaps) para realizar comparaciones e intercambios entre elementos distantes, reduciendo gradualmente las brechas hasta ordenar la lista completa.
```Java
    public DynamicList<Venta> shellSort(DynamicList<Venta> lista, String field, Integer type) throws EmptyException{
        tiempoInicio = 0;
        tiempoFinal = 0;
        Field attribute = Utiles.getField(Venta.class, field);
        int n = lista.getLenght();
        Venta[] personas = lista.toArray();
        tiempoInicio = System.nanoTime();
        if (attribute != null) {
            for (int gap = n / 2; gap > 0; gap /= 2) {
                for (int i = gap; i < n; i++) {
                    Venta aux = personas[i];
                    int j = i;
                    while (j >= gap && !personas[j - gap].compare(aux, field, type)) {
                        personas[j] = personas[j - gap];
                        j -= gap;
                    }
                    personas[j] = aux;
                }
            }
        } else {
            System.out.println("no existe el crieterio de busqueda");
        }
        tiempoFinal = System.nanoTime();
        System.out.println("Tiempo shell sort: " + (tiempoFinal-tiempoInicio) + " nanosegundos");
        return lista.toList(personas);
    }
  
```
