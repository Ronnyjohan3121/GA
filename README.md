# GA
Creación de un algoritmo genetico , como selección de metaheurística para la solución de un problema de compra y venta de energía eléctrica

# Instalar e importar la biblioteca 'GA' para algoritmos genéticos (Metaheurística Definida)
install.packages("GA")  # Instala la biblioteca GA si aún no está instalada
library(GA)             # Importa la biblioteca GA para usar funciones de algoritmos genéticos

# Función de evaluación para un escenario en específico
evaluate <- function(solution) {
  return(-sum(solution))  # Ejemplo simple, debes personalizar esta función según las necesidades de un escenario específico
}

# Configuración de los parámetros del algoritmo genético
ga_config <- function() {
  return(list(
    popSize = 50,      # Tamaño de la población
    pcrossover = 0.8,  # Probabilidad de cruce
    pmutation = 0.1,   # Probabilidad de mutación
    maxiter = 100,     # Número máximo de generaciones
    run = 100,         # Número máximo de evaluaciones de la función objetivo
    crossover = 2,     # Tipo de operador de cruce (2 para cruce uniforme)
    monitor = FALSE    # No mostrar información de todo el progreso (puedes cambiar a TRUE si deseas ver detalles)
    # Otros parámetros...
  ))
}

# Ejecutar el algoritmo genético
run_genetic_algorithm <- function() {
  # Definir el espacio de búsqueda y restricciones
  search_space <- matrix(c(0, 100), nrow = 1, ncol = 2)  # Ejemplo simple, ajusta según las variables de decisión y rangos, para el problema doctorando (5 variables de decisión para los prosumers - 4 más no consideradas principales)

  # Ejecutar el algoritmo genético
  result <- ga(type = "real-valued",  # Tipo de problema (variables continuas)
               fitness = evaluate,     # Función de evaluación definida por el usuario
               lower = rep(search_space[1, ], times = 2),  # Límites inferiores del espacio de búsqueda
               upper = rep(search_space[1, ], times = 2),  # Límites superiores del espacio de búsqueda
               popSize = 50,            # Tamaño de la población
               pcrossover = 0.8,        # Probabilidad de cruce
               pmutation = 0.1,         # Probabilidad de mutación
               maxiter = 100,           # Número máximo de generaciones
               run = 100,               # Número máximo de evaluaciones de la función objetivo
               crossover = 2,           # Tipo de operador de cruce (2 para cruce uniforme)
               monitor = FALSE)         # No mostrar información de todo el progreso

  # Devolver los resultados
  return(result)
}

# Ejemplo de ejecución del algoritmo genético
result <- run_genetic_algorithm()
print(result)

