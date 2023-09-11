<div align="right">
<img width="32px" src="img/algo2.svg">
</div>

# TP1

## Repositorio de Lucas Aldonate - 100030 - laldonate@fi.uba.ar

- Para compilar:

```bash
gcc pruebas_chanutron.c -o <nombre>
```

- Para ejecutar:

```bash
./<nombre>
```

- Para ejecutar con valgrind:
```bash
valgrind --leak-check=full --track-origins=yes --show-reachable=yes --error-exitcode=2 --show-leak-kinds=all --trace-children=yes ./<nombre>
```
---
##  Funcionamiento

### Función principal:

El programa recibe un archivo el cuál intetna abrir en caso de ser válido. Si se logra abrir, se aloja memoria para el vector de pokemones. Se lee linea por linea
guardando los valores de cada linea en cada iteración, se guardan dichos datos en el vector en caso de ser posible y en caso contrario se utiliza un realloc 
(el cuál a su vez utiliza una variable auxiliar en caso de fallos), para agrandar el vector y poder seguir guardando los datos de los pokemones. El programa
continua siempre y cuando no se encuentren errores o hasta llegar al final del archivo.

<div align="center">
<img width="100%" src="img/diagrama-code.png">
</div>

### Funciones auxiliares:

Aparte de la función principal, se crearon 4 funciones aparte. Dos de ellas se utilizan para finalizar el programa, liberar la memoria y retornar NULL (en caso de que
los ataques sean inválidos) o el vector (en caso de que algun tipo de pokemon/ataque sea inválido). Se creó una función para determinar el tipo de pokemon/ataque
dependiendo de lo leído en el archivo y por último una función de ordenamiento (Bubble Sort), para ordenar alfabéticamente el vector de pokemones. Esta última 
utiliza una función que simplemente sirve para intercambiar dos valores en el vector.
A continuación se listan dichas funciones:

```c
informacion_pokemon_t *ataques_invalidos(informacion_pokemon_t *ip,
					 FILE *archivo)
{
	fclose(archivo);
	for (int k = 0; k < 3; k++) {
		free(ip->pokemones[ip->cantidad]->ataques[k]);
	}
	free(ip->pokemones[ip->cantidad]);
	free(ip->pokemones);
	free(ip);
	return NULL;
}
```

```c
informacion_pokemon_t *tipo_invalido(informacion_pokemon_t *ip, FILE *archivo)
{
	fclose(archivo);
	for (int k = 0; k < 3; k++) {
		free(ip->pokemones[ip->cantidad]->ataques[k]);
	}
	free(ip->pokemones[ip->cantidad]);
	return ip;
}
```



```c
enum TIPO tipo_pokemon(const char tipo)
{
	switch (tipo) {
	case 'N':
		return NORMAL;
	case 'F':
		return FUEGO;
	case 'A':
		return AGUA;
	case 'P':
		return PLANTA;
	case 'E':
		return ELECTRICO;
	case 'R':
		return ROCA;
	default:
		return -1;
	}
}
```

```c
void cambiar_posicion(pokemon_t *xp, pokemon_t *yp)
{
	pokemon_t temp = *xp;
	*xp = *yp;
	*yp = temp;
}

```

```c
void bubble_sort(pokemon_t **pokemones, int cantidad)
{
	int i, j;
	int es_mayor;
	bool cambio;
	for (i = 0; i < cantidad - 1; i++) {
		cambio = false;
		for (j = 0; j < cantidad - i - 1; j++) {
			es_mayor = strcmp(pokemones[j]->nombre,
					  pokemones[j + 1]->nombre);
			if (es_mayor > 0) {
				cambiar_posicion(pokemones[j],
						 pokemones[j + 1]);
				cambio = true;
			}
		}

		if (cambio == false)
			break;
	}
}
```

En el archivo `sarasa.c` la función `funcion1` utiliza `realloc` para agrandar la zona de memoria utilizada para conquistar el mundo. El resultado de `realloc` lo guardo en una variable auxiliar para no perder el puntero original en caso de error:

```c
int *vector = realloc(vector_original, (n+1)*sizeof(int));

if(vector == NULL)
    return -1;
vector_original = vector;
```


<div align="center">
<img width="70%" src="img/diagrama2.svg">
</div>

---

## Respuestas a las preguntas teóricas
Incluír acá las respuestas a las preguntas del enunciado (si aplica).
