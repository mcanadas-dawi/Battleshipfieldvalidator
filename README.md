# BATTLESHIP FIELD VALIDATOR
## Code Wars 3kyu Kata
### TAREA
Escribe un método que reciba un array 2D 10x10 con el tablero y la posición de los barcos y devuelva true si la distribución es válida o false si no lo es.
### REGLAS
1.  Hay 1 battleship (4 celdas) 2 cruisers (3 celdas) 3 destroyers (2 celdas) y 4 submarinos (1 celda).

2.  Cada barco tiene que estar en linea recta (horizontal,vertical,diagonal)

3.  Los barcos no se pueden tocar 

### CÓDIGO

```java
public class BattleField {

 public static Integer comprobador(int x, int y, int[][] field) { //función para identificar el tipo de barco
        //descarto los casos que no cumplen las reglas devolviendo 5 (no seran comprobados en el switch)
        if ((x > 0) && (y < 9))
            if (field[x - 1][y + 1] == 1) return 5;
        if ((x < 9) && (y < 9)) {
            if (field[x + 1][y + 1] == 1) return 5;
            if ((field[x + 1][y] == 1) && (field[x][y + 1] == 1)) return 5;
        }
        // uso la recursividad para devolver el tipo de barco que es
        if (y < 9)
            if (field[x][y + 1] == 1) return 1 + comprobador(x, y + 1, field);

        if (x < 9)
            if (field[x + 1][y] == 1) return 1 + comprobador(x + 1, y, field);

        return 1;
    }


    public static boolean fieldValidator(int[][] field) { //función para validar el tablero
        Integer submarines = 0;
        int cruisers = 0;
        int destroyers = 0;
        int battleship = 0;
        for (int y = 0; y < 10; y++)
            for (int x = 0; x < 10; x++) {


                if (field[x][y] == 1) {
                    if ((x > 0) && (field[x - 1][y] == 1)) continue;
                    if ((y > 0) && (field[x][y - 1] == 1)) continue;

                    //Sumar a sus respectivos contadores los barcos encontrados
                    switch (comprobador(x, y, field)) {
                        case 1:
                            submarines++;
                            break;
                        case 2:
                            destroyers++;
                            break;
                        case 3:
                            cruisers++;
                            break;
                        case 4:
                            battleship++;
                            break;
                        default:
                            return false;
                    }
                }
            }
        //Comprobar si he encontrado todos los barcos
        if (submarines != 4) return false;
        if (destroyers != 3) return false;
        if (cruisers != 2) return false;
        if (battleship != 1) return false;

        return true;
    }
}
```
####  ENLACE AL KATA
[Battleship field validator](https://www.codewars.com/kata/52bb6539a4cf1b12d90005b7/java "Battleship field validator")
