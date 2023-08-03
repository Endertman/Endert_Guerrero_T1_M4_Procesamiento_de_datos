# DataFrame

Importamos el DataFrame de la actividad del M3 y solucionamos sus errores.

    Ventas_Clientes_2021 = pd.Series([100.0,200.0,"110,0",90.0, 150.0,80.0,70.0,100.0,110.0,90.0,"100,00"])
    Ventas_Clientes_2021 = Ventas_Clientes_2021.replace({',':   '.', '"': ''},regex=True).astype(float)

    Clientes_2021 = pd.Series (["JUan","camila","DanIel",   "Luis","Juan","Ana","Camila","Ana","LuiS","Ana","Juan"])
    Clientes_2021 = Clientes_2021.str.title()

## Le agregamos nuevos valores encontrados en el DataFrame del caso de estudio

Haremos uso de "iloc" para agregar un valor faltante en las ventas y un cliente faltante en la posición correcta, luego guardaremos los cambios en nuevas variables.

    nuevo_cliente = "Juan"
    Clientes_2021.iloc[10] = nuevo_cliente

    nuevo_valor = 100.0
    Ventas_Clientes_2021.iloc[9] = nuevo_valor

# Ítem 1

## Creamos y mostramos en pantalla el DataFrame

    print(df)

## Agrupamos por clientes y organizamos de mayor a menor

Ahora crearemos un nuevo DataFrame ("df2") donde agruparemos a los clientes y sumaremos sus compras.

    df2 = df.groupby("Clientes").sum()
    print(df2)

                   Ventas
        Clientes         
        Ana        270.0
        Camila     270.0
        Daniel     110.0
        Juan       460.0
        Luis       190.0

También podemos disponer dicho DataFrame de forma descendente para que, al mostrarlo en pantalla, podamos ver cuánto fue el total de las compras realizadas por el cliente organizado jerárquicamente según dicho total. 

    jerarquia = df2.sort_values(by="Ventas", ascending = 0)
    print(jerarquia)
                   Ventas
        Clientes         
        Juan       460.0
        Ana        270.0
        Camila     270.0
        Luis       190.0
        Daniel     110.0

## Generamos un gráfico de barras.

Usaremos la función plot de matplotlib agregando el valor "bar" para obtener el gráfico deseado, haciéndolo de esta forma nos ahorramos el código para separar el indice de sus valores para generar los ejes, también asi nos genera automáticamente el "label" de "Clientes". agregaremos el color en este caso "darkblue" en la misma función "df2.plot", especificaremos el "ylabel" y "title" para asi tener un gráfico mas completo.

en este ejemplo la separación y ancho de las barras se genera automáticamente pero esto valores también los podemos modificar agregando "width" en la función "df2.plot" o usando la función "plt.bar()".

En el ejemplo de estudio no existe una leyenda como se puede ver en este en la parte superior derecha, esta la podemos modificar usando la función "plt.legend", para este caso debemos acompañar la función con ".set_visible(False)".

    df2.plot(kind = "bar", color = "darkblue")
    plt.ylabel("Ventas en Millones")
    plt.title("Ventas del año 2021 por cliente")

    plt.show()


# Ítem 2

## Análisis de los datos

Ahora realizaremos un análisis y mostraremos los resultados para así sacar conclusiones mas fácilmente.

Primero mostraremos la media, mínimo, máximo y desviación estándar usando las funciones pertinentes que nos ofrece Pandas para realizar esta operaciones.

    med_gral = df["Ventas"].mean()
    min_gral = df["Ventas"].min()
    max_gral = df["Ventas"].max()
    des_est_gral = df["Ventas"].std()

    print("Media de ventas durante 2021 en millones:", med_gral)
    print("Menor venta durante 2021 en millones:", min_gral)
    print("Mayor venta durante 2021 en millones:", max_gral)
    print("Desviación estándar de las ventas durante 2021 en millones:", des_est_gral)























https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.iloc.html

https://www.statology.org/pandas-groupby-bar-plot/#:~:text=Pandas%3A%20How%20to%20Create%20Bar%20Plot%20from%20GroupBy,df.groupby%28%5B%27group_var%27%5D%29%20%5B%27values_var%27%5D.sum%28%29%20%23create%20bar%20plot%20by%20group%20df_groups.plot%28kind%3D%27bar%27%29

https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html

https://matplotlib.org/stable/tutorials/intermediate/legend_guide.html

https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.boxplot.html

https://content.lameca.com.ar/canvas/0IPP/procesamientodedatos_may22/L4/M4.%20Qu%C3%A9%20es%20el%20an%C3%A1lisis%20exploratorio%20de%20datos.pdf

https://datapeaker.com/big-data/deteccion-y-tratamiento-de-valores-atipicos-como-manejar-valores-atipicos/#:~:text=4.1%20Detecci%C3%B3n%20de%20valores%20at%C3%ADpicos%20mediante%20Boxplot%3A%20El,vert%3DFalse%29%20plt.title%20%28%22Detecting%20outliers%20using%20Boxplot%22%29%20plt.xlabel%20%28%27Sample%27%29

https://www.analyticslane.com/2022/08/11/graficos-boxplot-con-matplotlib-en-python/